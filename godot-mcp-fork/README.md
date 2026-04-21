# godot-mcp-fork

Cowork / Claude Code plugin for [BackendOutput/godot-mcp](https://github.com/BackendOutput/godot-mcp) — a fork of [@coding-solo/godot-mcp](https://github.com/Coding-Solo/godot-mcp) with three correctness fixes pending upstream review.

## Why a fork?

Three issues found while dogfooding the upstream MCP for a real prototype:

1. **`load_sprite` rejected `res://` texture paths.** The FS pre-flight check concatenated `projectPath + "res://icon.svg"`, producing nonsense like `<proj>/res:/icon.svg` and failing before reaching GDScript. Fixed: strip the prefix before the existence check.
2. **`add_node` silently dropped Variant-typed property values.** Passing `properties.color = "Color(0.18, 0.2, 0.23, 1)"` would set `Color(0, 0, 0, 1)` with no warning. Fixed: try `str_to_var()` for non-String target properties; falls through to the raw string for `Label.text` etc.
3. **`create_scene` hardcoded root node name to `"root"`.** Added optional `rootNodeName` param so callers can name scene roots semantically.

Once [the upstream PR](https://github.com/Coding-Solo/godot-mcp/compare/main...BackendOutput:godot-mcp:fix/scene-composition-correctness) merges, switch back to the upstream `godot-mcp` plugin in this same marketplace.

## How it runs

The `.mcp.json` invokes:

```
npx -y github:BackendOutput/godot-mcp#fix/scene-composition-correctness
```

`npx` clones the branch, runs the `prepare` hook (`tsc && node scripts/build.js`), and launches the `bin` entry (`build/index.js`). First launch is slower (~20-30s for npm install + build); subsequent launches use the npm cache.

## Setup

Same as upstream — Godot 4 installed, Node 18+, optionally set `GODOT_PATH` if auto-detection misses your binary.

## Credit

All Godot integration code is by [Solomon Elias](https://github.com/Coding-Solo). MIT licensed. Fork patches are for upstream consideration via PR.
