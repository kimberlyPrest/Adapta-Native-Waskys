# Índice de SPECs — Fase 1

**Fase:** Núcleo de casos, fontes e baseline  
**Status:** SPECs planejadas; execução condicionada aos gates do escopo  
**Override:** geração autorizada explicitamente pelo cliente apesar dos checks pendentes  
**Run:** `20260827T122601285Z-a36c8be1`

| ID | SPEC | Resultado observável | Requisitos/origem | Aceite principal | Evidência |
|---|---|---|---|---|---|
| SPEC-1-001 | [Caso de competência e preservação das fontes](spec-1-001-caso-e-fontes.md) | Caso com manifesto, hash e fonte original imutável | F01, F02, TR-01, TR-04 | fonte válida aceita; duplicata idempotente; inválida em quarentena | caso, manifesto e logs |
| SPEC-1-002 | [Parser e normalização de fontes estruturadas](spec-1-002-parser-e-normalizacao.md) | Tabela canônica com referência de origem | F02, F03, TR-01, TR-04 | OFX/XLSX/CSV equivalentes e rejeições explicáveis | tabela e relatório |
| SPEC-1-003 | [Qualidade, completude e estados do caso](spec-1-003-completude-e-estados.md) | Relatório de qualidade e estados controlados | F02, F08, G1, TR-04 | incompleto/divergente bloqueia; nova versão preserva histórico | relatório e auditoria |
| SPEC-1-004 | [Painel de status e baseline operacional](spec-1-004-dashboard-e-baseline.md) | Painel interno e baseline reproduzível | F08, TR-10 | contadores reconciliados; acesso segregado; tempos ausentes não inventados | captura, exportação e logs |

## Ordem da onda

1. SPEC-1-001 — caso e preservação;
2. SPEC-1-002 — parsing e normalização;
3. SPEC-1-003 — qualidade, completude e estados;
4. SPEC-1-004 — painel e baseline.

## Tasks vinculadas

Nenhuma. A decomposição em tasks só será feita pelo job `gerar-tasks` após revisão das SPECs.

## Gates da fase

- `check-escopo.md` permanece `PENDENTE` por autorização explícita do cliente; isso não equivale a aprovação.
- `check-cliente.md` ainda não existe.
- G1 (mapa As-Is real), G2 (rulebook), G3 (dados/ambiente) e a política de fontes precisam ser validados antes de dados reais.
- Nenhuma SPEC autoriza Domínio produtivo, transmissão, DCTFWeb, DARF, e-CAC ou RPA.
