# SPEC-1-004 — Painel de status e baseline operacional

**Fase:** 1  
**Status:** planejada — override explícito do cliente; checks permanecem pendentes  
**Dono:** gestor operacional, com validação do analista fiscal  
**Origem no escopo:** F08, resultado palpável da Fase 1, TR-10  
**Degrau da solução:** construção mínima — painel interno derivado dos casos e relatórios já produzidos, sem portal externo.

## Contexto e decisões fechadas

- **Estado atual:** volume, tempo e bloqueios são acompanhados em planilhas e conversas dispersas.
- **Estado desejado:** o gestor enxerga o estado da coorte, a qualidade das fontes e a baseline da preparação REINF.
- **Decisões já fechadas:** o painel é interno; não libera lote, não substitui revisão e não promete 80% antes da medição.
- **Bloqueios:** coorte e meta final serão definidas pela Waskys após a primeira observação real.

## Resultado observável

Uma tela ou relatório exportável lista cada caso por cliente/competência com estado, número de fontes, linhas, bloqueios, idade, responsável e última atualização. O mesmo relatório registra a baseline de tempo de recebimento até `aceito`/`bloqueado`, sem expor dados além do necessário.

## Limites e dependências

- **Inclui:** filtros por competência, estado, responsável e motivo; contadores; exportação de relatório; registro de baseline.
- **Fora de escopo:** gestão por exceção automática, transmissão, aprovação fiscal automática, portal do cliente e notificações externas.
- **Entradas e pré-condições:** casos e relatórios das SPECs 1-001 a 1-003; relógio e coorte definidos.
- **Saídas/artefatos:** painel interno; CSV/JSON de baseline; relatório de demonstração; log de consulta.
- **Dependências e responsáveis:** gestor define filtros e leitura; administrador configura permissões; analista confere os números.
- **Atores e permissões mínimas:** gestor vê agregados; analista vê sua carteira; revisor vê casos atribuídos; administrador configura sem editar fatos.
- **Superfícies/arquivos/configurações afetadas:** painel, consultas, exportação e métricas.
- **Risco e plano B:** painel mascarar casos bloqueados por agregação; oferecer drill-down controlado e exportar lista de bloqueios.
- **Rollback ou reversão:** remover somente views/relatórios de teste; os casos e logs permanecem.

## Fora desta fase

Gestão por exceção automática, transmissão, aprovação fiscal automática, portal do cliente e notificações externas.

## Dados e integrações

| Origem/destino | Fonte de verdade | Campos/contrato | Autenticação/permissão | Timeout/retry/idempotência | Tratamento de erro |
|---|---|---|---|---|---|
| Casos → painel | registro de caso e relatórios de qualidade | cliente, CNPJ, competência, estado, idade, fontes, pendências, responsável | perfil por carteira | consulta repetível; exportação identificada por timestamp | erro de consulta não muda estado |
| Painel → baseline | eventos de estado | recebido_em, normalizado_em, aceito/bloqueado_em, motivo | gestor/analista | não recalcular eventos históricos silenciosamente | marcar métrica incompleta |

| Regra de negócio | Condição | Ação/resultado | Exceção | Fonte |
|---|---|---|---|---|
| RN-10 | caso `bloqueado` | aparecer no painel e no relatório | nunca ocultar por filtro padrão | F08 |
| RN-11 | evento de estado ausente | métrica fica `incompleta` | pedir correção do caso, não estimar | baseline |
| RN-12 | usuário sem carteira | impedir acesso ao detalhe | gestor vê somente agregado autorizado | G3 |

## Fluxo e regras

1. Usuário entra no painel com perfil autorizado.
2. Sistema consulta casos da carteira/coorte.
3. Sistema mostra contadores e tabela de detalhe permitido.
4. Usuário filtra, exporta relatório ou abre pendência.
5. Sistema registra consulta e não altera estado fiscal.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | coorte com casos em vários estados | contadores e lista conferem com fonte | nenhum |
| Limite | evento de tempo ausente | caso aparece, baseline marcada incompleta | corrigir evento; não interpolar |
| Falha | usuário sem permissão | acesso negado e log mínimo | administrador revisa carteira |

## Instruções de execução para o Ethos

1. **Ler antes de alterar:** SPECs 1-001 a 1-003, escopo e política de acesso aprovada.
2. **Alterar somente:** consultas, painel, exportação e métricas da Fase 1.
3. **Não alterar:** dados-fonte, rulebook, estado fiscal, Domínio ou conectores externos.
4. **Executar nesta ordem:** consultas → filtros → permissões → exportação → baseline → testes.
5. **Parar e pedir validação quando:** surgir pedido de notificação externa, gestão por exceção ou ampliação de carteira.
6. **Estado válido ao parar:** painel é somente leitura para fatos e não oculta bloqueios.

## Checklist de execução

- [ ] Todos os estados da Fase 1 aparecem.
- [ ] Casos bloqueados são visíveis por padrão.
- [ ] Filtros não alteram dados.
- [ ] Exportação contém timestamp, coorte e origem.
- [ ] Permissões segregam carteira e detalhe.
- [ ] Baseline identifica medições incompletas.

## Critérios de aceite

- [ ] **CA-1-013:** contadores do painel reconciliam com a tabela de casos.
- [ ] **CA-1-014:** caso bloqueado aparece sem depender de alerta manual.
- [ ] **CA-1-015:** perfil sem permissão não acessa detalhe de outra carteira.
- [ ] **CA-1-016:** relatório de baseline é reproduzível e não inventa tempos ausentes.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | painel sem bloqueios visíveis e acesso cruzado | executar cenários de permissão/contagem | falhas antes das regras | log RED |
| GREEN | carregar massa sintética e consultar painel | aplicar filtros e exportar baseline | CA-1-013 a CA-1-016 passam | captura/exportação |
| REFACTOR/REGRESSÃO | adicionar caso e remover evento de tempo | atualizar fonte e consultar novamente | contadores e `incompleta` corretos | relatório |

**Dados/fixtures:** coorte sintética com pelo menos um caso em cada estado e um usuário por perfil.  
**Caminhos de erro obrigatórios:** carteira vazia, caso bloqueado, evento ausente, acesso negado e exportação interrompida.  
**Evidência exigida:** captura do painel, exportação e logs de permissão.

## Handoff e operação

- **Como demonstrar:** abrir a coorte, filtrar bloqueados, acessar um caso permitido e tentar acessar um caso não permitido.
- **Como operar depois:** gestor acompanha baseline; analista trata pendências; revisor confere a demonstração.
- **Como monitorar:** contagem de casos por estado, idade e motivo de bloqueio.
- **Pendência conhecida:** coorte, baseline real e metas quantitativas (G1/G5).

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| | | | | | | | | |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
