# Exercise.com MCP server for ChatGPT and Claude

Connect Exercise.com to ChatGPT, Claude and other AI agents through Cotlet. Work with schedules, sessions, clients, messages and invoices in your own signed-in account. Cotlet is independent and not affiliated with Exercise.com. If Exercise.com offers an official API for your needs, we recommend it.

## What you can ask

> Show today’s schedule and who is booked.

> Add a session for the client, trainer and time I provide. Ask me before saving.

> Send the message I approve to the client I choose. Ask me before sending.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Claude

Add `https://cotlet.dev/mcp/v1` as a custom connector in Claude and sign in with Cotlet.dev. Follow the steps in your Cotlet console.

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

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Exercise.com tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers": {"exercise-com": {"command": "python3", "args": ["/absolute/path/to/exercise-com-mcp/exercise_com_agent.py", "serve"], "env": {"COTLET_API_KEY": "your-key"}}}}
```

Or with Docker:

```bash
docker build -t exercise-com-mcp .
docker run -i --rm -e COTLET_API_KEY exercise-com-mcp
```

Tools: `exercise_com_guide`, `exercise_com_status`, `exercise_com_open`, `exercise_com_read`, `exercise_com_click`, `exercise_com_type`, `exercise_com_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. Run from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 exercise_com_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 exercise_com_agent.py status    # is Exercise.com ready in your Cotlet.dev account
python3 exercise_com_agent.py guide     # Exercise.com screens and sign-in link
python3 exercise_com_agent.py read      # open Exercise.com, read the page, close the browser
python3 exercise_com_agent.py tools     # list Cotlet.dev tools
python3 exercise_com_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Exercise.com users

**How do I connect Exercise.com to ChatGPT or Claude?**

Sign up at cotlet.dev, log in to Exercise.com once in its Cloud Browser and add Cotlet to ChatGPT or Claude, following the steps in your console. No API key is needed. ChatGPT and Claude then work in your Exercise.com account through Cotlet, in their phone apps too.

**Can ChatGPT schedule a session in Exercise.com?**

ChatGPT adds the session for the client, trainer and time you choose on the Exercise.com calendar after you approve it.

**Can ChatGPT message a client in Exercise.com?**

ChatGPT writes or answers the message thread with the client you pick and sends it, by app or SMS, after you approve it.

**Does Exercise.com have an API?**

Yes, as a paid add-on: Exercise.com says "API access is an additional feature with variable pricing" and quotes it through your Account Representative (checked 11 Nov 2026). Cotlet needs no API add-on: it works through your own Exercise.com sign-in.

**Is Cotlet affiliated with Exercise.com?**

No. Cotlet is independent and not affiliated with Exercise.com.

## Find it on

- [Exercise.com on Cotlet](https://cotlet.dev/integrations/exercise-com-api-mcp-server)
- [All Cotlet packages](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/exercise-com-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=exercise-com

Request access: https://cotlet.dev/signup?app=exercise-com&utm_source=github&utm_medium=readme&utm_campaign=exercise-com
