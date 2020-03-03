# Ushaflow Core EE: Installation

## Environments

- [Cloud Run](#cloud-run)
- [App Engine Flexible](#app-engine-flexible)
- [Kubernetes]()
- [Docker]()

## Cloud Run

1. Open [Cloud Run console](https://console.cloud.google.com/run) and select the Project with your Dialogflow Agent
2. Press on "Create service"
3. Enter following container image URL

   ```
   gcr.io/ushaflow/core-ee
   ```

4. Select the deployment platform and region
5. Choose "Allow unauthenticated invocations" in the "Authentication" section

   ![](./images/cloudrun/create.png)

6. Press on "Show optional revision settings"
7. In the "Environment variables" section, add [desired configuration options](./configuration.md)

   ![](./images/cloudrun/token.png)

8. Press on "Create"

    ![](./images/cloudrun/overview.png)

9. Visit the given URL to check everything is working

    ![](./images/cloudrun/check.png)

## App Engine Flexible

1. Make sure you have [Google Cloud SDK](https://cloud.google.com/sdk/docs) installed
2. Create an App Engine application

   ```
   gcloud app create
   ```

3. Make and enter a new directory for your App Engine application

   ```
   mkdir core-ee && cd core-ee
   ```

4. Create `app.yaml` and add [desired configuration options](./configuration.md) to the `env_variables` field

   ```yaml
   runtime: custom
   env: flex
   env_variables:
      # your environment variables go here
   ```

5. Create a `Dockerfile`

   ```Dockerfile
   FROM gcr.io/ushaflow/core-ee
   ```

6. Deploy your app

   ```
   gcloud app deploy
   ```

7. See your app running

   ```
   gcloud app browse
   ```