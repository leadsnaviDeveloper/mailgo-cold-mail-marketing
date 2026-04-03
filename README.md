# Mailgo Campaign Suite MCP Server

AI-powered cold email campaign management through Model Context Protocol (MCP).

## Overview

Mailgo Campaign Suite MCP Server connects your AI assistant directly to the [Mailgo](https://app.mailgo.ai) cold email platform. Through natural conversation, you can verify email addresses, claim pre-warmed mailboxes, launch campaigns, manage their lifecycle, and pull analytics — without touching any UI.

The server runs as a remote HTTP service. To connect your AI client, you only need a Mailgo API token and the server URL.

## What You Can Do

### Email Verification

Before sending, verify your contact list for deliverability. The AI will submit up to 1000 addresses in one batch and return them categorized:

- `valid` — safe to send
- `invalid` — bad address format or non-existent
- `domain_error` — domain unreachable or misconfigured
- `unknown` — inconclusive result
- `unchecked` — not processed within timeout

**Example prompt:** *"Verify these 200 email addresses before I create a campaign"*

---

### Free Mailbox

Claim a free pre-warmed sending mailbox from Mailgo (60-day validity, sender score 90+). Useful for getting started without configuring your own domain.

**Example prompt:** *"Claim a free mailbox for me to use as a sender"*

---

### Campaign Creation

Create a fully personalized cold email campaign in one step. The AI handles:

- Uploading the HTML email content
- Creating the campaign with your send schedule and daily limit
- Adding all recipient leads (with name, company, title, domain)
- Activating the campaign

**Personalization placeholders** available in subject and body:

| Placeholder | Availability |
|-------------|-------------|
| `#{name}` | Always (auto-derived from email prefix) |
| `#{email}` | Always |
| `#{company name}` | When `recipient_companies` is provided |
| `#{title}` | When `recipient_titles` is provided |
| `#{domain}` | When `recipient_domains` is provided |

> **Note:** Always provide the corresponding data list when using a placeholder. Unresolved placeholders render as blank gaps in the email.

**Example prompt:** *"Create a campaign to these 50 leads, send Mon–Fri 9am–6pm Shanghai time, limit 30 per day"*

---

### Campaign Management

Control your campaigns at any stage:

| Action | What it does |
|--------|-------------|
| `activate` | Start or resume a campaign |
| `pause` | Temporarily pause sending |
| `delete` | Remove a campaign |
| `list` | Browse all campaigns with optional name/status filter |
| `info` | Get full details of a specific campaign |

**Example prompt:** *"Pause my Q2 Outreach campaign"* / *"List all active campaigns"*

---

### Campaign Reports

Pull analytics at any granularity:

| Report type | Content |
|-------------|---------|
| `overview` | Totals: leads, sent, delivered, opened, replied, clicked, bounced + rates |
| `rounds` | Per-round breakdown for multi-sequence campaigns |
| `daily` | Day-by-day stats for a given date range |
| `replies` | Full reply list, optionally with message body content |

**Example prompt:** *"How is my campaign performing?"* / *"Show me all replies from campaign 12345 with the message content"*

---

## Getting Started

### Step 1 — Get Your API Token

1. Open [app.mailgo.ai](https://app.mailgo.ai) and sign up / log in
2. Click your profile in the bottom-left corner and select **Personal Tokens**
3. Click **Create Token**, then copy the generated token

### Step 2 — Connect Your AI Client

#### Claude Desktop / claude.ai

Claude connects to remote MCP servers through the UI, not a config file:

1. Open **Settings → Connectors**
2. Click **"+" → Add custom connector**
3. Enter the server URL: `https://mcp.leadsnavi.com/mcp`
4. Click **Advanced settings** and add a custom header:
   - Header name: `X-API-Key`
   - Header value: your token from Step 1
5. Click **Add** to save

#### Cursor

Add the following to your Cursor MCP configuration (`~/.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "mailgo": {
      "url": "https://mcp.leadsnavi.com/mcp",
      "headers": {
        "X-API-Key": "<YOUR_MAILGO_TOKEN>"
      }
    }
  }
}
```

#### Other MCP clients

For any MCP client that supports remote Streamable HTTP transport, configure:

- **URL**: `https://mcp.leadsnavi.com/mcp`
- **Header**: `X-API-Key: <YOUR_MAILGO_TOKEN>`

### Step 3 — Start Using It

Once connected, just talk to your AI assistant naturally:

```
"Verify these emails: alice@example.com, bob@example.com"
"Claim a free sending mailbox for me"
"Create a cold email campaign to my lead list"
"Show me the performance overview for campaign 98765"
"List all my paused campaigns"
```

---

## Support

- GitHub Issues: [leadsnavi-mcp-server/issues](https://github.com/netease-im/leadsnavi-mcp-server/issues)

---

Made with by the Leadsnavi Team
