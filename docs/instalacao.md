# Instalação detalhada

Simulador da Reforma Tributária é um servidor MCP remoto. Aponte seu cliente pra `https://api.mcp.ai/p_simulador-reforma-tributaria`. Snippets rápidos: [INSTALL.md](../INSTALL.md).

| Cliente | URL | Auth |
|---|---|---|
| Claude Desktop | `https://api.mcp.ai/p_simulador-reforma-tributaria` | nenhuma (grátis) |
| Cursor | `https://api.mcp.ai/p_simulador-reforma-tributaria` | nenhuma |
| VS Code (Copilot) | `https://api.mcp.ai/p_simulador-reforma-tributaria` | nenhuma |

A config JSON é a mesma em todos: só a URL, sem headers.

## Desinstalar

Remova o bloco `mcpServers.simuladorreformatributaria` (ou `servers.simuladorreformatributaria` no VS Code) do config do cliente e reinicie.
