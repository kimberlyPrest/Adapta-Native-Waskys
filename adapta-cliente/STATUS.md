# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-001 ajustada e aguardando novo teste humano
**Data:** 10/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Task ativa:** TASK-2-001 — Modelar cadastro de beneficiários, vínculo e histórico
**Etapa atual:** aguardando novo teste humano da versão SKIP `0.0.103`

## Estado comprovado

- O projeto SKIP Cockpit Fiscal está na versão `0.0.103`.
- As migrações `0015` a `0030` estão aplicadas; a `0030` tornou o caso opcional para PF (apenas PJ exige caso) e ajustou as regras de acesso.
- Cadastros manuais podem nascer como `candidato` ou `confirmado`; confirmação exige evidência e registra operador/data.
- O status aparece somente na parte superior do card e do modal de detalhes; versão saiu do card e permanece no histórico.
- Em Casos, `Situação do lançamento` exibe apenas ✓ (regular) ou ✕ (divergência, com detalhe no tooltip); a coluna Direção exibe `C` ou `D`.
- Entrada e saída de sócio geram logs explicativos; a saída preserva os lançamentos já vinculados ao sócio.
- O seletor de alocação mantém o sócio removido como opção de vínculo anterior, para preservar o fato ocorrido antes da saída.
- O botão de revisão passou a se chamar `Confirmar`; o modal explica o que Confirmar e Bloquear fazem.
- `beneficiary_links` permanece append-only e sem cascade delete; exclusão de cadastro com dependências é bloqueada no backend.
- Setup, análise estática, build, integrações e teste do pipeline SKIP passaram.
- A SPEC-2-001 permanece aberta. Validação matemática de CPF/CNPJ, conflitos e fila pertencem à TASK-2-002; a prova de segregação entre owners pertence à TASK-2-003.

## Gates pendentes

- Matheus executar e aprovar o novo teste humano da TASK-2-001 na versão `0.0.103`.
- Somente após aprovação, concluir formalmente a TASK-2-001.
- Implementar e aprovar TASK-2-002 e TASK-2-003 antes de encerrar a SPEC-2-001.
- Identificar/aprovar o responsável tributário e liberar G2 antes da SPEC-2-002.

## Limitações

- `check-escopo` e `check-cliente` continuam pendentes e não são substituídos pelo avanço autorizado da Fase 2.
- Não há autorização para transmissão, alteração do Domínio ou decisão tributária autônoma.
- Dados reais para rulebook e golden set dependem de aprovação do responsável tributário.
