# Aprendizado — feedback visual exige estado estrutural verificável

- **Sinal:** uma solução tecnicamente lateral pode continuar visualmente ruim quando mantém um trilho vazio; elementos em `flex-col` não satisfazem “ao lado”; e texto mapeado não garante quebra perceptível.
- **Orientação:** converter requisitos visuais em estados estruturais binários: painel ausente/presente; linha/coluna; seleção padrão explícita; timestamp não nulo; colunas e listas semânticas.
- **Aplicação:** regressões da TASK-2-005 agora verificam ausência de `w-14`, abertura do primeiro registro ordenado, `flex-row`, fallback de data, coluna Versão e `ul/li`.
