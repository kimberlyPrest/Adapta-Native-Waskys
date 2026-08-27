# SPEC-1-001 — Caso de competência e preservação das fontes

**Fase:** 1  
**Status:** planejada — override explícito do cliente; `check-escopo` e `check-cliente` permanecem pendentes  
**Dono:** administrador do sistema, com validação do analista fiscal  
**Origem no escopo:** F01, F02, G1, G3, TR-01, TR-04  
**Degrau da solução:** construção mínima — registro interno de casos e manifesto de fontes, sem substituir o Domínio.

## Contexto e decisões fechadas

- **Estado atual:** arquivos de extrato e cobrança chegam em formatos diferentes e são conferidos manualmente.
- **Estado desejado:** cada cliente/competência possui um caso com fontes preservadas, identificadas e imutáveis.
- **Decisões já fechadas:** escopo somente REINF; Domínio é sistema oficial; entrada inicial é OFX/XLSX/CSV; nenhum dado é transmitido externamente.
- **Bloqueios:** autorização de ambiente e política de retenção ainda precisam ser confirmadas pela Waskys antes de dados reais.

## Resultado observável

Ao importar uma fonte, o cockpit cria um caso de competência contendo cliente, CNPJ, período, remetente, origem, versão, tamanho e SHA-256 do arquivo, além de manter o arquivo original somente para leitura. Uma segunda importação do mesmo arquivo é reconhecida como duplicata e não cria novo processamento.

## Limites e dependências

- **Inclui:** cadastro mínimo de cliente/competência; upload local controlado; manifesto; hash; estado `recebido`, `quarentena` ou `aceito`; vínculo entre caso e fonte.
- **Fora de escopo:** classificação fiscal, cálculo, geração de eventos, importação no Domínio, transmissão, portal externo e OCR.
- **Entradas e pré-condições:** arquivo OFX, XLSX ou CSV; CNPJ e competência informados; remetente autorizado pelo operador.
- **Saídas/artefatos:** registro do caso; manifesto JSON/CSV; arquivo original preservado; log de validação.
- **Dependências e responsáveis:** Waskys fornece coorte, ambiente e autoridade dos remetentes; administrador configura armazenamento.
- **Atores e permissões mínimas:** administrador cria configurações; analista cria/reabre caso; revisor somente lê fontes; nenhum agente altera original.
- **Superfícies/arquivos/configurações afetadas:** módulo de casos, armazenamento de fontes, tabela de permissões e logs.
- **Risco e plano B:** se armazenamento seguro não estiver aprovado, usar somente dados sintéticos; se o hash não puder ser calculado, bloquear.
- **Proteção de entrada:** limitar cada arquivo a 25 MB, validar conteúdo além da extensão, não executar macros/conteúdo incorporado e rejeitar arquivo criptografado ou corrompido.
- **Rollback ou reversão:** excluir somente registro de teste criado pelo executor, preservando o arquivo original; produção exige procedimento de retenção aprovado.

## Fora desta fase

Classificação fiscal, cálculo, geração de eventos REINF, importação no Domínio, transmissão, portal externo e OCR.

## Dados e integrações

| Origem/destino | Fonte de verdade | Campos/contrato | Autenticação/permissão | Timeout/retry/idempotência | Tratamento de erro |
|---|---|---|---|---|---|
| Upload → armazenamento interno | arquivo recebido e registro do caso | `case_id`, CNPJ, competência, nome, tipo, tamanho, SHA-256, origem, recebido_em | usuário autenticado; acesso segregado por CNPJ | retry manual; idempotência por CNPJ+competência+tipo+hash | quarentena e mensagem objetiva |

| Regra de negócio | Condição | Ação/resultado | Exceção | Fonte |
|---|---|---|---|---|
| RN-1 | extensão fora de OFX/XLSX/CSV | rejeitar antes de persistir | suporte manual pode registrar motivo | F01 / política de entrada |
| RN-2 | mesmo hash para mesmo caso | não criar novo processamento | nova versão exige justificativa e novo hash | F01 / idempotência |
| RN-3 | CNPJ ou competência ausente | estado `quarentena` | analista corrige em nova versão | F02 / G1 |

## Fluxo e regras

1. Usuário seleciona cliente e competência.
2. Usuário envia arquivo e declara origem.
3. Sistema valida extensão, tamanho, CNPJ, período e hash.
4. Sistema grava o manifesto e preserva o original.
5. Sistema marca `aceito` ou `quarentena` e mostra o motivo.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | OFX/XLSX/CSV legível e metadados completos | caso `aceito`, manifesto e hash visíveis | nenhum |
| Limite | arquivo igual já importado | caso não duplicado; usuário recebe referência do original | nenhuma nova versão automática |
| Falha | extensão inválida, arquivo vazio ou CNPJ ausente | caso `quarentena`; arquivo não entra no processamento | corrigir e reenviar como nova versão |

## Instruções de execução para o Ethos

1. **Ler antes de alterar:** `02-Escopo-Definitivo.md`, `requisitos.md`, `matriz-de-rastreabilidade.md` e esta SPEC.
2. **Alterar somente:** módulo de casos, armazenamento de fontes, validações e testes desta SPEC.
3. **Não alterar:** Domínio, e-CAC, DCTFWeb, rulebook fiscal ou arquivos originais.
4. **Executar nesta ordem:** modelo de caso → persistência/manifesto → validações → estados → testes.
5. **Parar e pedir validação quando:** for necessário usar dados reais, escolher política de retenção ou ampliar formatos.
6. **Estado válido ao parar:** casos sintéticos aceitos/quarentenados são consultáveis e fontes originais permanecem intactas.

## Checklist de execução

- [ ] Caso identifica CNPJ, competência e remetente.
- [ ] Fonte original é preservada e somente leitura.
- [ ] Manifesto registra tamanho, hash, tipo e origem.
- [ ] Duplicata é idempotente.
- [ ] Arquivo inválido vai para quarentena.
- [ ] Logs não expõem conteúdo financeiro desnecessário.

## Critérios de aceite

- [ ] **CA-1-001:** um arquivo válido cria um caso consultável com manifesto completo e SHA-256 verificável.
- [ ] **CA-1-002:** reenviar o mesmo arquivo não cria segundo processamento.
- [ ] **CA-1-003:** arquivo inválido ou sem metadado obrigatório fica em `quarentena` com motivo acionável.
- [ ] **CA-1-004:** nenhuma rotina desta SPEC acessa Domínio, e-CAC ou transmissão externa.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | teste de duplicidade e extensão inválida | executar fixture válida duas vezes e uma `.pdf` | testes falham antes da implementação | log de teste |
| GREEN | criar caso e manifesto | importar fixture OFX/XLSX/CSV válida | CA-1-001 a CA-1-003 passam | caso e manifesto |
| REFACTOR/REGRESSÃO | permissão e integridade | alterar cópia, tentar abrir original e repetir upload | original intacto, acesso segregado e sem duplicidade | relatório de regressão |

**Dados/fixtures:** arquivo sintético pequeno de cada formato e um arquivo duplicado por hash.  
**Caminhos de erro obrigatórios:** vazio, extensão inválida, CNPJ ausente, competência inválida, usuário sem carteira.  
**Evidência exigida:** captura do caso, manifesto, hash e log dos testes.

## Handoff e operação

- **Como demonstrar:** criar um caso sintético, importar uma fonte válida, repetir o upload e importar uma fonte inválida.
- **Como operar depois:** analista usa o caso como ponto de entrada de cada competência.
- **Como monitorar:** contagem de `recebido`, `quarentena`, `aceito` e duplicatas por competência.
- **Pendência conhecida:** aprovação de ambiente, retenção e dados reais (G3).

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| | | | | | | | | |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
