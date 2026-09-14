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
- TASK-2-004 analisada e implementada tecnicamente até a SKIP `0.0.130`; debug de RLS interrompido por 503.

## 2026-09-14

- DEBUG TASK-2-004: migração 0044 reconciliou escrita direta para `null`; segurança, rota atômica, concorrência, histórico, 21 testes, QA e preview passaram na SKIP `0.0.131`.
- 2026-09-14 · Matheus Lohse · TESTE HUMANO TASK-2-004 falhou: Enter era removido nos campos multilinha; erros não eram destacados nem repetidos junto ao botão; “Regras: 1” era ambíguo e fixture técnica aparecia como Matheus.
- 2026-09-14 · Matheus Lohse · DEBUG TASK-2-004: causa raiz foi normalização destrutiva a cada tecla, validação somente no backend e autoria relacional sem separar fixture técnica de ação humana → corrigido na SKIP `0.0.133`: Enter preservado, validação local com destaque e dois alertas, rótulo “Quantidade de regras nesta revisão”, revisões técnicas 1–3 Jarvis (IA) e revisão humana 4 Matheus; migrações 0045/0047, 23 testes, QA e preview passaram; aguardando reteste humano.
