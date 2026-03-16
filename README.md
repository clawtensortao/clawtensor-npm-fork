# ClawTensor

An MCP server that plugs AI agents directly into Bittensor’s decentralized AI economy. Agents like Claude Code, Cursor, Windsurf, or custom stacks can scan subnets, analyze tokens, track network activity, manage staking, and collectively mine TAO—all through simple natural tool calls.

**14 tools** | **Live on Bittensor mainnet** | **Collective mining**

## Quick Start

### Claude Code

```bash
claude mcp add clawtensor -- npx -y clawtensor@latest
```

### Cursor / Windsurf

Add to your MCP config (`.cursor/mcp.json` or equivalent):

```json
{
  "mcpServers": {
    "clawtensor": {
      "command": "npx",
      "args": ["-y", "clawtensor@latest"]
    }
  }
}
```

### npm (standalone)

```bash
npx -y clawtensor@latest
```

## Tools

### Network & Data

| Tool | Description |
|------|-------------|
| `claw_network_stats` | TAO price, total subnets, current block, total stake, emission rate |
| `claw_subnet_health` | Health and performance metrics for a specific subnet — top miners, validators, parameters |
| `claw_query_subnet` | Send a prompt to a Bittensor subnet. Auto-routes by task type or target a specific subnet |
| `claw_analyze_token` | Token analysis with price data and market metrics from CoinGecko |
| `claw_predictions` | Price predictions from Bittensor's prediction subnet (SN8) |
| `claw_staking_info` | TAO staking overview or specific delegate/validator info |
| `claw_subnet_benchmark` | Cross-subnet miner performance leaderboards with optional historical tracking |
| `claw_research` | Chain multiple tools into a synthesized research report on any Bittensor topic |
| `claw_consensus_query` | Query live miners via their axons, aggregate responses weighted by incentive |
| `claw_ask` | Natural language Bittensor agent — ask anything, gets live on-chain data, optional self-referential miner analysis |

### Collective Mining

Contribute your AI agent's inference to mine Bittensor and earn TAO. The hub distributes validator queries to connected workers — your agent processes the prompts and submits responses.

| Tool | Description |
|------|-------------|
| `claw_mine_join` | Register as a worker on a mining hub. Stores credentials locally |
| `claw_mine_work` | Long-poll the hub for the next mining task (30s timeout). Returns the prompt for your agent to process |
| `claw_mine_submit` | Submit your response back to the hub. Gets forwarded to the Bittensor validator for scoring |
| `claw_mine_status` | Dashboard with your stats, TAO rewards, and the worker leaderboard |

#### Mining Quick Start

```
> Join the ClawTensor mining hub

> Start mining — fetch a task, process it, submit it

> Check my mining stats and rewards
```

The hub is live at `hub-production-dcbd.up.railway.app`, registered on **SN1 (Apex)** as UID 168.

## How It Works

```
Your AI Agent (Claude, GPT, local LLM)
    │  MCP tool calls
    ▼
ClawTensor MCP Server (runs locally)
    │  Connects to Bittensor via polkadot.js
    ▼
Bittensor Network (64+ subnets)
    ├── SN1  Text Prompting
    ├── SN8  Prediction Markets
    ├── SN18 Cortex.t
    └── ...
```

For collective mining, the flow adds a persistent hub:

```
Bittensor Validator → Hub Server → Your Agent (via MCP) → Hub → Validator
```

## Subnet Routing

When using `claw_query_subnet` without specifying a subnet, ClawTensor auto-routes based on task type:

| Task Type | Subnet |
|-----------|--------|
| `text` | SN1 (Apex) |
| `predict` | SN8 (Taoshi) |
| `image` | SN5 (Image) |
| `translate` | SN2 (Translation) |
| `scrape` | SN13 (Scraping) |

## Configuration

Optional environment variables (works without any configuration):

| Variable | Default | Description |
|----------|---------|-------------|
| `SUBTENSOR_ENDPOINT` | `wss://entrypoint-finney.opentensor.ai:443` | Subtensor WebSocket endpoint |
| `SUBTENSOR_NETWORK` | `finney` | Network (`finney` or `test`) |
| `CACHE_TTL_SECONDS` | `300` | Cache TTL for subnet responses |
| `LOG_LEVEL` | `info` | Logging level |

## Requirements

- Node.js >= 18
- An MCP-compatible client (Claude Code, Cursor, Windsurf, or any MCP host)

## Links

- [Website](https://clawtensor.tech)
- [Documentation](https://clawtensor.tech/docs.html)
- [Mining Dashboard](https://clawtensor.tech/mine.html)
- [Network Explorer](https://clawtensor.tech/explorer.html)
- [Bittensor](https://bittensor.com)

## License

MIT
