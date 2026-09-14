# Debug — TASK-2-005 — revisões misturadas, conflito genérico e navegação

- **Data:** 2026-09-14
- **Sintomas:** revisão do golden set parecia não avançar; conflito não identificava as regras; regras sem seção clara; golden set sem explicação; lista de versões sempre aberta; navegação linear; validação parecia exclusiva do golden set.
- **Causa raiz 1:** a tela exibia o histórico do rulebook (revisão 1) enquanto a alteração do usuário criava a revisão 4 do golden set; os dois contadores se misturavam.
- **Causa raiz 2:** o backend enviava apenas chave e quantidade do conflito, sem detalhes das regras.
- **Causas 3–7:** layout linear sem seções, sem explicação do conceito, lista sempre expandida e validação posicionada como se pertencesse apenas ao golden set.
- **Correções:** rótulos “Revisão do rulebook” e “Revisão do golden set” com históricos separados; conflito com ordem, evento, código, nome e cenário de cada regra; página em abas Regras/Golden set/Histórico; explicação “exemplos de validação”; lista de versões recolhível; botão “Validar regras desta versão”.
- **Verificação:** SKIP 0.0.141; 39 testes e QA; execução 4/4 com conflito detalhado; preview validou as três abas, versões recolhíveis e históricos separados.
- **Gate:** aguardando reteste humano.
