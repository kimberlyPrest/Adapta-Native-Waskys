# Aprendizado — imutabilidade e cópia de Rulebook

- **Sinal:** alteração legislativa após aprovação exige atualização, mas editar diretamente a versão aprovada compromete a reprodução de processamentos históricos.
- **Orientação:** manter a versão Aprovada imutável e criar atomicamente um novo Rascunho a partir dela, copiando regras e a última revisão do Golden Set. A cópia precisa ser revisada, validada e aprovada novamente.
- **Garantia:** qualquer falha reverte toda a operação; o original, seus históricos e processamentos nunca são modificados.
- **Aplicação:** TASK-2-006, SKIP 0.0.168.
