# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-006 concluída na SKIP `0.0.180` após aprovação humana  
**Data:** 18/09/2026  
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos  
**Progresso:** 6 de 16 tasks formalmente concluídas (37,5%); SPEC-2-002 tecnicamente concluída (3/3 tasks)

## Tasks concluídas

- TASK-2-001 — SKIP `0.0.108`.
- TASK-2-002 — SKIP `0.0.121`.
- TASK-2-003 — SKIP `0.0.126`.
- TASK-2-004 — SKIP `0.0.133`.
- TASK-2-005 — SKIP `0.0.163`; teste humano aprovado em 14/09/2026.
- TASK-2-006 — SKIP `0.0.180`; teste humano aprovado em 18/09/2026 ("Teste aprovado podemos continuar").

## TASK-2-006 — ciclo do Rulebook (concluída)

### Rastreabilidade P0 (SKIP 0.0.178)

- Migração `0062_add_rulebook_traceability` aplicada, com identidade append-only das regras (`regra_id`, `revisao_regra`, `atual`, `origem_regra_id`) e IDs canônicos obrigatórios de Evento/Natureza.
- Salvamento de Rascunho deixou de apagar e recriar regras; casos e execuções do Golden Set usam IDs canônicos, `catalog_snapshot` e `rastreabilidade`.
- Cópia de versão remapeia Eventos, Naturezas, Regras e casos do Golden Set; snapshots de aprovação/retirada incluem regras atuais e catálogos identificados.

### Ajustes de UX do ciclo (SKIP 0.0.180, feedback de 18/09)

1. Motivo obrigatório somente ao editar; na criação, o histórico registra "Cadastro inicial — a informação ainda não existia." (backend e UI).
2. Botões Editar e Inativar/Reativar não são mais exibidos em versões Aprovadas/Retiradas (antes ficavam desabilitados).
3. Campo "Nome da natureza" removido do editor de regras; o nome passa a vir do cadastro da Natureza (`natureza_nome` segue gravado no banco a partir do catálogo).
4. Histórico do Rulebook passou a exibir o resumo real gravado pelo backend (`alteracoes`), com diff fiel por `regra_id`; alteração de catálogo registra exatamente "Evento/Natureza <código> <ação>".
5. Inativar/Reativar/Editar catálogo atualiza histórico, revisão e contadores da versão sem exigir recarregar a página.
- Higiene: remoção dos arquivos de migração duplicados nunca aplicados (0008, 0017, 0037, 0043); migrações aplicadas permanecem 0001–0062.

**Encerramento:** aprovação humana registrada em 18/09/2026; QA completo da `0.0.180` aprovado (setup, análise estática, build, integrações e testes); logs de hooks sem erros.

## Próxima ação

- Aguardar direcionamento do Matheus para a próxima task da Fase 2 (TASK-2-007 em diante).
- P1/P2 da auditoria de rastreabilidade (preflight de dependências, concorrência de catálogo, motivo da seleção por competência e ajuste de vigência) permanecem como backlog.