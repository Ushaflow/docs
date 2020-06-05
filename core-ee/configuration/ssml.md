# SSML

Core EE's Cloud Text-To-Speech feature allows you to produce audio from text and SSML  

### Prerequisites

* Make sure your Core EE endpoint runs correctly with your current configuration options

### Installation

Enable [Cloud Text-to-Speech API](https://console.cloud.google.com/marketplace/details/google/texttospeech.googleapis.com) in your project

Add `SSML_CONFIG` environment variable to your Core EE deployment

**Example**

`{"audioEncoding": "MP3", "sampleRateHertz": "44100"}`

Optionally specify `SSML_VOICE` and `SSML_VOICE_GENDER` enviroment variables

### Usage

After SSML feature was configured you should be able to access `outputAudio` field in your responses

**Note**: the audio is encoded in base64

