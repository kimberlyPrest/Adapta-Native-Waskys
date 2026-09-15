# Estado atual — Adapta Cliente

- task_id: TASK-2-006
- champion: Matheus Lohse
- spec: adapta-cliente/04_fase-atual/02-SPECs/spec-2-002-rulebook-naturezas.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada em 2026-09-15T11:23:00-03:00 — "Implemente na TASK-2-006 a explicação clara da seleção e o fluxo recomendado de criar nova versão a partir de um Rulebook aprovado, preservando o original."
- teste_humano: pendente — correção aguarda teste na SKIP 0.0.168
- verificacao_automatica: passou — SKIP 0.0.168; setup, análise estática, build, integrações e suíte completos. Seleção por competência agora explica consulta, bloqueios e registro auditável. Nova rota atômica clone-as-draft aceita somente origem Aprovada, cria novo Rascunho, copia regras e última revisão do Golden Set, cria histórico/log e não altera o original. API real: tentativa com origem Rascunho retornou 400 e manteve versões 2→2, sem resíduo. .skip.config.json preexistente preservado.
- aprendizado: capturado:adapta-cliente/06_notas/aprendizado-continuo/AP-2026-09-15-1135-imutabilidade-copia-rulebook.md
- ultima_acao: explicação e cópia versionada implementadas e verificadas na SKIP 0.0.168
- proxima_acao: Matheus executar o teste humano da TASK-2-006 na SKIP 0.0.168
- atualizado_em: 2026-09-15T11:38:00-03:00
