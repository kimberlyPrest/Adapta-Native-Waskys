# Debug — TASK-2-005 — proximidade do resultado da validação

- **Data:** 2026-09-14
- **Champion:** Matheus Lohse
- **Versão com falha residual:** SKIP 0.0.158
- **Versão corrigida:** SKIP 0.0.159

## Sintoma

O badge resumido `4/4 casos passaram` estava junto ao botão, porém o painel com conflitos e resultados por caso continuava depois de todo o formulário do Golden Set.

## Causa raiz

A regressão anterior verificava somente a presença do texto `Resultado detalhado logo abaixo` e da classe visual do painel. Ela não comprovava a posição relativa entre botão, resultado detalhado e formulário, permitindo um falso positivo.

## Correção

- Movido o painel completo `Última validação das regras` para imediatamente depois do bloco do botão e do badge, antes dos alertas e do formulário.
- Removida a renderização antiga para impedir duplicidade.
- Padronizados os históricos do Rulebook e Golden Set com `Data / Usuário / O que mudou / Motivo`.
- Regressão alterada para comprovar `botão < resultado detalhado < formulário` e uma única ocorrência do painel.
- Regressões adicionais comprovam a ordem dos quatro cabeçalhos e o recolhimento lateral `w-80 → w-14`.

## Evidência

`skip_project_apply_changes` criou a versão `0.0.159`; setup, análise estática, build, integrações e testes passaram sem erros. A inspeção pública alcançou somente a tela de login; a verificação autenticada permanece no gate humano.
