# Desafio 03 - Escolha o modelo adequado e controle o tamanho da resposta

[< Desafio anterior](./Challenge-02.md) - **[Início](../README.md)** - [Próximo desafio >](./Challenge-04.md)

## O que você vai aprender

Nem toda tarefa exige o mesmo tipo de raciocínio. Ordenar versões de software é diferente de planejar um produto com requisitos incompletos.

Neste desafio, você vai executar as mesmas tarefas em dois modelos, avaliar os resultados e decidir quando uma opção de menor custo é suficiente e quando vale usar outra com maior capacidade de raciocínio.

Ao final, você deverá conseguir:

- Comparar modelos sem mudar o prompt ou o contexto entre as execuções.
- Avaliar uma resposta objetiva e uma resposta aberta.
- Distinguir quantidade de texto, uso de tokens e consumo de créditos.
- Restringir a saída sem remover requisitos importantes.

> **Ideia central:** o melhor custo-benefício é o menor custo para chegar a um resultado aceitável, não necessariamente o menor custo da primeira resposta.

## Antes de começar

1. Abra o GitHub Copilot Chat no VS Code.
2. Escolha dois modelos disponíveis na sua organização:
   - **Modelo A:** uma opção de menor custo para o seu plano.
   - **Modelo B:** uma opção com capacidade de raciocínio diferente, que você queira comparar com A.
3. Registre os nomes e as condições de cobrança exibidas no seu ambiente. Não presuma que um modelo seja gratuito ou tenha um multiplicador específico.
4. Copie o [modelo de medições](./Resources/Challenge-03-ModelSelection/measurements-template.md) para registrar seus resultados.

Não é necessário criar uma aplicação. Os [prompts](./Resources/Challenge-03-ModelSelection/prompts.md) e o [guia de restrições de saída](./Resources/Challenge-03-ModelSelection/output-constraints.md) estão na pasta de recursos.

Se apenas um modelo estiver disponível, acompanhe uma demonstração do instrutor e identifique quais resultados foram demonstrados, em vez de medidos por você.

## Prepare uma comparação justa

- Use uma conversa nova para cada combinação de modelo e tarefa.
- Mantenha o mesmo modo do chat, as mesmas instruções e os mesmos anexos. Prefira uma janela sem projeto aberto para não adicionar contexto de código.
- Não habilite ferramentas externas para estas tarefas.
- Use exatamente os prompts fornecidos.
- Na comparação principal, registre apenas a primeira resposta de cada modelo, sem corrigir ou reformular a solicitação.
- Preserve as respostas para avaliá-las depois.

Você terá quatro execuções principais:

| Execução | Tarefa | Modelo |
|---|---|---|
| 1 | Ordenação de versões | A |
| 2 | Ordenação de versões | B |
| 3 | Esclarecimento de um produto | A |
| 4 | Esclarecimento de um produto | B |

> **Sem resultado predeterminado:** qualquer um dos modelos pode acertar, errar, perguntar ou produzir uma resposta melhor. O objetivo é analisar o que ocorreu, não comprovar que um modelo sempre vence.

---

## Parte 1 - Compare uma tarefa objetiva

### Etapa 1 - Envie o mesmo prompt aos dois modelos

Em uma nova conversa para cada modelo, envie:

```text
Ordene estes números de versão de software do mais antigo para o mais recente e liste-os
em ordem, separados por vírgulas: 1.9.0, 1.10.0, 1.2.0, 1.11.0, 1.9.5
```

### Etapa 2 - Confira a correção

O gabarito é:

```text
1.2.0, 1.9.0, 1.9.5, 1.10.0, 1.11.0
```

Compare os componentes numéricos de cada versão. Uma ordenação puramente alfabética não resolve a tarefa.

### Etapa 3 - Registre o resultado

| Critério | Modelo A | Modelo B |
|---|---|---|
| Acertou a ordem? | | |
| Respeitou o formato pedido? | | |
| Tokens de entrada, se disponíveis | | |
| Tokens de saída, se disponíveis | | |
| Créditos atribuíveis à execução, se disponíveis | | |
| Tempo aproximado de resposta | | |

Se ambos acertarem, compare o consumo observado e o tempo. Uma explicação longa não agrega necessariamente valor a uma tarefa que pediu apenas uma lista.

---

## Parte 2 - Compare uma tarefa aberta

Nesta parte, não há um único gabarito. Você avaliará como cada modelo lida com uma ideia que ainda precisa de esclarecimentos.

### Etapa 1 - Envie o mesmo prompt aos dois modelos

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

O prompt separa duas coisas: **investigar o problema agora** e **planejar depois de receber respostas**.

### Etapa 2 - Avalie apenas a primeira resposta

Não responda às perguntas durante a comparação principal. O plano completo não é uma entrega desta etapa.

Use a mesma escala para os dois modelos:

- **0:** não atendeu ao critério.
- **1:** atendeu parcialmente, com lacunas importantes.
- **2:** atendeu de forma clara e útil.

| Critério | O que observar | A (0 a 2) | B (0 a 2) |
|---|---|---|---|
| Respeito às instruções | Fez até 5 perguntas e aguardou antes de planejar? | | |
| Utilidade das perguntas | Esclareceu quem usa o produto, para quê e com quais regras? | | |
| Tratamento de incerteza | Evitou assumir funcionalidades como requisitos confirmados? | | |
| Qualidade dos riscos | Apresentou 5 riscos concretos, em vez de apenas “prazo” e “orçamento”? | | |
| Relação com o domínio | Relacionou os riscos às possíveis atividades de pickleball? | | |
| **Total** | **Máximo de 10 pontos** | | |

Por exemplo, conflitos de reserva só fazem sentido **se houver reserva de quadras**. O modelo deve explicitar essa condição, não decidir sozinho que o produto terá reservas.

Mais perguntas, mais palavras ou mais termos técnicos não significam automaticamente mais qualidade. Justifique suas notas citando trechos das respostas.

### Etapa 3 - Registre o consumo separadamente

Anote tokens, créditos e tempo quando disponíveis. Uma nota de qualidade maior pode justificar maior consumo, mas isso precisa ser explicado a partir da resposta, não do nome do modelo.

> Uma única resposta não mede a confiabilidade geral de um modelo. Se quiser repetir o experimento, faça o mesmo número de repetições para ambos, em conversas novas, e mantenha esses resultados separados da primeira rodada.

---

## Parte 3 - Decida com base nas evidências

Reúna os resultados:

| Tarefa | Resultado de A | Consumo de A | Resultado de B | Consumo de B | Qual escolheria e por quê? |
|---|---|---|---|---|---|
| Ordenação de versões | | | | | |
| Esclarecimento do produto | | | | | |

Indique a unidade de consumo em cada célula: tokens de saída, tokens totais informados ou créditos. Não misture unidades como se fossem equivalentes.

### Como interpretar o custo

O custo total de uma tarefa inclui todas as interações necessárias para concluí-la, inclusive esclarecimentos, correções e novas tentativas.

Na cobrança por uso, tokens de entrada, saída e cache podem ter tarifas diferentes. Por isso:

- Não estime tokens contando palavras ou comparando visualmente o tamanho das respostas.
- Não use a ocupação da janela de contexto como se fosse o total faturado.
- Não converta tokens em créditos sem as tarifas aplicáveis ao modelo e ao seu plano.
- Se não houver medição por execução, escreva **“não disponível”**. Ainda é possível comparar correção e qualidade.

Se houver créditos individualizados, o consumo de uma rodada é a soma dos créditos das suas interações. O tempo de revisão humana também deve ser considerado na decisão, mas registrado separadamente.

Responda:

1. Qual modelo entregou uma resposta aceitável com menor consumo medido em cada tarefa?
2. Se faltarem métricas, o que você consegue concluir e o que permanece desconhecido?
3. Que tipo de erro exigiria mais revisão ou retrabalho no seu contexto?
4. O resultado sustenta uma escolha para esta tarefa ou uma afirmação geral sobre todos os modelos?

---

## Parte 4 - Aplique a comparação ao seu trabalho

Escolha duas tarefas reais que você possa compartilhar sem expor dados sensíveis:

- Uma tarefa bem definida, com resultado verificável.
- Uma tarefa com ambiguidade ou necessidade de avaliar alternativas.

Antes de executar, registre sua previsão. Depois, use o mesmo prompt nos dois modelos e avalie a saída com critérios definidos antecipadamente.

| Tarefa | Critério de aceitação | Modelo previsto | Melhor resultado observado | O que você aprendeu? |
|---|---|---|---|---|
| 1 | | | | |
| 2 | | | | |

Não é necessário escolher um vencedor quando os dados forem insuficientes ou os resultados equivalentes.

---

## Opcional - Reduza a saída sem perder correção

Escolha um dos modelos e execute os prompts abaixo em duas conversas novas.

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

Confira nas duas versões: `"ovo"` e `""` devem resultar em `True`; `"Ovo"` e `"python"`, em `False`.

Compare os tokens de saída, se disponíveis, e o respeito ao formato. Não presuma que o código será idêntico nem que a restrição sempre reduzirá o custo total. Ela não elimina necessariamente processamento interno ou chamadas adicionais.

## Critérios de sucesso

- [ ] Registrei os modelos e mantive prompt, modo e contexto equivalentes.
- [ ] Executei as quatro combinações principais em conversas novas.
- [ ] Conferi a ordenação pelo gabarito, incluindo o formato da resposta.
- [ ] Avaliei a tarefa aberta com a mesma escala e evidências para ambos os modelos.
- [ ] Registrei métricas disponíveis sem estimar tokens a partir do tamanho do texto.
- [ ] Justifiquei minhas escolhas sem pressupor que um modelo precisa vencer.
- [ ] Comparei duas tarefas reais e revi minhas previsões.
- [ ] Se fiz a etapa opcional, conferi a correção das duas funções.

## Recursos de aprendizagem

- [Documentação do GitHub Copilot e modelos disponíveis](https://docs.github.com/en/copilot)
- [Cobrança baseada em uso para organizações e empresas](https://docs.github.com/en/copilot/concepts/billing-and-usage/organizations-and-enterprises/billing)
- [Recursos deste desafio](./Resources/Challenge-03-ModelSelection/README.md)
