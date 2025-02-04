<p align="center">
  <img src="./images/tasknet-color@2x.png" alt="TaskNet Logo" width="300"/>
</p>

<h1 align="center">typescript-sdk</h1>

[![npm version](https://badge.fury.io/js/@ajent-foundation%2Ftypescript-sdk.svg)](https://badge.fury.io/js/@ajent-foundation%2Ftypescript-sdk)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Official TypeScript SDK for the TaskNet API. This SDK provides a simple and intuitive way to interact with the TaskNet API in TypeScript/JavaScript applications.

## Installation

Install the package using npm:
```bash
npm install @ajent-foundation/typescript-sdk
```

## Getting Started

### 1. Environment Setup

Create a `.env` file in your project root with your TaskNet credentials:
```env
API_KEY_ID=your_api_key_id
API_KEY=your_api_key
ENVIRONMENT_UUID=your_environment_uuid
ENVIRONMENT_SECRET=your_environment_secret
```

### 2. Basic Usage

Here's a simple example of how to create a session and navigate to a webpage:
```typescript
import { SessionsApi, PageApi } from "@ajent-foundation/typescript-sdk"
import as dotenv from "dotenv"

// Load environment variables
dotenv.config()

async function main() {
    // Setup authentication
    const mode = "private"
    const apiKeyHeaders = {
        "x-api-key-id": process.env.API_KEY_ID,
        "x-api-key": process.env.API_KEY
    }
    const environmentUUID = process.env.ENVIRONMENT_UUID || ""
    const environmentSecret = process.env.ENVIRONMENT_SECRET || ""
    // Create a new session
    const sessionsApi = new SessionsApi()
    const session = await sessionsApi.modeV1SessionsPost(mode, {
        leaseTime: 5,
        isVncEnabled: true,
        vncMode: "rw",
        driver: "api",
        showMouse: true,
        isProxyEnabled: false
        }, undefined, environmentUUID, environmentSecret, {
        headers: apiKeyHeaders
    })
    // Navigate to a webpage
    const pageApi = new PageApi()
    await pageApi.modeV1PageGoToPagePost(mode, {
        sessionUUID: session.data.sessionUUID,
        url: "https://google.com"
        }, {
        headers: apiKeyHeaders
    })
}
```


## Available APIs

The SDK provides access to several API endpoints:

- `SessionsApi`: Manage browser sessions
- `PageApi`: Control page navigation and interactions
- `OperatorsApi`: Access operator-related functionality
- `ExtensionsApi`: Manage browser extensions
- `FingerprintApi`: Handle browser fingerprinting

## Documentation

For detailed API documentation and advanced usage, please visit our [official documentation](https://dev-docs.tasknet.co/).

## License

This project is licensed under the MIT License - see the LICENSE file for details.