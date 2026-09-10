# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-002 implementada e aguardando teste humano
**Data:** 10/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Progresso:** 1 de 16 tasks concluída (6,25%); SPEC-2-001 com 1 concluída e 1 em teste

## TASK-2-001 — concluída

- Versão validada: SKIP `0.0.108`.
- Vínculos append-only preservados na `0.0.111`: update/delete bloqueados e sem cascade delete.

## TASK-2-002 — aguardando teste humano

- Versão: SKIP `0.0.111`.
- Validação matemática de CPF/CNPJ no frontend e no backend.
- Sequências repetidas, tamanho incorreto e dígitos verificadores inválidos são identificados.
- Cadastro confirmado exige documento válido; candidato pode ficar sem documento ou com documento inválido e entra na fila.
- Duplicidade é impedida por owner/carteira e por índice único parcial no banco.
- Tentativas duplicadas apontam o cadastro existente da mesma carteira e geram pendência.
- Possíveis correspondências por nome viram pendência, sem fusão automática.
- Coleção `beneficiary_issues` possui RLS por owner, exclusão bloqueada e campos de origem imutáveis.
- Pendências inválidas/ausentes só se resolvem após correção válida; duplicidade/correspondência exige justificativa, operador e data.
- Backfill preservou os registros existentes; inválidos foram versionados como bloqueados e encaminhados à fila.
- O teste placeholder foi substituído por 8 testes reais de normalização, CPF, CNPJ, curto, repetição, dígitos inválidos, ausente e nome semelhante.
- QA passou em setup, análise estática, build, integrações e testes.

## Gate pendente

- Matheus validar o fluxo autenticado da TASK-2-002 na versão `0.0.111`.
- A TASK-2-003 não será iniciada antes da aprovação e conclusão formal desta task.

## Limitações

- Prova final de acesso cruzado entre owners pertence à TASK-2-003.
- Não há consulta à Receita, fusão automática, OCR ou alteração do Domínio.
