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
