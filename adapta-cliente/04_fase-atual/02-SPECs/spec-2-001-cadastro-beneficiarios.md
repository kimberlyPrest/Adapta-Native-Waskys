# SPEC-2-001 — Cadastro fiscal e carteira de beneficiários

**Fase:** 2  
**Status:** planejada — avanço autorizado explicitamente pela consultora; gates permanecem pendentes  
**Dono:** administrador e analista fiscal, com validação do responsável tributário  
**Origem no escopo:** F03, F04, TR-02, TR-04, G2, G3  
**Degrau da solução:** construção mínima — cadastro interno vinculado aos casos existentes, sem substituir cadastro oficial do Domínio.

## Resultado observável

O analista consegue consultar e versionar beneficiários PF/PJ por CPF/CNPJ, nome, carteira e evidências. Uma transação pode apontar para um beneficiário confirmado, permanecer como candidato ou ficar bloqueada. Ausência, conflito ou alteração cadastral nunca é resolvida silenciosamente.

## Limites e dependências

- **Inclui:** cadastro CPF/CNPJ; normalização; status candidato/confirmado/bloqueado; vínculo com caso e fonte; histórico de alterações; evidência de validação.
- **Fora de escopo:** consulta automática a Receita, enriquecimento externo, decisão tributária, cadastro completo do Domínio e OCR.
- **Entradas e pré-condições:** transações normalizadas; CPF/CNPJ e nome quando disponíveis; operador autenticado; caso existente.
- **Saídas/artefatos:** registro do beneficiário; vínculo transação-beneficiário; log de decisão; lista de conflitos.
- **Dependências e responsáveis:** Fase 1; Waskys valida casos de borda e autoridade das fontes.
- **Risco e plano B:** documento ausente ou inválido permanece candidato sem evento; conflito é fila de exceção.
- **Rollback ou reversão:** nova versão do vínculo; nunca sobrescrever a decisão ou evidência anterior.

## Fluxo e regras

1. Sistema extrai documentos e nomes das transações e tenta localizar registro existente.
2. Analista confirma, corrige ou cria beneficiário com evidência.
3. Sistema registra versão, usuário, data, motivo e transações afetadas.
4. Conflitos ficam bloqueados até decisão humana.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | CPF válido e único no caso | vínculo confirmado com fonte e operador | reabrir vínculo mantendo histórico |
| Limite | mesmo beneficiário em duas grafias | sugestão de possível correspondência, sem fusão automática | analista decide e registra motivo |
| Falha | CPF com tamanho inválido ou CNPJ conflitante | status bloqueado e exceção acionável | corrigir em nova versão |

## Checklist de execução

- [ ] CPF/CNPJ é normalizado sem perder valor original.
- [ ] Beneficiário guarda origem, versão e responsável pela confirmação.
- [ ] Conflitos e ausências aparecem em fila.
- [ ] Vínculo pode ser refeito sem apagar histórico.
- [ ] Acesso respeita o owner/carteira do caso.

## Critérios de aceite

- [ ] **CA-2-001:** CPF válido pode ser confirmado e fica associado a cada transação afetada.
- [ ] **CA-2-002:** CPF/CNPJ inválido, ausente ou conflitante não gera vínculo confirmado.
- [ ] **CA-2-003:** alteração de beneficiário preserva versão anterior, usuário, data e motivo.
- [ ] **CA-2-004:** usuário sem acesso ao caso não consulta nem altera beneficiário vinculado.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | associação inválida é aceita | fixture com CPF curto e conflito | falha reproduzida antes da validação | log do cenário |
| GREEN | confirmar PF/PJ rastreável | importar fixture, confirmar e consultar transação | CA-2-001 e CA-2-002 passam | captura + registros |
| REFACTOR/REGRESSÃO | versionamento e permissão | alterar vínculo e tentar acesso cruzado | histórico preservado e acesso negado | auditoria |

**Dados/fixtures:** três transações: CPF válido, CNPJ válido e documento inválido; duas grafias do mesmo nome; dois owners.  
**Caminhos de erro obrigatórios:** vazio, documento inválido, conflito, duplicidade e acesso cruzado.  
**Evidência exigida:** exportação do cadastro, histórico de decisão e log de permissão.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| TASK-2-001 | Modelar cadastro de beneficiários, vínculo e histórico | Engenheiro | SPEC-2-001 | CA-2-001, CA-2-003 | RED/GREEN da SPEC: criar PF/PJ, vínculo e nova versão do vínculo | migração/modelo, fixture e log de versão | Fase 1 disponível; G3 sem dados reais | ☐ Leva 1 |
| TASK-2-002 | Implementar normalização e validação de CPF/CNPJ com conflitos | Engenheiro | SPEC-2-001 | CA-2-001, CA-2-002 | TDD RED/GREEN: fixture válida, ausente, curta e conflitante | testes/fixtures e relatório de bloqueios | TASK-2-001 | ☐ Leva 2 |
| TASK-2-003 | Implementar revisão de beneficiário e segregação por owner | Engenheiro | SPEC-2-001 | CA-2-003, CA-2-004 | TDD de regressão: alterar vínculo, consultar histórico e tentar acesso cruzado | auditoria, evidência de acesso negado e histórico | TASK-2-001, TASK-2-002 | ☐ Leva 3 |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
