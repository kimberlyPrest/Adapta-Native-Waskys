# Debug — TASK-2-002 — linguagem de inativação e autoria Jarvis (IA)

- **Data:** 2026-09-10
- **Sintoma:** o fluxo que preserva cadastros ainda usava “Excluir/Desligar”; Jarvis (IA) existia como usuário, mas não aparecia como autor no histórico ou nos Logs.
- **Reprodução:** versão 0.0.115 testada pelo champion; inspeção confirmou bifurcação entre exclusão definitiva e desligamento, além de fallback visual “Usuário atual”.
- **Causa raiz:** a UI decidia excluir cadastros sem vínculos; o usuário Jarvis havia sido criado, porém logs manuais sempre usavam o autenticado e relações com usuário de sistema não eram expandidas para a sessão humana.
- **Correção:** versão 0.0.119 usa Inativar/Inativo no fluxo preservado; adiciona autoria textual auditável; cria empresa e sócio sintéticos, associa ambos, inativa a empresa e registra histórico/logs como Jarvis (IA).
- **Verificação automática:** setup, análise estática, build, integrações e testes passaram na 0.0.119.
- **Verificação visual parcial:** na 0.0.116 o botão Inativar e a fixture em Inativos foram confirmados; o histórico revelou o fallback incorreto, corrigido depois. A prova final da 0.0.119 está bloqueada porque o Skip Cloud responde HTTP 503.
- **Gate:** bloqueada até o backend voltar; depois, repetir a verificação visual completa e pedir novo teste humano.
