# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-006 concluída; início da TASK-2-007  
**Data:** 18/09/2026  
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos  
**Progresso:** 6 de 16 tasks formalmente concluídas (37,5%); SPEC-2-001 e SPEC-2-002 concluídas

## Tasks concluídas

- TASK-2-001 — SKIP `0.0.108`.
- TASK-2-002 — SKIP `0.0.121`.
- TASK-2-003 — SKIP `0.0.126`.
- TASK-2-004 — SKIP `0.0.133`.
- TASK-2-005 — SKIP `0.0.163`; teste humano aprovado em 14/09/2026.
- TASK-2-006 — SKIP `0.0.182`; teste humano aprovado em 18/09/2026 ("Pode encerrar e começar a próxima").

## TASK-2-006 — ciclo do Rulebook (concluída)

### Rastreabilidade P0 (SKIP 0.0.178)

- Migração `0062_add_rulebook_traceability` aplicada, com identidade append-only das regras (`regra_id`, `revisao_regra`, `atual`, `origem_regra_id`) e IDs canônicos obrigatórios de Evento/Natureza.
- Salvamento de Rascunho deixou de apagar e recriar regras; casos e execuções do Golden Set usam IDs canônicos, `catalog_snapshot` e `rastreabilidade`.
- Cópia de versão remapeia Eventos, Naturezas, Regras e casos do Golden Set; snapshots de aprovação/retirada incluem regras atuais e catálogos identificados.

### Ajustes de UX do ciclo (SKIP 0.0.180, feedback de 18/09 manhã)

1. Motivo obrigatório somente ao editar; na criação, o histórico registra "Cadastro inicial — a informação ainda não existia." (backend e UI).
2. Botões Editar e Inativar/Reativar não são mais exibidos em versões Aprovadas/Retiradas.
3. Campo "Nome da natureza" removido do editor de regras; o nome vem do cadastro da Natureza.
4. Histórico do Rulebook exibe o resumo real do backend com diff fiel por `regra_id`.
5. Inativar/Reativar/Editar catálogo atualiza histórico, revisão e contadores sem recarregar a página.
- Higiene: remoção dos arquivos de migração duplicados nunca aplicados (0008, 0017, 0037, 0043); migrações aplicadas permanecem 0001–0062.

### Ajustes de navegação e motivo (SKIP 0.0.181/0.0.182, feedback de 18/09 tarde)

1. Ao trocar de versão, a lista lateral NÃO colapsa e a aba atual permanece selecionada (aprovação/retirada/clonagem também preservam).
2. Cadastro separado das regras: aba própria "Cadastro da versão" (nome, fonte, vigência, motivo; botão "Salvar cadastro") e aba "Regras da versão" só com regras ("Salvar rascunho"); validação por aba. "Nova versão" abre no Cadastro.
3. Nome da versão acompanha o número nos títulos: "Ciclo/Cadastro/Regras da versão v<n> — <nome>".
4. Campo "Motivo da alteração" também na aba "Regras da versão", sincronizado com o Cadastro (0.0.182).

**Encerramento:** teste humano da `0.0.182` aprovado em 18/09/2026; QA completo aprovado; SPEC-2-002 concluída (3/3 tasks).

## Próxima ação

- Início da TASK-2-007: análise da SPEC correspondente, plano submetido ao Matheus e implementação após autorização.
- P1/P2 da auditoria de rastreabilidade (preflight de dependências, concorrência de catálogo, motivo da seleção por competência e ajuste de vigência) permanecem como backlog.