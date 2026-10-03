---
repo_key: ableton-live-mcp-server
aliases: []
---

# ableton-live-mcp-server

A Python bridge that exposes Ableton Live controls through the Model Context Protocol, a tool interface for compatible clients. A separate daemon translates local TCP requests into Open Sound Control messages for AbletonOSC, an external Ableton Live control script.

## Components

| Component | Path | What it is | Surfaces | Stack |
|---|---|---|---|---|
| mcp server | `mcp_ableton_server.py` | FastMCP tool server that sends commands to the local OSC daemon. | api, resident | python, mcp |
| osc daemon | `osc_daemon.py` | Async TCP listener that forwards commands to AbletonOSC over UDP and returns responses. | api, resident | python |

## Relationships and shared configuration

An MCP client starts the tool server over standard input and output. The server connects to the daemon on loopback port 65432. The daemon sends OSC to port 11000 and receives responses on port 11001. Both components share the Python dependencies in `pyproject.toml` and `uv.lock`.

## Limits

Ableton Live and AbletonOSC are external prerequisites, not repository components. The daemon must run separately; the MCP entrypoint does not start it. Connection defaults live in the Python source rather than a shared configuration file.
