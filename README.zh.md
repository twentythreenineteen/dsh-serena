# dsh-serena

[English](README.md)

DeepSeek Harness（DSH）插件包：通过 `@deepseek-ai/dsh-mcp-client` 将 [Serena](https://github.com/oraios/serena) 挂载为 `serena` 工具命名空间（`mcp__serena__*`）。

## 前置条件

安装 Serena 并确保 `serena` 在 `PATH` 中可用（例如使用 `uv`）：

```sh
uv tool install --from git+https://github.com/oraios/serena serena-agent
```

## 安装到 DSH

```sh
dsh plugin --profile web add github:twentythreenineteen/dsh-serena
```

然后在 DSH 的插件页面启用 `dsh-serena`（或在 profile 的 `package.json` 的 `dsh.profile.bundles` 中启用）。

## 配置说明

默认在 `cordis.patch.yml` 中插入 `id: serena-mcp`：

- `serverName`: `serena`
- `transport`: `stdio`
- `command`: `serena`
- `args`: `["start-mcp-server", "--context", "agent", "--agent-interface", "tools", "--project-from-cwd", "--open-web-dashboard", "false"]`
- `toolCallTimeoutMs`: `120000`
- `failOnStartupError`: `false`

如需自定义（例如改用 `uvx` 启动或切换 `--context`），可在 profile 的 `cordis.patch.yml` 中按 `id: serena-mcp` 完整重写 `config`。

## 许可证

MIT
