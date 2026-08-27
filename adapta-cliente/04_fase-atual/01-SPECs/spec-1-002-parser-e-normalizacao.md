# SPEC-1-002 — Parser e normalização de fontes estruturadas

**Fase:** 1  
**Status:** planejada — override explícito do cliente; checks permanecem pendentes  
**Dono:** executor do sistema, com validação do analista fiscal  
**Origem no escopo:** F02, F03, TR-01, TR-04  
**Degrau da solução:** construção mínima — modelo canônico único para OFX/XLSX/CSV, sem depender de API bancária ou Domínio.

## Contexto e decisões fechadas

- **Estado atual:** o extrato Excel contém Data, Lançamento, Razão Social, CPF/CNPJ, Valor e Saldo; o OFX usa blocos `STMTTRN`; CSVs podem variar.
- **Estado desejado:** cada linha de fonte vira uma transação canônica com referência à linha original e direção do valor.
- **Decisões já fechadas:** parser determinístico; não classificar natureza fiscal nesta fase; não inferir que uma saída é lucro, pró-labore ou salário.
- **Bloqueios:** mapeamentos de CSV que não estejam documentados devem ser configurados pelo analista antes do uso.

## Resultado observável

Para cada fonte aceita, o cockpit produz uma tabela normalizada com `transaction_id`, data, descrição, beneficiário, CPF/CNPJ normalizado, valor decimal, direção, saldo quando disponível e referência de origem. A tela/arquivo permite filtrar rapidamente saídas com CPF ou CNPJ para análise posterior.

## Limites e dependências

- **Inclui:** parser OFX SGML/XML compatível com o arquivo fornecido; parser XLSX por cabeçalho; CSV com mapa explícito; normalização de datas, valores, documentos e sinais.
- **Fora de escopo:** OCR/PDF, interpretação de texto livre por IA, cálculo fiscal, escolha de evento REINF e conciliação bancária completa.
- **Tratamento do XLS legado:** `Contas.xls` é fonte de referência do plano de contas; nesta fase não será importado diretamente. Se necessário, o operador deve convertê-lo para XLSX fora do cockpit e preservar ambos os arquivos.
- **Entradas e pré-condições:** caso `aceito` da SPEC-1-001; cabeçalhos ou tags conhecidos; encoding detectável.
- **Saídas/artefatos:** tabela canônica; relatório de linhas rejeitadas; contagem por direção e identificador.
- **Dependências e responsáveis:** executor implementa os parsers; analista confirma cabeçalhos/mapeamentos desconhecidos.
- **Atores e permissões mínimas:** executor e administrador escrevem configuração; analista consulta e adjudica; revisor somente lê.
- **Superfícies/arquivos/configurações afetadas:** módulo de parsing, mapa de colunas, tabela canônica e log de rejeições.
- **Risco e plano B:** campo ausente ou valor ambíguo bloqueia a linha; não preencher com zero ou texto inventado. Plano B é correção manual da fonte/configuração.
- **Rollback ou reversão:** reprocessar a mesma fonte com versão de parser; manter resultado anterior imutável para comparação.

## Fora desta fase

OCR/PDF, interpretação de texto livre por IA, cálculo fiscal, escolha de evento REINF e conciliação bancária completa.

## Dados e integrações

| Origem/destino | Fonte de verdade | Campos/contrato | Autenticação/permissão | Timeout/retry/idempotência | Tratamento de erro |
|---|---|---|---|---|---|
| OFX → transações | tags `STMTTRN` e `MEMO` | `DTPOSTED`, `TRNAMT`, `FITID`, `MEMO` | somente caso aceito | reprocessamento por `case_id` + hash + versão parser | linha rejeitada com motivo |
| XLSX → transações | cabeçalho da planilha | Data, Lançamento, Razão Social, CPF/CNPJ, Valor, Saldo | somente caso aceito | idem; sem duplicar `FITID`/linha | coluna ausente bloqueia formato |
| CSV → transações | mapa aprovado de colunas | mapa explícito por versão | somente caso aceito | idem | mapa inexistente bloqueia formato |

| Regra de negócio | Condição | Ação/resultado | Exceção | Fonte |
|---|---|---|---|---|
| RN-4 | valor positivo/negativo em fonte | guardar decimal e `direction` sem alterar magnitude | sinal ausente vira bloqueio | F02 |
| RN-5 | CPF/CNPJ informado | remover máscara, validar dígitos e preservar valor original | inválido fica `identificador_invalido` | F03 |
| RN-6 | linha sem data/valor/identificador mínimo | não criar transação elegível | registrar rejeição por linha | F02 / completude |

## Fluxo e regras

1. Ler o manifesto e selecionar parser pela extensão/conteúdo.
2. Detectar encoding, cabeçalho ou tags.
3. Converter datas para ISO-8601 e valores para decimal sem arredondamento indevido.
4. Normalizar documentos e preservar os campos originais.
5. Gerar transações e relatório de rejeições.
6. Marcar o caso como `normalizado` somente se as linhas obrigatórias forem processadas ou justificadas.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | fonte válida com campos conhecidos | todas as linhas canônicas com origem | nenhum |
| Limite | pagamento para CPF/CNPJ sem nome | documento preservado; nome vazio gera sinal, não associação automática | revisão posterior |
| Falha | coluna ausente, data inválida ou sinal ambíguo | linha/caso bloqueado com diagnóstico | corrigir mapa ou fonte e reprocessar |

## Instruções de execução para o Ethos

1. **Ler antes de alterar:** SPEC-1-001, escopo definitivo, amostras anexadas e mapa de rastreabilidade.
2. **Alterar somente:** parsers, mapeamento, normalização e testes.
3. **Não alterar:** rulebook, cadastro fiscal, Domínio, fonte original ou classificação de natureza.
4. **Executar nesta ordem:** fixtures → contrato canônico → parser OFX → parser XLSX → parser CSV → validações → relatório.
5. **Parar e pedir validação quando:** surgir formato novo, campo fiscal não previsto ou necessidade de interpretar texto.
6. **Estado válido ao parar:** transações normalizadas são reproduzíveis pela mesma fonte e versão do parser.

## Checklist de execução

- [ ] OFX do período é lido sem perder `FITID`, data, valor ou memo.
- [ ] XLSX é lido pelos cabeçalhos documentados.
- [ ] CSV só é aceito com mapa de colunas versionado.
- [ ] Datas e valores são tipados e auditáveis.
- [ ] CPF/CNPJ original e normalizado são preservados.
- [ ] Linhas rejeitadas têm motivo e referência de origem.

## Critérios de aceite

- [ ] **CA-1-005:** OFX e XLSX de fixture produzem o mesmo modelo canônico para linhas equivalentes.
- [ ] **CA-1-006:** cada transação aponta para caso, fonte e linha/tag de origem.
- [ ] **CA-1-007:** nenhuma linha com campo obrigatório inválido é promovida silenciosamente.
- [ ] **CA-1-008:** o parser não classifica evento REINF nem natureza fiscal.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | fixtures com coluna ausente, data inválida e documento inválido | executar suíte inicial | casos falham antes das validações | log RED |
| GREEN | parse de OFX/XLSX/CSV conhecido | executar suíte com fixtures válidas | CA-1-005 a CA-1-008 passam | tabela canônica |
| REFACTOR/REGRESSÃO | sinais, encoding e linha rejeitada | repetir com valores negativos, acentos e linha truncada | nenhuma regressão; rejeição explicável | relatório |

**Dados/fixtures:** OFX fornecido; XLSX de lançamentos fornecido; CSV sintético com mapa documentado.  
**Caminhos de erro obrigatórios:** encoding inválido, cabeçalho ausente, data impossível, valor sem sinal, CPF/CNPJ inválido, linha truncada.  
**Evidência exigida:** amostra normalizada, relatório de rejeições e logs.

## Handoff e operação

- **Como demonstrar:** importar as duas fontes estruturadas e comparar linhas equivalentes; filtrar transações por CPF/CNPJ.
- **Como operar depois:** analista confirma formatos novos antes de habilitá-los.
- **Como monitorar:** taxa de linhas normalizadas, rejeitadas e identificadores inválidos.
- **Pendência conhecida:** mapa de fontes adicionais e regra de completude (G1/G2).

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| | | | | | | | | |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
