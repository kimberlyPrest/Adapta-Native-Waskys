# SPEC-2-004 — Consolidação por beneficiário e fato gerador

**Fase:** 2  
**Status:** planejada — execução condicionada às SPECs 2-001, 2-002 e 2-003  
**Dono:** analista fiscal, com revisão do responsável tributário  
**Origem no escopo:** F02, F05, F06, TR-01, TR-04  
**Degrau da solução:** construção mínima — agregação determinística sobre transações rastreáveis, sem criar valores de transição.

## Resultado observável

O sistema consolida pagamentos relacionados por beneficiário, competência, data/fato gerador, natureza e evento. O total agregado pode ser aberto até cada transação original, sem duplicidade nem perda silenciosa.

## Limites e dependências

- **Inclui:** chave de consolidação; múltiplos pagamentos; reversões identificadas; totais bruto e retenções quando existentes; reconciliação; detecção de duplicidade.
- **Fora de escopo:** cálculo tributário não definido no rulebook, compensação, saldo de transição e conciliação contábil ampla.
- **Entradas e pré-condições:** transações com beneficiário e classificação; rulebook vigente; competência válida.
- **Saídas/artefatos:** grupos de fatos geradores; totalizadores; relatório de reconciliação; itens bloqueados.
- **Dependências e responsáveis:** dados Fase 1 e SPECs anteriores.
- **Risco e plano B:** data insuficiente impede agrupamento; manter itens separados e bloquear consolidação.
- **Rollback ou reversão:** nova versão do agrupamento com diff; grupo anterior preservado.

## Fluxo e regras

1. Sistema determina chave com competência, beneficiário, evento, natureza e data aplicável.
2. Agrupa itens elegíveis e mantém referências de origem.
3. Calcula totalizadores determinísticos conforme rulebook.
4. Reconciliador compara grupo com transações e sinaliza diferenças.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | dois pagamentos do mesmo fato | um grupo com duas origens e total correto | abrir detalhes |
| Limite | pagamentos do mesmo beneficiário em fatos distintos | grupos separados | revisar chave |
| Falha | transação repetida ou sem data | duplicidade bloqueada ou item pendente | corrigir versão e reprocessar |

## Checklist de execução

- [ ] Chave de agrupamento é exibida e versionada.
- [ ] Cada grupo abre até as transações originais.
- [ ] Total bruto reconcilia com as fontes.
- [ ] Duplicidades são identificadas antes da saída.
- [ ] Reprocessamento não duplica grupos.

## Critérios de aceite

- [ ] **CA-2-013:** pagamentos do mesmo beneficiário e fato gerador consolidam com total reconciliado.
- [ ] **CA-2-014:** fatos geradores distintos não são fundidos pela semelhança do beneficiário.
- [ ] **CA-2-015:** cada totalizador aponta para suas transações de origem.
- [ ] **CA-2-016:** reprocessar a mesma versão é idempotente e não cria duplicidade.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | duplicidade altera total | fixture com FITID repetido e datas distintas | reconciliação falha antes do bloqueio | relatório |
| GREEN | consolidar lote conhecido | executar fixture com dois fatos e quatro pagamentos | CA-2-013 a CA-2-015 passam | matriz + total |
| REFACTOR/REGRESSÃO | reprocessar versão e alterar regra | executar duas vezes e depois nova versão | idempotência e diff preservados | hashes/logs |

**Dados/fixtures:** quatro pagamentos, dois beneficiários, duas datas de fato, uma reversão e uma duplicidade.  
**Caminhos de erro obrigatórios:** duplicidade, data ausente, beneficiário conflitante, total divergente e reprocessamento.  
**Evidência exigida:** matriz de grupos, reconciliação por origem e prova de idempotência.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| TASK-2-010 | Implementar chave e agrupamento por beneficiário e fato gerador | Engenheiro | SPEC-2-004 | CA-2-013, CA-2-014 | RED/GREEN: dois pagamentos do mesmo fato e dois fatos distintos | matriz de grupos com chave visível | TASK-2-003, TASK-2-006, TASK-2-009 | ☐ Leva 7 |
| TASK-2-011 | Implementar reconciliação de total e detecção de duplicidades | Engenheiro | SPEC-2-004 | CA-2-013, CA-2-015 | Fixture com FITID repetido, reversão e total divergente | relatório de reconciliação e bloqueios | TASK-2-010 | ☐ Leva 8 |
| TASK-2-012 | Implementar reprocessamento idempotente e histórico do agrupamento | Engenheiro | SPEC-2-004 | CA-2-016 | Regressão: executar mesma versão duas vezes e depois uma nova versão | hashes, diff e contagem sem duplicidade | TASK-2-010, TASK-2-011 | ☐ Leva 9 |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
