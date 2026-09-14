# Estado atual — Adapta Cliente

- task_id: TASK-2-004
- champion: Matheus Lohse
- spec: adapta-cliente/04_fase-atual/02-SPECs/spec-2-002-rulebook-naturezas.md
- etapa: em_correcao
- autorizacao_implementacao: confirmada em 2026-09-12T12:44:00-03:00 — "Pode implementar o plano analisado da TASK-2-004."
- teste_humano: pendente
- verificacao_automatica: falhou — ao retomar em 2026-09-14, a lista do Cloud mostrou 0041 e 0042 aplicadas, mas não mostrou a migração 0043 de bloqueio de escrita direta
- aprendizado: capturado:adapta-cliente/06_notas/aprendizado-continuo/AP-2026-09-12-1253-regras-rls-pocketbase.md
- ultima_acao: indisponibilidade 503 cessou e divergência entre a versão 0.0.130 e as migrações efetivamente aplicadas foi reproduzida
- proxima_acao: reconciliar a migração de segurança e repetir provas HTTP de RLS, escrita direta e rota atômica
- atualizado_em: 2026-09-14T10:00:00-03:00
