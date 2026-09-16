# Estado atual — Adapta Cliente

- task_id: TASK-2-006
- champion: Matheus Lohse
- spec: adapta-cliente/04_fase-atual/02-SPECs/spec-2-002-rulebook-naturezas.md
- etapa: em_correcao
- autorizacao_implementacao: confirmada em 2026-09-15T17:09:00-03:00 — "Pode implementar o plano analisado dos dois catálogos de Eventos e Naturezas na TASK-2-006."
- teste_humano: falhou em 2026-09-16T09:56:00-03:00 — inativar Natureza desassociou regras da versão 2 Retirada sem log; catálogos não estavam claros nem isolados por versão
- verificacao_automatica: pendente — corrigir versionamento dos catálogos, preservação histórica e cópia com retirada/fim de vigência opcionais
- aprendizado: pendente
- ultima_acao: causa raiz confirmada — Eventos e Naturezas eram registros globais mutáveis ligados por relação viva às regras de todas as versões
- proxima_acao: aplicar correção versionada e atômica na TASK-2-006 e executar regressões
- atualizado_em: 2026-09-16T10:05:00-03:00
