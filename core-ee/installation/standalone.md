# Standalone

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

Download compressed \(.gz\) binary for your operating system from [our Cloud Storage Bucket](https://console.cloud.google.com/storage/browser/ushaflow-core-ee-bin)

* [Linux \(latest\)](https://storage.googleapis.com/ushaflow-core-ee-bin/ushaflow-core-ee-linux.gz)
* [MacOS \(latest\)](https://storage.googleapis.com/ushaflow-core-ee-bin/ushaflow-core-ee-macos.gz)
* [Windows \(latest\)](https://storage.googleapis.com/ushaflow-core-ee-bin/ushaflow-core-ee-win.exe.gz)

{% hint style="info" %}
The bucket in question is using object versioning feature to retain older versions. You can access them using [gstuil tool](https://cloud.google.com/storage/docs/gsutil)

```text
gsutil ls -a gs://ushaflow-core-ee-bin
```
{% endhint %}

```text
wget https://storage.googleapis.com/ushaflow-core-ee-bin/ushaflow-core-ee-linux.gz
```

Uncompress the binary using `gzip` or 7-Zip on Windows

```text
gzip -d ./ushaflow-core-ee-linux.gz
```

Make it executable

```text
chmod +x ./ushaflow-core-ee-linux
```

Set desired [configuration options](../configuration/) in your environment or in `.env` file next to your executable

```text
# .env
SERVER=Ushaflow Core EE
PORT=8090
REALTIME=true
TARGETS=DIALOGFLOW,ACTIONS_ON_GOOGLE
TOKEN=<your license key>
GOOGLE_APPLICATION_CREDENTIALS=./service_account.json
```

Execute the binary

```text
./ushaflow-core-ee-linux
```

```text
Ushaflow Core EE listening on 8090
```

