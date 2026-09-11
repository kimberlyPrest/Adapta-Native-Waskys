# AP-2026-09-10-2235 — Hooks PocketBase devem evitar helpers de transpiração não suportados

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: TASK-2-003 / SPEC-2-001
- Sinal: operador spread em objeto dentro de hook foi convertido para `__spreadValues`, ausente no runtime, e a rota falhou antes do commit.
- Evidência: `06_notas/debug/debug-2026-09-10-task-2-003-revisao-atomica.md`; teste da rota na SKIP 0.0.123 falhou sem resíduo e passou na 0.0.124 após objeto explícito.
- Regra reutilizável: em hooks PocketBase, preferir objetos explícitos e construções JavaScript suportadas diretamente pelo runtime; sempre exercitar a rota real após o build, porque análise estática não detecta helper ausente em runtime.
- Quando aplicar: qualquer hook ou migração que use spread, transformação de sintaxe moderna ou helper injetado pelo build.
- Quando não aplicar: frontend React, onde o pipeline Vite fornece os helpers necessários.
- Confiança: alta — falha reproduzida, causa registrada no log e correção confirmada por teste HTTP real.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto
