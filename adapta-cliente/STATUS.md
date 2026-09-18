# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-007 implementada na SKIP `0.0.183`; aguardando teste humano  
**Data:** 18/09/2026  
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos  
**Progresso:** 6 de 16 tasks formalmente concluídas (37,5%); TASK-2-007 implementada (SPEC-2-003 em 1/3)

## Tasks concluídas

- TASK-2-001 — SKIP `0.0.108`.
- TASK-2-002 — SKIP `0.0.121`.
- TASK-2-003 — SKIP `0.0.126`.
- TASK-2-004 — SKIP `0.0.133`.
- TASK-2-005 — SKIP `0.0.163`; teste humano aprovado em 14/09/2026.
- TASK-2-006 — SKIP `0.0.182`; teste humano aprovado em 18/09/2026 ("Pode encerrar e começar a próxima").

## TASK-2-007 — motor de sugestão explicável (SKIP 0.0.183, SPEC-2-003 · CA-2-009)

- **Migração `0063_create_transaction_suggestions`** aplicada: coleção `transaction_suggestions` append-only com RLS por owner, escrita direta bloqueada (create/update/delete = null) e novo tipo de log `sugestao_classificacao`.
- Cada sugestão grava: transação de origem (relation), versão do rulebook, Evento do catálogo, `regra_id` + snapshot completo da regra aplicada, fonte oficial (título + URL da versão), evidência (campos presentes + dados da transação), justificativa textual e autoria/horário.
- **Rota transacional** `POST /backend/v1/suggestions/evaluate`: seleciona o caso, a fonte e o Evento; resolve a versão Aprovada vigente para a competência do caso (sobreposição de vigência bloqueia a avaliação); aplica as regras daquele Evento às transações da fonte.
- Resultado por transação — sempre um dos dois, nunca nada (CA-2-009):
  - **Sugestão**: exatamente uma regra corresponde e todos os campos obrigatórios estão presentes.
  - **Bloqueio**: ambiguidade (mais de uma regra corresponde — item permanece pendente, sem escolha automática), fora do rulebook (nenhuma regra para o Evento) ou evidência insuficiente (campos obrigatórios ausentes).
- Auditoria: toda avaliação grava log em `system_logs` com totais de sugestões/bloqueios, versão do rulebook e autoria.
- **UI "Sugestões"** (rota `/suggestions`, navegação principal): seleção de caso → fonte → Evento, botão "Avaliar transações", resultado consolidado junto ao botão e lista de cartões por transação com regra, fonte, origem, justificativa e motivo do bloqueio.
- 9 testes estáticos provando: RLS e escrita bloqueada, gravação de regra/fonte/origem/evidência, sugestão-ou-bloqueio para toda transação, ambiguidade nunca promovida, vigência/sobreposição, auditoria e navegação protegida.

**Estado do gate:** TASK-2-007 aberta em `aguardando_teste_humano` na SKIP `0.0.183`.

## Próxima ação

- Matheus testa a SKIP `0.0.183` (roterio: caso com rulebook aprovado vigente → Sugestões → selecionar caso/fonte/Evento → Avaliar).
- Se aprovada, encerrar TASK-2-007 e seguir para TASK-2-008 (fila de exceções com severidade, responsável e prazo).
- P1/P2 da auditoria de rastreabilidade do rulebook permanecem como backlog.