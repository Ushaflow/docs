# App Engine Flexible

Make sure you have [Google Cloud SDK](https://cloud.google.com/sdk/docs) installed 

Create an App Engine application

```text
gcloud app create
```

Make and enter a new directory for your App Engine application

```text
mkdir core-ee && cd core-ee
```

Create `app.yaml` and add desired [configuration options](../configuration/) to the `env_variables` field

```yaml
runtime: custom
env: flex
env_variables:
  # your environment variables go here
```

Create a `Dockerfile`

```text
FROM gcr.io/ushaflow/core-ee
```

Deploy your app

```text
gcloud app deploy
```

See your app running

```text
gcloud app browse
```

