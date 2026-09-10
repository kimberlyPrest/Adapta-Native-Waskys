# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-001 e TASK-2-002 concluídas
**Data:** 10/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Progresso:** 2 de 16 tasks concluídas (12,5%); SPEC-2-001 com 2 de 3 tasks concluídas

## TASK-2-001 — concluída

- Versão validada: SKIP `0.0.108`.
- Vínculos append-only preservados: update/delete bloqueados e sem cascade delete.

## TASK-2-002 — concluída

- Versão validada: SKIP `0.0.121`.
- Teste humano aprovado por Matheus Lohse em 10/09/2026.
- Validação matemática de CPF/CNPJ no frontend e no backend.
- Sequências repetidas, tamanho incorreto e dígitos verificadores inválidos são identificados.
- Documento original é preservado e o valor normalizado alimenta a chave única por owner/carteira.
- Cadastro confirmado exige documento válido; inválidos, ausentes e possíveis correspondências entram na fila sem confirmação silenciosa.
- Duplicidade é impedida no frontend, hook e índice único parcial por owner/documento.
- Coleção `beneficiary_issues` tem RLS por owner e exclusão bloqueada.
- Cadastros vinculados são inativados e reativáveis; botão Inativos possui ícone e contador por categoria.
- Ações automáticas usam autoria Jarvis (IA); ações manuais preservam o operador autenticado.
- Oito testes reais passaram; QA completo, migrações, schema e fluxo no preview foram revalidados.

## Próximo gate

- A TASK-2-003 permanece não iniciada e exige novo pedido para análise.
- A SPEC-2-002 continua bloqueada até o fechamento da SPEC-2-001 e a liberação do gate G2.

## Limitações

- Prova final de acesso cruzado entre owners pertence à TASK-2-003.
- Não há consulta à Receita, fusão automática, OCR ou alteração do Domínio.
