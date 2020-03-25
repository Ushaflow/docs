# Ushaflow Core EE

* [API](api.md#api)
  * [Response Codes](api.md#response-codes)
  * [Errors](api.md#errors)
    * [Example Error](api.md#example-error)
  * [Endpoints](api.md#endpoints)
    * [Base Endpoint](api.md#base-endpoint)
    * [Base Endpoint Variables](api.md#base-endpoint-variables)
    * [Base Endpoint Example](api.md#base-endpoint-example)
* [Requests](api.md#requests)
  * [Retrieving Agents](api.md#retrieving-agents)
    * [Request](api.md#request)
    * [Request Variables](api.md#request-variables)
    * [Response Body](api.md#response-body)
    * [Example Request](api.md#example-request)
    * [Example Response](api.md#example-response)
  * [Detecting Intents](api.md#detecting-intents)
    * [Request](api.md#request-1)
    * [Request Variables](api.md#request-variables-1)
    * [Request Body](api.md#request-body)
    * [Response Body](api.md#response-body-1)
    * [Example Request](api.md#example-request-1)
    * [Example Response](api.md#example-response-1)
* [Realtime API](api.md#realtime-api)
  * [Close Codes](api.md#close-codes)
  * [Errors](api.md#errors-1)
    * [Example Error](api.md#example-error-1)
  * [Endpoints](api.md#endpoints)
    * [Base Endpoint](api.md#base-endpoint-1)
    * [Base Endpoint Variables](api.md#base-endpoint-variables-1)
    * [Base Endpoint Example](api.md#base-endpoint-example-1)
  * [Requests](api.md#requests-1)
  * [Detecting Intents](api.md#detecting-intents-1)
    * [Request](api.md#request-2)
    * [Request Variables](api.md#request-variables-2)
    * [Request Body](api.md#request-body-1)
    * [Response Body](api.md#response-body-2)
    * [Example Request](api.md#example-request-2)
    * [Example Response](api.md#example-response-2)

## API

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

