# AP-2026-09-10-1515 — Auditoria não pode ser melhor esforço

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: TASK-2-001 / SPEC-2-001
- Sinal: operações principais podiam anunciar sucesso enquanto o logger ocultava falha ou a tela de Logs permanecia desatualizada.
- Evidência: Debug Summary `debug-2026-09-10-auditoria-status-modais.md`; requisições HTTP 200 para `system_logs`; ausência de chamada no caminho de edição cadastral; correção validada no pipeline SKIP 0.0.102.
- Regra reutilizável: em operações auditáveis, o log deve ser obrigatório e sua falha deve impedir a confirmação visual de sucesso; telas de auditoria devem recarregar por evento ou foco.
- Quando aplicar: criação, edição, revisão, alocação ou decisão que prometa trilha imutável.
- Quando não aplicar: telemetria diagnóstica opcional que não constitui evidência de negócio.
- Confiança: alta — causa reproduzida no código e confirmada pelos logs HTTP.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
