# AP-2026-09-14-1125 — JSON do PocketBase no JSVM exige decoder explícito

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: TASK-2-005 / SPEC-2-002
- Sinal: arrays JSON persistidos chegaram ao hook como bytes numéricos ou strings numéricas; spread em `String.fromCharCode` falhou e fallback silencioso transformou campos obrigatórios em lista vazia.
- Evidência: `06_notas/debug/debug-2026-09-14-task-2-005-runtime-fixture.md`; execução real exibiu códigos numéricos antes da correção e nomes CPF/VALOR BRUTO depois.
- Regra reutilizável: em hooks PocketBase deste projeto, decodificar JSON aceitando array normal, bytes numéricos, strings numéricas e string JSON; construir texto byte a byte sem spread; JSON inválido deve falhar explicitamente, nunca virar lista vazia silenciosa.
- Quando aplicar: leitura de campos JSON persistidos dentro de hooks e rotas do JSVM.
- Quando não aplicar: JSON recebido diretamente do body HTTP já validado como objeto/array JavaScript.
- Confiança: alta — duas representações foram reproduzidas e a correção foi verificada por API e preview.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto
