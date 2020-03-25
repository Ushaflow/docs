# Docker

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

Run the container with desired [configuration options](../configuration.md)

```text
docker run -d \
-e "TOKEN=<your license key>" \
-e "GOOGLE_APPLICATION_CREDENTIALS=/app/service_account.json" \
-p 8090:8090 \
-v "$(pwd)"/service_account.json:/app/service_account.json \
gcr.io/ushaflow/core-ee
```

