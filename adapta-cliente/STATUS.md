# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-001 implementada tecnicamente e aguardando teste humano
**Data:** 10/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Task ativa:** TASK-2-001 — Modelar cadastro de beneficiários, vínculo e histórico
**Etapa atual:** aguardando teste humano da versão SKIP `0.0.100`

## Estado comprovado

- O projeto SKIP Cockpit Fiscal está na versão `0.0.100`.
- As migrações `0015` a `0029` relacionadas a beneficiários, vínculos, históricos e correções cadastrais estão aplicadas.
- Existem cadastro PF/PJ, relacionamentos cliente–sócio, vínculos versionados por transação, históricos append-only e regras de acesso por owner.
- Cadastros candidatos podem ser confirmados ou bloqueados por nova versão, com motivo, evidência, operador e data.
- Alocações podem ser revisadas como confirmadas ou bloqueadas por nova versão; o histórico completo da transação fica consultável na tela de Casos.
- `beneficiary_links` não permite update/delete e não é apagado em cascata ao excluir beneficiário.
- Exclusão de beneficiário com vínculo, histórico ou relacionamento é bloqueada no backend.
- Setup, análise estática, build, integrações e teste do pipeline SKIP passaram. O script de teste do projeto ainda é placeholder; o fluxo autenticado depende do teste humano.
- A SPEC-2-001 permanece aberta. Validação matemática de CPF/CNPJ, conflitos e fila pertencem à TASK-2-002; a prova de segregação entre owners pertence à TASK-2-003.
- A SPEC-2-002 não foi iniciada e continua dependente do fechamento da SPEC-2-001 e do gate G2.

## Gates pendentes

- Matheus executar e aprovar o teste humano da TASK-2-001 na versão `0.0.100`.
- Somente após aprovação, concluir formalmente a TASK-2-001.
- Implementar e aprovar TASK-2-002 e TASK-2-003 antes de encerrar a SPEC-2-001.
- Identificar/aprovar o responsável tributário e liberar G2 antes da SPEC-2-002.

## Limitações

- `check-escopo` e `check-cliente` continuam pendentes e não são substituídos pelo avanço autorizado da Fase 2.
- Não há autorização para transmissão, alteração do Domínio ou decisão tributária autônoma.
- Dados reais para rulebook e golden set dependem de aprovação do responsável tributário.
