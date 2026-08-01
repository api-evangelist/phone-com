---
name: Send an SMS from a Phone.com extension
description: Send a text message from a Phone.com extension using the v4 API.
api: phone-com-api
generated: '2026-07-20'
method: generated
source: https://apidocs.phone.com/llms.txt
operations:
  - POST /v4/accounts/{voip_id}/extensions/{extension_id}/sms
  - GET /v4/accounts/{voip_id}/extensions
  - GET /v4/accounts/{voip_id}/extensions/{extension_id}/sms
---

# Send an SMS from a Phone.com extension

Send a text message from a Phone.com phone number tied to an extension.

## Prerequisites

- An OAuth 2.0 Bearer access token with a scope that permits messaging
  (`account-owner` or an `extension-user` token for the sending extension).
  See `authentication/phone-com-authentication.yml`.
- Base URL: `https://api.phone.com/v4`.

## Steps

1. **Resolve the extension.** If you only know the account, call
   `GET /v4/accounts/{voip_id}/extensions` and pick the `extension_id` whose
   phone number should send the message.
2. **Send the message.** Call
   `POST /v4/accounts/{voip_id}/extensions/{extension_id}/sms` with the
   recipient number and message text in the JSON body.
3. **Confirm delivery.** List sent messages with
   `GET /v4/accounts/{voip_id}/extensions/{extension_id}/sms` to verify the
   message was created.

## Conventions

- All requests carry `Authorization: Bearer <token>`.
- Responses are JSON; list endpoints paginate with `limit`/`offset`.
- No idempotency-key mechanism is documented — avoid blind retries on a
  non-error timeout to prevent duplicate sends.
