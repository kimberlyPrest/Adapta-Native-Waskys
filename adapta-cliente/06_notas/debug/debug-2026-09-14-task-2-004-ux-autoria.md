# Debug — TASK-2-004 — campos multilinha, validação e autoria

- **Data:** 2026-09-14
- **Sintomas:** Enter desaparecia em campos multilinha; erro era exibido apenas no topo; autoria e “Regras: 1” eram ambíguos.
- **Causa 1:** o `onChange` executava split/trim/filter a cada tecla e eliminava a linha vazia criada pelo Enter.
- **Causa 2:** a validação dependia apenas da resposta do backend, sem mapa local de campos inválidos nem mensagem próxima ao botão.
- **Causa 3:** a fixture técnica foi criada com sessão técnica do Matheus; o histórico expandia só a relação. O número era a quantidade de regras no snapshot, mas o rótulo não explicava isso.
- **Correção:** preservar linhas durante edição; normalizar somente na fronteira backend; validar no frontend; marcar campos em vermelho/laranja; repetir alerta junto ao botão; adicionar autoria textual; atribuir revisões técnicas 1–3 a Jarvis (IA), preservar revisão humana 4 como Matheus; trocar rótulo para “Quantidade de regras nesta revisão”.
- **Verificação:** SKIP 0.0.133; migrações 0045/0047 aplicadas; 23 testes, setup, análise estática, build, integrações e preview passaram. Navegador confirmou Enter, dois alertas e autoria correta.
- **Gate:** aguardando reteste humano.
