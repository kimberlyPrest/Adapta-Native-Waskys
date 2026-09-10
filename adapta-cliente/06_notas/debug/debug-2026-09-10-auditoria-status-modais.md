# Debug TASK-2-001 — auditoria, status e modais

- **Data:** 2026-09-10
- **Champion:** Matheus Lohse
- **Versão com falha:** SKIP 0.0.100
- **Versão corrigida:** SKIP 0.0.102
- **Gate:** aguardando novo teste humano

## Sintomas reproduzidos

1. Logs gravados não apareciam enquanto a página de Logs permanecia aberta.
2. Edição cadastral comum não criava `system_logs`.
3. Status existia no card, mas não tinha destaque e não aparecia no cabeçalho dos detalhes.
4. Cadastro manual sempre nascia candidato.
5. Alocação rápida candidata não preenchia operador/data; desalocação bloqueada era rejeitada por faltar motivo.
6. Os três modais novos da v0.0.100 não tinham X superior.

## Causa raiz

- `createSystemLog` tratava auditoria como melhor esforço e ocultava erros.
- A página de Logs consultava somente na montagem/filtro, sem realtime ou refresh ao recuperar foco.
- O caminho de edição cadastral não chamava o logger.
- O formulário de criação fixava `status: candidato`.
- O caminho rápido de alocação não preenchia os campos de auditoria exigidos pelo hook.
- Os novos modais não reutilizaram o padrão visual de fechamento existente.

## Correção

- Falhas do logger agora são propagadas; a interface não anuncia sucesso sem auditoria.
- Logs assinam novos registros e recarregam ao recuperar foco/visibilidade.
- Edição comum cria log com motivo, versão e diff.
- Cadastro manual oferece candidato/confirmado; confirmado exige evidência e registra operador/data.
- Alocação candidata e desalocação registram operador/data/motivo/evidência.
- Status destacado nos cards e detalhes.
- X superior adicionado aos modais que faltavam.
- Coluna de Casos renomeada para `Situação do lançamento`.

## Verificação

- Setup: passou.
- Análise estática: passou.
- Build: passou.
- Integrações: passou.
- Teste do pipeline: passou.
- Arquivos publicados relidos com os pontos críticos presentes.
- Limitação: o script de teste do projeto é placeholder; o fluxo autenticado exige novo teste humano.
