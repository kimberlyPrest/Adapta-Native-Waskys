# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-004 concluída; SPEC-2-002 com 1 de 3 tasks concluídas
**Data:** 14/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Progresso:** 4 de 16 tasks concluídas (25%); SPEC-2-002 com 1 de 3 tasks concluídas

## Tasks concluídas

- TASK-2-001 — SKIP `0.0.108`.
- TASK-2-002 — SKIP `0.0.121`.
- TASK-2-003 — SKIP `0.0.126`.
- TASK-2-004 — SKIP `0.0.133`.

## TASK-2-004 — concluída

- Teste humano aprovado por Matheus Lohse em 14/09/2026.
- Modelo versionado de Rascunhos com fonte, vigência, eventos R-4010/R-4020, naturezas, cenários, campos obrigatórios e bloqueios.
- Rota atômica com controle de concorrência, histórico e autoria textual.
- Leitura segregada por owner; create/PATCH/DELETE diretos bloqueados.
- Entrada incompleta e revisão obsoleta retornam 400 sem histórico residual.
- Campos multilinha preservam Enter; validação destaca campos e mostra alertas no topo e junto ao botão.
- Revisões técnicas atribuídas a Jarvis (IA); revisões humanas atribuídas a Matheus Lohse.
- Migrações 0044, 0045 e 0047 aplicadas; 23 testes, QA, schema e preview aprovados.

## Próxima ação elegível

- TASK-2-005 pode ser analisada mediante novo pedido explícito.
- Golden set, sobreposição, aprovação/retirada e seleção por competência ainda não foram implementados.
