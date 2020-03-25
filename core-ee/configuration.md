---
description: Configuration is done using Environment Variables
---

# Configuration

<table>
  <thead>
    <tr>
      <th style="text-align:left">Variable</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Default</th>
      <th style="text-align:left">Required</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>SERVER</code>
      </td>
      <td style="text-align:left">Server name</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Ushaflow Core EE</td>
      <td style="text-align:left">no</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>PORT</code>
      </td>
      <td style="text-align:left">Server port</td>
      <td style="text-align:left">integer between 1 and 65535</td>
      <td style="text-align:left">8090</td>
      <td style="text-align:left">yes</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>TOKEN</code>
      </td>
      <td style="text-align:left">License key token</td>
      <td style="text-align:left">
        <p>a JWT-Encoded Token</p>
        <p></p>
        <p><b>Note</b>: must be signed with Ushaflow private key</p>
      </td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">yes</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>TARGETS</code>
      </td>
      <td style="text-align:left">Target platforms</td>
      <td style="text-align:left">
        <p>A comma-separated list, containing platform names:</p>
        <p><code>DIALOGFLOW</code>, <code>ACTIONS_ON_GOOGLE</code>, <code>FACEBOOK</code>, <code>SLACK</code>, <code>TELEGRAM</code>, <code>KIK</code>, <code>VIBER</code>, <code>SKYPE</code>, <code>LINE</code>, <code>GOOGLE_HANGOUTS</code>
        </p>
        <p></p>
        <p><b>Note</b>: no space after comma</p>
      </td>
      <td style="text-align:left">all</td>
      <td style="text-align:left">no</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>CHATBASE</code>
      </td>
      <td style="text-align:left">Chatbase integration</td>
      <td style="text-align:left">Chatbase API key</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">no</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>WEBHOOKS</code>
      </td>
      <td style="text-align:left">List of URLs to trigger after request</td>
      <td style="text-align:left">
        <p>A comma-separated list of URLs</p>
        <p></p>
        <p><b>Note</b>: no space after comma</p>
      </td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">no</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>REALTIME</code>
      </td>
      <td style="text-align:left">Enable Realtime (WebSocket API)</td>
      <td style="text-align:left">boolean: <code>true</code> or <code>false</code>
      </td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">no</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>GOOGLE_APPLICATION_CREDENTIALS</code>
      </td>
      <td style="text-align:left">Path to Google Cloud Project Service Account</td>
      <td style="text-align:left">
        <p>A valid URI</p>
        <p></p>
        <p><b>Note</b>: the credentials are configured automatically when running
          inside Google Cloud</p>
      </td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">no</td>
    </tr>
  </tbody>
</table>