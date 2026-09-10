# AP-2026-09-10-2016 — Autoria de automação exige identidade persistida e exibição verificável

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: TASK-2-002 / SPEC-2-001
- Sinal: criar um usuário de sistema não tornou sua autoria visível; relações de autenticação do operador de sistema não expandiam de forma confiável na sessão humana, e uma migração pendente com identidade incorreta atrasou a correção.
- Evidência: `06_notas/debug/debug-2026-09-10-inativacao-autoria-jarvis.md`; SKIP 0.0.121; preview confirmou Jarvis (IA) no histórico e nos Logs, enquanto ações manuais permaneceram atribuídas a Matheus Lohse.
- Regra reutilizável: em ações automáticas, persistir o ID do usuário de sistema canônico e uma autoria textual auditável; antes de aplicar, reler a migração pendente e validar a identidade por e-mail canônico; depois, provar a exibição no histórico e nos logs com sessão do proprietário.
- Quando aplicar: backfills, migrações, resoluções automáticas e fixtures operacionais atribuídas a Jarvis (IA).
- Quando não aplicar: ações iniciadas manualmente por operador autenticado, que devem manter a autoria humana real.
- Confiança: alta — causa reproduzida, corrigida e confirmada no banco, histórico, Logs e teste humano.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto
