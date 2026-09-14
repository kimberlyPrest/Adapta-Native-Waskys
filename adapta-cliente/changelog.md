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
- 2026-09-14 · Matheus Lohse · TESTE HUMANO TASK-2-005 falhou: contadores de revisão se misturavam; conflito não identificava as regras; falta de seções, explicação e lista recolhível; validação parecia exclusiva do golden set.
- 2026-09-14 · Matheus Lohse · DEBUG TASK-2-005: causa raiz foi histórico do rulebook exibido no lugar do golden set e backend sem detalhes de conflito → corrigido na SKIP `0.0.141`: rótulos e históricos separados, conflito com regras detalhadas, abas de navegação, explicação do golden set, versões recolhíveis e botão “Validar regras desta versão”; 39 testes, QA e preview passaram; aguardando reteste humano.
