---
name: Register a Phone.com event webhook (callback + listener)
description: Subscribe to Phone.com account events by creating a callback and binding it with a listener.
api: phone-com-api
generated: '2026-07-20'
method: generated
source: https://apidocs.phone.com/llms.txt
operations:
  - POST /v4/accounts/{voip_id}/integrations/events/callbacks
  - POST /v4/accounts/{voip_id}/integrations/events/listeners
  - GET /v4/accounts/{voip_id}/integrations/events/callbacks
  - GET /v4/accounts/{voip_id}/integrations/events/listeners
---

# Register a Phone.com event webhook

Receive HTTP callbacks when Phone.com account events fire (calls, messages, etc.)
by creating a callback target and binding it to event types with a listener.

## Prerequisites

- An OAuth 2.0 Bearer access token (`account-owner`, or `oauth-management` for
  management operations). See `authentication/phone-com-authentication.yml`.
- A publicly reachable HTTPS endpoint to receive callbacks.
- Base URL: `https://api.phone.com/v4`.

## Steps

1. **Create the callback (webhook target).** Call
   `POST /v4/accounts/{voip_id}/integrations/events/callbacks` with your HTTPS
   receiver URL. Save the returned callback id.
2. **Create the listener.** Call
   `POST /v4/accounts/{voip_id}/integrations/events/listeners`, referencing the
   callback id and the event type(s) you want. Add filters/subscriptions to
   narrow which events fire.
3. **Verify.** List with
   `GET /v4/accounts/{voip_id}/integrations/events/listeners` and
   `.../callbacks` to confirm the binding.

## Notes

- A callback that is used by a listener (or as another callback's fallback)
  cannot be deleted until it is unreferenced.
- Callbacks and listeners also exist at the extension level under
  `/v4/accounts/{voip_id}/extensions/{extension_id}/integrations/events/...`.
- See `asyncapi/phone-com-events-webhooks.yml` for the event surface overview.
