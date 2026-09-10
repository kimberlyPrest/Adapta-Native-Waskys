# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-001 aguardando validação humana final
**Data:** 10/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Task ativa:** TASK-2-001 — Modelar cadastro de beneficiários, vínculo e histórico
**Etapa atual:** validação final da versão SKIP `0.0.105`

## Estado comprovado

- O projeto SKIP Cockpit Fiscal está na versão `0.0.105`.
- As migrações `0015` a `0031` estão aplicadas.
- `case_id` é opcional para PF e PJ; nenhum cadastro exige caso na criação.
- `owner` é obrigatório em beneficiários e históricos; RLS usa o proprietário da carteira, mantendo segregação mesmo sem caso.
- O card exibe o status apenas no topo e lista os nomes dentro do bloco `Sócios`/`Empresas vinculadas`; versão permanece no histórico.
- Colunas de Casos usam ✓/✕ e C/D; entrada/saída de sócio gera log; vínculos históricos permanecem preservados.
- Setup, análise estática, build, integrações e teste do pipeline SKIP passaram.
- Todos os demais itens do último teste foram declarados funcionando corretamente pelo Matheus.
- A SPEC-2-001 permanece aberta até o fechamento formal da TASK-2-001; TASK-2-002 e TASK-2-003 continuam pendentes.

## Gates pendentes

- Matheus confirmar cadastro de empresa sem caso e nomes dos sócios dentro do card na versão `0.0.105`.
- Após aprovação explícita, concluir formalmente a TASK-2-001.
- A próxima task só pode ser analisada depois do fechamento desta task.

## Limitações

- `check-escopo` e `check-cliente` continuam pendentes.
- Não há autorização para transmissão, alteração do Domínio ou decisão tributária autônoma.
