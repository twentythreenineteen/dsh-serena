# dsh-serena

[中文](README.zh.md)

DeepSeek Harness (DSH) bundle plugin that mounts [Serena](https://github.com/oraios/serena) via `@deepseek-ai/dsh-mcp-client` under the `serena` tool namespace (`mcp__serena__*`).

## Prerequisites

Install Serena so `serena` is available on `PATH` (for example with `uv`):

```sh
uv tool install --from git+https://github.com/oraios/serena serena-agent
```

## Install in DSH

```sh
dsh plugin --profile web add github:twentythreenineteen/dsh-serena
```

Then enable `dsh-serena` in the DSH Plugins page (or add it to `dsh.profile.bundles` in your profile `package.json`).

## Configuration

The bundle patch inserts row `id: serena-mcp` with:

- `serverName`: `serena`
- `transport`: `stdio`
- `command`: `serena`
- `args`: `["start-mcp-server", "--context", "agent", "--agent-interface", "tools", "--project-from-cwd", "--open-web-dashboard", "false"]`
- `toolCallTimeoutMs`: `120000`
- `failOnStartupError`: `false`

To customize (e.g., run via `uvx` instead of a global `serena` binary, or change `--context`), restate the full `config` for `id: serena-mcp` in your profile's `cordis.patch.yml`:

```yaml
- id: serena-mcp
  config:
    serverName: serena
    transport: stdio
    command: uvx
    args:
      - --from
      - git+https://github.com/oraios/serena
      - serena
      - start-mcp-server
      - --context
      - agent
      - --agent-interface
      - tools
      - --project-from-cwd
      - --open-web-dashboard
      - "false"
    toolCallTimeoutMs: 120000
    failOnStartupError: false
```

## License

MIT
