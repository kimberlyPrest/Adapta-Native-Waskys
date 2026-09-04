# SPEC-2-005 — Rascunho R-4010/R-4020 e pacote de revisão

**Fase:** 2  
**Status:** planejada — depende de rulebook, classificação e consolidação aprováveis  
**Dono:** analista fiscal; aprovação humana do responsável tributário  
**Origem no escopo:** F06, F08, F09, TR-03, TR-04, G2, G4  
**Degrau da solução:** construção mínima — gerar artefato interno revisável, sem prometer leiaute de importação ou transmissão.

## Resultado observável

Para a competência piloto, o cockpit gera um pacote de revisão contendo rascunhos de R-4010/R-4020, matriz de campos, itens bloqueados, totalizadores, fontes, rulebook, versão, aprovadores e checklist. O pacote é reproduzível e explicitamente marcado como não transmitido.

## Limites e dependências

- **Inclui:** seleção de evento por beneficiário; campos obrigatórios; rascunho estruturado; relatório de bloqueios; pacote JSON/CSV/HTML ou formato interno definido; checksum e versão.
- **Fora de escopo:** assinatura, transmissão, importação no Domínio, R-4099 produtivo, geração de DARF e leiaute oficial não confirmado.
- **Entradas e pré-condições:** grupos consolidados; rulebook aprovado; beneficiários e exceções tratadas; competência definida.
- **Saídas/artefatos:** pacote de revisão; relatório de reconciliação; checklist; hash; histórico da geração.
- **Dependências e responsáveis:** SPECs 2-001 a 2-004; operador/tributário validam campos.
- **Risco e plano B:** leiaute oficial não confirmado → saída fica como pacote de digitação assistida, sem declarar compatibilidade.
- **Rollback ou reversão:** invalidar pacote por versão e gerar novo sem apagar o anterior.

## Fluxo e regras

1. Sistema valida pré-condições e lista bloqueios.
2. Analista solicita geração do rascunho.
3. Sistema gera eventos por tipo de beneficiário e impede mistura PF/PJ incompatível.
4. Pacote exibe origem por linha, rulebook, aprovadores e aviso de não transmissão.
5. Revisor confere e aprova, rejeita ou devolve com motivo.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | lote completo e rulebook aprovado | pacote revisável com rascunhos e checksum | seguir para revisão humana |
| Limite | item pendente não bloqueante | pacote inclui item destacado e não aprovado | resolver ou registrar pendência |
| Falha | rulebook ausente, total divergente ou campo obrigatório vazio | geração bloqueada com motivo | corrigir e gerar nova versão |

## Checklist de execução

- [ ] Evento PF/PJ corresponde ao beneficiário e à regra.
- [ ] Todo campo do rascunho possui origem ou justificativa.
- [ ] Bloqueios aparecem antes da aprovação.
- [ ] Pacote tem rulebook, versão, aprovador e checksum.
- [ ] Aviso de não transmissão aparece no pacote e na tela.
- [ ] Nova geração não sobrescreve pacote anterior.

## Critérios de aceite

- [ ] **CA-2-017:** lote completo gera rascunho R-4010/R-4020 com origem por linha e checksum.
- [ ] **CA-2-018:** item PF não é gerado como R-4020 e item PJ não é gerado como R-4010 sem bloqueio explícito.
- [ ] **CA-2-019:** pacote sem rulebook, fonte, aprovador ou campo obrigatório fica bloqueado.
- [ ] **CA-2-020:** pacote reproduzido da mesma versão tem conteúdo e checksum idênticos.
- [ ] **CA-2-021:** pacote informa claramente que não foi transmitido nem importado no Domínio.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | gerar pacote com pré-condição faltante | fixture sem aprovador e campo obrigatório | geração bloqueada | erro + log |
| GREEN | gerar lote completo | executar fixture PF/PJ e exportar pacote | CA-2-017 a CA-2-021 passam | pacote + checksum |
| REFACTOR/REGRESSÃO | gerar novamente e reabrir versão antiga | repetir geração e consultar pacote anterior | conteúdo idêntico e histórico intacto | hashes + auditoria |

**Dados/fixtures:** lote com PF e PJ, item ambíguo, campo obrigatório ausente, regra aprovada e regra retirada.  
**Caminhos de erro obrigatórios:** PF/PJ incompatível, campo vazio, total divergente, rulebook ausente, checksum e tentativa de transmissão.  
**Evidência exigida:** pacote exportado, relatório de bloqueios, checksum, captura do aviso e aprovação humana registrada.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| TASK-2-013 | Implementar modelo de rascunho R-4010/R-4020 e mapeamento PF/PJ | Engenheiro + Analista fiscal | SPEC-2-005 | CA-2-017, CA-2-018 | RED/GREEN: lote misto gera eventos compatíveis com o beneficiário | rascunho estruturado e matriz de campos | TASK-2-010, TASK-2-012 | ☐ Leva 10 |
| TASK-2-014 | Implementar validação de pré-condições e bloqueios do pacote | Engenheiro | SPEC-2-005 | CA-2-019 | Fixture sem rulebook, fonte, aprovador, campo e total conciliado | relatório de bloqueios acionáveis | TASK-2-013 | ☐ Leva 11 |
| TASK-2-015 | Implementar exportação do pacote, checksum e reprodução | Engenheiro | SPEC-2-005 | CA-2-017, CA-2-020 | Regressão: exportar duas vezes a mesma versão e comparar hashes | pacote exportado, checksum e log | TASK-2-014 | ☐ Leva 12 |
| TASK-2-016 | Implementar revisão humana e aviso de não transmissão | Analista fiscal + Responsável tributário | SPEC-2-005 | CA-2-019, CA-2-021 | Fluxo manual de revisar, aprovar/devolver e tentar ação externa | checklist assinado, auditoria e aviso persistente | TASK-2-015 | ☐ Leva 13 |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
