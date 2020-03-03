# Ushaflow Core EE: Configuration

Configuration is done using Environment Variables

## Variables

### `SERVER`

Server Name

#### Values

Any string

#### Default

Ushaflow Core EE

---

### `PORT`

Port Ushaflow Core EE should listen to

#### Values

Integer between 1 and 65535

#### Default

`8090`

---

### `TOKEN`

License key token

#### Values

A JWT-Encoded Token, signed with Ushaflow secret key

#### Default

none

---

### `TARGETS`

Which Platforms to target

#### Values

A comma-separated list, containing Platform strings:

`DIALOGFLOW`, `ACTIONS_ON_GOOGLE`, `FACEBOOK`, `SLACK`, `TELEGRAM`, `KIK`, `VIBER`, `SKYPE`, `LINE`, `GOOGLE_HANGOUTS`

Example:

`TARGETS=DIALOGFLOW,ACTIONS_ON_GOOGLE`

**Note**: no space after comma

#### Default

all

---

### `CHATBASE`

Chatbase integration

#### Values

Chatbase API key

#### Default

disabled

---

### `WEBHOOKS`

List of URLs to trigger, when Ushaflow Core EE receives a request

#### Values

Example:

`WEBHOOKS=https://example.com,https://example.com`

**Note**: no space after comma

#### Default

disabled

---

#### `REALTIME`

Enable Realtime (WebSocket) API

#### Values

`true` or `false`

#### Default

`false` (disabled)

---

#### `GOOGLE_APPLICATION_CREDENTIALS`

Path to Google Cloud Project Service Account

#### Values

A URI

Example:

`/tmp/service_account.json`

**Note**: the credentials are configured automatically when running inside Google Cloud

#### Default

none