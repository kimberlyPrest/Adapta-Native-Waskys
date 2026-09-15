# Estado atual — Adapta Cliente

- task_id: TASK-2-006
- champion: Matheus Lohse
- spec: adapta-cliente/04_fase-atual/02-SPECs/spec-2-002-rulebook-naturezas.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada em 2026-09-15T15:14:00-03:00 — "Aplique a recomendação: Positivo, Negativo e Bloqueado sempre obrigatórios; Ambíguo obrigatório somente quando houver sobreposição real, mantendo teste sistêmico separado."
- teste_humano: pendente — correção aguarda teste na SKIP 0.0.170
- verificacao_automatica: passou — SKIP 0.0.170; setup, análise estática, build, integrações e suíte completos. Backend calcula sobreposição real por Evento+Código normalizado dentro da transação: Positivo/Negativo/Bloqueado sempre obrigatórios; Ambíguo obrigatório somente com sobreposição. UI inicia novos Golden Sets com três casos, mostra diagnóstico de sobreposição e aplica o mesmo gate. Teste sistêmico permanente continua provando que múltiplas regras geram Ambíguo sem escolha automática. Prova API real não executada nesta rodada porque a autenticação da fixture recusou a credencial sintética; nenhuma mutação ocorreu. .skip.config.json preexistente preservado.
- aprendizado: capturado:adapta-cliente/06_notas/aprendizado-continuo/AP-2026-09-15-1528-golden-set-condicional.md
- ultima_acao: obrigatoriedade condicional do caso Ambíguo implementada e QA completo aprovado na SKIP 0.0.170
- proxima_acao: Matheus executar o teste humano da TASK-2-006 na SKIP 0.0.170
- atualizado_em: 2026-09-15T15:31:00-03:00
