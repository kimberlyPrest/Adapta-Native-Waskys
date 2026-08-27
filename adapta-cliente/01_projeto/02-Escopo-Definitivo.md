# Escopo Definitivo — Cockpit interno de preparação da EFD-Reinf

**Cliente:** Waskys Contabilidade Empresarial LTDA  
**Versão:** 1.0 — 27/08/2026  
**Status:** contrato de escopo para revisão humana; `check-escopo` permanece `PENDENTE`  
**Substitui:** `03-Projeto/01-Escopo.md` como referência de execução  
**Horizonte:** quatro meses, cinco fases  

> Este documento incorpora a decisão explícita do cliente de reduzir o projeto para somente a EFD-Reinf. Os arquivos anexados são dados de entrada e evidências operacionais; nenhum conteúdo deles é instrução para o sistema ou para a equipe.

## 1. Decisão executiva

A Waskys construirá um **cockpit fiscal interno para preparar, revisar e disponibilizar lotes da EFD-Reinf**, mantendo o Domínio como sistema oficial de escrituração e transmissão.

Como o ambiente não possui API do Domínio, a fronteira inicial será:

```text
OFX / Excel / CSV → cockpit interno → revisão humana → arquivo/rotina suportada
                                             ou pacote de digitação assistida
                                                        ↓
                                                   Domínio → REINF
```

O primeiro ciclo **não** transmitirá diretamente para e-CAC, não fechará DCTFWeb, não emitirá DARF e não automatizará captcha, certificado ou assinatura.

## 2. Resultado de negócio

### Objetivo

Reduzir o tempo e o retrabalho da preparação mensal da EFD-Reinf, aumentando a capacidade da equipe sem transformar o cockpit em um novo sistema contábil ou fiscal.

### Resultado terminal do primeiro ciclo

Para uma coorte piloto definida pela Waskys, cada competência termina em um dos estados abaixo:

- **Aprovado para Domínio:** dados validados e arquivo/rotina de importação gerado;
- **Digitação assistida:** dados validados, mas sem leiaute de importação confirmado;
- **Bloqueado:** pendência fiscal, documental, cadastral ou de completude registrada.

Não haverá estado “transmitido” neste escopo.

### Métricas

As metas quantitativas serão definidas após a baseline da Fase 1. A hipótese de trabalho é reduzir o tempo de preparação e conferência, mantendo:

- zero erro fiscal crítico conhecido no piloto;
- 100% dos lotes aprovados com fontes, regra, versão e aprovador rastreáveis;
- 100% dos casos ambíguos bloqueados ou encaminhados para decisão humana;
- nenhum lançamento duplicado causado pelo cockpit.

O antigo alvo de “80%” não é compromisso deste documento; só poderá ser adotado após medição comparável antes/depois.

## 3. Limites arquiteturais

### Sistema oficial

O Domínio continua sendo a fonte oficial para escrituração e transmissão. O cockpit não replica o razão contábil, não substitui o módulo fiscal e não mantém uma obrigação paralela.

### Integração sem API

Será usada, nesta ordem, a alternativa comprovada em teste:

1. importação nativa por TXT/Excel ou rotina entre módulos do Domínio;
2. arquivo compatível com leiaute confirmado pelo dono do ERP;
3. pacote de digitação assistida com campos, totais e evidências;
4. RPA supervisionada somente como evolução posterior, após fluxo estável e decisão específica.

Nenhum arquivo será importado em produção sem reconciliação, idempotência, cópia de segurança e autorização imediatamente anterior.

### Agentes de IA

O cockpit terá **dois agentes de IA**, sem autonomia fiscal ou externa:

1. **Agente de triagem e classificação:** identifica candidatos, associa beneficiários e aponta ambiguidades nos dados estruturados.
2. **Agente revisor da REINF:** verifica consistência, evento provável, campos obrigatórios, duplicidade e divergências para aprovação humana.

O orquestrador, o motor de regras, os importadores, o gerador de arquivos, os totalizadores e a trilha de auditoria são componentes determinísticos, não agentes.

Nenhum agente pode aprovar regra tributária, criar saldo de transição, transmitir, alterar o Domínio ou interpretar silêncio como aprovação.

## 4. Atores e responsabilidades

| Ator | Responsabilidade | Permissão mínima |
|---|---|---|
| Analista fiscal | importar fontes, revisar candidatos, tratar exceções e preparar o lote | leitura/escrita na carteira atribuída |
| Responsável tributário | aprovar o rulebook, casos de borda e alterações normativas | aprovar/bloquear cálculo e versão |
| Revisor independente | executar a segunda conferência no piloto | revisar sem alterar a fonte original |
| Gestor operacional | acompanhar fila, prazo, baseline e capacidade | visão agregada, sem editar regra |
| Operador do Domínio | testar/importar o pacote aprovado | acesso ao ambiente definido pela Waskys |
| Administrador | configurar usuários, coortes, retenção e logs | administração técnica, sem aprovar fiscal |
| Cliente final | fora da operação do primeiro ciclo | eventual participação futura, não necessária para o MVP |

O nome do responsável tributário, operador substituto e responsável por incidentes permanece pendente de preenchimento pela Waskys.

## 5. Fontes de dados e tratamento dos anexos

| Fonte | Uso no cockpit | Limite |
|---|---|---|
| Extrato OFX | fonte estruturada de transações e reconciliação de totais | não prova sozinho a completude tributária |
| Extrato Excel | fonte alternativa com data, descrição, beneficiário, CPF/CNPJ, valor e saldo | deve preservar linhas e versão original |
| Relatório de boletos | evidência auxiliar de cobrança, vencimento e pagamento | boleto não é automaticamente evento REINF |
| Plano de contas | apoio ao mapeamento contábil e à investigação | conta contábil isolada não prova natureza fiscal |
| Cadastro societário e procurações | identificação de beneficiários e autoridade | deve ser validado e segregado por CNPJ |
| Atas e documentos societários | lastro quando a regra aplicável exigir | não serão interpretados automaticamente no MVP |
| Rulebook tributário | fonte normativa operacional aprovada | toda versão tem vigência, fonte e aprovador |

Nos arquivos analisados, o extrato de lançamentos já apresenta campos estruturados e contém transações para CPF e CNPJ. Essas linhas são **candidatas** a análise, não uma conclusão de que houve distribuição de lucros ou retenção.

## 6. Eventos REINF cobertos

O motor deve decidir o evento a partir do beneficiário, da natureza e do fato gerador, e não apenas do tipo de transferência:

- **R-4010:** pagamentos/créditos a beneficiário pessoa física, quando a natureza estiver no universo do evento;
- **R-4020:** pagamentos/créditos a beneficiário pessoa jurídica, quando houver hipótese aplicável;
- **R-4099:** fechamento/reabertura da série R-4000, somente como preparação e validação do pacote;
- **R-1000 e demais pré-requisitos:** somente conferência cadastral e indicação de pendência, salvo decisão posterior de ampliar o escopo.

A Receita Federal diferencia R-4010 para pessoa física e R-4020 para pessoa jurídica, e define R-4099 como fechamento/reabertura dos eventos periódicos da série R-4000. O leiaute e a Tabela 01 vigentes sempre prevalecem sobre vídeos, planilhas ou regras antigas:

- https://www.gov.br/receitafederal/pt-br/acesso-a-informacao/perguntas-frequentes/sped/efd-reinf/efdr/1-geral/1-17-as-informacoes-sobre
- https://www.gov.br/receitafederal/pt-br/centrais-de-conteudo/publicacoes/manuais/sped/manuais-efd-reinf/manual-de-orientacao-do-usuario/manual-da-efd-reinf-versao-2-1-2-1.pdf
- https://www.gov.br/sped/pt-br/assuntos/comunicados/efd-reinf/tabelas-da-efd-reinf

## 7. Capacidades funcionais

### F01 — Recepção e preservação da fonte

Receber OFX, XLSX, CSV e preenchimento interno controlado; registrar cliente, CNPJ, competência, remetente, data, versão, hash e origem. Arquivo ilegível, duplicado ou sem autoridade fica em quarentena.

### F02 — Normalização e completude

Converter fontes para um modelo comum, preservar o original, validar totais e identificar lacunas de conta, período, beneficiário ou documento. O cockpit não declara “completo” somente porque o saldo do extrato fecha.

### F03 — Triagem de beneficiários

Usar CPF/CNPJ, nome, histórico e cadastro para indicar candidatos. Associação incerta, documento conflitante, CPF ausente ou pagamento misto gera exceção.

### F04 — Rulebook versionado

Manter regras, fontes normativas, vigência, cenários, campos obrigatórios, códigos de natureza, tratamentos de transição, política de retificação e aprovador. Regra sem fonte ou vencida bloqueia o lote.

### F05 — Classificação fiscal assistida

Separar candidato a distribuição, pró-labore, salário, adiantamento, reembolso ou outra natureza somente com evidência aprovada. O agente sugere; o motor determinístico calcula conforme a versão aprovada; o humano decide bordas.

### F06 — Preparação R-4010/R-4020

Montar os registros de trabalho com beneficiário, competência, data do fato gerador, natureza, valor bruto, retenções, isenções, documentos e origem. O sistema deve impedir o uso de R-4010 para um CNPJ sem regra aplicável.

### F07 — Preparação R-4099

Validar pré-requisitos e montar o fechamento como artefato de trabalho, sem transmiti-lo. Competência incompleta, evento pendente ou divergência de total bloqueia o fechamento.

### F08 — Painel de exceções e aprovação

Exibir pendências, severidade, evidência, responsável, prazo, decisão, comentário e histórico. No piloto, todos os casos passam por revisão integral.

### F09 — Saída para o Domínio

Gerar arquivo ou conjunto de dados somente no formato confirmado em teste; quando não houver leiaute, gerar pacote de digitação assistida com campos, totais, ordem, fonte e checklist.

### F10 — Auditoria e reprocessamento

Registrar versões, hash, alterações, decisões, agente que sugeriu, pessoa que aprovou, exportações e reprocessamentos. Nova fonte ou norma invalida resultados posteriores afetados, sem sobrescrever o histórico.

## 8. Fluxo e estados

```text
recebido
  → quarentena (incompleto/sem autoridade)
  → aceito
  → normalizado
  → triado
  → consolidado
  → calculado
  → revisado
  → aprovado
  → exportado ou digitação-assistida
  → concluído localmente
```

Qualquer divergência pode levar a `bloqueado`. A recuperação exige correção versionada, reprocessamento, nova revisão e nova aprovação. Timeout, duplicidade, mudança normativa ou alteração da fonte nunca são tratados como sucesso.

## 9. Cinco fases de evolução

As fases abaixo são incrementos verticais do sistema. A Fase 4 acrescenta os dois agentes e loops operacionais; a Fase 5 acrescenta a validação transversal, sem transformar as fases finais em atividades apenas de automação ou teste.

### Fase 1 — Núcleo de casos, fontes e baseline (semanas 1–3)

**Sistema entregue:** cadastro interno de cliente/competência, upload controlado, parser OFX/XLSX/CSV, preservação de fonte, hash, modelo normalizado, validações básicas e painel inicial de status.

**Atores:** analista, administrador e gestor.  
**Dados:** arquivos anonimizados ou sintéticos; uma competência real somente após aprovação de ambiente.  
**Integrações:** sistema de arquivos controlado; nenhum acesso ao Domínio.  
**Regras:** autoridade do remetente, duplicidade, período, total do arquivo e completude declarada.  
**Demonstração:** importar uma competência, listar transações com CPF/CNPJ, reconciliar o total da fonte e gerar relatório de pendências.

**Fora desta fase:** cálculo fiscal, importação no Domínio, transmissão, portal externo e OCR.

**Aceite binário:** a competência é carregada sem alterar o original, cada linha tem origem rastreável e arquivos inválidos ficam bloqueados.

### Fase 2 — Motor determinístico e preparação de eventos (semanas 4–7)

**Sistema entregue:** cadastro societário mínimo, mapeamento CPF/CNPJ, rulebook versionado, classificação assistida, consolidação por beneficiário/fato gerador e rascunho de R-4010/R-4020 com validações de leiaute.

**Atores:** analista, responsável tributário e revisor.  
**Dados:** fontes da Fase 1, cadastro societário, folha/contabilidade quando necessário e documentos de lastro selecionados.  
**Integrações:** somente importação de arquivos; tabelas oficiais da REINF armazenadas com versão e data.  
**Regras:** evento por tipo de beneficiário, natureza conforme tabela vigente, múltiplos pagamentos, bloqueio de regra sem evidência e tratamento explícito de transição.

**Demonstração:** processar a amostra da Fase 1 e produzir uma matriz que mostre, para cada pagamento candidato, evento, natureza, valor, evidência e motivo de bloqueio.

**Fora desta fase:** fechamento produtivo, DCTFWeb, DARF e automação de portal.

**Aceite binário:** cada saída tem rulebook, fonte, versão e aprovador; toda ambiguidade aparece como exceção; nenhum valor é classificado silenciosamente.

### Fase 3 — Aprovação, lote e ponte com o Domínio (semanas 8–11)

**Sistema entregue:** revisão integral, aprovação segregada, geração de arquivo/pacote, idempotência, reconciliação pós-exportação e teste de importação em sandbox ou cópia controlada do Domínio.

**Atores:** analista, revisor independente, responsável tributário e operador do Domínio.  
**Dados:** somente coorte aprovada; dados reais restritos apenas com autorização.  
**Integrações:** leiaute nativo do Domínio, se confirmado; caso contrário, pacote de digitação assistida.  
**Regras:** uma competência por versão, checksum do arquivo, proibição de duplicidade, rollback e bloqueio de produção.

**Demonstração:** gerar um pacote, importar/testar no ambiente não produtivo ou executar o checklist de digitação assistida, reconciliando totais antes e depois.

**Fora desta fase:** importação produtiva sem gate, transmissão direta, DCTFWeb/DARF e RPA.

**Aceite binário:** o pacote pode ser reproduzido a partir da mesma fonte e versão; uma segunda execução não cria duplicidade; qualquer falha recupera o estado anterior.

### Fase 4 — Operação assistida com agentes e loops (semanas 12–14)

**Sistema entregue:** fila multiempresa interna, priorização por competência/prazo/risco, permissões por carteira, templates de exceção, monitoramento de SLA e relatórios de produtividade.

**Atores:** todos os papéis internos definidos; clientes continuam fora do fluxo obrigatório.  
**Dados:** coorte piloto ampliada somente conforme a baseline e aprovação de governança.  
**Integrações:** arquivos, repositório controlado e ponte já validada na Fase 3.  
**Regras:** revisão integral mantida; gestão por exceção é apenas experimento controlado, nunca padrão implícito.

**Loops/agentes adicionais à entrega do sistema:**

- **Loop L1 — Triagem diária:** o Agente de triagem classifica novos arquivos e mede taxa de associação correta, exceções e tempo até a fila revisável. O analista valida uma amostra diária.
- **Loop L2 — Revisão de lote:** o Agente revisor compara o rascunho com fontes e rulebook e mede divergências, falso negativo e tempo de aprovação. O responsável tributário decide o veredito.

Cada loop possui meta, baseline, amostra, limite de autonomia, cadência, fonte de medição e recuperação. Nenhum loop transmite ou altera o Domínio.

**Demonstração:** uma fila com casos de pelo menos duas competências, agentes produzindo sugestões identificáveis e analista aprovando/rejeitando cada sugestão.

**Aceite binário:** o sistema continua funcionando com agentes desligados; toda sugestão tem justificativa e pode ser revertida; nenhum caso bloqueado é promovido automaticamente.

### Fase 5 — Hardening e validação ponta a ponta (semanas 15–16)

**Sistema entregue:** controles finais de acesso, retenção, backup/restauração, relatórios de auditoria, tratamento de incidentes, regressão e pacote operacional de encerramento.

**Atores:** analista, revisor, responsável tributário, gestor, administrador e operador do Domínio.  
**Dados:** coorte final autorizada, com dados anonimizados quando possível.  
**Integrações:** todas as entradas e a ponte comprovada da Fase 3; nenhum conector novo é presumido.  
**Regras:** versão normativa efetiva, reprocessamento, retificação, duplicidade, timeout, perda de arquivo, segregação e rollback.

**Validação transversal obrigatória:**

- regressão funcional das entregas das Fases 1–4;
- fluxo completo arquivo → cockpit → revisão → pacote → Domínio não produtivo;
- validação de R-4010/R-4020/R-4099 conforme o universo aprovado;
- teste de permissões, privacidade, trilha de auditoria e restauração;
- teste de falha, duplicidade, timeout, mudança de regra e reprocessamento;
- medição dos loops L1/L2 e comparação com a baseline;
- aceite humano do responsável tributário e do champion operacional;
- decisão documentada de continuar, ajustar, ampliar ou encerrar.

**Demonstração:** relatório final por caso, fonte, versão, evento, aprovação, pacote exportado, divergência e evidência de validação.

**Aceite binário:** qualquer item não testado permanece pendente; o projeto não é considerado pronto por ausência de erro relatado.

## 10. Fora de escopo

- Transmissão direta à Receita/e-CAC ou automação de certificado, captcha e Assinador SERPRO.
- DCTFWeb, emissão, pagamento ou comunicação automática de DARF.
- API própria do Domínio ou promessa de webservice inexistente no ambiente da Waskys.
- Portal externo para os aproximadamente 700 clientes.
- Reconciliação contábil ampla, contas a pagar, cobrança e fechamento contábil.
- OCR, visão computacional ou interpretação automática de atas/PDF no MVP.
- Aprovação fiscal autônoma por agente.
- Uso produtivo de RPA antes de uma decisão específica e de uma prova reversível.
- Cobertura de todos os eventos REINF além do universo aprovado no rulebook.
- Migração massiva de histórico sem projeto e retenção aprovados.

## 11. Riscos e controles

| Risco | Consequência | Controle |
|---|---|---|
| Arquivo bancário incompleto | omissão de fato tributário | contrato de completude, fontes auxiliares e bloqueio |
| CPF/CNPJ ou natureza incorreta | evento REINF errado | validação cadastral, regra por evento e revisão humana |
| Regra tributária desatualizada | cálculo ou retenção incorreta | rulebook versionado, golden set e aprovação tributária |
| Domínio sem leiaute importável | retrabalho de digitação | prova de importação na Fase 3 e pacote assistido |
| Duplicidade na exportação | lançamento repetido | idempotência, hash e reconciliação |
| Vazamento de dados | incidente de privacidade | segregação por CNPJ, menor privilégio, retenção e logs |
| Falso negativo do agente | caso incorreto liberado | revisão integral, amostra adjudicada e bloqueio |
| Mudança normativa | resultado inválido | invalidação de versões afetadas e reprocessamento |
| Dependência de uma pessoa | parada operacional | substituto, runbook e retomada testada |

## 12. Critérios globais de aceite

O escopo só poderá ser considerado entregue quando:

1. o fluxo de estados estiver implementado e auditável;
2. cada resultado apontar para fonte, versão do rulebook, evento e aprovador;
3. a revisão humana integral estiver comprovada no piloto;
4. a ponte com o Domínio estiver testada sem produção ou, se impossível, o pacote de digitação assistida estiver validado;
5. os dois agentes puderem ser desligados sem interromper o sistema;
6. não houver transmissão externa, credencial ou alteração irreversível acionada pelo cockpit;
7. a regressão das cinco fases e os loops L1/L2 estiverem registrados na Fase 5;
8. o responsável tributário e o champion operacional assinarem o aceite humano.

## 13. Gates humanos

| Gate | Momento | Decisor | Evidência mínima |
|---|---|---|---|
| G1 — processo real | antes da SPEC da Fase 1 | operador + tributário | mapa As-Is validado |
| G2 — rulebook | antes de calcular | responsável tributário | versão, fonte, cenários e golden set |
| G3 — dados/ambiente | antes de dados reais | Waskys + Adapta | autorização, segregação e retenção |
| G4 — leiaute Domínio | antes da ponte | dono do ERP | teste em sandbox/cópia controlada |
| G5 — promoção operacional | antes de ampliar coorte | consultor + Waskys | métricas, divergências e rollback |
| G6 — encerramento | Fase 5 | tributário + champion | validação transversal e decisão de go/no-go |

Nenhum gate é aprovado por silêncio, ausência de erro ou execução parcial.

## 14. Rastreabilidade

| Fonte/achado | Decisão | Requisitos/capacidades | Fases |
|---|---|---|---|
| AC-001 / pedido atual | somente REINF | F01–F10; sem DCTFWeb/DARF | 1–5 |
| AC-006 / ausência de API Domínio | arquivo ou digitação assistida | F09; G4 | 3–5 |
| AC-005 / risco de falso negativo | revisão integral no piloto | F08; L1/L2 monitorados | 2–5 |
| AC-007 / OFX não prova completude | gate de completude | F02; G1/G2 | 1–2 |
| AC-013 / PF e PJ em eventos distintos | matriz R-4010/R-4020 | F04–F07 | 2–5 |
| AC-009 / excesso do hub | componente mínimo interno | fora de escopo; G5 | 1–5 |
| Conselho de decisão | shadow e prova reversível | F02–F03; G4 | 2–3 |
| Restrição de privacidade | menor privilégio e trilha | F01/F10; G3/G6 | 1–5 |

## 15. Decisões pendentes e condições de regeneração

Antes de gerar SPECs executáveis, a Waskys precisa preencher:

- responsável tributário e aprovador substituto;
- coorte, competência e amostra do piloto;
- fontes obrigatórias e definição de completude;
- versão/licença do Domínio e leiaute de importação disponível;
- ambiente autorizado, retenção, descarte e restauração;
- baseline e meta de produtividade;
- universo tributário final (PF, PJ e residentes/não residentes quando aplicável).

Se qualquer decisão alterar o terminal, o universo REINF, o leiaute, a autonomia ou a fronteira externa, este documento deve ser revisado antes da SPEC correspondente. O `check-escopo` continua pendente até a validação humana desses itens.
