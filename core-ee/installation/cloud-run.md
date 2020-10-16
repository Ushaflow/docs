# Cloud Run

Open [Cloud Run console](https://console.cloud.google.com/run) and select the Project with your Agent

Press on "Create service"

![](../../.gitbook/assets/screenshot-2020-03-25-at-15.03.33.png)

Enter following container image URL

```text
ghcr.io/ushaflow/core-ee
```

Select the deployment platform and region  
Choose "Allow unauthenticated invocations" in the "Authentication" section

![](../../.gitbook/assets/create.png)

Press on "Show optional revision settings"

In the "Environment variables" section, add desired [configuration options](../configuration/)

![](../../.gitbook/assets/token.png)

Press on "Create"

![](../../.gitbook/assets/overview.png)

Visit the given URL to check everything works

![](../../.gitbook/assets/check.png)

