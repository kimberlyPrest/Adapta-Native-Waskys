# SPEC-2-002 — Rulebook versionado e catálogo de naturezas

**Fase:** 2  
**Status:** planejada — depende do gate G2  
**Dono:** responsável tributário  
**Origem no escopo:** F04, TR-02, TR-03, G2  
**Degrau da solução:** construção mínima — catálogo interno versionado com fonte e vigência, sem inferir regra de material não homologado.

## Resultado observável

O responsável tributário publica uma versão do rulebook com fontes, vigência, universo de eventos, naturezas e cenários. O motor só pode usar uma regra vigente e aprovada; versões antigas permanecem consultáveis e resultados afetados podem ser invalidados.

## Limites e dependências

- **Inclui:** versão; status rascunho/aprovada/retirada; vigência; fonte; aprovador; natureza; evento aplicável; campos obrigatórios; regra de bloqueio; golden set.
- **Fora de escopo:** interpretação autônoma da legislação, atualização automática, parecer jurídico e transmissão.
- **Entradas e pré-condições:** tabela oficial e decisões da Waskys; responsável tributário identificado.
- **Saídas/artefatos:** rulebook aprovado; diff entre versões; golden set; log de aprovação/retirada.
- **Dependências e responsáveis:** decisão humana G2; Fase 1; validação do cliente.
- **Risco e plano B:** fonte ou vigência ausente bloqueia publicação; operar somente com dados sintéticos até aprovação.
- **Rollback ou reversão:** retirar versão para novos processamentos; resultados históricos apontam para a versão original.

## Fluxo e regras

1. Responsável cria rascunho com fonte, vigência e cenários.
2. Sistema valida campos mínimos e compara com versão anterior.
3. Responsável aprova ou rejeita.
4. Processamento seleciona a versão vigente pela competência e registra o ID.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | regra completa e aprovada | disponível para classificação na competência | registrar rulebook_id |
| Limite | duas regras cobrem a mesma natureza | conflito visível; nenhuma escolha silenciosa | decisão tributária explícita |
| Falha | regra sem fonte, vigência ou aprovador | publicação bloqueada | completar dados e reenviar |

## Checklist de execução

- [ ] Cada regra tem fonte, vigência e aprovador.
- [ ] Eventos e naturezas são delimitados pelo universo homologado.
- [ ] Golden set cobre casos positivos, negativos e ambíguos.
- [ ] Diferenças entre versões são visualizáveis.
- [ ] Retirada de regra preserva resultados históricos.

## Critérios de aceite

- [ ] **CA-2-005:** regra incompleta não pode ser aprovada nem usada pelo motor.
- [ ] **CA-2-006:** classificação registra a versão exata do rulebook usada.
- [ ] **CA-2-007:** regra retirada não é aplicada a novo processamento, mas permanece no histórico.
- [ ] **CA-2-008:** golden set reproduz as decisões aprovadas pelo responsável tributário.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | publicar regra sem fonte/vigência | fixture incompleta | publicação rejeitada | mensagem e log |
| GREEN | aprovar versão completa | cadastrar rulebook + golden set | CA-2-005 a CA-2-008 passam | versão aprovada |
| REFACTOR/REGRESSÃO | retirar e substituir versão | reprocessar competência histórica e nova | histórico usa versão antiga; novo uso bloqueia retirada | diff + log |

**Dados/fixtures:** catálogo sintético com R-4010/R-4020, três naturezas, regra sobreposta, versão v1 e v2.  
**Caminhos de erro obrigatórios:** fonte ausente, vigência inválida, sobreposição, retirada e alteração normativa.  
**Evidência exigida:** rulebook exportado, aprovação do responsável tributário e execução do golden set.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| TASK-2-004 | Criar modelo e editor de rulebook versionado | Responsável tributário + Engenheiro | SPEC-2-002 | CA-2-005, CA-2-006 | RED/GREEN: regra incompleta rejeitada; regra completa recebe versão | schema, tela/API e registro da versão | G2: responsável tributário identificado | ☐ Leva 1 |
| TASK-2-005 | Implementar golden set e validação de sobreposição de regras | Responsável tributário | SPEC-2-002 | CA-2-005, CA-2-008 | TDD GREEN: casos positivos, negativos, ambíguos e regra sobreposta | golden set versionado e relatório de execução | TASK-2-004 | ☐ Leva 2 |
| TASK-2-006 | Implementar aprovação, retirada e seleção do rulebook por competência | Engenheiro + Responsável tributário | SPEC-2-002 | CA-2-006, CA-2-007 | Regressão: retirar v1, aprovar v2 e reprocessar competência histórica | diff, logs e prova de seleção por vigência | TASK-2-004, TASK-2-005 | ☐ Leva 3 |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
