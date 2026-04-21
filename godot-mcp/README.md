# godot-mcp

One-click Cowork / Claude Code plugin for [@coding-solo/godot-mcp](https://github.com/Coding-Solo/godot-mcp) — a Model Context Protocol server that connects Claude to the Godot game engine.

## What it does

Exposes Godot as a set of tools Claude can call directly:

- **Editor & project control** — launch the Godot editor for a project, run projects in debug mode, stop running projects, capture stdout/stderr, list projects in a directory
- **Scene management** — create scenes with specific root node types, add nodes with custom properties, load sprites/textures into `Sprite2D`, export 3D scenes as `MeshLibrary` resources for `GridMap`, save scenes (including variants)
- **UID management** (Godot 4.4+) — get UIDs for files, update UID references by resaving resources
- **Inspection** — retrieve Godot version, analyze project structure, get debug output

## Setup

### Prerequisites

- **Godot 4** installed. Download from [godotengine.org](https://godotengine.org/download).
- **Node.js 18+** installed. The underlying MCP server runs via `npx`.

### Godot path

The underlying MCP server tries to find your Godot executable at a few common locations. If auto-detection fails (very likely on Windows, where there's no standard install path), set the `GODOT_PATH` environment variable to the full path of your Godot binary. The plugin's `.mcp.json` forwards `GODOT_PATH` through to the MCP subprocess, so setting it at the user level is enough — you don't need to edit Cowork's connector UI.

**Windows (PowerShell, permanent for your user):**

```powershell
[Environment]::SetEnvironmentVariable("GODOT_PATH", "C:\Godot\Godot_v4.6.2-stable_win64.exe", "User")
```

**macOS / Linux (bash/zsh, add to your shell rc):**

```bash
export GODOT_PATH="/Applications/Godot.app/Contents/MacOS/Godot"   # macOS
export GODOT_PATH="/usr/local/bin/godot"                           # Linux
```

Then fully quit and relaunch Cowork / Claude Code so the new env var is picked up at spawn. Verify with: *"What godot-mcp tools do you have? Get the Godot version."*

## Components

| Type | Count | Details |
|------|-------|---------|
| MCP server | 1 | `godot` — stdio server, runs `@coding-solo/godot-mcp` via `npx` |
| Skills | 0 | — |
| Commands | 0 | — |

Once installed, the MCP tools become available in new sessions automatically.

## Usage

Ask Claude naturally. Examples:

- "Open my Godot project at `~/projects/my-game`."
- "Create a new scene called `Player` with a `CharacterBody2D` root."
- "Run the project and show me any errors."
- "Add a `Sprite2D` to the `Player` scene and load `res://assets/player.png` into it."

Claude will pick the right tool (`launch_editor`, `create_scene`, `run_project`, `get_debug_output`, `load_sprite`, etc.) and report back.

## Credit

This plugin is a thin wrapper. All the actual Godot integration work — the MCP server, tool implementations, and GDScript glue — is by [Solomon Elias](https://github.com/Coding-Solo) at [Coding-Solo/godot-mcp](https://github.com/Coding-Solo/godot-mcp). MIT licensed.

## Issues

- Bugs in Godot tool behavior: file upstream at [Coding-Solo/godot-mcp/issues](https://github.com/Coding-Solo/godot-mcp/issues)
- Bugs specific to this plugin wrapper: file against whichever repo hosts this plugin
