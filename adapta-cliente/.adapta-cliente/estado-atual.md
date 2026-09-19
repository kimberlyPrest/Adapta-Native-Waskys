# Estado atual — Adapta Cliente

- task_id: TASK-2-007
- champion: Matheus Lohse
- spec: adapta-cliente/04_fase-atual/02-SPECs/spec-2-003-classificacao-excecoes.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada em 2026-09-18 ("Autorização")
- teste_humano: pendente — validar a SKIP `0.0.189` (motor de sugestão + criação de rulebook do zero + páginas Casos/Sugestões/Golden set ajustadas)
- verificacao_automatica: aprovada — SKIP `0.0.189`; setup, análise estática, build, integrações e testes passaram
- ultima_acao: ajuste de 19/09 no Golden set — o campo "Código da natureza" virou dropdown alimentado pelas naturezas com regra ativa na versão, filtrado pelo Evento do caso (auto-seleção quando só há uma opção; troca de Evento re-filtra e re-auto-seleciona; códigos legados sem regra continuam visíveis marcados "sem regra ativa nesta versão"; sem Evento selecionado, pede o Evento primeiro). Verificado no preview (v5: 12001 auto-selecionada em R-4010 e R-4020; v4: naturezas com regra no dropdown e códigos legados preservados)
- proxima_acao: teste humano de Matheus na SKIP `0.0.189`; se aprovado, encerrar TASK-2-007 e seguir para TASK-2-008
- atualizado_em: 2026-09-19
