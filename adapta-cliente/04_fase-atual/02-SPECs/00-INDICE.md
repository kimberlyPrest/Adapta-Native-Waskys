# Índice de SPECs — Fase 2

**Fase:** Motor determinístico e preparação de eventos
**Status:** SPECs e tasks geradas; execução condicionada à revisão dos contratos e aos gates humanos
**Override:** geração autorizada explicitamente pela consultora; não equivale a aprovação de `check-escopo` ou `check-cliente`

| ID | SPEC | Resultado observável | Aceite principal | Evidência |
|---|---|---|---|---|
| SPEC-2-001 | [Cadastro fiscal e carteira de beneficiários](spec-2-001-cadastro-beneficiarios.md) | beneficiários identificados por CPF/CNPJ e vinculados à carteira | conflito ou ausência bloqueia associação silenciosa | cadastro, histórico e log |
| SPEC-2-002 | [Rulebook versionado e catálogo de naturezas](spec-2-002-rulebook-naturezas.md) | regra vigente aplicável por competência | regra sem fonte/aprovador não pode ser usada | versão, fonte e aprovação |
| SPEC-2-003 | [Classificação assistida e fila de exceções](spec-2-003-classificacao-excecoes.md) | cada pagamento recebe sugestão, decisão ou bloqueio | IA não aprova nem elimina ambiguidade | fila, decisão e justificativa |
| SPEC-2-004 | [Consolidação por beneficiário e fato gerador](spec-2-004-consolidacao-fato-gerador.md) | pagamentos relacionados são agrupados sem duplicidade | totais e origem permanecem reconciliáveis | matriz e reconciliação |
| SPEC-2-005 | [Rascunho R-4010/R-4020 e pacote de revisão](spec-2-005-rascunho-eventos.md) | pacote revisável com eventos, campos e pendências | saída sem rulebook, fonte ou aprovador fica bloqueada | exportação e checklist |

## Tasks vinculadas

A tabela operacional completa de 16 tasks está em `../fase_2.md` e em `../matriz-specs-fases.md`.

## Gates da fase

- G2 — rulebook: versão, fonte, vigência, cenários e golden set aprovados pelo responsável tributário.
- G3 — dados/ambiente: autorização, segregação e retenção antes de dados reais.
- O leiaute produzido é rascunho interno; não autoriza transmissão nem importação no Domínio.
