# Aprendizado — proximidade estrutural em interfaces

- **Sinal:** uma asserção de presença de texto ou classe visual não prova proximidade entre componentes.
- **Causa observada:** o teste aceitava o badge perto do botão enquanto o resultado detalhado permanecia após um formulário extenso.
- **Orientação reutilizável:** para requisitos como “junto”, “logo abaixo”, “antes” ou “depois”, testar a ordem estrutural dos elementos e a quantidade de ocorrências; quando possível, complementar com teste visual autenticado.
- **Aplicação:** a regressão da TASK-2-005 agora exige `botão < resultado detalhado < formulário` e exatamente um painel detalhado.
