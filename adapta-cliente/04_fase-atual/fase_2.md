# Fase 2 — Motor determinístico e preparação de eventos

**Status:** planejada — avanço autorizado explicitamente pela consultora; checks documentais permanecem pendentes
**Objetivo:** transformar as transações normalizadas da Fase 1 em uma matriz fiscal revisável, rastreável e bloqueável.

## Resultado da fase

Para uma competência piloto, o analista consegue revisar pagamentos candidatos, associar beneficiário CPF/CNPJ, aplicar um rulebook versionado, consolidar por beneficiário/fato gerador e gerar um rascunho auditável de R-4010/R-4020. Toda ambiguidade vira exceção; nenhuma saída é tratada como transmitida ou aprovada automaticamente.

## Onda de SPECs

1. SPEC-2-001 — cadastro fiscal e carteira de beneficiários;
2. SPEC-2-002 — rulebook versionado e catálogo de naturezas;
3. SPEC-2-003 — classificação assistida e fila de exceções;
4. SPEC-2-004 — consolidação por beneficiário/fato gerador;
5. SPEC-2-005 — rascunho R-4010/R-4020 e pacote de revisão.

## Dependências e gates

- Fonte e transações da Fase 1 disponíveis e rastreáveis.
- CNPJ, competência e coorte piloto definidos.
- Responsável tributário deve aprovar o rulebook e o golden set antes de dados reais.
- Tabelas oficiais usadas devem registrar versão, vigência, fonte e data de consulta.
- O avanço foi autorizado pela consultora apesar de `check-escopo` e `check-cliente` pendentes; isso não equivale à aprovação desses checks.

## Fora desta fase

- R-4099 produtivo, fechamento e transmissão;
- importação, alteração ou automação no Domínio;
- DCTFWeb, DARF, e-CAC, certificado, captcha ou RPA;
- aprovação fiscal autônoma por IA;
- interpretação automática de atas, contratos ou PDFs não estruturados;
- cobertura de eventos REINF fora do universo explicitamente homologado.

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

## Evidência mínima de encerramento

- matriz de classificação da competência piloto;
- versão do rulebook e aprovação humana;
- exceções resolvidas ou bloqueadas com responsável e motivo;
- rascunhos R-4010/R-4020 com origem por linha;
- pacote de revisão exportado e reproduzível;
- checklist manual demonstrando que nenhum resultado foi transmitido.
