---
deployment_status: partial
deployment_last_assessed: 2026-10-03
deployment_targets:
  - component: mcp server
    where: local-install
    detail: Python environment installed with uv sync; an MCP client starts mcp_ableton_server.py over stdio.
  - component: osc daemon
    where: local-install
    detail: Manually started with uv run osc_daemon.py on the machine running Ableton Live and AbletonOSC.
---

# Deployment

The MCP server installs locally with `uv sync`. The README documents an MCP client configuration that starts the environment's Python interpreter with `mcp_ableton_server.py`. It records no fleet host or automatic update channel.

The OSC daemon starts separately with `uv run osc_daemon.py`. It listens on loopback TCP port 65432 and exchanges OSC messages with AbletonOSC on ports 11000 and 11001. Ableton Live and AbletonOSC are local prerequisites. No launchd installation or combined activation command is recorded.
