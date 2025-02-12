---
sidebar_position: 2
---

# Webhooks

## Subscription
Subscribe to webhook events in the dashboard by providing the `URL` where you want to receive event notifications.
You will get `secret` that should be used for request validation.

## Request validation
Header `webhook-signature-hmac-sha256` contains webhook event signature. It is generated via `HMAC` with `SHA256` hash and the signature secret as the key. The expected value of the signature is request body as json string. Your service should validate the header matches what you expect.

```typescript
import crypto from 'crypto';

const isSignatureValid = (secret, requestBody, signature) => {
  const genereatedSignature = crypto
    .createHmac('sha256', secret)
    .update(JSON.stringify(requestBody))
    .digest('hex');

  return genereatedSignature === signature;
}
```

## Event format

### Structure
Events follow the proto3 [Event](https://buf.build/toffeecard/toffee/docs/main:event.v1#event.v1.Event) format and are serialized in JSON.

### Supported event types
Refer to the list of supported event types in [EventType](https://buf.build/toffeecard/toffee/docs/main:event.v1#event.v1.EventType).

### Dynamic event body
The structure of the event body varies depending on the event type.
```
EVENT_TYPE_REWARD -> body.reward
```
