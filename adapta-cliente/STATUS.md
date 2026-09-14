# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-004 aguardando reteste humano na SKIP 0.0.133
**Data:** 14/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Progresso:** 3 de 16 tasks concluídas (18,75%); TASK-2-004 permanece aberta

## TASK-2-001 a TASK-2-003 — concluídas

- SPEC-2-001 tecnicamente concluída e aprovada.
- Versões validadas: SKIP `0.0.108`, `0.0.121` e `0.0.126`.

## TASK-2-004 — aguardando reteste humano

- Versão para teste: SKIP `0.0.133`.
- Modelo, RLS, escrita exclusiva do backend, rota atômica, histórico e concorrência permanecem validados.
- Campos multilinha agora preservam Enter e aceitam vários campos/regras, um por linha.
- Validação local destaca campos inválidos em vermelho/laranja.
- Aviso aparece no topo e também junto ao botão Salvar.
- Histórico exibe “Quantidade de regras nesta revisão”, esclarecendo que o número representa o conteúdo da revisão.
- Revisões técnicas 1–3 da fixture: Jarvis (IA); revisão humana 4: Matheus Lohse; novas alterações usam autoria textual do usuário autenticado.
- Migrações 0045 e 0047 aplicadas; 23 testes e QA completo passaram; preview autenticado validado.

## Próxima ação

- Matheus repetir o teste humano dos três pontos corrigidos e informar se funcionou.
- TASK-2-005 não foi iniciada.
