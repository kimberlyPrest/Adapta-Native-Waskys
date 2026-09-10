# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-001 concluída; SPEC-2-001 aberta
**Data:** 10/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Progresso:** 1 de 16 tasks concluída (6,25%); SPEC-2-001 com 1 de 3 tasks concluída

## TASK-2-001 — concluída

- Versão validada: SKIP `0.0.108`.
- Teste humano: aprovado explicitamente por Matheus em 10/09/2026.
- QA: setup, análise estática, build, integrações e teste passaram.
- Migrações `0015` a `0032` aplicadas.
- Cadastro PF/PJ sem caso, owner obrigatório, RLS por carteira, confirmação manual com evidência automática, logs, relacionamentos e nomes dos sócios no card.
- Vínculos com transações são versionados e append-only.
- Schema final de `beneficiary_links`: `updateRule = ''`, `deleteRule = ''` e `beneficiary_id.cascadeDelete = false`.
- Correções criam nova versão; versões antigas não podem ser alteradas nem excluídas pela API.

## Pendências da SPEC-2-001

- TASK-2-002: normalização e validação matemática de CPF/CNPJ, duplicidade, conflitos e fila de bloqueios.
- TASK-2-003: revisão final e prova de acesso cruzado entre owners.
- A SPEC-2-001 não está concluída e a SPEC-2-002 continua bloqueada pelo fechamento da SPEC-2-001 e pelo gate G2.

## Limitações

- O script de testes do projeto ainda é placeholder; o fluxo real foi validado humanamente e o schema foi conferido no Skip Cloud.
- `check-escopo` e `check-cliente` continuam pendentes.
- Não há autorização para transmissão, alteração do Domínio ou decisão tributária autônoma.
