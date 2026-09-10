# Status da pasta do cliente

**Status:** Fase 2 em execução controlada — TASK-2-002 analisada e aguardando autorização
**Data:** 10/09/2026
**Fase disponível:** Fase 2 — Motor determinístico e preparação de eventos
**Progresso:** 1 de 16 tasks concluída (6,25%); SPEC-2-001 com 1 de 3 tasks concluída

## TASK-2-001 — concluída

- Versão validada: SKIP `0.0.108`.
- Teste humano aprovado; vínculos append-only confirmados no schema.

## TASK-2-002 — análise concluída, sem implementação

### Baseline observado

- A interface remove pontuação e verifica apenas 11 dígitos para CPF e 14 para CNPJ.
- O hook de backend verifica apenas tamanho e somente durante atualização; criação pela API pode contornar a validação.
- Não existe algoritmo de dígitos verificadores de CPF/CNPJ.
- Não existe unicidade por `owner + documento_normalizado`.
- Não existe detecção formal de documento duplicado, documento conflitante ou grafias semelhantes.
- Não existe coleção/página de pendências cadastrais para inválidos, ausentes e conflitos.
- Fixtures antigas com números repetidos têm tamanho correto, mas são matematicamente inválidas; não podem ser apagadas silenciosamente.
- O script de testes continua placeholder.

### Recorte planejado

- Validador determinístico compartilhado para normalização e dígitos verificadores.
- Validação obrigatória na fronteira do backend para criação, atualização e confirmação.
- Duplicidade restrita à carteira do mesmo owner, sem vazamento entre usuários.
- Fila auditável de pendências cadastrais com tipos inválido, ausente, duplicado e possível correspondência.
- Bloqueio de confirmação e de vínculo confirmado enquanto houver pendência impeditiva.
- Migração segura dos registros inválidos existentes para bloqueado/pendente, preservando histórico.
- Fixtures/testes executáveis para CPF/CNPJ válido, curto, dígitos inválidos, vazio, duplicado e conflito de nome.

## Pendências seguintes

- TASK-2-003: revisão final e prova de acesso cruzado entre owners.
- SPEC-2-002 continua bloqueada pelo fechamento da SPEC-2-001 e pelo gate G2.

## Limitações

- Não haverá consulta automática à Receita, fusão automática de cadastros ou alteração do Domínio.
- `check-escopo` e `check-cliente` continuam pendentes.
