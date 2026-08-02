---
name: Urban Sky AI Assistant Guide (provider-published prompts)
description: >-
  Urban Sky's own published prompts for AI assistants (ChatGPT, Claude, GitHub
  Copilot) to generate working Urban Sky SDK implementations. Captured verbatim
  from the provider's docs.
api: https://docs.urbansky.com/guide/ai-prompt.html
generated: '2026-07-21'
method: searched
source: https://docs.urbansky.com/guide/ai-prompt.html
operations:
  - UrbanSkySDK.init
  - sdk.on('balloon:update')
---

# Urban Sky AI Assistant Guide

Urban Sky publishes copy-paste prompts for AI assistants at
https://docs.urbansky.com/guide/ai-prompt.html. The prompts below are the
provider's own text, captured verbatim.

## JavaScript/Node.js Implementation Prompt

```
Create a simple Node.js script that connects to the Urban Sky SDK and logs balloon updates.

**Requirements:**
- Load the SDK from https://sdk.atmosys.com/runtime/js/current/loader.js
- Connect and listen for balloon:update events
- Log device locations when updates are received
- Use environment variables for the API token
- Include basic error handling

**Documentation links (please review for implementation details):**
- Getting Started: https://docs.atmosys.com/guide/getting-started
- JavaScript Guide: https://docs.atmosys.com/guide/javascript-sdk
- Examples: https://docs.atmosys.com/examples/basic-usage

**Provide:**
1. Simple main script file
2. Package.json with required dependencies
3. Example .env file

Keep it simple - just enough to connect and receive data.
```

## Python Implementation Prompt

```
Create a simple Python script that connects to the Urban Sky SDK and logs balloon updates.

**Requirements:**
- Load the SDK from https://sdk.atmosys.com/runtime/py/current/loader.py
- Connect and listen for balloon:update events
- Log device locations when updates are received
- Use environment variables for the API token
- Include basic error handling

**Documentation links (please review for implementation details):**
- Getting Started: https://docs.atmosys.com/guide/getting-started
- Python Guide: https://docs.atmosys.com/guide/python-sdk
- Examples: https://docs.atmosys.com/examples/basic-usage

**Provide:**
1. Simple main script file
2. Requirements.txt with dependencies
3. Example .env file

Keep it simple - just enough to connect and receive data.
```

## Data Processing Prompt

```
Create a script that connects to the Urban Sky SDK and saves balloon data for analysis.

**Features needed:**
- Connect to Urban Sky telemetry feed
- Save balloon updates to JSON files
- Calculate distance between position updates
- Basic error handling and logging

**Documentation for reference:**
- Balloon Examples: https://docs.atmosys.com/examples/balloon-updates
- Error Handling: https://docs.atmosys.com/guide/error-handling

Choose JavaScript or Python and provide a simple, working solution. Focus on
getting data saved first - additional features can be added later.
```

## Web Dashboard Prompt

```
Create a basic web application that displays balloon data on a map.

**Core features:**
- Backend that connects to Urban Sky SDK
- Simple web page with a map
- Display balloon positions in real-time
- Basic error handling

**Documentation for reference:**
- SDK Guide: https://docs.atmosys.com/guide/javascript-sdk
- Examples: https://docs.atmosys.com/examples/basic-usage

Use simple technologies (Node.js + Express + Leaflet map). Focus on getting a
working prototype first - advanced features can be added later.
```
