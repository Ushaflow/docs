# API

### Response Codes

| HTTP-Code | Reason |
| :--- | :--- |
| 200 | Request was successful |
| 400 | The request body or session ID is invalid and/or missing |
| 403 | The deployment was blocked or the service account key is no longer valid |
| 404 | The deployment was not found |
| 500 | Internal server error |
| 503 | The service is unavailable |

### Errors

#### Example Error

```javascript
{"error": "Deployment was not found", "code": 404}
```

### Endpoints

#### Base Endpoint

```text
https://<HOST>
```

#### Base Endpoint Variables

| Variable | Description |
| :--- | :--- |
| HOST | Required, Host of the Core |

#### Base Endpoint Example

```text
https://dialogflow-web-v2.core.ushaflow.com
```

## Requests

#### Retrieving Agents

#### Request

```http
GET <BASE_ENDPOINT>
```

#### Request Variables

| Variable | Description |
| :--- | :--- |
| BASE\_ENDPOINT | Required, Endpoint of the Core |

#### Response Body

[Agent](https://cloud.google.com/dialogflow/docs/reference/rest/v2beta1/projects.agent)

#### Example Request

```http
GET https://dialogflow-web-v2.core.ushaflow.com
```

#### Example Response

```javascript
{
  "parent": "projects/dialogflow-web-v2",
  "displayName": "DialogflowWebV2",
  "defaultLanguageCode": "en",
  "supportedLanguageCodes": [
    "ru"
  ],
  "timeZone": "Europe/Madrid",
  "description": "This is a unofficial Progressive Web Application for Dialogflow V2, with support for rich-responses and amazing features you need to check out. Choose your language and send Hello to get started",
  "avatarUri": "https://storage.googleapis.com/cloudprod-apiai/ce408f19-7966-487d-8614-f5b1f0474ba6_x.png",
  "enableLogging": true,
  "matchMode": "MATCH_MODE_HYBRID",
  "classificationThreshold": 0.3
}
```

### Detecting Intents

#### Request

```http
POST <BASE_ENDPOINT>
```

#### Request Variables

| Variable | Description |
| :--- | :--- |
| BASE\_ENDPOINT | Required, Endpoint of the Core |

#### Request Body

[DetectIntentRequest](https://cloud.google.com/dialogflow/docs/reference/rpc/google.cloud.dialogflow.v2#google.cloud.dialogflow.v2.DetectIntentRequest)

#### Response Body

[DetectIntentResponse](https://cloud.google.com/dialogflow/docs/reference/rest/v2beta1/DetectIntentResponse)

#### Example Request

```http
POST https://app-of-the-day-9a9f6.gateway.dialogflow.cloud.ushakov.co
Content-Type: application/json

{
  "session": "test",
  "queryInput": {
    "text": {
      "text": "Hello",
      "languageCode": "en"
    }
  }
}
```

**Note**: `session` field is converted into `projects/<Project ID>/agent/sessions/<Session ID>`

#### Example Response

```javascript
{
  "responseId": "85c3d6bd-6f8c-4000-a1ec-fdd6f636b2e8",
  "queryResult": {
    "queryText": "Hello",
    "action": "input.welcome",
    "parameters": {},
    "allRequiredParamsPresent": true,
    "fulfillmentText": "Cannot display response in Dialogflow simulator. Please test on the Google Assistant simulator instead.",
    "fulfillmentMessages": [...],
    "webhookPayload": {...},
    "intent": {
      "name": "projects/app-of-the-day-9a9f6/agent/intents/1e00bd68-62f0-4b8e-9cdd-a81c19f73855",
      "displayName": "Default Welcome Intent"
    },
    "intentDetectionConfidence": 1,
    "diagnosticInfo": {
      "end_conversation": true,
      "webhook_latency_ms": 187
    },
    "languageCode": "en"
  },
  "webhookStatus": {
    "message": "Webhook execution successful"
  }
}
```

## Realtime API

Realtime API implements [Secure WebSocket](https://en.wikipedia.org/wiki/WebSocket) communication between Core and the clients

### Close Codes

| Code | Reason |
| :--- | :--- |
| 4400 | The request body or session ID is invalid and/or missing |
| 4403 | The deployment was blocked or the service account key is no longer valid |
| 4404 | The deployment was not found |
| 4500 | Internal server error |
| 1006 | Realtime API unavailable |

### Errors

#### Example Error

```text
4404 'Deployment was not found'
```

### Endpoints

#### Base Endpoint

```text
wss://<HOST>
```

#### Base Endpoint Variables

| Variable | Description |
| :--- | :--- |
| HOST | Required, Host of the Core |

#### Base Endpoint Example

```text
wss://dialogflow-web-v2.core.ushaflow.com
```

## Requests

### Detecting Intents

#### Request

```http
POST <BASE_ENDPOINT>
```

#### Request Variables

| Variable | Description |
| :--- | :--- |
| BASE\_ENDPOINT | Required, Endpoint of the Core |

#### Request Body

[DetectIntentRequest](https://cloud.google.com/dialogflow/docs/reference/rpc/google.cloud.dialogflow.v2#google.cloud.dialogflow.v2.DetectIntentRequest)

#### Response Body

[DetectIntentResponse](https://cloud.google.com/dialogflow/docs/reference/rest/v2beta1/DetectIntentResponse)

#### Example Request

**Note**: The examples are using NodeJS

**Note**: `session` field is converted into `projects/<Project ID>/agent/sessions/<Session ID>`

```javascript
const WebSocket = require('ws')
const ws = new WebSocket('ws://app-of-the-day-9a9f6.core.ushaflow.com')

ws.send(
  JSON.stringify({
    session: "123",
    queryInput: {
      text: {
        text: "Hello",
        languageCode: "en"
      }
    }
  })
)

ws.on('message', data => {
  console.log(data)
})

ws.on('close', (code, error) => {
  console.log(code, error)
})
```

#### Example Response

```javascript
{
  "responseId": "85c3d6bd-6f8c-4000-a1ec-fdd6f636b2e8",
  "queryResult": {
    "queryText": "Hello",
    "action": "input.welcome",
    "parameters": {},
    "allRequiredParamsPresent": true,
    "fulfillmentText": "Cannot display response in Dialogflow simulator. Please test on the Google Assistant simulator instead.",
    "fulfillmentMessages": [...],
    "webhookPayload": {...},
    "intent": {
      "name": "projects/app-of-the-day-9a9f6/agent/intents/1e00bd68-62f0-4b8e-9cdd-a81c19f73855",
      "displayName": "Default Welcome Intent"
    },
    "intentDetectionConfidence": 1,
    "diagnosticInfo": {
      "end_conversation": true,
      "webhook_latency_ms": 187
    },
    "languageCode": "en"
  },
  "webhookStatus": {
    "message": "Webhook execution successful"
  }
}
```

