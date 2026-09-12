# AP-2026-09-12-1253 — Regra vazia no PocketBase é pública, não bloqueada

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: TASK-2-004 / SPEC-2-002
- Sinal: uma coleção com updateRule `""` aceitou PATCH direto cross-owner apesar da expectativa de bloqueio.
- Evidência: `06_notas/debug/debug-2026-09-12-task-2-004-rls.md`; prova HTTP retornou 200 antes da migração 0043; documentação PocketBase v0.36 define `null` como superuser-only e `""` como público.
- Regra reutilizável: ao criar coleções, nunca usar string vazia para bloquear acesso; usar `null` para escrita exclusiva do backend ou expressão RLS explícita para acesso de usuário, e sempre provar GET/POST/PATCH/DELETE por HTTP real.
- Quando aplicar: toda nova coleção PocketBase e toda alteração de regras create/update/delete.
- Quando não aplicar: endpoints ou coleções intencionalmente públicas, documentados e testados como tal.
- Confiança: alta — comportamento reproduzido, documentado e corrigido em migração dedicada.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto
