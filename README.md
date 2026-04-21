# cowork-plugins

A plugin marketplace by [BackendOutput](https://github.com/BackendOutput) for [Cowork](https://claude.ai) and [Claude Code](https://code.claude.com).

## Install in Cowork

1. Open Cowork, click the **+** next to **Personal plugins**, then **Create plugin → Add marketplace**.
2. Paste the marketplace URL: `https://github.com/BackendOutput/cowork-plugins`
3. Browse the plugins in this marketplace and install the ones you want.

## Install in Claude Code

```
/plugin marketplace add BackendOutput/cowork-plugins
/plugin install godot-mcp@cowork-plugins
```

## Plugins in this marketplace

| Plugin | Description |
|--------|-------------|
| [`godot-mcp`](./godot-mcp) | Connect Claude to the Godot game engine. Wraps [`@coding-solo/godot-mcp`](https://github.com/Coding-Solo/godot-mcp). |

## License

Marketplace infrastructure is MIT-licensed. Individual plugins may carry their own licenses — see each plugin's directory.

## Adding your own plugin

PRs welcome. Add your plugin as a subdirectory at the repo root, register it in `.claude-plugin/marketplace.json`, and open a PR.
