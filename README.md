# EchoCall MCP server

The official MCP (Model Context Protocol) server of [EchoCall](https://echocall.de/en/mcp), the platform for AI phone and chat agents. It connects ChatGPT, Claude, Cursor, VS Code, Claude Code and any other MCP client to your EchoCall workspace. Your AI app can then review calls and chats, adjust your voice and chat agents, keep their knowledge current, manage phone numbers and prepare call campaigns, all in plain sentences.

This is a hosted (remote) server. There is nothing to install: you add one URL to your AI app and sign in to EchoCall in your browser.

| | |
| --- | --- |
| Server URL | `https://hub.echocall.de/mcp` |
| Transport | Streamable HTTP |
| Sign-in | OAuth with PKCE in the browser, or an EchoCall API key as a bearer token |
| Access levels | Read only, or read and change |
| Tools | Every function of the EchoCall API v1 as a tool, 168 tools in 17 areas |
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
| `agents` | 9 | Create and edit voice agents: greeting, instructions, voice, language |
| `chatbots` | 9 | Web chat agents and their chat widget |
| `conversations` | 6 | Calls and chats with transcripts, from the phone, the website chat and WhatsApp |
| `analytics` | 4 | Call counts, durations and agent performance per day, week or agent |
| `knowledge` | 8 | Add website pages and other sources to an agent's knowledge, refresh or remove them |
| `voices` | 2 | The EchoCall voice library |
| `phonenumbers` | 10 | Search numbers by country, buy them and assign them to agents |
| `batchcalling` | 7 | Create, review, start or cancel outbound call campaigns |
| `tickets` | 4 | Support tickets |
| `webhooks` | 7 | Event notifications for your own systems |
| `integrations` | 15 | Calendar and contact center integrations of your agents |
| `billing` | 7 | Usage, invoices and plans |
| `users` | 3 | Your profile |
| `notifications` | 3 | Your notification inbox |
| `utilities` | 2 | Service health and localization helpers |
| `reseller` | 66 | Customer accounts, credits and branding, for reseller accounts only |
| `provisioning` | 6 | Account lifecycle hooks, for reseller accounts only |

Example requests:

- "How many calls did we get yesterday, and what were they about?"
- "Add to the greeting that we are closed on December 24."
- "Add our new pricing page to the knowledge of the Reception agent."
- "Set up a campaign for tomorrow's appointment reminders, but do not start it yet."

Every tool tells your AI app whether it only reads. Irreversible tools and tools that cost money, such as buying a number, say so at the start of their description.

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
