# Ushaflow Core EE: Installation

## Using Google Cloud Run

Simplest, fastest and cheapest way to run Ushaflow Core EE is using [Google Cloud Run](https://cloud.google.com/run)

1. Open [Cloud Run console](https://console.cloud.google.com/run) and select the Project with your Dialogflow Agent
2. Press on "Create service" and enter the container image URL
   `gcr.io/ushaflow/core-ee`

   ![](./images/cloudrun/create.png)

3. Select deployment platform and region
4. Choose "Allow unauthenticated invocations" in the "Authentication" section
5. Press on "Show optional revision settings"
6. Set the "Container port" to `8090`

   ![](./images/cloudrun/port.png)

8. In the "Environment variables" section, add [desired configuration options](./configuration.md)

   ![](./images/cloudrun/token.png)

9. Press on "Create"

    ![](./images/cloudrun/overview.png)

10. Visit the given URL to check everything is working

    ![](./images/cloudrun/check.png)