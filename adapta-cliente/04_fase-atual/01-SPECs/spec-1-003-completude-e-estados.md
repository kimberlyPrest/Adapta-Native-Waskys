# SPEC-1-003 — Qualidade, completude e estados do caso

**Fase:** 1  
**Status:** planejada — override explícito do cliente; checks permanecem pendentes  
**Dono:** analista fiscal; revisão do responsável tributário quando a lacuna for fiscal  
**Origem no escopo:** F02, F08, G1, TR-04  
**Degrau da solução:** construção mínima — validações determinísticas sobre o modelo canônico, sem julgamento fiscal autônomo.

## Contexto e decisões fechadas

- **Estado atual:** a equipe confere arquivos e saldos manualmente, sem estado único de completude.
- **Estado desejado:** cada caso tem qualidade mensurável e transição controlada entre `normalizado`, `bloqueado` e `aceito`.
- **Decisões já fechadas:** arquivo íntegro não prova completude tributária; fonte faltante bloqueia; nenhum fechamento automático.
- **Bloqueios:** universo de fontes obrigatórias além do extrato ainda será definido no G1/G2.

## Resultado observável

O cockpit apresenta um relatório de qualidade por caso: linhas recebidas, normalizadas, rejeitadas, débitos/créditos, período coberto, totais de origem e diferença de reconciliação. O caso só pode avançar para `aceito` quando todas as validações determinísticas passarem e as fontes obrigatórias estiverem declaradas.

## Limites e dependências

- **Inclui:** regras de qualidade, reconciliação de contagens/totais, período, documentos, linhas rejeitadas, checklist de completude e máquina de estados da Fase 1.
- **Fora de escopo:** decidir se o pagamento é tributável, calcular IRRF, aprovar Ata, gerar REINF ou transmitir.
- **Entradas e pré-condições:** caso `normalizado` da SPEC-1-002; declaração de universo esperado; tolerância numérica definida no teste.
- **Saídas/artefatos:** relatório de qualidade; checklist; histórico de transições; bloqueios com responsável e motivo.
- **Dependências e responsáveis:** Waskys define fontes obrigatórias; analista confirma exceções; executor implementa estados.
- **Atores e permissões mínimas:** analista pode tratar pendência; revisor pode revisar; responsável tributário aprova exceção de completude; agente não altera estado terminal.
- **Superfícies/arquivos/configurações afetadas:** motor de validação, estados, relatório e auditoria.
- **Risco e plano B:** tolerância indevida mascara falta de linha; usar comparação exata quando a fonte tiver totais confiáveis e bloquear diferenças sem justificativa.
- **Rollback ou reversão:** reabrir apenas com nova versão de fonte e motivo; preservar o relatório anterior.

## Fora desta fase

Decidir se o pagamento é tributável, calcular IRRF, aprovar Ata, gerar REINF ou transmitir.

## Dados e integrações

| Origem/destino | Fonte de verdade | Campos/contrato | Autenticação/permissão | Timeout/retry/idempotência | Tratamento de erro |
|---|---|---|---|---|---|
| Transações canônicas → relatório | SPEC-1-002 + manifesto | contagens, soma de valores, período, linhas rejeitadas | acesso ao caso | cálculo repetível; sem efeito externo | relatório `bloqueado` |
| Checklist de fontes → estado do caso | declaração aprovada do universo | fontes esperadas, presentes, justificadas | analista/revisor | versionado por competência | pendência com dono |

| Regra de negócio | Condição | Ação/resultado | Exceção | Fonte |
|---|---|---|---|---|
| RN-7 | período da linha fora da competência | marcar fora do período e não promover | competência parcial exige decisão | F02 |
| RN-8 | total/contagem canônica diverge da fonte | bloquear caso | diferença pode ser justificada em nova versão | F02 / completude |
| RN-9 | fonte esperada não recebida | estado `bloqueado` | responsável pode registrar justificativa, sem liberar automaticamente | F02 / G1 |

## Fluxo e regras

1. Calcular estatísticas sobre as transações normalizadas.
2. Comparar período e totais com o manifesto/fonte.
3. Comparar fontes presentes com o checklist do universo.
4. Gerar pendências com severidade e responsável.
5. Permitir `aceito` somente sem bloqueios abertos.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | contagem, total e fontes conformes | caso `aceito`; relatório arquivado | nenhum |
| Limite | diferença explicada e aprovada | caso permanece `bloqueado` até nova versão ou decisão formal | registrar justificativa, nunca mascarar |
| Falha | fonte ausente, linha rejeitada ou período incompleto | caso `bloqueado` com checklist e responsável | corrigir fonte, reprocessar e revisar |

## Instruções de execução para o Ethos

1. **Ler antes de alterar:** SPECs 1-001/1-002, escopo, matriz e política de completude aprovada.
2. **Alterar somente:** validações, estados, relatórios e testes.
3. **Não alterar:** cálculo fiscal, rulebook, fontes originais, Domínio ou integração externa.
4. **Executar nesta ordem:** regras de qualidade → relatório → estados → bloqueios → testes.
5. **Parar e pedir validação quando:** uma fonte não estiver no checklist ou uma tolerância precisar ser inventada.
6. **Estado válido ao parar:** caso bloqueado é visível, reprocessável e não pode ser exportado.

## Checklist de execução

- [ ] Contagens e totais de origem são comparados.
- [ ] Período e competência são verificados.
- [ ] Fontes ausentes aparecem no checklist.
- [ ] Linhas rejeitadas impedem `aceito` sem justificativa aprovada.
- [ ] Transições são auditadas e reprocessáveis.
- [ ] Não existe fechamento automático.

## Critérios de aceite

- [ ] **CA-1-009:** caso com fonte incompleta não alcança `aceito`.
- [ ] **CA-1-010:** divergência de total/contagem é exibida com valor, origem e motivo.
- [ ] **CA-1-011:** cada bloqueio possui responsável, data e ação de recuperação.
- [ ] **CA-1-012:** reprocessar uma nova versão preserva o relatório e o estado anteriores.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | fixture com fonte ausente e total divergente | executar validações iniciais | caso incorretamente liberado antes da implementação | log RED |
| GREEN | aplicar regras RN-7 a RN-9 | executar fixtures completas e incompletas | CA-1-009 a CA-1-012 passam | relatório de qualidade |
| REFACTOR/REGRESSÃO | reprocessar nova versão | corrigir fonte, reprocessar e comparar estados | histórico preservado e sem liberação silenciosa | auditoria |

**Dados/fixtures:** caso completo sintético, caso com fonte ausente, caso com linha rejeitada e caso com total divergente.  
**Caminhos de erro obrigatórios:** competência parcial, total divergente, duplicidade, tolerância excedida e usuário sem permissão.  
**Evidência exigida:** relatório, checklist, histórico de estados e logs.

## Handoff e operação

- **Como demonstrar:** carregar um caso completo e três casos com falhas diferentes; mostrar bloqueios e recuperação.
- **Como operar depois:** analista trata pendências; revisor confirma; responsável tributário decide exceções de completude.
- **Como monitorar:** casos bloqueados por motivo, idade da pendência e taxa de aceitação.
- **Pendência conhecida:** checklist definitivo de fontes (G1/G2).

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| | | | | | | | | |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
