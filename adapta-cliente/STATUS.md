# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-005 aguardando teste humano na SKIP 0.0.140
**Data:** 14/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Progresso:** 4 de 16 tasks concluídas (25%); TASK-2-005 permanece aberta; SPEC-2-002 em 1 de 3 concluídas

## Tasks concluídas

- TASK-2-001 — SKIP `0.0.108`.
- TASK-2-002 — SKIP `0.0.121`.
- TASK-2-003 — SKIP `0.0.126`.
- TASK-2-004 — SKIP `0.0.133`.

## TASK-2-005 — aguardando teste humano

- Versão para teste: SKIP `0.0.140`.
- Golden set versionado e append-only vinculado a uma versão do rulebook.
- Casos Positivo, Negativo, Bloqueado e Ambíguo são obrigatórios.
- Executor determinístico usa Evento + Código da natureza normalizado; cenário textual não é interpretado automaticamente.
- Duas regras na mesma chave geram conflito visível e nenhuma escolha automática.
- Relatório mostra Esperado, Observado, PASSOU/FALHOU, campos ausentes e autoria Jarvis (IA).
- Fixture isolada na v2 preserva a v1 e seus históricos; v2 possui quatro regras e snapshot coerente.
- Entrada incompleta e concorrência retornam 400 sem resíduo; escrita direta 403; cross-owner 404.
- Revisão divergente produziu 2 reprovações; revisão correta restaurada append-only e executada com 4/4 aprovados.
- Migrações 0048–0051 aplicadas; 34 testes, QA, schema, API e preview passaram.

## Próxima ação

- Matheus executar o teste humano da TASK-2-005 e informar se funcionou.
- Aprovação, retirada e seleção por competência permanecem fora desta task e reservadas à TASK-2-006.
