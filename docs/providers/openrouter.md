---
summary: "Use OpenRouter's unified API to access many models in OpenClaw"
read_when:
  - You want a single API key for many LLMs
  - You want to run models via OpenRouter in OpenClaw
title: "OpenRouter"
---

# OpenRouter

OpenRouter provides a **unified API** that routes requests to many models behind a single
endpoint and API key. It is OpenAI-compatible, so most OpenAI SDKs work by switching the base URL.

## CLI setup

```bash
export OPENROUTER_API_KEY="your_key_here"
openclaw onboard --auth-choice apiKey --token-provider openrouter --token "$OPENROUTER_API_KEY"
```

## Config examples

Routing default (cost-aware):

```js
{
  agents: {
    defaults: {
      model: {
        primary: "openrouter/openrouter/auto",
        fallbacks: []
      }
    }
  }
}
```

Pinned model example (Kimi K2.5):

```js
{
  agents: {
    defaults: {
      model: {
        primary: "openrouter/moonshotai/kimi-k2.5",
        fallbacks: ["openrouter/openrouter/auto"]
      }
    }
  }
}
```

## Notes

- Model refs are `openrouter/<provider>/<model>`.
- For more model/provider options, see [/concepts/model-providers](/concepts/model-providers).
- OpenRouter uses a Bearer token with your API key under the hood.
