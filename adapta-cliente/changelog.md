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
- 2026-09-14 · Matheus Lohse · DEBUG TASK-2-005: auditoria do 3º feedback confirmou que a SKIP `0.0.158` aproximou apenas o badge 4/4, enquanto o resultado detalhado permanecia depois de todo o formulário → causa raiz: teste verificava presença de texto/classe, não a ordem estrutural → corrigido na SKIP `0.0.159`; painel detalhado movido para antes do formulário, cabeçalhos padronizados como "O que mudou" e regressão passou a provar botão < resultado < formulário. QA completo passou; aguardando reteste humano.
- 2026-09-14 · Matheus Lohse · DEBUG TASK-2-005: aprovação da 0.0.159 foi substituída por novo feedback visual/funcional antes do fechamento; lista lateral estreita, versão não abria por padrão, badge/horário/histórico e erros ainda inadequados → corrigido na SKIP `0.0.160`: lista redesenhada e removida ao recolher, versão mais nova abre automaticamente, badge fica ao lado do botão, timestamp tem fallback imediato, históricos incluem Versão e número da Regra/Caso, erros usam lista semântica com quebra real. QA completo e regressões específicas passaram; aguardando reteste humano.
- 2026-09-14 · Matheus Lohse · AJUSTE FINAL TASK-2-005: teste humano da SKIP `0.0.160` aprovado, com pedido de remover somente a coluna Versão dos históricos → rollback cirúrgico aplicado na SKIP `0.0.161`, preservando número da Regra/Caso em "O que mudou". QA completo passou; aguarda confirmação visual final antes do fechamento.
- 2026-09-14 · Matheus Lohse · DEBUG TASK-2-005: captura de tela da 0.0.161 mostrou célula "v2" residual na coluna Data do histórico do Rulebook → causa: célula multilinha escapou da verificação anterior → corrigido na SKIP `0.0.162` e regressão reforçada na `0.0.163` para provar ausência de coluna E célula nos dois históricos. QA completo passou; aguarda confirmação visual final.
