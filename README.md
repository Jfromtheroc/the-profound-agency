# The Profound Agency MCP Server

A hosted MCP server for buying press. It gives an AI agent direct access to The Profound Agency's network of 1,600+ publications: search placements by price and authority, price a set of them, build a plan for a budget, and open an order for a human to pay. It can also request paid-media quotes and run AI-visibility checks.

No API key, no account, no signup. Point your client at the endpoint and go.

- **Endpoint:** `https://theprofound.agency/api/mcp/` (Streamable HTTP, stateless, no auth)
- **Docs:** https://theprofound.agency/mcp/
- **Manifest:** https://theprofound.agency/.well-known/mcp.json

This repository holds the registry metadata only. The server itself runs on theprofound.agency.

## Who it's for

- Founders and marketers who want to plan and price PR from inside Claude, Cursor or any MCP client
- Agencies building agents that quote press placements for their clients
- Anyone who wants to know whether AI assistants can find and cite their website

## Connect

Add this to your MCP client config:

```json
{
  "mcpServers": {
    "profound-agency": {
      "type": "http",
      "url": "https://theprofound.agency/api/mcp/"
    }
  }
}
```

Keep the trailing slash on the URL.

**Claude Code:**

```bash
claude mcp add --transport http profound-agency https://theprofound.agency/api/mcp/
```

## Tools

24 tools, 22 of them read-only. The ones you'll use most:

| Tool | What it does |
| --- | --- |
| `search_placements` | Search the network by price, Domain Authority, Domain Rating, category, region, turnaround, Google indexing and AI-crawler readiness. |
| `quote_placements` | Price a set of placements exactly as checkout would, fees included. Returns a link that opens the store with those placements in the cart. Reserves nothing. |
| `plan_placements` | Give it a goal, audience and budget; get back a recommended set of publications, already quoted and inside budget. |
| `submit_campaign_brief` | Ask for a quote on a paid media campaign (display, CTV, social, search, audio, out-of-home). A person prices it and replies. Buys nothing. |
| `quick_visibility_check` | An instant check of five AI-visibility basics for any site: AI crawlers in robots.txt, llms.txt, structured data, title and description. |
| `request_audit` | Request the full, free AI-visibility audit, scored out of 100. A person runs it and replies by email. |

The rest cover publication detail and comparisons, categories, advertising channels and restricted-category rules, meeting availability, order status, and the client content workflow. The full list with descriptions is in the [manifest](https://theprofound.agency/.well-known/mcp.json) and on the [docs page](https://theprofound.agency/mcp/).

## Agents can't spend money

The server is built so an agent can do the research and the paperwork, but never the paying.

- No payment method is reachable through any tool.
- `create_order` opens an unpaid order and returns a payment link. Nothing happens until a human opens that link and pays.
- Unpaid orders are deleted automatically after 72 hours.
- Quotes and plans reserve nothing and commit nobody.

## About

The Profound Agency (Profound Agency LLC) is a visibility agency in Hillsborough, New Jersey.

- Website: https://theprofound.agency
- MCP docs: https://theprofound.agency/mcp/
- Email: theprofoundagency@gmail.com
- Phone: +1-908-448-4001
