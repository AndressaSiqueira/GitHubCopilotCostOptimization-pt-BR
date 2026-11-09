# Desafio 03 — Seleção de modelos — Recursos

Esta pasta contém tudo de que você precisa para o Desafio 03. **Não há uma base de código para executar** —
o desafio consiste em enviar dois prompts curtos a dois modelos diferentes e medir o que
é retornado.

## O que há aqui

| Arquivo | Finalidade |
|---|---|
| `prompts.md` | Os dois prompts exatos (fácil + difícil) e suas respostas corretas |
| `measurements-template.md` | Tabelas em branco para registrar o resultado + tokens de cada execução |
| `output-constraints.md` | Guia rápido de restrições de saída para reduzir o custo de tokens |

## Como realizar o desafio (VS Code + GitHub Copilot Chat)

1. Abra o GitHub Copilot Chat no VS Code. Inicie uma **nova conversa para cada par modelo/prompt**.
2. Use o **seletor de modelos** para selecionar um modelo de menor custo disponível para sua organização.
3. Cole um prompt de `prompts.md` exatamente como está escrito. Registre a resposta e o uso de tokens medido.
4. Inicie outra **nova conversa**, selecione um modelo mais forte e execute o **mesmo** prompt.
   Mantenha os anexos e as instruções idênticos aos da primeira execução. Registre a resposta e o uso de tokens medido.
5. Repita esse procedimento para ambos os prompts, usando uma nova conversa para cada execução.
6. Preencha `measurements-template.md` e responda às perguntas da Parte 3; depois, faça o exercício
   "classifique suas próprias tarefas" da Parte 4.

> **Regra:** Não tente novamente nem oriente o modelo básico quando ele errar a tarefa difícil. Uma
> primeira resposta errada é um resultado válido — e importante. Em vez disso, você refletirá sobre o custo de tentar novamente
> na Parte 2.

> **Se seu seletor mostrar apenas um nível:** pergunte ao instrutor quais modelos correspondem a "básico" e
> "premium" na sua organização ou use os números de referência do instrutor como demonstração.
