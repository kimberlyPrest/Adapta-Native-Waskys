# Estado atual — Adapta Cliente

- task_id: TASK-2-007
- champion: Matheus Lohse
- spec: adapta-cliente/04_fase-atual/02-SPECs/spec-2-003-classificacao-excecoes.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada em 2026-09-18 ("Autorização")
- teste_humano: pendente — validar a SKIP `0.0.193` (motor de sugestão + páginas Casos/Sugestões/Golden set + correções de save e UTF-8)
- verificacao_automatica: aprovada — SKIP `0.0.193`; QA completo passou; provas reais via curl e API
- ultima_acao: correção do encoding UTF-8 (reportada por Matheus em 22/09 ~12h — "campos salvos com formatação incorreta"). Causa raiz: 4 hooks (golden_set, suggestions, rulebook_lifecycle, rulebook_save_draft) decodificavam campos JSON (bytes do JSVM) com String.fromCharCode (latin-1), corrompendo acentos ("RazÃ£o") e quebrando o casamento de campos no golden set. Fix na 0.0.191 (percent-encoding + decodeURIComponent = UTF-8). Migrações 0064/0065 repararam os registros já gravados: 13 runs do golden set, 3 snapshots de histórico e 6 logs de texto, incluindo caixa errada ("RAZãO" → "RAZÃO"). Verificado via API: tudo legível em UTF-8.
- proxima_acao: teste humano de Matheus na SKIP `0.0.193`; se aprovado, encerrar TASK-2-007 e seguir para TASK-2-008
- atualizado_em: 2026-09-22
