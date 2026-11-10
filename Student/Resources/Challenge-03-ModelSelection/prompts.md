# Desafio 03 - Prompts da comparação

Use estes prompts conforme o [Desafio 03](../../Challenge-03.md), em uma conversa nova para cada modelo e tarefa. Mantenha o restante do contexto equivalente.

## Parte 1 - Ordenação de versões

```text
Ordene estes números de versão de software do mais antigo para o mais recente e liste-os
em ordem, separados por vírgulas: 1.9.0, 1.10.0, 1.2.0, 1.11.0, 1.9.5
```

**Gabarito:**

```text
1.2.0, 1.9.0, 1.9.5, 1.10.0, 1.11.0
```

Confira a ordem e o respeito ao formato. Não presuma que um modelo usará menos tokens: registre a medição.

## Parte 2 - Esclarecimento de um produto

```text
Quero construir uma aplicação de pickleball, um esporte de raquete.

Antes de propor uma solução, faça no máximo 5 perguntas para esclarecer
o público, o objetivo principal e as regras do produto.

Não invente minhas respostas. Aguarde minhas respostas antes de produzir
um plano de implementação.

Também identifique 5 riscos ou complexidades que precisam ser investigados.
Se um risco depender de uma funcionalidade ainda não confirmada, deixe essa
condição explícita.
```

Avalie somente a primeira resposta. Não responda às perguntas nesta rodada.

Não há gabarito único. Use os cinco critérios do desafio: respeito às instruções, utilidade das perguntas, tratamento de incerteza, qualidade dos riscos e relação com o domínio. Dê de 0 a 2 pontos por critério e justifique com evidências.

## Opcional - Restrição de saída

Execute as duas variantes no mesmo modelo, em conversas novas.

**Sem restrição de formato:**

```text
Escreva uma função Python chamada is_palindrome(text: str) -> bool.
Compare a string exatamente como recebida, diferenciando maiúsculas,
espaços e pontuação. Considere a string vazia um palíndromo.
```

**Com restrição de formato:**

```text
Escreva uma função Python chamada is_palindrome(text: str) -> bool.
Compare a string exatamente como recebida, diferenciando maiúsculas,
espaços e pontuação. Considere a string vazia um palíndromo.
Retorne apenas o código, sem explicação e sem blocos delimitados de Markdown.
```

Confira `"ovo"` e `""` como `True`, e `"Ovo"` e `"python"` como `False`. Compare o formato e as métricas disponíveis sem presumir que o código ou o consumo serão iguais.
