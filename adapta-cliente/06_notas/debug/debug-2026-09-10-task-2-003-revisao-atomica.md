# Debug — TASK-2-003 — compatibilidade do hook e regressão de exclusão

- **Data:** 2026-09-10
- **Sintoma 1:** primeira execução da rota atômica retornou 400 sem alterar cadastro nem histórico.
- **Causa raiz 1:** operador spread no hook gerou helper `__spreadValues`, indisponível no runtime PocketBase.
- **Correção 1:** objeto de snapshot passou a ser construído explicitamente; rota revalidada com sucesso v1→v2.
- **Sintoma 2:** preview mostrava Excluir para cadastros sem vínculo e não mostrava a evidência no histórico.
- **Causa raiz 2:** bifurcação antiga por `canDelete` permanecia na UI e no backend.
- **Correção 2:** todos os cadastros usam Inativar; exclusão direta é bloqueada; histórico mostra evidência.
- **Provas:** conflito de versão retornou 400 sem resíduo; acesso cross-owner retornou 404 para leitura e alteração; exclusão direta retornou 400; QA e 14 testes passaram na SKIP 0.0.126.
