# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-006 reaberta com feedback de UX e atendida na SKIP `0.0.181`; aguardando novo teste humano  
**Data:** 18/09/2026  
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos  
**Progresso:** 6 de 16 tasks formalmente concluídas (37,5%); TASK-2-006 reaberta para ajuste de UX; SPEC-2-002 tecnicamente concluída (3/3 tasks)

## Tasks concluídas

- TASK-2-001 — SKIP `0.0.108`.
- TASK-2-002 — SKIP `0.0.121`.
- TASK-2-003 — SKIP `0.0.126`.
- TASK-2-004 — SKIP `0.0.133`.
- TASK-2-005 — SKIP `0.0.163`; teste humano aprovado em 14/09/2026.
- TASK-2-006 — SKIP `0.0.180`; teste humano aprovado em 18/09/2026 ("Teste aprovado podemos continuar"); reaberta no mesmo dia com novo feedback de UX.

## TASK-2-006 — ciclo do Rulebook

### Rastreabilidade P0 (SKIP 0.0.178)

- Migração `0062_add_rulebook_traceability` aplicada, com identidade append-only das regras (`regra_id`, `revisao_regra`, `atual`, `origem_regra_id`) e IDs canônicos obrigatórios de Evento/Natureza.
- Salvamento de Rascunho deixou de apagar e recriar regras; casos e execuções do Golden Set usam IDs canônicos, `catalog_snapshot` e `rastreabilidade`.
- Cópia de versão remapeia Eventos, Naturezas, Regras e casos do Golden Set; snapshots de aprovação/retirada incluem regras atuais e catálogos identificados.

### Ajustes de UX do ciclo (SKIP 0.0.180, feedback de 18/09 manhã)

1. Motivo obrigatório somente ao editar; na criação, o histórico registra "Cadastro inicial — a informação ainda não existia." (backend e UI).
2. Botões Editar e Inativar/Reativar não são mais exibidos em versões Aprovadas/Retiradas (antes ficavam desabilitados).
3. Campo "Nome da natureza" removido do editor de regras; o nome passa a vir do cadastro da Natureza (`natureza_nome` segue gravado no banco a partir do catálogo).
4. Histórico do Rulebook passou a exibir o resumo real gravado pelo backend (`alteracoes`), com diff fiel por `regra_id`; alteração de catálogo registra exatamente "Evento/Natureza <código> <ação>".
5. Inativar/Reativar/Editar catálogo atualiza histórico, revisão e contadores da versão sem exigir recarregar a página.
- Higiene: remoção dos arquivos de migração duplicados nunca aplicados (0008, 0017, 0037, 0043); migrações aplicadas permanecem 0001–0062.

### Ajustes de UX da navegação (SKIP 0.0.181, feedback de 18/09 tarde)

1. Ao trocar de versão na lista lateral, a lista NÃO colapsa mais e a tela permanece na aba selecionada (antes saltava para "Regras da versão" e recolhia a lista).
2. Cadastro separado das regras: nova aba "Cadastro da versão" com nome, fonte oficial, vigência e motivo, com botão "Salvar cadastro"; a aba "Regras da versão" contém apenas as regras, com botão "Salvar rascunho". A validação de erros passou a ser por aba (cada salvar valida só o que está visível).
3. Nome da versão acompanha o número nos títulos: "Ciclo da versão v4 — <nome>", "Cadastro da versão v4 — <nome>" e "Regras da versão v4 — <nome>".
- "Nova versão" abre direto na aba Cadastro.

**Estado do gate:** TASK-2-006 permanece aberta até o novo teste humano de Matheus na `0.0.181`.

## Próxima ação

- Matheus deve revalidar os 3 pontos na SKIP `0.0.181`.
- Se aprovado, revalidar evidências e encerrar formalmente TASK-2-006.
- P1/P2 da auditoria de rastreabilidade (preflight de dependências, concorrência de catálogo, motivo da seleção por competência e ajuste de vigência) permanecem como backlog.