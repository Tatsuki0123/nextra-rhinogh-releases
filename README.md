# Nextra for Rhino + Grasshopper

Let Claude (or any MCP client) build and edit Rhino 8 models and Grasshopper definitions. It uses six token-lean tools: `view`, `query`, `run`, `gh_edit`, `undo` and `memory`. Every edit can be undone.

**Requirements:** Windows, Rhino 8 (recent service release), Claude Desktop.

## Install (3 parts, all needed)

| # | Part | What it does | Where to get it |
|---|---|---|---|
| 1 | **Rhino plug-in** | runs a local server inside Rhino | Rhino Package Manager → search **`Nextra-RhinoGh`** |
| 2 | **Bridge** (`.mcpb`) | gives Claude the tools and connects them to Rhino | [Releases](../../releases/latest) → `nextra-rhinogh-<version>.mcpb` |
| 3 | **Skill** (`.zip`) | teaches Claude how to use the tools well | [Releases](../../releases/latest) → `nextra-rhinogh-skill.zip` |

### 1. Rhino plug-in
1. In Rhino, run `PackageManager`, search for `Nextra-RhinoGh` and click **Install**.
2. **Restart Rhino.**
3. Check that a small dot appears at the bottom-right of the Rhino window:
   - 🟢 green: Claude is connected
   - 🟠 amber: ready, waiting for Claude
   - 🔴 red: click it to restart the server

   Commands: `NextraOn`, `NextraOff`, `NextraFolder`, `Nextra`.

> No Package Manager access? Download the `.yak` from Releases and drag it onto the Rhino window, then restart Rhino.

### 2. Bridge (Claude Desktop)
1. Download `nextra-rhinogh-<version>.mcpb` from [Releases](../../releases/latest).
2. Double-click it, or in Claude Desktop go to **Settings → Extensions → Advanced settings → Install Extension…** and pick the file.
3. **Fully quit Claude Desktop** (also from the system tray) and open it again.
4. **nextra-rhinogh** should now be listed under your tools/connectors in a new chat.

### 3. Skill
1. Download `nextra-rhinogh-skill.zip` from [Releases](../../releases/latest).
2. In Claude, go to **Settings → Capabilities → Skills → Upload skill** and pick the zip. Do not unzip it.

### Try it
With Rhino open and the dot showing, ask Claude:

> Create a simple timber house in Rhino.

## Other MCP clients
- **Claude Code:** extract the `.mcpb` (it is a zip), then run `claude mcp add nextra-rhinogh -- node <folder>/server/index.js`.
- **Anything else:** run `node server/index.js` over stdio. It needs Node 18 or later and has no dependencies.

## Troubleshooting

| Symptom | Fix |
|---|---|
| `Unknown command: NextraOn` | The plug-in is not loaded. Restart Rhino after installing. Still missing? Run `PlugInManager`, find **Nextra.Host**, right-click → **Load**. |
| `Blocking plug-in Nextra.Host` | Usually happens after uninstalling and reinstalling in the same session. Close **all** Rhino windows and start Rhino again. |
| No dot in Rhino | Run `NextraOn`. |
| Claude says "Nextra isn't connected" / can't find the tools | The bridge (part 2) is missing. The skill alone has no tools. Install the `.mcpb` and fully restart Claude Desktop. |
| Claude says "Rhino is not reachable" | Rhino isn't running, or the dot is red (click it) or off (`NextraOn`). |
| Several Rhino windows open | Tell Claude which file to use, e.g. "use house.3dm". |
