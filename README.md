# AWS Polly Text-to-Speech Server

This Express.js server provides an API endpoint for text-to-speech synthesis using AWS Polly.

## Features

1. Uses AWS Polly for speech synthesis
2. Exposes a single API endpoint for text-to-speech conversion
3. Supports custom voice selection
4. Returns a pre-signed URL for the synthesized speech audio

## Setup

1. The server uses environment variables for configuration (loaded via dotenv)
2. CORS is enabled for cross-origin requests
3. JSON parsing middleware is used for request body parsing
4. Static file serving is set up for the "public" directory

## AWS Polly Configuration

- Uses the AWS SDK for JavaScript v3
- Configures the Polly client with region, access key ID, and secret access key from environment variables

## Main Functionality

### `speakText(voice, text)`

This asynchronous function generates a speech URL using AWS Polly:
- Takes `voice` (Voice ID) and `text` as parameters
- Sets up speech parameters including output format (mp3) and text type
- Uses `getSynthesizeSpeechUrl` to generate a pre-signed URL for the synthesized speech
- Returns the generated URL or throws an error if the process fails

### API Endpoint: POST `/api/synthesize`

- Accepts JSON payload with `voice` and `text` properties
- Calls `speakText` with the provided parameters
- Returns a JSON response with the `audioUrl` or a 500 error if synthesis fails

## Server Initialization

- The server listens on the port specified in the environment variable PORT, or defaults to 3333
- Logs a message when the server starts successfully