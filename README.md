# Feb 18 — Custom OpenClaw Setup

This repo is a custom OpenClaw configuration focused on OpenRouter routing, Kimi K2.5, and budget-friendly fallbacks. It keeps setup docs and examples in one place and avoids hardcoding any secrets.

## Quick start (OpenRouter)

```bash
export OPENROUTER_API_KEY="your_key_here"
openclaw onboard \
  --auth-choice apiKey \
  --token-provider openrouter \
  --token "$OPENROUTER_API_KEY"
```

If you prefer a local env file, copy the example:

```bash
cp .env.example .env
```

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

## Routing vs pinned

- `openrouter/openrouter/auto` dynamically selects models based on OpenRouter routing.
- Direct model IDs (for example `openrouter/moonshotai/kimi-k2.5`) pin a specific model.

## Where to look

- Docs and config examples live in `docs/`.
- This repo does not store any API keys. Use environment variables only.

## Safety

- Never commit `OPENROUTER_API_KEY`.
- If you use a `.env` file locally, keep it untracked.
- Pricing and credits can change; verify current rates in your OpenRouter dashboard before relying on any model.
