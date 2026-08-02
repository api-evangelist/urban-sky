---
name: Receive real-time balloon telemetry from Urban Sky
description: >-
  Connect to the Urban Sky telemetry feed with the JavaScript or Python SDK,
  listen for balloon and unassigned-device updates, verify the pipeline with
  the published test endpoint, and handle the documented error codes.
api: https://docs.urbansky.com/
generated: '2026-07-21'
method: generated
source: https://docs.urbansky.com/guide/getting-started.html
operations:
  - UrbanSkySDK.init
  - sdk.on('balloon:update')
  - sdk.on('unassigned:devices')
  - sdk.on('error')
  - sdk.off
  - sdk.disconnect
  - POST /sdk/test/balloon
---

# Receive real-time balloon telemetry from Urban Sky

There is no self-serve sign-up: obtain an organization-scoped API token by
contacting Urban Sky support (support@atmosys.com); it arrives via secure
email. Keep it server-side only and out of version control.

## Steps

1. **Load the SDK from the CDN loader** (no npm/pip packages yet):
   - JavaScript: fetch `https://sdk.atmosys.com/runtime/js/current/loader.js` and eval it; `UrbanSkySDK` becomes global.
   - Python: `exec(requests.get('https://sdk.atmosys.com/runtime/py/current/loader.py').text)`.
2. **Initialize and connect**: `const sdk = await UrbanSkySDK.init({ apiToken: process.env.URBAN_SKY_TOKEN })`. `init()` connects automatically — do not call `connect()` yourself. Default baseUrl is `https://api.ops.atmosys.com` (only override for custom deployments).
3. **Register handlers before relying on data**: `sdk.on('balloon:update', handler)` for balloon telemetry (`{balloonId, missionId, devices[]}`; devices carry `deviceId`, `deviceType` (PLD/APX/BLS), `lat`, `lng`, optional `altitude` in meters, ISO 8601 `timestamp`) and `sdk.on('unassigned:devices', handler)` for devices not assigned to a balloon. Track connection state with `connected`/`disconnected`.
4. **Verify end-to-end** with the published test endpoint: `POST https://api.ops.atmosys.com/sdk/test/balloon` with headers `x-api-token: <token>` and `Content-Type: application/json`, body `{}` — the test update arrives on your `balloon:update` listener.
5. **Handle the documented error codes** on `sdk.on('error', ...)`: `INVALID_TOKEN` / `AUTH_INVALID_TOKEN` (fix credentials), `AUTH_INSUFFICIENT_PERMISSIONS`, `CONNECTION_LOST` (SDK reconnects automatically — do not roll your own), `NETWORK_ERROR`, `TIMEOUT` (retry), `RATE_LIMITED` (back off before retrying), `SERVICE_UNAVAILABLE`.
6. **Shut down cleanly** with `sdk.disconnect()`; remove listeners with `sdk.off(event, handler)`.

## Rules

- Wrap update processing in try/catch so a bad payload never kills the listener (validate `balloonId` and `devices` exist).
- No pagination, idempotency, or versioning contracts are documented; the feed is push-only WebSocket — never poll.
- See `errors/urban-sky-error-codes.yml`, `conventions/urban-sky-conventions.yml`, and `asyncapi/urban-sky-telemetry-asyncapi.yml` in this repo for the captured surface.
