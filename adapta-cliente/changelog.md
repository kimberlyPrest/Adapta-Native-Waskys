# Changelog

## 2026-08-27

- Criada pasta provisória do cliente.
- Exportados o escopo definitivo e as SPECs da Fase 1.
- Registrado que o handoff oficial permanece bloqueado por gates documentais e template público ausentes.
- 04/09/2026: avanço para a Fase 2 autorizado explicitamente pela consultora; geradas 5 SPECs locais para motor determinístico, beneficiários, exceções, consolidação e rascunho R-4010/R-4020.
- 04/09/2026: decompostas 16 tasks executáveis da Fase 2. Produção/transmissão continuam fora do escopo.

## 2026-09-10

- TASK-2-001 implementada em ciclos nas versões `0.0.100` a `0.0.108`: cadastro/revisão versionados, vínculos, logs, cadastro PF/PJ sem caso, owner/RLS por carteira e imutabilidade por API.
- 2026-09-10 · Matheus Lohse · Task TASK-2-001 concluída: teste humano aprovado; QA e schema comprovados no SKIP `0.0.108`.
- TASK-2-002 analisada sem implementação: baseline aceita documentos apenas pelo tamanho, inclusive via criação API; não há dígitos verificadores, unicidade por owner, conflito formal ou fila de pendências.
- Plano da TASK-2-002 delimitado: validação determinística frontend/backend, duplicidade por carteira, pendências auditáveis, bloqueio de confirmação, migração preservando históricos e fixtures executáveis.
- Registros inválidos existentes serão bloqueados e encaminhados à fila, nunca apagados ou corrigidos silenciosamente.
