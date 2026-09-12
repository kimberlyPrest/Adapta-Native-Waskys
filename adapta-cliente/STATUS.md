# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-004 implementada tecnicamente na SKIP 0.0.130, bloqueada para verificação final por indisponibilidade do Skip Cloud
**Data:** 12/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Progresso:** 3 de 16 tasks concluídas (18,75%); TASK-2-004 permanece aberta

## TASK-2-001 a TASK-2-003 — concluídas

- SPEC-2-001 tecnicamente concluída e aprovada.
- Versões validadas: SKIP `0.0.108`, `0.0.121` e `0.0.126`.

## Gate G2 — liberado

- Responsável tributário: Matheus Lohse.
- Consultoria externa atua como apoio para dúvidas, sem substituir sua aprovação.

## TASK-2-004 — bloqueada para verificação final

- Versão atual: SKIP `0.0.130`.
- Criadas coleções `rulebook_versions`, `rulebook_rules` e `rulebook_history` com RLS por owner.
- Criada rota transacional para criar e editar somente Rascunhos.
- Criada página Rulebook e navegação desktop/mobile.
- Fonte, URL HTTPS, consulta, vigência, regras, campos obrigatórios e bloqueios são validados.
- Prova parcial: rascunho incompleto retornou 400 sem resíduo; versão completa criou v1/revisão 1; edição preservou v1 e criou revisão 2; concorrência obsoleta retornou 400 sem novo histórico.
- Falha de segurança encontrada: regras de escrita `""` eram públicas no PocketBase. Migração 0043 mudou create/update/delete para `null` (somente backend/superuser).
- 21 testes e QA completo passaram na 0.0.130.
- Verificação final do bloqueio e preview não foi concluída porque o Skip Cloud passou a responder HTTP 503.

## Próxima ação

- Quando o Cloud voltar, revalidar escrita direta negada, rota transacional, schema e editor; só então solicitar teste humano.
- TASK-2-005 não foi iniciada.
