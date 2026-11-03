# Makernice plugin

Generate Seedance, Kling, Wan and MiniMax videos and Seedream and Qwen images with [Makernice](https://makernice.com) from Claude Code and other agents. The plugin connects your agent to the Makernice remote MCP server and adds four skills that guide the agent through pricing, generating and fetching results.

## What it calls

- **Remote service**: `https://mcp.makernice.com/mcp` (MCP over HTTP), run by Makernice. Your prompts, the image links you provide and the job parameters are sent to Makernice to price and run generation jobs. See the [privacy policy](https://makernice.com/privacy/) and [terms](https://makernice.com/terms/).
- **No other services**. The plugin contains no code that runs on your machine; it only holds the server address and the skill instructions.
- **Connecting**: the first time you use it, approve the connection on the Makernice page that opens in your browser (in Claude Code, run `/mcp` and choose `makernice`). Nothing about your Makernice account is stored in this repository.

## Pricing

- Prices are in **USD** and are deducted from your prepaid Makernice balance. The live price list is at [makernice.com/pricing](https://makernice.com/pricing/).
- Every job is priced before it runs. The agent shows you the price, and the job is refused if the price is higher than the cap you approved (`max_cost_usd`).
- **Failed jobs are not charged**: the held amount is released in full. Queued jobs can be canceled for a full release. If a finished output is blocked by output moderation for a policy violation, the job is still charged; you can contact support for a manual review. See [failed generations](https://makernice.com/pricing/failed-generations/).
- Each connection has a per-job limit and the account has a daily limit, both shown by `get_balance`.

## Skills

| Skill | Use it for |
|---|---|
| `makernice-setup` | Check the connection, balance and limits, and make a first low-cost test video. |
| `product-video` | Product and e-commerce clips: mode, prompt writing, aspect ratio and resolution. |
| `trend-remix` | Turn your photos into a video with a trend template. |
| `cost-planner` | Plan models, resolutions and durations that fit a budget, without generating anything. |

## Tools provided by the server

`list_models`, `estimate_cost`, `generate`, `check_job`, `cancel_job`, `list_trends`, `get_balance`, `get_topup_link`.

## Install

Claude Code:

```
/plugin marketplace add makernice/makernice-plugin
/plugin install makernice@makernice
```

Cursor: copy this repository to `~/.cursor/plugins/local/makernice/`, then run Developer: Reload Window.

Gemini CLI:

```
gemini extensions install https://github.com/makernice/makernice-plugin
```

Hermes Agent: install and enable the plugin, then add the server to `~/.hermes/config.yaml` with `auth: oauth` so Hermes connects your Makernice account through the browser. The browser step uses a localhost callback, so run it on the machine where your browser is.

```
hermes plugins install makernice
hermes plugins enable makernice
```

```yaml
mcp_servers:
  makernice:
    url: "https://mcp.makernice.com/mcp"
    auth: oauth
```

LobeHub: add Makernice from the LobeHub MCP market.

Skills only, for other agents:

```
npx skills add makernice/makernice-plugin
```

The skills need the Makernice MCP server. If your agent does not install it from `.mcp.json`, add `https://mcp.makernice.com/mcp` as a remote MCP server in its settings.

## License

MIT
