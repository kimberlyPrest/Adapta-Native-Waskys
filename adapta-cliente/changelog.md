# Changelog

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
- 2026-09-14 · Matheus Lohse · TASK-2-006 implementada na SKIP `0.0.166`: aprovação/retirada atômicas com autoria e histórico, seleção única por competência, RLS append-only e UI do ciclo. Migração 0057 aplicada; QA passou. Provas reais: 401 sem auth, 403 escrita direta, 400 para competência inválida/sem vigente e concorrência obsoleta sem resíduo. Gate ajustado para Golden Set 100% aprovado, preservando o caso Ambíguo visível sem escolha automática. Aguardando teste humano.

## 2026-09-15

- 2026-09-15 · Matheus Lohse · DEBUG TASK-2-006: seleção por competência não explicava claramente que consulta e registra; versão Aprovada não oferecia fluxo para alteração legislativa → corrigido na SKIP `0.0.168`: texto operacional explícito e ação "Criar nova versão a partir desta". Rota atômica copia regras e última revisão do Golden Set para novo Rascunho, registra histórico/log e preserva integralmente o original. QA passou; origem não aprovada retornou 400 sem resíduo (versões 2→2). Aguardando teste humano.
- 2026-09-15 · Matheus Lohse · DEBUG TASK-2-006: título alterado para "Consulta de Rulebook por Competência" na SKIP `0.0.169`; QA passou. DÚVIDA tributária registrada: exigir caso Ambíguo em toda revisão força duas regras sobrepostas no próprio Rulebook; decidir entre obrigatoriedade por versão ou teste sistêmico separado antes de alterar o gate.
- 2026-09-15 · Matheus Lohse · DECISÃO TRIBUTÁRIA TASK-2-006: Positivo, Negativo e Bloqueado sempre obrigatórios; Ambíguo obrigatório somente quando houver sobreposição real. Implementado na SKIP `0.0.170`: backend e UI calculam sobreposição por Evento+Código normalizado; novos Golden Sets iniciam com três casos; diagnóstico visual orienta quando incluir Ambíguo. Teste sistêmico permanente continua provando detecção sem escolha automática. QA completo passou; aguarda teste humano.
- 2026-09-15 · Matheus Lohse · AMPLIAÇÃO TASK-2-006 implementada na SKIP `0.0.172`: criados catálogos separados e editáveis de Eventos e Naturezas, aplicabilidade PF/PJ/Ambos, vínculo Natureza–Evento, datas, autoria, inativação reativável e históricos append-only. Migração 0058 fez backfill de R-4010/R-4020 e naturezas existentes; regras preservam snapshot e vínculos. Editor e cópia versionada usam os catálogos. QA completo, RLS, 401 e 403 passaram; aguarda teste humano.
- 2026-09-15 · Matheus Lohse · TESTE HUMANO TASK-2-006 falhou (feedback dos catálogos): tela em tabela com formulário lateral fixo não atende; adição, edição e histórico devem abrir em MODAL a partir de uma lista → corrigido na SKIP `0.0.173`: painel refeito em lista de cartões com botão "Adicionar Evento/Natureza", Editar, Histórico e Inativar/Reativar abrindo modais (adição/edição com motivo obrigatório; histórico em tabela Data/Usuário/O que foi modificado/Motivo; inativação/reativação com motivo em modal). QA completo passou; aguarda reteste humano.
