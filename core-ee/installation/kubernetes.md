# Kubernetes

{% hint style="info" %}
This guide assumes you have some experience with Kubernetes already, if not feel free to begin with [Cloud Run](cloud-run.md), [App Engine Flexible](app-engine-flexible.md) or [Standalone](standalone.md) guide
{% endhint %}

{% hint style="info" %}
Make sure you have [Google Cloud SDK](https://cloud.google.com/sdk/docs) installed
{% endhint %}

Create a Service Account

```text
gcloud iam service-accounts create ushaflow-core-ee
```

Grant `dialogflow.reader` and `dialogflow.client` roles to the Service Account

```text
gcloud projects add-iam-policy-binding <your-project-id> --member serviceAccount:ushaflow-core-ee@<your-project-id>.iam.gserviceaccount.com --role roles/dialogflow.reader
```

```text
gcloud projects add-iam-policy-binding <your-project-id> --member serviceAccount:ushaflow-core-ee@<your-project-id>.iam.gserviceaccount.com --role roles/dialogflow.client
```

Generate Service Account key

```text
gcloud iam service-accounts keys create service_account.json --iam-account ushaflow-core-ee@<your-project-id>.iam.gserviceaccount.com
```

Using `kubectl` create a `Secret` ressource, containing the service account key

```text
kubectl create secret generic ushaflow-core-ee --from-file=service_account.json
```

Create a `ConfigMap` containing desired [configuration options](../configuration/)

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: ushaflow-core-ee
data:
  TOKEN: <your license key>
  GOOGLE_APPLICATION_CREDENTIALS: /app/service_account.json
```

Create a `Deployment` contaning the container

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ushaflow-core-ee
spec:
  selector:
    matchLabels:
      app: ushaflow-core-ee
  template:
    metadata:
      labels:
        app: ushaflow-core-ee
    spec:
      containers:
      - name: ushaflow-core-ee
        image: ghcr.io/ushaflow/core-ee
        envFrom:
        - configMapRef:
            name: ushaflow-core-ee
        volumeMounts:
          - name: service-account
            subPath: service_account.json
            mountPath: /app/service_account.json
            readOnly: true
      volumes:
        - name: service-account
          secret:
            secretName: ushaflow-core-ee
```

Expose the `Deployment` using a `Service`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: ushaflow-core-ee
spec:
  selector:
    app: ushaflow-core-ee
  ports:
  - name: http
    targetPort: 8090
    port: 80
```

Expose the `Service` using `Ingress`

```yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: ushaflow-core-ee
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /
        backend:
          serviceName: ushaflow-core-ee
          servicePort: http
```

