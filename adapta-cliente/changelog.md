# Changelog

## 2026-08-27

- Criada pasta provisória do cliente.
- Exportados o escopo definitivo e as SPECs da Fase 1.
- Registrado que o handoff oficial permanece bloqueado por gates documentais e template público ausentes.
- 04/09/2026: avanço para a Fase 2 autorizado explicitamente pela consultora; geradas 5 SPECs locais para motor determinístico, beneficiários, exceções, consolidação e rascunho R-4010/R-4020. Tasks ainda não decompostas e nenhum push/publicação realizado.
- 04/09/2026: decompostas 16 tasks executáveis da Fase 2, sincronizadas na fase, nas 5 SPECs e na matriz de rastreabilidade. Produção/transmissão continuam fora do escopo.

## 2026-09-10

- Documentação operacional atualizada para refletir o estado observado do projeto SKIP Cockpit Fiscal `0.0.99`.
- TASK-2-001 implementada em ciclos nas versões `0.0.100`, `0.0.102` e `0.0.103`: cadastro/revisão versionados, vínculos append-only, logs obrigatórios/realtime, status visível, confirmação manual, operador em alocações, modais com X, colunas compactas e preservação de lançamentos após saída de sócio.
- Migração `0029` tornou `beneficiary_links` append-only e sem exclusão em cascata.
- Migração `0030` tornou `case_id` opcional inicialmente para PF.
- 2026-09-10 · Matheus Lohse · ciclos de teste humano: fluxo de revisão/fechamento aprovado; demais itens da versão `0.0.103` declarados funcionando, restando corrigir cadastro PJ sem caso e nomes dos sócios dentro do card.
- SKIP `0.0.105`: migração `0031` adicionou `owner` obrigatório a beneficiários/históricos, aplicou RLS por proprietário e manteve `case_id` opcional para PF/PJ; formulário deixou de exigir caso; card passou a listar os nomes dos sócios/empresas vinculadas dentro do próprio bloco.
- QA da versão `0.0.105` passou em setup, análise estática, build, integrações e teste; schema confirmou `owner` obrigatório e `case_id` opcional.
