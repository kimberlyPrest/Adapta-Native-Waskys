# Changelog

## 2026-08-27

- Criada pasta provisória do cliente.
- Exportados o escopo definitivo e as SPECs da Fase 1.
- Registrado que o handoff oficial permanece bloqueado por gates documentais e template público ausentes.
- 04/09/2026: avanço para a Fase 2 autorizado explicitamente pela consultora; geradas 5 SPECs locais para motor determinístico, beneficiários, exceções, consolidação e rascunho R-4010/R-4020.
- 04/09/2026: decompostas 16 tasks executáveis da Fase 2. Produção/transmissão continuam fora do escopo.

## 2026-09-10

- TASK-2-001 implementada em ciclos nas versões `0.0.100` a `0.0.107`: cadastro/revisão versionados, vínculos, logs obrigatórios/realtime, cadastro PF/PJ sem caso, owner/RLS por carteira, status, confirmação manual, operador em alocações, modais, colunas compactas, preservação de lançamentos e sócios no card.
- Migração `0029` tornou `beneficiary_links` append-only e sem exclusão em cascata.
- Migrações `0030`/`0031` tornaram caso opcional e adicionaram owner obrigatório aos beneficiários/históricos.
- SKIP `0.0.107`: evidência automática `Cadastro manual realizado pelo operador`; QA passou.
- Validação de documento duplicado delimitada para a TASK-2-002.
- 2026-09-10 · Matheus Lohse · teste humano da TASK-2-001 aprovado na versão `0.0.107`.
- Verificação independente de fechamento encontrou regressão: migração `0030` havia reativado `beneficiary_links.updateRule`; conclusão foi interrompida.
- Matheus confirmou a regra: deve ser impossível alterar versões antigas, inclusive pela API.
- SKIP `0.0.108`: migração `0032` restaurou a imutabilidade. QA completo passou; schema confirmou `updateRule` e `deleteRule` vazios e `cascadeDelete=false`.
- 2026-09-10 · Matheus Lohse · Task TASK-2-001 concluída: fluxo humano aprovado; modelo, vínculos versionados, histórico, logs, owner/RLS e imutabilidade por API comprovados no SKIP `0.0.108`.
