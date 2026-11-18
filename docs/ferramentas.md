# Ferramentas

Simulador da Reforma Tributária expõe 8 ferramentas (todas somente leitura).

### 1. `calculadora_rtc_regime_regular`
**Input**: `operacao`

Calcula CBS, IBS (UF e município) e Imposto Seletivo de uma operação do REGIME REGULAR (LC 214/2025) pela calculadora oficial da Receita, com erros por item (um item inválido não derruba os outros).

### 2. `calculadora_rtc_simples_nacional`
**Input**: `operacao`

Calcula CBS e IBS de uma operação de empresa do SIMPLES NACIONAL pela calculadora oficial da Receita (NT 2026.005), com erros por item.

### 3. `calculadora_rtc_aliquotas`
**Input**: `data` (opcional), `ano` (opcional), `uf` (opcional), `municipio_ibge` (opcional)

Alíquotas de REFERÊNCIA de CBS (União), IBS estadual (UF) e IBS municipal vigentes numa data, direto da base oficial.

### 4. `calculadora_rtc_consultar_tabela`
**Input**: `tipo`, `codigos` (opcional), `busca` (opcional), `data` (opcional), `ano` (opcional)

Consulta as tabelas oficiais da calculadora numa data de vigência.

### 5. `calculadora_rtc_explicar_erro`
**Input**: `codigos`

Explica códigos de erro das calculadoras oficiais: REG-xxx (regime regular) e VSN-xxx (Simples Nacional), com título, descrição e orientação do catálogo oficial.

### 6. `calculadora_rtc_base_calculo`
**Input**: `documento` (opcional), `entrada`

Base de cálculo UNIFICADA oficial de um item de NF-e/NFC-e (documento 'nfe') ou NFS-e ('nfse'): devolve as bases do regime regular, do Imposto Seletivo e do Simples Nacional, aplicando a vigência de cada componente no…

### 7. `calculadora_rtc_gerar_xml`
**Input**: `operacao`, `tipo` (opcional)

Calcula a operação do regime regular (modo estrito: qualquer item inválido recusa a operação inteira) e gera o XML dos grupos de tributação IBS/CBS/IS para o documento fiscal (`tipo`: nfe, nfce, cte, bpe, nf3e, nfcom…

### 8. `calculadora_rtc_validar_xml`
**Input**: `xml`, `tipo` (opcional), `subtipo` (opcional)

Valida um XML contra o XSD oficial: só os grupos de tributação (subtipo 'grupo') ou a nota completa ('nota').

## Prompts de exemplo

```
Simule a CBS e o IBS de uma venda de R$ 10.000 em 2033 com alíquotas de 8,8% de CBS e 17,7% de IBS
Compare uma venda de R$ 950 de empresa do Simples Nacional com a mesma venda no regime regular
```
