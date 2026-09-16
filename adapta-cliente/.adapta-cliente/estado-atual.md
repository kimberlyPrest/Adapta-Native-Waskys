# Estado atual — Adapta Cliente

- task_id: TASK-2-006
- champion: Matheus Lohse
- spec: adapta-cliente/04_fase-atual/02-SPECs/spec-2-002-rulebook-naturezas.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada em 2026-09-15T17:09:00-03:00 — "Pode implementar o plano analisado dos dois catálogos de Eventos e Naturezas na TASK-2-006."
- teste_humano: pendente — retestar rastreabilidade versionada e modal de cópia/retirada na SKIP 0.0.175
- verificacao_automatica: passou — SKIP 0.0.175; migração 0060 aplicada; Eventos/Naturezas e históricos isolados por rulebook_version_id; versões Aprovadas/Retiradas somente leitura; cópia duplica catálogos/regras/Golden Set; opção de retirar origem exige fim de vigência e grava tudo atomicamente com histórico/log. Setup, análise estática, build, integrações e testes passaram; schema confirmou RLS/null e sem cascade; zero erros de hook; preview carregou.
- aprendizado: capturado: adapta-cliente/06_notas/debug/debug-2026-09-16-rastreabilidade-catalogos-rulebook.md
- ultima_acao: correção de rastreabilidade entregue e verificada na SKIP 0.0.175
- proxima_acao: Matheus executar o teste humano da SKIP 0.0.175
- atualizado_em: 2026-09-16T10:15:00-03:00
