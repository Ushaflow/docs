# Pub/Sub

Core EE Pub/Sub feature allows you to publish processed messages to your Pub/Sub topics

### Prerequisites

* Make sure your Core EE endpoint runs correctly with your current configuration options

### Installation

Enable [Cloud Pub/Sub API](https://console.cloud.google.com/apis/api/pubsub.googleapis.com) in your project

Specify desired topic in `PUBSUB_TOPIC`  environment variable \(make sure it exists\)

Additionally, if you're using Docker, Kubernetes or custom service account with App Engine or Cloud Run, grant `pubsub.publisher` role to that service account

```text
gcloud projects add-iam-policy-binding <your-project-id> --member serviceAccount:ushaflow-core-ee@<your-project-id>.iam.gserviceaccount.com --role roles/pubsub.publisher
```

###  Usage

Create a subscription to consume messages

Reference: [https://cloud.google.com/pubsub/docs/subscriber](https://cloud.google.com/pubsub/docs/subscriber)

