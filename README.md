# DemandBird for Claude Code

Write, schedule and publish social posts in your own voice, and read your
analytics, without leaving Claude Code.

DemandBird runs a hosted MCP server, so this plugin adds no local process. It
points Claude Code at `https://app.demandbird.com/mcp` and authenticates with an
API token you mint yourself.

## What you get

Once it is connected, you can ask Claude Code things like:

- "Draft a LinkedIn post about the pricing change" — written through DemandBird's
  Voice Engine, so it sounds like you and carries your brand positioning.
- "Make that shorter and less salesy" — revises the same draft, keeping its images.
- "Schedule it for Tuesday at 9am" / "Put it in the queue."
- "How did last week's posts do?" / "What's my best time to post on LinkedIn?"
- "Publish 123" — returns a link you open in DemandBird and press the button
  yourself. Claude cannot publish on your behalf.

Read-only tools are annotated as such, so analytics and `list_*` calls do not
ask you to confirm every time.

## Setup

### 1. Install the plugin

Claude Code installs plugins from a *marketplace*, so add this repo as one
first, then install from it:

```
/plugin marketplace add Wildfront/demandbird-claude-plugin
/plugin install demandbird@demandbird-claude-plugin
```

Run both lines inside a Claude Code session.

### 2. Mint an API token

In DemandBird, go to **Settings → API Tokens** (`https://app.demandbird.com/api_tokens`)
and create a token. Copy it when it is shown — it is only shown once.

Grant the token the permissions you want Claude Code to have. A token can never
hold a permission you do not hold yourself.

### 3. Set the environment variable

```
export DEMANDBIRD_API_TOKEN="your-token-here"
```

Put that line in your shell profile (`~/.zshrc`, `~/.bashrc`) so it survives a
new terminal, then restart Claude Code.

On macOS, a safer home for it is the login keychain:

```
security add-generic-password -a "$USER" -s demandbird-api-token -w "your-token-here"
export DEMANDBIRD_API_TOKEN="$(security find-generic-password -a "$USER" -s demandbird-api-token -w)"
```

### 4. Check it

Ask Claude Code "what DemandBird tools do you have?" — it should list drafting,
scheduling and analytics tools.

## Multiple accounts

If you belong to more than one DemandBird account, the tools will ask you to
pick one. Two ways to answer:

- Ask Claude Code to "list my DemandBird accounts", then "switch to <name>".
  The choice sticks for the rest of the session.
- Or pin one account permanently by adding an `X-Account-Id` header to the
  server config, alongside `Authorization`:

  ```json
  {
    "mcpServers": {
      "demandbird": {
        "type": "http",
        "url": "https://app.demandbird.com/mcp",
        "headers": {
          "Authorization": "Bearer ${DEMANDBIRD_API_TOKEN}",
          "X-Account-Id": "acct_xxxxxxxxxxxx"
        }
      }
    }
  }
  ```

  Your account id is shown at the top of **Settings → API Tokens**.

If you run an agency, each client is a *workspace* inside the account. Ask
Claude Code to "list my workspaces" and "switch to <client>"; drafts, channels
and analytics follow the workspace you picked.

## Plan requirement

MCP access currently requires the **Business** plan. A token on a lower plan
authenticates fine, but the tools return a message saying the plan is needed.
The REST API is not affected.

## Troubleshooting

**"No API token supplied."** `DEMANDBIRD_API_TOKEN` is not set in the shell that
started Claude Code. Set it and restart.

**"API token has expired."** Mint a new one at Settings → API Tokens.

**No tools appear.** Run `/mcp` in Claude Code to see the server's connection
state and any error it reported.

## Support

- Docs: https://demandbird.com/docs/mcp/
- Email: hello@demandbird.com

## License

MIT
