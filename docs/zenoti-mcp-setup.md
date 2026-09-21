# Zenoti MCP integration

Connects Claude to your Zenoti salon/spa account (bookings, guests, invoices,
sales reports) via the community MCP server
[`tacit-code/zenoti-mcp-server`](https://github.com/tacit-code/zenoti-mcp-server)
(MIT license, published to npm as `zenoti-mcp-server`).

## Why this server

Reviewed the source before wiring it up: it only calls Zenoti's own API
(`https://api.zenoti.com` by default), sends your key as an `Authorization`
header, has no telemetry and no other outbound calls, and its write-path
retry logic is conservative (never retries a write on ambiguous failure, to
avoid double-booking or double-charging a guest). It's a small,
single-maintainer project — solid code, but not vendor-endorsed by Zenoti,
so treat it as any other third-party integration.

## 1. Get your Zenoti API key

You need dashboard admin access (which you have) — this step can't be done
on your behalf, since it requires your live login session:

1. Log into Zenoti → **Admin → Settings → Apps**
2. Create a **backend application** — this issues an API key
3. Copy the key

## 2. Configure credentials

```bash
cp .env.example .env
```

Fill in `.env`:

```
ZENOTI_API_KEY=<your key>
ZENOTI_API_URL=https://api.zenoti.com
ZENOTI_CENTER_ID=            # leave blank for now
```

## 3. Find your center ID

Once the key works, ask Claude to run the `zenoti-centers-list` tool (after
step 4) to get your center GUID(s), then add it to `ZENOTI_CENTER_ID` in
`.env` so you don't have to pass `center_id` on every call.

## 4. Register the MCP server with Claude

This repo ships a project-scoped `.mcp.json` that Claude Code picks up
automatically when you open this repo — it runs the server via
`npx -y zenoti-mcp-server` and reads `ZENOTI_API_KEY` / `ZENOTI_API_URL` /
`ZENOTI_CENTER_ID` from your shell environment (export the values from
`.env`, or use a tool like `direnv`/`dotenv-cli`).

If instead you're using **Claude Desktop** or **claude.ai** rather than
Claude Code locally, register it there instead:

- **Claude Desktop**: add the same block from `.mcp.json` to your Desktop
  config (`claude_desktop_config.json`), with the literal key values instead
  of `${...}` placeholders.
- **Claude Code CLI**, from anywhere:
  ```bash
  claude mcp add zenoti -- npx -y zenoti-mcp-server
  claude mcp env zenoti ZENOTI_API_KEY=<your key> ZENOTI_API_URL=https://api.zenoti.com
  ```
- **claude.ai (web)**: this server runs over stdio (a local process), not
  as a hosted HTTP/SSE endpoint, so it can't be added as a claude.ai custom
  connector as-is — it needs Claude Desktop or Claude Code running on a
  machine you control. Say the word if you want it deployed as a hosted
  remote MCP server instead (e.g. on a small VPS), which *would* work with
  claude.ai connectors.

## 5. Start read-only

The server also exposes write tools (booking, rescheduling, invoice/payment
processing, guest profile edits). Until you've watched it operate safely
against your real account, treat write actions as something you review
before confirming — don't let an automated flow book, cancel, or charge
guests unattended. Read tools (reports, guest lookup, appointment/service
lists) are safe to use freely for the marketing analysis use case.
