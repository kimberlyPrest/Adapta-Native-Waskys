# Changelog

## 2026-08-27

- Criada pasta provisória do cliente.
- Exportados o escopo definitivo e as SPECs da Fase 1.
- 04/09/2026: avanço para a Fase 2 autorizado; geradas 5 SPECs e 16 tasks executáveis.

## 2026-09-10

- TASK-2-001 concluída no SKIP `0.0.108`.
- TASK-2-002 concluída na SKIP `0.0.121`.
- TASK-2-003 implementada na SKIP `0.0.126`.

## 2026-09-12

- TASK-2-003 concluída: teste humano aprovado; SPEC-2-001 tecnicamente concluída.
- Gate G2 liberado: Matheus designado responsável tributário.
- TASK-2-004 analisada e implementada tecnicamente até a SKIP `0.0.130`; debug de RLS interrompido por 503.

## 2026-09-14

- TASK-2-004 concluída na SKIP `0.0.133` após teste humano; modelo/editor de Rascunhos, RLS, atomicidade, histórico, autoria e UX revalidados.
- TASK-2-005 analisada: golden set ausente; sobreposição delimitada a Evento + Código da natureza normalizado, sem interpretar cenário textual.
- 2026-09-14 · Matheus Lohse · TASK-2-005 implementada tecnicamente na SKIP `0.0.140`: golden set versionado, quatro tipos de caso, executor determinístico, conflito explícito sem escolha automática, relatório e painel no Rulebook. Debug corrigiu zero numérico obrigatório, escopo isolado do JSVM, JSON entregue como bytes/string numérica e fixture que contaminava a v1. Fixture final isolada na v2 executou 4/4; 34 testes, QA, RLS, 400/403/404 sem resíduo, autoria Jarvis e preview passaram; aguardando teste humano.
