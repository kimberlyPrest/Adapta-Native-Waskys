# Matriz de rastreabilidade — Fase 2

**Status:** planejada — SPECs e tasks geradas; execução condicionada à revisão e aos gates humanos
**Fase:** Motor determinístico e preparação de eventos
**Regra:** a matriz não substitui a aprovação humana do rulebook nem autoriza dados reais, Domínio ou transmissão.

| Requisito / origem | SPEC | Critérios de aceite | Prova principal | Dependência / gate |
|---|---|---|---|---|
| F03, F04, TR-02, TR-04 | SPEC-2-001 | CA-2-001..004 | cadastro, vínculo, histórico e permissão | Fase 1; G2/G3 |
| F04, TR-02, TR-03 | SPEC-2-002 | CA-2-005..008 | rulebook, diff, golden set e aprovação | G2 |
| F03, F05, F08, TR-02, TR-04 | SPEC-2-003 | CA-2-009..012 | fila, decisão humana, justificativa e fallback | SPEC-2-001/002; G2 |
| F02, F05, F06, TR-01, TR-04 | SPEC-2-004 | CA-2-013..016 | matriz de grupos, reconciliação e idempotência | SPEC-2-001/002/003 |
| F06, F08, F09, TR-03, TR-04 | SPEC-2-005 | CA-2-017..021 | pacote, checksum, bloqueios e aviso de não transmissão | SPEC-2-001..004; G2/G4 |

## Critérios e evidências

| Critério | SPEC | Evidência mínima |
|---|---|---|
| CA-2-001..004 | SPEC-2-001 | exportação do cadastro, vínculos e log de acesso |
| CA-2-005..008 | SPEC-2-002 | rulebook versionado, aprovação e golden set |
| CA-2-009..012 | SPEC-2-003 | fila de exceções e auditoria de decisão |
| CA-2-013..016 | SPEC-2-004 | matriz de consolidação, reconciliação e hashes |
| CA-2-017..021 | SPEC-2-005 | pacote de revisão, checksum e checklist manual |

## Tasks

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| TASK-2-001 | Modelar cadastro de beneficiários, vínculo e histórico | Engenheiro | SPEC-2-001 | CA-2-001, CA-2-003 | RED/GREEN da SPEC: criar PF/PJ, vínculo e nova versão do vínculo | migração/modelo, fixture e log de versão | Fase 1 disponível; G3 sem dados reais | ☐ Leva 1 |
| TASK-2-002 | Implementar normalização e validação de CPF/CNPJ com conflitos | Engenheiro | SPEC-2-001 | CA-2-001, CA-2-002 | TDD RED/GREEN: fixture válida, ausente, curta e conflitante | testes/fixtures e relatório de bloqueios | TASK-2-001 | ☐ Leva 2 |
| TASK-2-003 | Implementar revisão de beneficiário e segregação por owner | Engenheiro | SPEC-2-001 | CA-2-003, CA-2-004 | TDD de regressão: alterar vínculo, consultar histórico e tentar acesso cruzado | auditoria, evidência de acesso negado e histórico | TASK-2-001, TASK-2-002 | ☐ Leva 3 |
| TASK-2-004 | Criar modelo e editor de rulebook versionado | Responsável tributário + Engenheiro | SPEC-2-002 | CA-2-005, CA-2-006 | RED/GREEN: regra incompleta rejeitada; regra completa recebe versão | schema, tela/API e registro da versão | G2: responsável tributário identificado | ☐ Leva 1 |
| TASK-2-005 | Implementar golden set e validação de sobreposição de regras | Responsável tributário | SPEC-2-002 | CA-2-005, CA-2-008 | TDD GREEN: casos positivos, negativos, ambíguos e regra sobreposta | golden set versionado e relatório de execução | TASK-2-004 | ☐ Leva 2 |
| TASK-2-006 | Implementar aprovação, retirada e seleção do rulebook por competência | Engenheiro + Responsável tributário | SPEC-2-002 | CA-2-006, CA-2-007 | Regressão: retirar v1, aprovar v2 e reprocessar competência histórica | diff, logs e prova de seleção por vigência | TASK-2-004, TASK-2-005 | ☐ Leva 3 |
| TASK-2-007 | Implementar motor de sugestão explicável por regra e evidência | Engenheiro | SPEC-2-003 | CA-2-009 | RED/GREEN: item claro gera sugestão com regra, fonte e origem | resultado da sugestão e log de execução | TASK-2-001, TASK-2-002, TASK-2-006 | ☐ Leva 4 |
| TASK-2-008 | Implementar fila de exceções com severidade, responsável e prazo | Engenheiro | SPEC-2-003 | CA-2-009, CA-2-010 | RED/GREEN: ambiguidade e falta de evidência entram na fila | captura da fila e registro de exceção | TASK-2-007 | ☐ Leva 5 |
| TASK-2-009 | Implementar decisão humana, justificativa e fallback sem IA | Analista fiscal + Engenheiro | SPEC-2-003 | CA-2-011, CA-2-012 | Regressão: aprovar/rejeitar e executar com serviço indisponível | auditoria de decisão e lote pendente sem promoção | TASK-2-008 | ☐ Leva 6 |
| TASK-2-010 | Implementar chave e agrupamento por beneficiário e fato gerador | Engenheiro | SPEC-2-004 | CA-2-013, CA-2-014 | RED/GREEN: dois pagamentos do mesmo fato e dois fatos distintos | matriz de grupos com chave visível | TASK-2-003, TASK-2-006, TASK-2-009 | ☐ Leva 7 |
| TASK-2-011 | Implementar reconciliação de total e detecção de duplicidades | Engenheiro | SPEC-2-004 | CA-2-013, CA-2-015 | Fixture com FITID repetido, reversão e total divergente | relatório de reconciliação e bloqueios | TASK-2-010 | ☐ Leva 8 |
| TASK-2-012 | Implementar reprocessamento idempotente e histórico do agrupamento | Engenheiro | SPEC-2-004 | CA-2-016 | Regressão: executar mesma versão duas vezes e depois uma nova versão | hashes, diff e contagem sem duplicidade | TASK-2-010, TASK-2-011 | ☐ Leva 9 |
| TASK-2-013 | Implementar modelo de rascunho R-4010/R-4020 e mapeamento PF/PJ | Engenheiro + Analista fiscal | SPEC-2-005 | CA-2-017, CA-2-018 | RED/GREEN: lote misto gera eventos compatíveis com o beneficiário | rascunho estruturado e matriz de campos | TASK-2-010, TASK-2-012 | ☐ Leva 10 |
| TASK-2-014 | Implementar validação de pré-condições e bloqueios do pacote | Engenheiro | SPEC-2-005 | CA-2-019 | Fixture sem rulebook, fonte, aprovador, campo e total conciliado | relatório de bloqueios acionáveis | TASK-2-013 | ☐ Leva 11 |
| TASK-2-015 | Implementar exportação do pacote, checksum e reprodução | Engenheiro | SPEC-2-005 | CA-2-017, CA-2-020 | Regressão: exportar duas vezes a mesma versão e comparar hashes | pacote exportado, checksum e log | TASK-2-014 | ☐ Leva 12 |
| TASK-2-016 | Implementar revisão humana e aviso de não transmissão | Analista fiscal + Responsável tributário | SPEC-2-005 | CA-2-019, CA-2-021 | Fluxo manual de revisar, aprovar/devolver e tentar ação externa | checklist assinado, auditoria e aviso persistente | TASK-2-015 | ☐ Leva 13 |
