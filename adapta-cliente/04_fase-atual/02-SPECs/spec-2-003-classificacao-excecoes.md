# SPEC-2-003 — Classificação assistida e fila de exceções

**Fase:** 2  
**Status:** planejada — execução condicionada ao rulebook aprovado  
**Dono:** analista fiscal; decisão final do responsável tributário  
**Origem no escopo:** F03, F05, F08, TR-02, TR-04, G2  
**Degrau da solução:** construção mínima — sugestões determinísticas e, se habilitada, IA advisory; humano permanece no loop.

## Resultado observável

Cada pagamento candidato recebe uma sugestão explicável, uma decisão humana ou um bloqueio. A fila mostra motivo, severidade, evidência, responsável, prazo e próximo passo. Nenhuma sugestão vira classificação fiscal apenas por existir.

## Limites e dependências

- **Inclui:** sugestão por regras; justificativa; confiança como sinal não decisório; exceções; decisão aprovar/rejeitar/solicitar evidência; comentários; histórico.
- **Fora de escopo:** agente autônomo, aprovação automática, decisão tributária sem rulebook e envio externo.
- **Entradas e pré-condições:** beneficiário e rulebook; transação com origem; permissão do analista.
- **Saídas/artefatos:** fila de exceções; decisão por item; relatório de pendências; trilha de auditoria.
- **Dependências e responsáveis:** SPECs 2-001 e 2-002; responsável tributário adjudica casos ambíguos.
- **Risco e plano B:** IA indisponível não interrompe fluxo determinístico; sugestão incerta vira bloqueio.
- **Rollback ou reversão:** reabrir decisão e reprocessar mantendo decisões anteriores.

## Fluxo e regras

1. Sistema aplica regras à transação e gera sugestão com evidências.
2. Casos incompletos, conflitantes ou fora do rulebook entram na fila.
3. Analista decide ou encaminha ao responsável tributário.
4. Sistema registra decisão, justificativa e estado resultante.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | transação completa e regra única | sugestão explicável para revisão | analista confirma ou rejeita |
| Limite | baixa confiança ou regra sobreposta | exceção bloqueante | responsável decide com evidência |
| Falha | motor/IA indisponível | item permanece pendente; sistema continua acessível | reprocessar depois sem duplicar |

## Checklist de execução

- [ ] Sugestão identifica regra, fonte e transação de origem.
- [ ] Severidade e próximo passo são visíveis.
- [ ] Exceção tem responsável e prazo.
- [ ] Aprovação exige usuário autorizado.
- [ ] IA pode ser desligada sem perda de dados.

## Critérios de aceite

- [ ] **CA-2-009:** todo item classificado possui sugestão ou bloqueio explícito.
- [ ] **CA-2-010:** item ambíguo não pode ser promovido para saída de evento.
- [ ] **CA-2-011:** decisão humana registra usuário, data, motivo, evidência e rulebook.
- [ ] **CA-2-012:** indisponibilidade da IA/motor não aprova nem descarta itens.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | item ambíguo passa sem exceção | fixture com regra sobreposta | cenário falha antes do bloqueio | log |
| GREEN | fila e decisão humana | processar fixtures e decidir uma exceção | CA-2-009 a CA-2-011 passam | fila + auditoria |
| REFACTOR/REGRESSÃO | desligar serviço de sugestão | executar lote com IA/motor indisponível | item pendente, sem promoção ou perda | captura + log |

**Dados/fixtures:** transação clara, transação sem documento, regra sobreposta e beneficiário conflitante.  
**Caminhos de erro obrigatórios:** baixa confiança, ausência de evidência, permissão, timeout e serviço desligado.  
**Evidência exigida:** fila exportada, decisão adjudicada e log de reprocessamento.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| TASK-2-007 | Implementar motor de sugestão explicável por regra e evidência | Engenheiro | SPEC-2-003 | CA-2-009 | RED/GREEN: item claro gera sugestão com regra, fonte e origem | resultado da sugestão e log de execução | TASK-2-001, TASK-2-002, TASK-2-006 | ☐ Leva 4 |
| TASK-2-008 | Implementar fila de exceções com severidade, responsável e prazo | Engenheiro | SPEC-2-003 | CA-2-009, CA-2-010 | RED/GREEN: ambiguidade e falta de evidência entram na fila | captura da fila e registro de exceção | TASK-2-007 | ☐ Leva 5 |
| TASK-2-009 | Implementar decisão humana, justificativa e fallback sem IA | Analista fiscal + Engenheiro | SPEC-2-003 | CA-2-011, CA-2-012 | Regressão: aprovar/rejeitar e executar com serviço indisponível | auditoria de decisão e lote pendente sem promoção | TASK-2-008 | ☐ Leva 6 |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
