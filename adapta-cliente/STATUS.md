# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-003 implementada e aguardando teste humano
**Data:** 10/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Progresso:** 2 de 16 tasks concluídas (12,5%); SPEC-2-001 com 2 concluídas e 1 em teste

## TASK-2-001 — concluída

- Versão validada: SKIP `0.0.108`.
- Vínculos append-only preservados: update/delete bloqueados e sem cascade delete.

## TASK-2-002 — concluída

- Versão validada: SKIP `0.0.121`.
- Teste humano aprovado; CPF/CNPJ, conflitos, fila, inativação e autoria auditável validados.

## TASK-2-003 — aguardando teste humano

- Versão: SKIP `0.0.126`.
- Revisão cadastral executada por rota autenticada e transação atômica.
- Cadastro, histórico e log são gravados juntos; falha ou versão obsoleta não deixa histórico órfão.
- Vínculos de transação continuam append-only: alterações criam nova versão.
- Fixture de segundo owner usa senha aleatória gerada no servidor, sem credencial fixa versionada.
- Prova HTTP real: leitura e alteração cross-owner retornaram 404.
- Exclusão direta de cadastro retorna 400; interface usa Inativar e preserva reativação.
- Histórico exibe data, usuário, alteração, motivo e evidência.
- 14 testes passaram; setup, análise estática, build, integrações e preview foram validados.

## Gate pendente

- Matheus validar o fluxo autenticado da TASK-2-003 na versão `0.0.126`.
- Nenhuma task posterior será iniciada antes da aprovação e conclusão formal.

## Limitações

- A SPEC-2-002 continua bloqueada até o fechamento da SPEC-2-001 e a liberação do gate G2.
- Não há consulta à Receita, fusão automática, OCR ou alteração do Domínio.
