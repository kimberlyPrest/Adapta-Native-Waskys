# Changelog

## 2026-08-27

- Criada pasta provisória do cliente.
- Exportados o escopo definitivo e as SPECs da Fase 1.
- Registrado que o handoff oficial permanece bloqueado por gates documentais e template público ausentes.
- 04/09/2026: avanço para a Fase 2 autorizado explicitamente pela consultora; geradas 5 SPECs locais para motor determinístico, beneficiários, exceções, consolidação e rascunho R-4010/R-4020.
- 04/09/2026: decompostas 16 tasks executáveis da Fase 2. Produção/transmissão continuam fora do escopo.

## 2026-09-10

- TASK-2-001 concluída no SKIP `0.0.108`: teste humano, QA, owner/RLS e imutabilidade dos vínculos comprovados.
- TASK-2-002 analisada: baseline validava apenas tamanho; sem dígitos verificadores, unicidade, conflitos ou fila.
- Matheus autorizou a implementação da TASK-2-002: "Sim, pode implementar".
- RED reproduzido: `111.111.111-11` e `11.111.111/0001-11` eram aceitos pela regra de tamanho.
- SKIP `0.0.111`: implementado validador determinístico de CPF/CNPJ no frontend/backend, incluindo normalização, sequências repetidas e dígitos verificadores.
- Migração `0033` adicionou `documento_chave`, `documento_valido`, índice único parcial por owner/documento e coleção `beneficiary_issues` com RLS.
- Backfill preservou cadastros; inválidos/duplicados existentes foram bloqueados por nova versão e encaminhados à fila; ausentes permaneceram candidatos.
- Cadastro confirmado exige documento válido; candidato inválido/ausente gera pendência. Vínculo confirmado também exige beneficiário com documento válido.
- Duplicidade é bloqueada no frontend, hook e índice; possíveis correspondências por nome não são fundidas automaticamente.
- Fila cadastral permite resolução auditável e protege origem/owner; documento inválido/ausente só fecha após correção válida.
- Teste placeholder substituído por 8 testes reais, todos aprovados. QA completo passou; `beneficiary_links` permaneceu append-only.
- 2026-09-10 · Matheus Lohse · DEBUG task TASK-2-002: fluxos de preservação ainda exibiam “Excluir/Desligar” e a autoria Jarvis não aparecia → causa raiz: UI bifurcava exclusão definitiva e relações de usuários de sistema não expandiam na sessão humana → corrigido na SKIP `0.0.119` com Inativar/Inativo, autoria textual auditável e fixture sintética completa; QA passou, mas a prova visual final ficou bloqueada por 503 do Skip Cloud.
- 2026-09-10 · Matheus Lohse · DEBUG task TASK-2-002: autoria ainda incorreta e acesso a inativos discreto → causa raiz: migração de autoria pendente estava corrompida e o botão não informava volume → corrigido na SKIP `0.0.121`; `jarvis@waskys.local` aparece como Jarvis (IA), botão recebeu ícone e contador por categoria; QA e fluxo real no preview passaram.
- 2026-09-10 · Matheus Lohse · Task TASK-2-002 concluída: SKIP `0.0.121`; teste humano aprovado; normalização/validação de CPF/CNPJ, conflitos, fila, índice único por owner, autoria auditável, 8 testes, QA, schema e preview revalidados.
- 2026-09-10 · Matheus Lohse · TASK-2-003 analisada: revisão e históricos append-only já existem; faltam operação atômica para revisão cadastral, fixture/prova de dois owners e testes de acesso cruzado negado sem ampliar o escopo para o rulebook.
- 2026-09-10 · Matheus Lohse · TASK-2-003 implementada na SKIP `0.0.126`: revisão atômica com controle de versão, histórico/log transacionais, fixture segura de segundo owner, leitura/alteração cross-owner negadas (404), exclusão direta bloqueada (400), vínculos append-only e 14 testes aprovados; aguarda teste humano.

## 2026-09-12

- 2026-09-12 · Matheus Lohse · Task TASK-2-003 concluída: SKIP `0.0.126`; teste humano aprovado; revisão atômica, histórico com evidência, concorrência sem resíduo, segregação cross-owner, inativação e 14 testes revalidados. SPEC-2-001 tecnicamente concluída com 3 de 3 tasks.
