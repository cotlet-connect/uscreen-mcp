# Uscreen MCP server for ChatGPT and Claude

Connect ChatGPT, Claude and other AI agents to Uscreen through Cotlet.dev. The Cloud Browser stays signed in to your Uscreen business account so your agent can work on people, content, sales and analytics screens. Uscreen has an official MCP server in beta, as reported on the integration page checked 20 November 2026.

## What you can ask

> What were my top 5 videos by watch time this month?

> Which videos have no description or no tags?

> How many new subscribers joined in the last 30 days, by plan?

> Export the People table as CSV for the yearly review.

> Rewrite the descriptions of the 3 newest videos. Save nothing yet.

## Connect Uscreen

Sign up at https://cotlet.dev/signup?app=uscreen, enable Uscreen and sign in at app.uscreen.tv in your Cloud Browser. Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1/connect`, then sign in with Cotlet.dev. No API key needed.

### Claude

Open Connectors, add a custom connector with `https://cotlet.dev/mcp/v1/connect`, then sign in to Cotlet.dev and allow access.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run the local MCP bridge

Python 3.10+, with no dependencies. Clone this repository, set your Cotlet.dev API key, then run:

```bash
export COTLET_API_KEY="your-key"
python3 uscreen_agent.py serve
```

This local stdio bridge lists seven browser helper tools: `uscreen_guide`, `uscreen_status`, `uscreen_open`, `uscreen_read`, `uscreen_click`, `uscreen_type` and `uscreen_close`.
It forwards calls to the hosted Cotlet.dev MCP server.
The hosted connection provides browser tools that work on the screens available to your Uscreen login.

Without a key, the local bridge can list its helpers; calls return setup instructions.

```bash
python3 uscreen_agent.py connect
python3 uscreen_agent.py guide
python3 uscreen_agent.py status
```

## Questions from Uscreen users

**Does Uscreen have an official MCP server or API?**

Uscreen has an official MCP server in beta for stores in the beta on paid plans above Starter using the New Website Editor. It reads analytics, CRM and catalog and edits catalog and CRM. The Publisher API is for stores on UscreenPlus with a key from Uscreen. These facts were checked on 20 November 2026. Use the official integrations when they cover your task.

**How do I connect Uscreen to ChatGPT or Claude?**

Sign up at https://cotlet.dev/signup?app=uscreen and sign in to app.uscreen.tv in your Cotlet Cloud Browser. Add https://cotlet.dev/mcp/v1/connect in your AI client and sign in to Cotlet.dev with OAuth.

**Which changes should I approve?**

Ask your agent to wait for your approval before it changes member access, a price or a video, or sends member messages. Review the result in Uscreen. Keep account billing, payouts and your Uscreen plan in your own hands.

**Is Cotlet.dev affiliated with Uscreen?**

No. Cotlet.dev is an independent service and is not affiliated with Uscreen.

## Integration details

[Uscreen tools and setup on Cotlet.dev](https://cotlet.dev/integrations/uscreen-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=uscreen)

---

More: https://cotlet.dev/integrations/uscreen-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=uscreen

Start free: https://cotlet.dev/signup?app=uscreen&utm_source=github&utm_medium=readme&utm_campaign=uscreen
