# EchoCall MCP server

[![mcptry](https://mcptry.com/badge/de.echocall/echocall)](https://mcptry.com/servers/de.echocall/echocall)

The official MCP (Model Context Protocol) server of [EchoCall](https://echocall.de/en/mcp), the platform for AI phone and chat agents. It connects ChatGPT, Claude, Cursor, VS Code, Claude Code and any other MCP client to your EchoCall workspace. Your AI app can then review calls and chats, adjust your voice and chat agents, keep their knowledge current, manage phone numbers and prepare call campaigns, all in plain sentences.

This is a hosted (remote) server. There is nothing to install: you add one URL to your AI app and sign in to EchoCall in your browser.

| | |
| --- | --- |
| Server URL | `https://hub.echocall.de/mcp` |
| Transport | Streamable HTTP |
| Sign-in | OAuth with PKCE in the browser, or an EchoCall API key as a bearer token |
| Access levels | Read only, or read and change |
| Tools | Built from the EchoCall API v1: 168 tools in 18 areas, 254 tools in 20 areas for reseller accounts |
| MCP Registry | `de.echocall/echocall` |
| Price | Included in every EchoCall plan, the free starting credit counts (14 days, no credit card) |

Product page: [echocall.de/en/mcp](https://echocall.de/en/mcp) (German: [echocall.de/mcp](https://echocall.de/mcp))

## Connect

On first use your AI app opens EchoCall in the browser. Sign in, choose **Read only** or **Read and change**, and confirm. Your login details never reach the AI app.

### ChatGPT

Add a custom MCP server under **Plugins** and enter `https://hub.echocall.de/mcp`. ChatGPT currently offers custom MCP servers on the web with Business, Enterprise and Edu.

### Claude

Add a custom connector under **Connectors** and enter `https://hub.echocall.de/mcp`. This works on every Claude plan.

### Claude Code

```bash
claude mcp add --transport http echocall https://hub.echocall.de/mcp
```

Then sign in with `/mcp`.

### Cursor

Add EchoCall to `.cursor/mcp.json` in your project, or to `~/.cursor/mcp.json` for all projects:

```json
{
  "mcpServers": {
    "echocall": {
      "url": "https://hub.echocall.de/mcp"
    }
  }
}
```

### VS Code

Add EchoCall to `.vscode/mcp.json` in your project and start the server from there:

```json
{
  "servers": {
    "echocall": {
      "type": "http",
      "url": "https://hub.echocall.de/mcp"
    }
  }
}
```

### Other clients and API keys

Any client that speaks MCP over Streamable HTTP works. Clients without OAuth can send an EchoCall API key instead. Create the key in the hub under Developer and send it as a header:

```
Authorization: Bearer eck_live_...
```

The key carries the same rights as in the EchoCall API.

### Fewer tools

Append `?tags=` to the URL and EchoCall only offers those areas, for example:

```
https://hub.echocall.de/mcp?tags=agents,conversations
```

## What your AI app can do

| Area (`?tags=` value) | Tools | What it covers |
| --- | ---: | --- |
| `agents` | 9 | Create and edit voice agents: greeting, instructions, voice, language and the integrations they use |
| `chatbots` | 13 | Web chat agents, their chat widget, embed code and integrations |
| `conversations` | 6 | Calls and chats with transcripts, reply to a live chat and close it |
| `analytics` | 5 | Dashboard overview, calls and durations per day, voice and chat agent performance |
| `knowledge` | 15 | Add website pages, files and other sources to the knowledge of voice and chat agents, refresh, sync or remove them |
| `voices` | 3 | The EchoCall voice library and voice models |
| `phonenumbers` | 16 | Search and buy numbers, numbers available right away, verification, renewal and assignment to agents |
| `batchcalling` | 7 | Create, review, start or cancel outbound call campaigns |
| `tickets` | 5 | Open, answer and close support tickets |
| `webhooks` | 7 | Event notifications for your own systems |
| `integrations` | 20 | Calendar and contact center integrations of your agents, bookings and permissions |
| `billing` | 22 | Balance and top-ups, invoices, payment methods, plans, subscriptions, orders and usage |
| `team` | 10 | Team members and invites, live chat agents and their status |
| `presence` | 10 | AI avatar Presence: devices, commands, live sessions and usage |
| `developer` | 8 | API keys, API request logs and the AI apps connected to your workspace |
| `users` | 5 | Your profile, billing address, usage and limits |
| `notifications` | 5 | Your notification inbox and product announcements |
| `utilities` | 2 | Service health and localization helpers |
| `reseller` | 80 | Customer accounts, plans, credits, invoices, phone numbers, pricing, branding and email, for reseller accounts only |
| `provisioning` | 6 | Account lifecycle hooks, for reseller accounts only |

Example requests:

- "How many calls did we get yesterday, and what were they about?"
- "Add to the greeting that we are closed on December 24."
- "Add our new pricing page to the knowledge of the Reception agent."
- "Set up a campaign for tomorrow's appointment reminders, but do not start it yet."

Every tool tells your AI app whether it only reads. Irreversible tools and tools that cost money, such as buying a number, say so at the start of their description and only run after a confirmation: EchoCall first answers with a confirmation request, and your AI app has to ask you for a clear yes. A connection can run at most 10 actions that cost money per hour.

## Security

- **No login details in the AI app.** Sign-in runs through OAuth with PKCE directly at EchoCall. The AI app only receives an access token you can revoke at any time.
- **Read only as its own level.** With read only, the AI app cannot create, change or delete anything.
- **Every connection in view.** The hub lists each connection under Developer, Connected AI apps, with its access level, approval date and last use. Disconnect in one click and access ends immediately.
- **An email for every new connection** goes to the workspace owner.
- **Team roles still apply.** Members can approve at most what their role allows. IP and domain allowlists apply to AI apps as well.

Important: with read and change, an AI app can also delete agents, buy phone numbers and start campaigns, which can incur costs. When in doubt, choose read only. Whatever your AI app reads through EchoCall is processed by the provider of that AI app under its own terms.

## Requirements

An active EchoCall plan. The free starting credit counts, so you can connect right after signing up at [hub.echocall.de](https://hub.echocall.de) and try it for 14 days, no credit card required.

## Links

- Product page: [echocall.de/en/mcp](https://echocall.de/en/mcp)
- Guide: [Add an MCP server to ChatGPT and Claude](https://echocall.de/en/blog/mcp-server-chatgpt-claude)
- API documentation: [echocall.de/docs](https://echocall.de/docs)
- OpenAPI specification: [hub.echocall.de/openapi.json](https://hub.echocall.de/openapi.json)
- Questions: [team@echocall.de](mailto:team@echocall.de)

## About this repository

This repository documents the hosted EchoCall MCP server and holds its [`server.json`](server.json) for the official MCP Registry. The server itself runs as part of EchoCall Hub, so there is no code to install or run here.

## Deutsch

EchoCall MCP ist der offizielle MCP-Server von EchoCall unter `https://hub.echocall.de/mcp`. Er verbindet ChatGPT, Claude, Cursor, VS Code und Claude Code mit Ihrem EchoCall-Workspace. Die KI-App kann dann Anrufe, Chats und Auswertungen lesen und, wenn Sie es erlauben, Agenten, Wissen, Rufnummern und Kampagnen für Sie bearbeiten. Sie melden sich einmal im Browser bei EchoCall an und wählen Nur lesen oder Lesen und ändern. EchoCall MCP ist in jedem Paket enthalten, das kostenlose Startguthaben zählt (14 Tage, ohne Kreditkarte).

Alle Details und die Einrichtung Schritt für Schritt: [echocall.de/mcp](https://echocall.de/mcp)
