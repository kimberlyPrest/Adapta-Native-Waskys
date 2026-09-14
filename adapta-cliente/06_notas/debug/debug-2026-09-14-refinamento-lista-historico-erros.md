# Debug — TASK-2-005 — refinamento final de UX e histórico

- **Data:** 2026-09-14
- **Versão anterior:** SKIP 0.0.159
- **Versão corrigida:** SKIP 0.0.160

## Causas confirmadas

- A lista recolhida mantinha uma coluna vertical de 56 px, visualmente desconectada do conteúdo.
- O carregamento buscava versões em ordem decrescente, mas não abria o primeiro registro.
- O badge estava em contêiner vertical e `created` podia vir ausente na resposta imediata da execução.
- Os históricos não exibiam versão em coluna própria nem identificavam a posição da regra/caso.
- Os erros eram renderizados em blocos genéricos e não em uma lista semântica explícita.

## Correção

Lista lateral redesenhada; versão mais nova aberta automaticamente; badge e botão na mesma linha; fallback ISO para horário; coluna Versão e numeração de Regra/Caso; erros com `p`, `ul` e `li` em bloco.

## Evidência

A SKIP 0.0.160 passou por setup, análise estática, build, integrações e testes sem erros. Regressões específicas cobrem os seis requisitos.
