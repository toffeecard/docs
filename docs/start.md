---
sidebar_position: 2
---

# Getting Started

## Configuration

To begin using our system, reach out to us for assistance with setting up your API access. We’ll work with you to configure the games and customize the rules you’d like to implement, ensuring the system aligns perfectly with your requirements.

### Steps
  - Create [Access Token](#authentication) to make API calls
  - Configure [Client SDK](#client-sdk) to work with with API
  - Configure [Webhooks](/packages/webhooks) to receive events about requiered updates


## Authentication
To authenticate requests to the API use should get `access token` from the dashboard.

Pass it as `Bearer {your_access_token}` in `Authorization` header.

## Client SDK
We use [ConnectRPC Protocol](https://connectrpc.com/docs/introduction) to build our API, follow its documentation rules to setup your sdk client. The Proto3 schema for the SDK is available at [https://buf.build/toffeecard/toffee](https://buf.build/toffeecard/toffee). Simply install the appropriate [library](https://buf.build/toffeecard/toffee/sdks) for your programming language to get started.

```typescript
import { createClient } from "@connectrpc/connect";
import { createConnectTransport } from "@connectrpc/connect-node";

const transport = createConnectTransport({
  httpVersion: "2",
  baseUrl: "https://services.toffeecard.com",
});

const client = createClient(Service, transport);

const response = service.method({
  requestField: "value",
}, {
  headers: {
    authorization: `Bearer ${access_token}`,
  }
});
```
