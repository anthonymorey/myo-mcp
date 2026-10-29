# Money You're Owed: MCP server

<img src="assets/logo-512.png" alt="Money You're Owed logo" width="96">

A free, public, read-only [Model Context Protocol](https://modelcontextprotocol.io) server. It answers US consumer money-recovery questions with facts cited to the original statute, regulation or official agency page. Each answer links to a free guide on moneyyoureowed.com.

This repository only holds the listing metadata (`server.json`) and documentation. The server is hosted, so there's nothing to install or run.

- **Setup and docs:** https://moneyyoureowed.com/connect
- **Official MCP Registry name:** `com.moneyyoureowed/catalog`

## Connect

| Client | Endpoint |
| --- | --- |
| Claude, Gemini and other MCP clients | `https://mcp.moneyyoureowed.com/mcp` |
| ChatGPT app | `https://mcp.moneyyoureowed.com/chatgpt/mcp` |

- **Transport:** Streamable HTTP (MCP protocol version `2025-06-18`), returning a single JSON response.
- **Auth:** none. No API key, no OAuth, no account.
- **Claude users:** add "Money You're Owed" from the Claude connectors directory. You don't need to paste a URL.

Example client config:

```json
{
  "mcpServers": {
    "moneyyoureowed": {
      "type": "streamable-http",
      "url": "https://mcp.moneyyoureowed.com/mcp"
    }
  }
}
```

## Tool

The server exposes one tool, `answer_money_question`.

| | |
| --- | --- |
| Input | `question` (string, required): the consumer's question in plain language, e.g. "my landlord kept my security deposit" |
| Output | Source-cited facts, plus a link to a free resource on moneyyoureowed.com |
| Annotations | `readOnlyHint: true`, `destructiveHint: false`, `openWorldHint: false` |

The tool is a read-only lookup. It doesn't collect personal data, make payments, create accounts or change anything. The server has no other tools, resources or prompts.

## Topics covered

- Withheld security deposits (state deadlines, allowed deductions, small claims)
- Airline refunds for cancelled or changed flights
- Unclaimed property held by US states
- Ticket-resale refunds
- Frozen fintech accounts (Cash App, Chime and similar)
- Gig-worker deactivation, paid-seat refunds and other consumer refund disputes

## What it turns down

Both endpoints refuse the same things.

- **Medical, prescription and health-insurance questions**, including GLP-1 drugs, Medicare and Medicare Advantage, pharmacy refunds and health-insurance denials. These get this reply: "This app does not cover medical, prescription or health-insurance questions. It covers security deposits, airline refunds and unclaimed property." It never gives medical advice.
- **Debt, credit and investing:** questions like debt consolidation or which funds to buy get this reply: "This service covers money owed to you (deposits, refunds, unclaimed property), not debt, credit or investing." It does not offer debt relief or credit repair.
- **Anything it has no verified fact for:** it says so and doesn't guess.

## Disclaimer

Every answer from both endpoints ends with this line:

> General information only, not legal or financial advice. Rules vary by state and by your facts, and no outcome or refund is guaranteed.

The server doesn't provide legal representation and never acts on your behalf.

## Privacy

There's no account and no sign-in. Questions are matched in memory and aren't stored. See the privacy policy at https://moneyyoureowed.com/privacy.

## Publisher

Money You're Owed is a trading name of **Aussie-AI Ltd** (England and Wales).

Contact: hello@moneyyoureowed.com

## License

The files in this repository (README, `server.json`, logo) are released under the MIT License. See [LICENSE](LICENSE). The hosted service and its content are not covered by this license.
