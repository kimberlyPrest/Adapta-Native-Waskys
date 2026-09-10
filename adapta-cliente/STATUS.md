# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — fechamento da TASK-2-001 interrompido por regressão técnica
**Data:** 10/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Task ativa:** TASK-2-001 — Modelar cadastro de beneficiários, vínculo e histórico
**Etapa atual:** em correção após verificação independente da versão SKIP `0.0.107`

## Estado comprovado

- Matheus aprovou explicitamente o teste humano da versão `0.0.107`.
- O projeto SKIP está na versão `0.0.107`; migrações `0015` a `0031` estão aplicadas.
- Cadastro PF/PJ sem caso, owner obrigatório, nomes dos sócios no card, evidência automática, logs e fluxos de revisão foram aprovados humanamente.
- A verificação independente de fechamento encontrou uma regressão no schema: `beneficiary_links.updateRule` está ativo após as migrações `0030`/`0031`.
- Isso permitiria alterar uma versão antiga por API, contrariando o histórico append-only da TASK-2-001. `deleteRule` continua bloqueado.
- A TASK-2-001 não foi marcada como concluída e a próxima task não foi iniciada.

## Correção necessária

- Restaurar `beneficiary_links.updateRule = ''` por migração.
- Reexecutar setup, análise estática, build, integrações e testes.
- Confirmar no schema aplicado que `updateRule` e `deleteRule` estão vazios e que `cascadeDelete` continua desativado.
- Executar regressão completa antes do fechamento formal.

## Limitações

- Validação de CPF/CNPJ duplicado permanece corretamente delimitada para a TASK-2-002.
- `check-escopo` e `check-cliente` continuam pendentes.
- Não há autorização para transmissão, alteração do Domínio ou decisão tributária autônoma.
