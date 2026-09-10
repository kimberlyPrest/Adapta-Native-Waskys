# Changelog

## 2026-08-27

- Criada pasta provisória do cliente.
- Exportados o escopo definitivo e as SPECs da Fase 1.
- Registrado que o handoff oficial permanece bloqueado por gates documentais e template público ausentes.
- 04/09/2026: avanço para a Fase 2 autorizado explicitamente pela consultora; geradas 5 SPECs locais para motor determinístico, beneficiários, exceções, consolidação e rascunho R-4010/R-4020. Tasks ainda não decompostas e nenhum push/publicação realizado.
- 04/09/2026: decompostas 16 tasks executáveis da Fase 2, sincronizadas na fase, nas 5 SPECs e na matriz de rastreabilidade. Produção/transmissão continuam fora do escopo.

## 2026-09-10

- Documentação operacional atualizada para refletir o estado observado do projeto SKIP Cockpit Fiscal `0.0.99`.
- Registrado que a TASK-2-001 possui modelagem e interface parcialmente implementadas: cadastro PF/PJ, relacionamentos, vínculos versionados, históricos append-only e RLS por owner.
- Mantida a TASK-2-001 aberta porque a alocação por transação ainda gravava somente `candidato` ou `bloqueado`, sem confirmação rastreável com operador, data e motivo.
- Separadas as pendências por escopo: validação matemática, duplicidade, conflitos e fila pertencem à TASK-2-002; revisão completa e prova de acesso cruzado pertencem à TASK-2-003.
- SPEC-2-002 mantida como não iniciada e dependente do fechamento da SPEC-2-001 e do gate G2.
- Matheus autorizou explicitamente a implementação do plano da TASK-2-001 com a mensagem "Sim".
- SKIP `0.0.100`: implementada revisão de cadastro candidato para confirmado/bloqueado, criando nova versão com motivo, evidência, operador e data.
- SKIP `0.0.100`: implementada revisão da alocação por transação, com nova versão confirmada/bloqueada e consulta de todo o histórico na página de Casos.
- Migração `0029` aplicada: `beneficiary_links` passou a ser append-only (`updateRule`/`deleteRule` bloqueados) e deixou de ser apagado em cascata pelo beneficiário.
- Hook de integridade adicionado: decisões confirmadas/bloqueadas exigem motivo, evidência, operador e data; exclusão de beneficiário com vínculo, histórico ou relacionamento é rejeitada.
- Pipeline SKIP completo passou: setup, análise estática, build, integrações e teste. O teste automatizado do projeto continua sendo placeholder; fluxo autenticado aguarda validação humana.
- 2026-09-10 · Matheus Lohse · DEBUG task TASK-2-001: teste humano encontrou logs aparentemente ausentes, status pouco visível, criação manual sem confirmação, operador ausente na alocação candidata e modais novos sem X → causa raiz: logs não atualizavam em tempo real, edição comum não os criava, alocação rápida omitia auditoria e novos modais não herdaram o padrão visual → corrigido no SKIP `0.0.102`.
- SKIP `0.0.102`: criação manual permite `candidato` ou `confirmado`; confirmação exige evidência e registra operador/data; status destacado nos cards e detalhes.
- SKIP `0.0.102`: edição comum passa a gerar log; página de Logs atualiza por realtime/foco; falha de log deixa de ser silenciosa.
- SKIP `0.0.102`: alocação candidata/desalocação registra operador, data, motivo e evidência; coluna `Estado/Tipo` renomeada para `Situação do lançamento`.
- SKIP `0.0.102`: adicionados botões X superiores aos três modais que faltavam. Pipeline completo passou após tornar o hook compatível com o isolamento de callbacks do PocketBase JSVM.
