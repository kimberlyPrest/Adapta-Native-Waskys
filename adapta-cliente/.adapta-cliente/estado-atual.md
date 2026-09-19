# Estado atual — Adapta Cliente

- task_id: TASK-2-007
- champion: Matheus Lohse
- spec: adapta-cliente/04_fase-atual/02-SPECs/spec-2-003-classificacao-excecoes.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada em 2026-09-18 ("Autorização")
- teste_humano: pendente — validar a SKIP `0.0.190` (motor de sugestão + criação de rulebook do zero + páginas Casos/Sugestões/Golden set ajustadas + correção do save do golden set)
- verificacao_automatica: aprovada — SKIP `0.0.190`; setup, análise estática, build, integrações e testes passaram
- ultima_acao: correção do bug que impedia salvar nova revisão do golden set (reportado por Matheus em 19/09 ~15h). Causa raiz: no hook `golden_set.js`, a validação transacional comparava `event.getString('codigo') !== item.event` — mas o campo normalizado chama-se `evento`; `item.event` era sempre `undefined`, então TODO save-revision falhava com "O Evento do caso deve pertencer à versão selecionada..." desde a reescrita de rastreabilidade (0.0.178, 17/09). Fix na 0.0.190 (2 ocorrências: comparação e fallback de busca por filtro). Prova real via curl: save na v5 criou a revisão 1 com 3 casos e snapshots canônicos (201). Nota: a revisão 1 do golden set da v5 é fixture de teste do Jarvis ("Teste Jarvis v5 pos-fix") — salvar por cima gera a revisão 2 normalmente.
- proxima_acao: teste humano de Matheus na SKIP `0.0.190`; se aprovado, encerrar TASK-2-007 e seguir para TASK-2-008
- atualizado_em: 2026-09-19
