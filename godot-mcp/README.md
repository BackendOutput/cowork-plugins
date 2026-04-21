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

The plugin tries to find your Godot executable automatically. If auto-detection fails, set the `GODOT_PATH` environment variable to the full path of your Godot binary before launching Cowork / Claude Code:

- Windows: `C:\path\to\Godot_v4.6.2-stable_win64.exe`
- macOS: `/Applications/Godot.app/Contents/MacOS/Godot`
- Linux: `/usr/local/bin/godot`

Setting `GODOT_PATH` is only necessary if the MCP server can't find Godot on its own.

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
