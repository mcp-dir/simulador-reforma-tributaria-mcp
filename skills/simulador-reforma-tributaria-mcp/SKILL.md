---
name: simulador-reforma-tributaria-mcp
description: Simulador da Reforma Tributária: simula CBS, IBS e Imposto Seletivo de uma operação com o código aberto oficial da Receita Federal. Use quando o usuário pedir uma simulação da Reforma Tributária.
---

# Simulador da Reforma Tributária — REST API skill

Você tem acesso à **Simulador da Reforma Tributária** REST API na MCP.AI.

> **Simulador da Reforma Tributária** para IA. Veja quanto dá de CBS, IBS e Imposto Seletivo numa operação, no regime regular e no Simples Nacional. Usa o código aberto oficial da Receita Federal (regime regular 1.6.1, Simples Nacional 0.0.6, base V0059 de 30/09/2026), sem recálculo próprio. Base V0059: só tem alíquotas de referência de 2026. Não substitui a análise do seu contador. Serviço independente, sem vínculo com a Receita Federal.

## Base URL

```
https://api.mcp.ai/api/calculadora_rtc
```

Todo endpoint é um **POST** na Base URL + o path abaixo. Os parâmetros vão no corpo JSON.

## Autenticação

Inclua em toda request:

```
Authorization: Bearer sk_live_...
Content-Type: application/json
```

> Gere sua chave em **https://app.mcp.ai/settings/api-keys** (workspace API key `sk_live_…`, não expira, revogável). Uma única chave serve pra todos os seus MCPs.

## Formato de resposta

```json
{ "ok": true, "tool": "<tool_id>", "result": <payload> }
```

## Exemplo cURL

```bash
curl -X POST https://api.mcp.ai/api/calculadora_rtc/aliquotas \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/calculadora_rtc/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (8)

#### `calculadora_rtc_aliquotas`

Alíquotas de REFERÊNCIA de CBS (União), IBS estadual (UF) e IBS municipal vigentes numa data, direto da base oficial. _(POST /api/calculadora_rtc/aliquotas)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `data` | string | Não | Data de referência AAAA-MM-DD (vigência). Padrão: hoje. |
| `ano` | integer | Não | Ano de referência (usa 1º de janeiro). Alternativa a `data`. |
| `uf` | string | Não | UF: sigla ('MS') ou código IBGE ('50'). |
| `municipio_ibge` | string | Não | Código IBGE do município, 7 dígitos (ex.: '5002704'). |

#### `calculadora_rtc_base_calculo`

Base de cálculo UNIFICADA oficial de um item de NF-e/NFC-e (documento 'nfe') ou NFS-e ('nfse'): devolve as bases do regime regular, do Imposto Seletivo e do Simples Nacional, aplicando a vigência de c _(POST /api/calculadora_rtc/base/calculo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `documento` | string | Não | 'nfe' (NF-e/NFC-e, padrão) ou 'nfse'. (nfe, nfse) |
| `entrada` | object | Sim | Entrada no formato oficial da base de cálculo unificada. |

#### `calculadora_rtc_consultar_tabela`

Consulta as tabelas oficiais da calculadora numa data de vigência. _(POST /api/calculadora_rtc/consultar/tabela)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `tipo` | string | Sim |  (cst, cclasstrib, fundamentacao, ncm, nbs, atividade_simples) |
| `codigos` | string[] | Não | Códigos a consultar (ex.: ['200028','000001'] para cclasstrib; ['22030000'] para ncm). |
| `busca` | string | Não | Texto para filtrar a lista (ex.: 'educação'). |
| `data` | string | Não | Data de referência AAAA-MM-DD (vigência). Padrão: hoje. |
| `ano` | integer | Não | Ano de referência (usa 1º de janeiro). Alternativa a `data`. |

#### `calculadora_rtc_explicar_erro`

Explica códigos de erro das calculadoras oficiais: REG-xxx (regime regular) e VSN-xxx (Simples Nacional), com título, descrição e orientação do catálogo oficial. _(POST /api/calculadora_rtc/explicar/erro)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `codigos` | string[] | Sim | Códigos, ex.: ['REG-011', 'VSN-024']. |

#### `calculadora_rtc_gerar_xml`

Calcula a operação do regime regular (modo estrito: qualquer item inválido recusa a operação inteira) e gera o XML dos grupos de tributação IBS/CBS/IS para o documento fiscal (`tipo`: nfe, nfce, cte, _(POST /api/calculadora_rtc/gerar/xml)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `operacao` | object | Sim |  |
| `tipo` | string | Não | Tipo de documento do XML (padrão 'nfe'). |

#### `calculadora_rtc_regime_regular`

Calcula CBS, IBS (UF e município) e Imposto Seletivo de uma operação do REGIME REGULAR (LC 214/2025) pela calculadora oficial da Receita, com erros por item (um item inválido não derruba os outros). _(POST /api/calculadora_rtc/regime/regular)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `operacao` | object | Sim | Operação no formato oficial da calculadora (POST /regime-geral). |

#### `calculadora_rtc_simples_nacional`

Calcula CBS e IBS de uma operação de empresa do SIMPLES NACIONAL pela calculadora oficial da Receita (NT 2026.005), com erros por item. _(POST /api/calculadora_rtc/simples/nacional)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `operacao` | object | Sim | Operação no formato oficial (POST /observabilidade/simples-nacional). |

#### `calculadora_rtc_validar_xml`

Valida um XML contra o XSD oficial: só os grupos de tributação (subtipo 'grupo') ou a nota completa ('nota'). _(POST /api/calculadora_rtc/validar/xml)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `xml` | string | Sim | Texto do XML. |
| `tipo` | string | Não | Tipo de documento (padrão 'nfe'). |
| `subtipo` | string | Não | 'grupo' (padrão) ou 'nota'. (grupo, nota) |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_simulador-reforma-tributaria` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
