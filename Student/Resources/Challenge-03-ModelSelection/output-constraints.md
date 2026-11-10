# Restrições de saída - Peça o formato de que você precisa

Uma restrição de saída orienta como o modelo deve apresentar a resposta. Ela pode reduzir explicações desnecessárias, mas não garante correção, formato válido ou economia.

## Padrões úteis

| Objetivo | Exemplo de instrução | O que conferir |
|---|---|---|
| Apenas um valor | “Responda somente com o número.” | O valor continua correto? |
| Apenas código | “Retorne apenas o código, sem explicação ou Markdown.” | O código atende aos requisitos? |
| Explicação curta | “Explique em até 50 palavras.” | O limite foi respeitado sem omitir algo essencial? |
| JSON | “Retorne JSON com as propriedades `count` e `events`.” | O JSON é válido e segue o contrato? |
| Lista curta | “Liste no máximo 3 itens.” | Os itens são suficientes para a tarefa? |
| Evitar repetição | “Não repita o enunciado.” | A resposta continua compreensível? |

Essas instruções não são limites técnicos rígidos: a saída ainda precisa de validação.

## Experimento do Desafio 03

Use as duas variantes da função `is_palindrome` disponíveis em [prompts.md](./prompts.md). Elas possuem os mesmos requisitos funcionais; a segunda acrescenta apenas a restrição de formato.

1. Escolha um único modelo.
2. Abra uma conversa nova para cada variante.
3. Confira os quatro casos de aceitação.
4. Registre tokens de saída e créditos, se disponíveis.
5. Compare a utilidade e o consumo das respostas.

Não presuma que as duas versões produzirão código idêntico. O objetivo é verificar se a resposta restrita preserva o comportamento exigido.

## Limites da técnica

- Menos texto visível não mede necessariamente todo o processamento interno.
- A restrição não reduz automaticamente tokens de entrada ou chamadas de ferramentas.
- As tarifas de entrada, saída e cache podem diferir conforme o modelo e o plano.
- Uma resposta curta e incorreta não é uma otimização.
- Em tarefas abertas, explicações e alertas podem ser parte importante da entrega.

Consulte o [Desafio 03](../../Challenge-03.md) para os critérios de comparação e registre os resultados no [modelo de medições](./measurements-template.md).
