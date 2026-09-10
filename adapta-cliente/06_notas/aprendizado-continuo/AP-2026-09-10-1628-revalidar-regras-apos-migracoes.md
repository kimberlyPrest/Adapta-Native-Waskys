# AP-2026-09-10-1628 — Revalidar regras após migrações posteriores

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: TASK-2-001 / SPEC-2-001
- Sinal: uma migração posterior de domínio reativou `updateRule` em uma coleção que uma migração anterior havia tornado append-only.
- Evidência: schema Skip Cloud da versão 0.0.107 mostrou `beneficiary_links.updateRule` ativo; migração 0032 corrigiu; schema 0.0.108 confirmou update/delete bloqueados.
- Regra reutilizável: após qualquer migração que altere uma coleção existente, revalidar todas as regras finais de acesso e invariantes da coleção, não apenas o campo alterado.
- Quando aplicar: migrações sucessivas sobre RLS, relações, cascade delete ou imutabilidade.
- Quando não aplicar: criação isolada de coleção sem migração posterior que a modifique.
- Confiança: alta — regressão observada no schema aplicado e correção comprovada no backend.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
