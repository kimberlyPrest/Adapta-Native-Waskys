# Changelog

## 2026-08-27

- Criada pasta provisória do cliente.
- Exportados o escopo definitivo e as SPECs da Fase 1.
- Registrado que o handoff oficial permanece bloqueado por gates documentais e template público ausentes.
- 04/09/2026: avanço para a Fase 2 autorizado explicitamente pela consultora; geradas 5 SPECs locais para motor determinístico, beneficiários, exceções, consolidação e rascunho R-4010/R-4020.
- 04/09/2026: decompostas 16 tasks executáveis da Fase 2. Produção/transmissão continuam fora do escopo.

## 2026-09-10

- TASK-2-001 concluída no SKIP `0.0.108`: teste humano, QA, owner/RLS e imutabilidade dos vínculos comprovados.
- TASK-2-002 concluída na SKIP `0.0.121`: validação CPF/CNPJ, conflitos, fila, inativação e autoria auditável aprovados.
- TASK-2-003 implementada na SKIP `0.0.126`: revisão atômica, histórico, segregação cross-owner, inativação e 14 testes aprovados.

## 2026-09-12

- 2026-09-12 · Matheus Lohse · Task TASK-2-003 concluída: SKIP `0.0.126`; teste humano aprovado; SPEC-2-001 tecnicamente concluída com 3 de 3 tasks.
- 2026-09-12 · Matheus Lohse · Gate G2 liberado: Matheus designado responsável tributário; consultoria externa como apoio, sem substituir sua aprovação.
- 2026-09-12 · Matheus Lohse · TASK-2-004 analisada: plano limitado a modelo/editor de Rascunhos; golden set e aprovação/retirada permanecem nas TASK-2-005/006.
- 2026-09-12 · Matheus Lohse · TASK-2-004 implementada tecnicamente na SKIP `0.0.130`: modelo, rota atômica, editor, navegação, histórico e 21 testes. Debug encontrou escrita direta pública causada por regras `""`; tentativa de correção ficou sem prova final por 503.

## 2026-09-14

- 2026-09-14 · Matheus Lohse · DEBUG task TASK-2-004: Cloud voltou, mas a migração 0043 não constava como aplicada e o schema seguia público → causa raiz foi divergência após o 503 → migração idempotente 0044 aplicada na SKIP `0.0.131`; schema `null`, RLS, escrita direta negada, rota atômica, concorrência, histórico, 21 testes, QA e preview revalidados; aguardando teste humano.
