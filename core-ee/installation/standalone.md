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

Download compressed \(.gz\) binary for your operating system from [our S3 bucket](https://core-ee-bin.s3.eu-central-1.amazonaws.com)

{% hint style="info" %}
The bucket is using object versioning feature to retain older versions. You can access them using [AWS CLI](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/list-object-versions.html)
{% endhint %}

* [Linux \(latest\)](https://core-ee-bin.s3.eu-central-1.amazonaws.com/ushaflow-core-ee-linux.gz)
* [MacOS \(latest\)](https://core-ee-bin.s3.eu-central-1.amazonaws.com/ushaflow-core-ee-macos.gz)
* [Windows \(latest\)](https://core-ee-bin.s3.eu-central-1.amazonaws.com/ushaflow-core-ee-win.exe.gz)

System requirements

* 64-bit Linux, Mac or Windows \(amd64\)
* 100 MB of Storage
* 256 MB of RAM

```text
wget https://core-ee-bin.s3.eu-central-1.amazonaws.com/ushaflow-core-ee-linux.gz
```

Uncompress the binary using `gzip` or 7-Zip on Windows

```text
gzip -d ./ushaflow-core-ee-linux.gz
```

Make it executable

```text
chmod +x ./ushaflow-core-ee-linux
```

Set desired [configuration options](../configuration/) in `.env` file next to the executable or in a file specified in `ENV` 

```text
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

