# Simulador da Reforma Tributária

### Simulate Brazil's tax reform (CBS, IBS, Selective Tax) with your AI

**Brazil tax reform simulator** for AI. See how much CBS, IBS and Selective Tax an operation owes, in the regular regime and Simples Nacional. Runs Receita Federal's official open-source code (regular regime 1.6.1, Simples Nacional 0.0.6, database V0059 of 09/30/2026), with no recalculation of our own. Database V0059: only 2026 reference rates. It does not replace your accountant's review. Independent service, not affiliated with Receita Federal.

- 🧾 **CBS, state IBS, city IBS and Selective Tax** per item, with the official calculation memory and legal basis
- 🏪 **Regular regime and Simples Nacional**
- 📚 **Official tables**: CST, cClassTrib, legal basis, NCM, NBS and Simples activities
- 🧩 **XML**: generates the IBS/CBS/IS groups and validates against the official XSD
- 🔎 **Traceable**: every answer carries repository, version, commit and database version
- 🔒 **No login, no key**, free
- 💬 **Works with any MCP client**: Claude, ChatGPT, Cursor, VS Code

[Versão em português](README.md) · [Full docs (PT-BR)](docs/) · [Agent skill](skills/)

---

## One-click install

### Claude (Web and Desktop)

Anthropic unified MCP installation at `claude.ai/customize/connectors`. **The same link works for Claude Web and Claude Desktop** (just be logged in):

[➕ Open in Claude and connect](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (if the deeplink does not open): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Add custom connector** → paste **Name** `Simulador da Reforma Tributária` and **URL** `https://api.mcp.ai/p_simulador-reforma-tributaria`.

### Cursor

[➕ Install Simulador da Reforma Tributária in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=simuladorreformatributaria&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9zaW11bGFkb3ItcmVmb3JtYS10cmlidXRhcmlhIn0=)

### VS Code (Copilot Chat)

[➕ Install Simulador da Reforma Tributária in VS Code](vscode:mcp/install?name=simuladorreformatributaria&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_simulador-reforma-tributaria%22%7D)

### ChatGPT, Manus, OpenClaw and 40+ other clients

Works with any MCP client that speaks **MCP over HTTP**. The server URL is always:

```
https://api.mcp.ai/p_simulador-reforma-tributaria
```

Per-client details: [INSTALL.md](INSTALL.md).

---

## Example prompts

```
Simulate CBS and IBS on a R$ 10,000 sale in 2033 with 8.8% CBS and 17.7% IBS rates
Compare a R$ 950 sale by a Simples Nacional company with the same sale in the regular regime
```

---

## 8 tools available

| Tool | Description |
|---|---|
| `calculadora_rtc_regime_regular` | Calcula CBS, IBS (UF e município) e Imposto Seletivo de uma operação do REGIME REGULAR (LC 214/2025) pela calculadora oficial da Receita, com erros por item (um item inválido não derruba os outros). |
| `calculadora_rtc_simples_nacional` | Calcula CBS e IBS de uma operação de empresa do SIMPLES NACIONAL pela calculadora oficial da Receita (NT 2026.005), com erros por item. |
| `calculadora_rtc_aliquotas` | Alíquotas de REFERÊNCIA de CBS (União), IBS estadual (UF) e IBS municipal vigentes numa data, direto da base oficial. |
| `calculadora_rtc_consultar_tabela` | Consulta as tabelas oficiais da calculadora numa data de vigência. |
| `calculadora_rtc_explicar_erro` | Explica códigos de erro das calculadoras oficiais: REG-xxx (regime regular) e VSN-xxx (Simples Nacional), com título, descrição e orientação do catálogo oficial. |
| `calculadora_rtc_base_calculo` | Base de cálculo UNIFICADA oficial de um item de NF-e/NFC-e (documento 'nfe') ou NFS-e ('nfse'): devolve as bases do regime regular, do Imposto Seletivo e do Simples Nacional, aplicando a vigência de cada componente no… |
| `calculadora_rtc_gerar_xml` | Calcula a operação do regime regular (modo estrito: qualquer item inválido recusa a operação inteira) e gera o XML dos grupos de tributação IBS/CBS/IS para o documento fiscal (`tipo`: nfe, nfce, cte, bpe, nf3e, nfcom… |
| `calculadora_rtc_validar_xml` | Valida um XML contra o XSD oficial: só os grupos de tributação (subtipo 'grupo') ou a nota completa ('nota'). |

Details for each tool: [docs/ferramentas.md](docs/ferramentas.md) (PT-BR)

---

## Pricing

Free.

---

## Privacy & data protection

- **Read-only**, no tool changes data at the source.
- **Sub-processors**: the LLM host you choose (Claude, ChatGPT, Cursor, your own agent). Full list in [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Data returned by the tools is sent to **the LLM host you choose**, a sub-processor outside our control. We recommend plans with training opt-out.

---

## FAQ

**Is the calculation Receita Federal's?**
The calculation runs on the official open-source code Receita Federal published (MIT license), unmodified. The service is independent, not affiliated with or endorsed by Receita Federal.

**Which years does it cover?**
Official database V0059 (09/30/2026) only has 2026 reference rates. From 2027 on the calculator requires you to provide the rates and the result is a simulation.

**Does it replace my accountant?**
No. The result is the official calculator's for the data you provide; classification is up to you and your accountant.

**Do I need a login or key?**
No. It is free and platform-hosted.


---

## Support

- 📧 [simuladorreformatributaria@mcp.ai](mailto:simuladorreformatributaria@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/simulador-reforma-tributaria-mcp/issues)
- 📄 [docs/](docs/)

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_simulador-reforma-tributaria` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.
