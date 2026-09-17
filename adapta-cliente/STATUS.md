# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-006 implementada tecnicamente na SKIP `0.0.178`; teste humano pendente  
**Data:** 17/09/2026  
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos  
**Progresso:** 5 de 16 tasks formalmente concluídas (31,25%); SPEC-2-002 com TASK-2-006 tecnicamente implementada, aguardando aprovação humana

## Tasks concluídas

- TASK-2-001 — SKIP `0.0.108`.
- TASK-2-002 — SKIP `0.0.121`.
- TASK-2-003 — SKIP `0.0.126`.
- TASK-2-004 — SKIP `0.0.133`.
- TASK-2-005 — SKIP `0.0.163`; teste humano aprovado em 14/09/2026.

## TASK-2-005 — concluída

- Golden set versionado e append-only vinculado a uma versão do rulebook.
- Casos Positivo, Negativo, Bloqueado e Ambíguo obrigatórios.
- Executor determinístico por Evento + Código da natureza normalizado; cenário textual não é interpretado automaticamente.
- Sobreposição gera conflito visível e nenhuma escolha automática.
- Relatório mostra Esperado, Observado, PASSOU/FALHOU, campos ausentes, autoria e horário.
- Históricos do Rulebook e Golden Set mostram Data, Usuário, O que mudou e Motivo, com número da Regra/Caso e sem coluna/célula residual de versão.
- Lista de versões abre a mais nova e pode ser recolhida lateralmente.
- Entrada incompleta e concorrência retornam erro sem resíduo; escrita direta e acesso cruzado permanecem bloqueados.
- Migrações 0048–0056 aplicadas; setup, análise estática, build, integrações, suíte, regressões e teste humano da SKIP `0.0.163` aprovados.

## TASK-2-006 — implementação técnica na SKIP 0.0.178

- Migração `0062_add_rulebook_traceability` aplicada, com identidade append-only das regras (`regra_id`, `revisao_regra`, `atual`, `origem_regra_id`) e IDs canônicos obrigatórios de Evento/Natureza.
- Salvamento de Rascunho deixou de apagar e recriar regras: regras atuais são preservadas; alterações geram nova revisão; substituições ficam marcadas sem exclusão física.
- Casos do Golden Set passaram a registrar `event_catalog_id`, `nature_catalog_id` quando existente e `catalog_snapshot` da mesma versão.
- Execuções do Golden Set registram `rastreabilidade` com versão do Rulebook, revisão do Golden Set, snapshots dos catálogos e snapshots das regras avaliadas.
- Cópia de versão remapeia Eventos, Naturezas, Regras e casos do Golden Set para novos IDs, preservando `origin_catalog_id`/`origem_regra_id` e a origem no snapshot.
- Snapshots de aprovação e retirada incluem identidade/revisão das regras e snapshots de Evento/Natureza; o ciclo considera somente regras atuais.
- UI do Golden Set carrega os catálogos ativos da versão e envia os IDs canônicos; Código inexistente continua possível somente para caso Negativo.
- QA oficial da SKIP `0.0.178`: setup, análise estática, build, integrações e testes aprovados.
- Schema confirmado: `rulebook_rules` com IDs/revisões obrigatórios; `golden_set_cases.event_catalog_id` e `catalog_snapshot` obrigatórios; `golden_set_runs.rastreabilidade` obrigatório.
- Preview carregado até o login e logs de hooks sem erros após a implantação.

**Estado do gate:** implementação técnica aprovada automaticamente; TASK-2-006 permanece aberta até teste humano de Matheus.

## Próxima ação

- Matheus deve executar o roteiro humano de rastreabilidade na SKIP `0.0.178`.
- Se aprovado, revalidar evidências e encerrar formalmente TASK-2-006.
- P1/P2 da auditoria (preflight de dependências, concorrência de catálogo, motivo da seleção por competência e ajuste de vigência) não foram incluídos nesta entrega.
