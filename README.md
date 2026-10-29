# DemandBird for Claude Code

Write, schedule and publish social posts in your own voice, and read your
analytics, without leaving Claude Code.

DemandBird runs a hosted MCP server, so this plugin adds no local process and
runs nothing on your machine. It points Claude Code at
`https://app.demandbird.com/mcp`, and you sign in to DemandBird in your browser
the first time Claude Code uses it.

## What you get

Once it is connected, you can ask Claude Code things like:

- "Draft a LinkedIn post about the pricing change". It is written by
  DemandBird's Voice Engine, so it sounds like you and carries your brand
  positioning.
- "Make that shorter and less salesy". This revises the same draft and keeps
  its images.
- "Schedule it for Tuesday at 9am" / "Put it in the queue."
- "How did last week's posts do?" / "What's my best time to post on LinkedIn?"
- "Publish 123". This returns a link you open in DemandBird, where you press
  the button yourself. Claude cannot publish on your behalf.

Read-only tools are annotated as such, so analytics and `list_*` calls do not
ask you to confirm every time.

## What it sends and where

The plugin contains only this README, a licence and two small configuration
files. It connects to one server, `https://app.demandbird.com/mcp`, run by
DemandBird. What you ask Claude Code to do with DemandBird (post text, the
post you're asking about, analytics questions) is sent there. Sign-in uses
OAuth: Claude Code opens DemandBird's sign-in page in your browser, and
DemandBird never sees your Claude credentials. The plugin reads no files or
environment variables on your machine.

## Setup

### 1. Install the plugin

Claude Code installs plugins from a *marketplace*, so add this repo as one
first, then install from it:

```
/plugin marketplace add Wildfront/demandbird-claude-plugin
/plugin install demandbird@demandbird-claude-plugin
```

Run both lines inside a Claude Code session.

### 2. Sign in

The first time you use a DemandBird tool, Claude Code opens DemandBird's
sign-in page in your browser. Sign in, choose the DemandBird account Claude
Code may use, and press **Allow**. You can also start this yourself: run
`/mcp`, pick **demandbird** and choose to authenticate.

You need a paid DemandBird plan (Pro and up). To see or remove the connection
later, go to **Settings → Connected apps** in DemandBird
(`https://app.demandbird.com/oauth/grants`).

### 3. Check it

Ask Claude Code "what DemandBird tools do you have?". It should list drafting,
scheduling and analytics tools.

## Multiple accounts

The connection belongs to the DemandBird account you picked on the Allow
screen. To use a different account, run `/mcp`, pick **demandbird**, clear
its sign-in, and sign in again choosing the other account.

If you run an agency, each client is a *workspace* inside the account. Ask
Claude Code to "list my workspaces" and "switch to <client>". Drafts, channels
and analytics follow the workspace you picked.

## Troubleshooting

**The sign-in page doesn't open.** Run `/mcp`, pick **demandbird** and choose
to authenticate.

**"DemandBird's MCP server needs an active DemandBird subscription."** The
account you picked has no paid plan. Sign in again and pick another account,
or upgrade.

**No tools appear.** Run `/mcp` in Claude Code to see the server's connection
state and any error it reported.

## Support

- Docs: https://demandbird.com/docs/mcp/
- Email: hello@demandbird.com

## License

MIT
