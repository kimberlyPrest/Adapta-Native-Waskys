# Estado atual — Adapta Cliente

- task_id: TASK-2-006
- champion: Matheus Lohse
- spec: adapta-cliente/04_fase-atual/02-SPECs/spec-2-002-rulebook-naturezas.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada em 2026-09-15T17:09:00-03:00 — "Pode implementar o plano analisado dos dois catálogos de Eventos e Naturezas na TASK-2-006."
- teste_humano: pendente — catálogos aguardam teste na SKIP 0.0.172
- verificacao_automatica: passou — SKIP 0.0.172; migração 0058 aplicada; coleções rulebook_events, rulebook_natures e históricos append-only com RLS por owner e escrita direta bloqueada. Backfill criou R-4010/R-4020 e naturezas existentes, regras preservam snapshots e vínculos; editor usa apenas catálogos ativos e valida relação Natureza–Evento. Cópia de versão preserva vínculos. Setup, análise estática, build, integrações e testes passaram; API anônima: rota 401 e escrita direta 403. Preview carregou até o login; fluxo autenticado aguarda teste humano.
- aprendizado: pendente
- ultima_acao: catálogos editáveis e auditáveis de Eventos e Naturezas implementados e verificados na SKIP 0.0.172
- proxima_acao: Matheus executar o teste humano dos catálogos e do editor na SKIP 0.0.172
- atualizado_em: 2026-09-15T17:28:00-03:00
