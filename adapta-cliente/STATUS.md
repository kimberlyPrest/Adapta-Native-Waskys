# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-004 aguardando teste humano na SKIP 0.0.131
**Data:** 14/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Progresso:** 3 de 16 tasks concluídas (18,75%); TASK-2-004 permanece aberta

## TASK-2-001 a TASK-2-003 — concluídas

- SPEC-2-001 tecnicamente concluída e aprovada.
- Versões validadas: SKIP `0.0.108`, `0.0.121` e `0.0.126`.

## Gate G2 — liberado

- Responsável tributário: Matheus Lohse.
- Consultoria externa atua como apoio para dúvidas, sem substituir sua aprovação.

## TASK-2-004 — aguardando teste humano

- Versão para teste: SKIP `0.0.131`.
- Coleções `rulebook_versions`, `rulebook_rules` e `rulebook_history` com leitura por owner e escrita exclusiva do backend.
- Rota atômica para criar e editar somente Rascunhos.
- Página Rulebook e navegação desktop/mobile.
- Valida fonte, URL HTTPS, consulta, vigência, evento, natureza, cenário, campos obrigatórios e bloqueios.
- Preserva revisões com motivo, operador e snapshot.
- Migração 0044 aplicada para reconciliar o bloqueio de escrita direta.
- Provas: GET cross-owner 404; create/PATCH/DELETE diretos 403; rota segura 200; concorrência obsoleta 400 sem histórico órfão.
- 21 testes e QA completo passaram; preview autenticado validado com a versão sintética e três revisões.

## Próxima ação

- Matheus executar o teste humano da TASK-2-004 e informar se funcionou.
- TASK-2-005 não foi iniciada.
