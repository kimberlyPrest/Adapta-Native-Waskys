# Changelog

## 2026-09-18

- 2026-09-18 · Matheus Lohse · TASK-2-007 implementada na SKIP `0.0.183` (SPEC-2-003, CA-2-009): motor de sugestão explicável. Migração `0063` criou `transaction_suggestions` (append-only, RLS por owner, escrita só via rota) e o tipo de log `sugestao_classificacao`. Rota transacional `/backend/v1/suggestions/evaluate` resolve a versão Aprovada vigente da competência do caso, aplica as regras do Evento selecionado às transações da fonte e grava, por transação, uma **sugestão** (regra + snapshot + fonte oficial + evidência + justificativa) ou um **bloqueio** (ambiguidade / fora do rulebook / evidência insuficiente) — nunca nada, e ambiguidade nunca é promovida (CA-2-010 respeitado). UI "Sugestões" com avaliação por fonte e cartões por transação; 9 testes estáticos como provas. QA completo passou; migração aplicada; aguardando teste humano.
- 2026-09-18 · Matheus Lohse · TASK-2-006 concluída definitivamente: teste humano da SKIP `0.0.182` aprovado ("Pode encerrar e começar a próxima"). Ciclo do Rulebook completo e validado (rastreabilidade P0, catálogos versionados, UX do ciclo, navegação por abas e motivo nas duas abas); SPEC-2-002 concluída (3/3). Fase 2 em 6/16 (37,5%). Próxima: TASK-2-007.
- 2026-09-18 · Matheus Lohse · AJUSTE DE MOTIVO (SKIP `0.0.182`): campo "Motivo da alteração" replicado na aba "Regras da versão" (havia ficado só na aba Cadastro após a separação); os dois campos compartilham o mesmo estado e a validação da aba Regras destaca o campo vazio. QA completo passou.
- 2026-09-18 · Matheus Lohse · TESTE HUMANO TASK-2-006 falhou (feedback de navegação, 3 pontos): trocar de versão colapsava a lista lateral e saltava para "Regras da versão"; cadastro misturado com as regras no mesmo formulário; títulos mostravam só o número da versão → corrigido na SKIP `0.0.181`: `openVersion` não força mais aba nem recolhe a lista (aprovação/retiração/clonagem também preservam), criada a aba "Cadastro da versão" com botão "Salvar cadastro" (aba "Regras da versão" fica só com regras e "Salvar rascunho"; validação por aba) e títulos com "v<n> — <nome da versão>". "Nova versão" abre na aba Cadastro. QA completo passou.
- 2026-09-18 · Matheus Lohse · TESTE HUMANO TASK-2-006 falhou (feedback de UX do ciclo, 5 pontos): motivo exigido na criação de catálogo; botões Editar/Inativar visíveis e inúteis em versões somente leitura; campo redundante "Nome da natureza" no editor; histórico mostrava "múltiplas alterações" ao criar Evento/Natureza; contadores só atualizavam após recarregar a página → corrigido na SKIP `0.0.180`: motivo obrigatório somente na edição (criação registra "Cadastro inicial — a informação ainda não existia."), botões ocultos em versões Aprovadas/Retiradas, nome da natureza derivado do catálogo, histórico exibindo o resumo real do backend com diff fiel por `regra_id` e contadores ao vivo sem recarregar. Higiene: remoção das migrações duplicadas nunca aplicadas (0008, 0017, 0037, 0043); migrações aplicadas permanecem 0001–0062. QA completo passou.

## 2026-09-17

- 2026-09-17 · Matheus Lohse · TASK-2-006 P0 implementada na SKIP `0.0.178`; migração `0062_add_rulebook_traceability` aplicada.
- Regras agora preservam identidade append-only (`regra_id`, `revisao_regra`, `atual`, `origem_regra_id`) e o salvamento de Rascunho não exclui/recria registros históricos.
- Casos e execuções do Golden Set passaram a usar IDs canônicos de Evento/Natureza, snapshots da versão e rastreabilidade das regras avaliadas.
- Cópia de versão remapeia catálogos, regras e casos para novos IDs; aprovação/retirada registra snapshots completos das regras atuais e catálogos.
- Schema, setup, análise estática, build, integrações e testes da SKIP passaram; preview carregou e logs de hooks ficaram sem erros.
- Estado: aguardando teste humano de Matheus. P1/P2 da auditoria permanecem fora desta entrega.

## 2026-08-27

- Criada pasta provisória do cliente.
- Exportados o escopo definitivo e as SPECs da Fase 1.
- 04/09/2026: avanço para a Fase 2 autorizado; geradas 5 SPECs e 16 tasks executáveis.

## 2026-09-10

- TASK-2-001 concluída no SKIP `0.0.108`.
- TASK-2-002 concluída na SKIP `0.0.121`.
- TASK-2-003 implementada na SKIP `0.0.126`.

## 2026-09-12

- TASK-2-003 concluída: teste humano aprovado; SPEC-2-001 tecnicamente concluída.
- Gate G2 liberado: Matheus designado responsável tributário.
- TASK-2-004 concluída na SKIP `0.0.133` após teste humano.

## 2026-09-14

- TASK-2-005 implementada tecnicamente na SKIP `0.0.140`: golden set versionado, quatro tipos de caso, executor determinístico, conflito explícito, relatório e painel.
- 2026-09-14 · Matheus Lohse · TESTE HUMANO TASK-2-005 falhou (1º feedback): contadores de revisão se misturavam; conflito não identificava as regras; falta de seções, explicação e lista recolhível → corrigido na SKIP `0.0.141`.
- 2026-09-14 · Matheus Lohse · TESTE HUMANO TASK-2-005 falhou (2º feedback): validação atribuída a Jarvis em vez de quem acionou; resultado longe do botão; históricos não descreviam o que mudou; lista recolhia na vertical; erro não listava os campos → corrigido na SKIP `0.0.154`: execução atribuída à sessão (migração 0052), campo `alteracoes` com resumo verdadeiro nos dois históricos (0053–0056), resultado em card junto ao botão, recolhimento lateral, erro com campos nomeados como comportamento padrão. Provas: execução "Matheus Lohse" 4/4, resumo sem falsos Editou, erro listando "Motivo da alteração" no preview. Aguardando reteste humano.
- 2026-09-14 · Matheus Lohse · DEBUG TASK-2-005: auditoria do 3º feedback confirmou que a aproximação apenas do badge 4/4 não bastava; resultado detalhado permanecia depois de todo o formulário → causa raiz: teste verificava presença de texto/classe, não a ordem estrutural → corrigido na SKIP `0.0.159`; painel detalhado movido para antes do formulário, cabeçalhos padronizados como "O que mudou" e regressão passou a provar botão < resultado < formulário. QA completo passou; aguardando reteste humano.
- 2026-09-14 · Matheus Lohse · DEBUG TASK-2-005: aprovação da 0.0.159 foi substituída por novo feedback visual/funcional antes do fechamento; lista lateral estreita, versão não abria por padrão, badge/horário/histórico e erros ainda inadequados → corrigido na SKIP `0.0.160`: lista redesenhada e removida ao recolher, versão mais nova abre automaticamente, badge fica ao lado do botão, timestamp tem fallback imediato, históricos incluem Versão e número da Regra/Caso, erros usam lista semântica com quebra real. QA completo e regressões específicas passaram; aguardando reteste humano.
- 2026-09-14 · Matheus Lohse · AJUSTE FINAL TASK-2-005: teste humano da SKIP `0.0.160` aprovado, com pedido de remover somente a coluna Versão dos históricos → rollback cirúrgico aplicado na SKIP `0.0.161`, preservando número da Regra/Caso em "O que mudou". QA completo passou; aguarda confirmação visual final antes do fechamento.
- 2026-09-14 · Matheus Lohse · DEBUG TASK-2-005: captura de tela da 0.0.161 mostrou célula "v2" residual na coluna Data do histórico do Rulebook → causa: célula multilinha escapou da verificação anterior → corrigido na SKIP `0.0.162` e regressão reforçada na `0.0.163` para provar ausência de coluna E célula nos dois históricos. QA completo passou; aguarda confirmação visual final.
- 2026-09-14 · Task TASK-2-005 concluída: SKIP `0.0.163` aprovada em teste humano; golden set versionado com quatro resultados, sobreposição explícita sem escolha automática, execução atribuída ao operador, históricos auditáveis e regressões completas. Migrações 0048–0056 aplicadas; build vigente e QA aprovados.
- 2026-09-14 · Matheus Lohse · TASK-2-006 implementada na SKIP `0.0.166`: aprovação/retirada atômicas com autoria e histórico, seleção única por competência, RLS append-only e UI do ciclo. Migração 0057 aplicada. Aguardando teste humano.

## 2026-09-15

- 2026-09-15 · Matheus Lohse · DEBUG TASK-2-006: seleção por competência não explicava claramente que consulta e registra; versão Aprovada não oferecia fluxo para alteração legislativa → corrigido na SKIP `0.0.168`: texto operacional explícito e ação "Criar nova versão a partir desta". Rota atômica copia regras e última revisão do Golden Set para novo Rascunho, registra histórico/log e preserva integralmente o original. QA passou; aguardando teste humano.
- 2026-09-15 · Matheus Lohse · DEBUG TASK-2-006: título alterado para "Consulta de Rulebook por Competência" na SKIP `0.0.169`; QA passou. DÚVIDA tributária registrada: exigir caso Ambíguo em toda revisão força duas regras sobrepostas no próprio Rulebook.
- 2026-09-15 · Matheus Lohse · DECISÃO TRIBUTÁRIA TASK-2-006: Positivo, Negativo e Bloqueado sempre obrigatórios; Ambíguo obrigatório somente quando houver sobreposição real. Implementado na SKIP `0.0.170`; QA completo passou; aguarda teste humano.
- 2026-09-15 · Matheus Lohse · AMPLIAÇÃO TASK-2-006 implementada na SKIP `0.0.172`: criados catálogos separados e editáveis de Eventos e Naturezas, aplicabilidade PF/PJ/Ambos, vínculo, datas, autoria, inativação e históricos append-only. Migração 0058 aplicada; QA completo, RLS, 401 e 403 passaram; aguarda teste humano.
- 2026-09-15 · Matheus Lohse · TESTE HUMANO TASK-2-006 falhou (feedback dos catálogos): tela em tabela com formulário lateral fixo não atende; adição, edição e histórico devem abrir em modal a partir de uma lista → corrigido na SKIP `0.0.173`; QA completo passou; aguarda reteste humano.

## 2026-09-16

- 2026-09-16 · Matheus Lohse · DEBUG TASK-2-006: erros de inativar/criar/editar nos catálogos corrigidos na SKIP `0.0.174`; causa nos logs: spread de objeto não suportado no JSVM e bool `ativo` obrigatório rejeitando `false`. QA completo passou; migração `0059` aplicada.
- 2026-09-16 · Matheus Lohse · DEBUG TASK-2-006: inativar Natureza global alterava retroativamente versões históricas → corrigido na SKIP `0.0.175`; migração `0060` isolou catálogos e históricos por `rulebook_version_id`, cópia cria IDs próprios e versões Aprovadas/Retiradas são somente leitura. QA passou; aguardando teste humano.