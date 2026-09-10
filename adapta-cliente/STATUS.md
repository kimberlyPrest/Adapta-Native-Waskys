# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — SPEC-2-001 parcialmente implementada e em análise de correção
**Data:** 10/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Task ativa:** TASK-2-001 — Modelar cadastro de beneficiários, vínculo e histórico
**Etapa atual:** aguardando autorização para implementar o plano de correção

## Estado comprovado

- O projeto SKIP Cockpit Fiscal está na versão `0.0.99`.
- As migrações `0015` a `0028` relacionadas a beneficiários, vínculos, históricos e correções cadastrais estão aplicadas.
- Existem cadastro PF/PJ, relacionamentos cliente–sócio, vínculo versionado por transação, histórico append-only e regras de acesso por owner.
- A TASK-2-001 ainda não está concluída: o vínculo de transação é salvo como `candidato` ou `bloqueado`, sem fluxo completo de confirmação com operador, data e motivo.
- A SPEC-2-001 permanece aberta. Validação matemática de CPF/CNPJ, conflitos e fila pertencem à TASK-2-002; a prova de segregação entre owners pertence à TASK-2-003.
- A SPEC-2-002 não foi iniciada e continua dependente do fechamento da SPEC-2-001 e do gate G2.

## Gates pendentes

- Autorizar e implementar o recorte de correção da TASK-2-001.
- Executar verificações automáticas e teste humano da TASK-2-001.
- Implementar e aprovar TASK-2-002 e TASK-2-003 antes de encerrar a SPEC-2-001.
- Identificar/aprovar o responsável tributário e liberar G2 antes da SPEC-2-002.

## Limitações

- `check-escopo` e `check-cliente` continuam pendentes e não são substituídos pelo avanço autorizado da Fase 2.
- Não há autorização para transmissão, alteração do Domínio ou decisão tributária autônoma.
- Dados reais para rulebook e golden set dependem de aprovação do responsável tributário.
