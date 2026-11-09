# Restrições de saída — Guia rápido

Tokens de saída geralmente custam mais que tokens de entrada. Restringir o que o modelo *produz* é
uma alavanca de custo que você controla em **todos** os modelos. Use estes padrões quando não precisar de explicações.

| Objetivo | Adicione ao seu prompt | Efeito |
|---|---|---|
| Apenas a resposta | "Responda apenas com o número/valor, nada mais." | Remove o raciocínio reformulado + preâmbulo |
| Apenas código | "Retorne apenas o código. Sem explicação, sem blocos delimitados de Markdown." | Elimina os parágrafos de "Veja como funciona..." |
| Limitar o detalhamento | "Explique em 50 palavras ou menos." | Limite rígido para o tamanho da saída |
| Saída estruturada | "Responda em JSON no formato: `{ \"result\": number }`" | Evita divagações; fácil de interpretar |
| Sem reformulação | "Não repita a pergunta nem resuma a tarefa." | Remove a repetição da entrada |
| Lista limitada | "Liste no máximo 3 itens." | Impede a geração excessiva |

## Por que isso importa

Um modelo que recebe uma pergunta para a qual normalmente daria uma *explicação* gastará a maioria de seus tokens explicando uma
resposta em que você já confia. A restrição mantém a correção e reduz o custo. O efeito é
maior nas tarefas com **respostas detalhadas por padrão** (por exemplo, "escreva uma função") — nelas, sem a restrição, o modelo
envolve a resposta em explicações e Markdown.

## Experimente

Escolha uma tarefa com resposta detalhada no modelo básico e execute-a novamente com uma restrição de saída acrescentada:

```
Escreva uma função Python que verifique se uma string é um palíndromo.
Retorne apenas o código. Sem explicação, sem blocos delimitados de Markdown.
```

Compare o total de tokens — o código é idêntico, o custo é muito menor.

> Observações:
> - As restrições reduzem os tokens de **saída**. Elas têm pouco efeito quando a saída já é concisa
>   (por exemplo, uma resposta de uma linha) ou quando os tokens ocultos de "pensamento" de um modelo de raciocínio predominam.
> - As restrições **não** corrigem um modelo que está *errado* (veja a Parte 2). Para uma tarefa que o modelo básico
>   não consegue resolver com raciocínio, uma restrição apenas fornece uma resposta errada mais rápido — a seleção do modelo,
>   e não o formato da saída, é a solução nesse caso.
