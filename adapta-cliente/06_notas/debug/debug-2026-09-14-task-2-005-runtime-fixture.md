# Debug — TASK-2-005 — runtime, JSON e isolamento da fixture

- **Data:** 2026-09-14
- **Falhas encontradas:** JSON vazio obrigatório bloqueava casos sem campos; zero em campo numérico obrigatório bloqueava 0 reprovações; funções globais não eram visíveis nos callbacks do JSVM; JSON persistido chegava como bytes ou strings numéricas; spread no decoder falhava e o catch retornava lista vazia; regras da fixture foram inicialmente adicionadas à v1, divergindo do snapshot histórico.
- **Causas:** semântica de required do PocketBase para vazio/zero, pool isolado de callbacks do JSVM, representação variável de JSON e limitação de spread no runtime.
- **Correções:** campos legitimamente vazios/zero opcionais mas definidos pela rota; lógica inline nos callbacks; decoder byte a byte sem fallback silencioso; versão sintética v2 exclusiva com quatro regras, snapshot coerente e golden set realocado; v1 restaurada para uma regra.
- **Verificação:** SKIP 0.0.140; migrações 0048–0051; 34 testes e QA; v1 uma regra/snapshot uma, v2 quatro regras/snapshot quatro; execução 4/4, conflito único, campos ausentes CPF e VALOR BRUTO; entrada incompleta/concorrência 400 sem resíduo; escrita 403; cross-owner 404; preview aprovado.
- **Gate:** aguardando teste humano.
