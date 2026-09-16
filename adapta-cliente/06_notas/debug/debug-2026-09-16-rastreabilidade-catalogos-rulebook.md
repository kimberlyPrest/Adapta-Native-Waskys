# Debug — 2026-09-16 — rastreabilidade versionada de Eventos e Naturezas

## Task e problema
TASK-2-006. A inativação de uma Natureza global afetava as associações exibidas em regras de versões históricas, inclusive uma versão Retirada, sem registrar a repercussão no histórico do Rulebook.

## Reprodução e causa raiz
A implementação da SKIP 0.0.174 mantinha `rulebook_events` e `rulebook_natures` como registros globais mutáveis por proprietário. As regras guardavam snapshots textuais, mas também relações vivas (`event_catalog_id` e `nature_catalog_id`) para esses mesmos registros. A UI filtrava somente cadastros ativos. Assim, a inativação global ocultava o item e fazia versões antigas parecerem desassociadas, embora a versão devesse ser imutável.

## Correção — SKIP 0.0.175
- Migração 0060 criou `rulebook_version_id` em Eventos, Naturezas e respectivos históricos e reconstruiu catálogos próprios para cada versão a partir dos snapshots já preservados nas regras.
- Eventos e Naturezas só podem ser criados, editados, inativados ou reativados dentro de uma versão em Rascunho; versões Aprovadas/Retiradas são somente leitura.
- Toda alteração de catálogo grava histórico específico e `system_logs` com o ID/número do Rulebook.
- A cópia de versão duplica Eventos, Naturezas, regras e Golden Set para IDs próprios do novo Rascunho, sem relação viva compartilhada com a origem.
- O modal de “Criar nova versão a partir desta” pergunta se a origem também deve ser retirada. Se sim, exige data de fim da vigência e grava, na mesma transação, cópia + fim da vigência + retirada + histórico/log. Se não, registra somente a cópia no Rulebook.

## Evidências automáticas
- SKIP 0.0.175: setup, análise estática, build, integrações e testes passaram.
- Migração 0060 aplicada no Skip Cloud.
- Schema: `rulebook_version_id` presente nas quatro coleções; escrita direta permanece bloqueada (`createRule`, `updateRule`, `deleteRule` nulos); relações sem cascade delete.
- Logs de hooks: zero erros após a implantação.
- Preview carregou até o login.
- Arquivos TSX restaurados e verificados byte a byte após gravação: zero placeholders/truncamento.

## Gate
Aguardando novo teste humano de Matheus. A task permanece aberta.
