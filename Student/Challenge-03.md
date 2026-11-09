# Desafio 03 - Seleção de modelos e restrições de saída

[< Desafio anterior](./Challenge-02.md) - **[Início](../README.md)** - [Próximo desafio >](./Challenge-04.md)

## Introdução

Nem toda tarefa precisa do modelo mais poderoso. Na cobrança baseada em uso, o custo **não** é apenas o preço por token do modelo. Ele é:

> **Custo total = tarifa por token × tokens × tentativas**

Esse último termo — *tentativas* — é o que as pessoas esquecem. Um **modelo básico** que responde corretamente a uma tarefa simples com poucos tokens é uma ótima opção econômica. Mas coloque esse mesmo modelo básico em um trabalho que exige discernimento de verdade e ele entregará uma **resposta aparentemente plausível, porém superficial ou completamente errada** — e você nem sempre perceberá isso imediatamente. Agora você está pagando de novo (e de novo) para perceber a lacuna e refazer o trabalho. O modelo que parecia ter menor custo por solicitação acabou de se tornar o mais caro.

Neste desafio, você executará o **mesmo prompt em um modelo básico e em um modelo premium** para dois tipos de tarefa muito diferentes. Primeiro, uma tarefa **fácil e verificável**; depois, uma tarefa **aberta**, sem gabarito. Em cada execução, você mede o **resultado** — *ele acertou ou qual é a qualidade da resposta?* — e o **custo de tokens**. A partir desses dados, você desenvolverá a habilidade que é o verdadeiro foco deste desafio: decidir *qual modelo usar para cada trabalho.*

> **Conceito-chave:** Menor custo por solicitação não é o mesmo que menor custo por *resultado*.

### Por que isso importa para a programação

Este desafio usa um prompt rápido e verificável e um prompt aberto de planejamento para que você vivencie os dois lados dessa relação de custo-benefício. Mas a lição é a mesma que você enfrenta sempre que programa com o Copilot: um agente constantemente **raciocina dentro de uma tarefa** — escolhendo a lógica, ponderando opções e avaliando se sua própria saída é boa. É exatamente aí que um modelo mais fraco fica aquém — às vezes *errado com confiança*, às vezes apenas superficial. A seleção do modelo determina a qualidade desse raciocínio, não apenas se alguma saída é produzida. Escolha o modelo adequado ao *pensamento* que a tarefa exige.

## Descrição

Você executará **duas tarefas**, cada uma em **dois modelos**:

- Um **modelo básico** — incluído na sua assinatura, sem multiplicador de solicitações premium (por exemplo, GPT-4.1, GPT-4o). Rápido e econômico.
- Um **modelo premium** — um modelo de ponta / raciocínio cobrado como uma solicitação premium com um multiplicador de custo (por exemplo, GPT-5, Claude Sonnet, um modelo da série o).

> Use os modelos de nível básico e premium que sua organização disponibiliza no **seletor de modelos** do GitHub Copilot Chat. Os nomes exatos não importam — o *padrão* importa. O seletor mostra um multiplicador (por exemplo, `1×`) ao lado dos modelos premium; modelos básicos não mostram multiplicador.

Para cada execução, registre o **resultado** (correto / incorreto) e o **uso de tokens** (`Exibir → Saída → "GitHub Copilot Chat"`; `View → Output` na interface em inglês, e/ou sua visualização de uso do Copilot). Se seu ambiente não mostrar uma contagem exata de tokens por solicitação, você ainda poderá ver o padrão: o modelo premium produz muito mais texto. Anote *aproximadamente quanto a mais*.

> **Regra — apenas a primeira tentativa:** Execute cada prompt **uma vez** por modelo e registre o que receber. Não oriente, execute novamente ou reformule em busca de um resultado melhor. O objetivo é ver o que cada modelo produz *na primeira tentativa* para cada tipo de tarefa.

> **Uma observação sobre as contagens de tokens:** Os números exatos de tokens variam entre execuções — especialmente nos modelos premium de raciocínio. Concentre-se no **padrão e na proporção**, não no número absoluto. Se um resultado parecer estranho, execute-o de 2 a 3 vezes.

---

## Parte 1 — Uma tarefa fácil (o modelo básico deve vencer)

Forneça este prompt exato a **ambos** os modelos:

```
Ordene estes números de versão de software do mais antigo para o mais recente e liste-os
em ordem, separados por vírgulas: 1.9.0, 1.10.0, 1.2.0, 1.11.0, 1.9.5
```

✅ Resposta correta: `1.2.0, 1.9.0, 1.9.5, 1.10.0, 1.11.0`

### Registre

| | Modelo básico | Modelo premium |
|---|---|---|
| Correto? | ? | ? |
| Total de tokens | ? | ? |

### O que observar

Ambos os modelos devem acertar. Agora compare as **contagens de tokens**. O modelo premium frequentemente produz muito mais saída — raciocínio reformulado, explicações — para a *mesma resposta correta*. Em uma tarefa fácil, esse gasto extra não traz nenhum benefício.

---

## Parte 2 — Uma tarefa aberta (avalie a *qualidade*, não uma resposta certa)

A Parte 1 tinha uma resposta verificável. **A maior parte do trabalho real não tem.** Quando você planeja uma funcionalidade, projeta um schema ou define o escopo de um projeto com o Copilot, não há gabarito — *você* precisa avaliar se a saída é boa. Esse discernimento é a habilidade que esta parte desenvolve, e é onde a escolha do modelo mais importa.

Forneça este prompt exato a **ambos** os modelos:

```
Quero construir uma aplicação de pickleball. Produza um plano de implementação.
Primeiro, faça todas as perguntas de esclarecimento de que precisar. Depois, identifique os
5 principais riscos ou complexidades ocultas que poderiam inviabilizar este projeto
e destaque-os no plano.
```

Observe que o prompt é **deliberadamente vago** ("uma aplicação de pickleball" — para fazer *o quê*?). Isso é intencional: um modelo forte deve *perceber a lacuna e perguntar* antes de planejar. A pergunta sobre riscos então força o modelo a realmente **pensar**, não apenas preencher um modelo de documento.

### Registre e avalie

Não há uma resposta correta; portanto, avalie cada resposta com base nestes critérios:

| Critério | Modelo básico | Modelo premium |
|---|---|---|
| Fez perguntas de esclarecimento *antes* de planejar? (quantas, quão pertinentes) | ? | ? |
| Os 5 principais riscos são genéricos ("aumento descontrolado de escopo, orçamento") ou realmente perspicazes? | ? | ? |
| O plano é específico de *pickleball* — ou um modelo genérico para "qualquer aplicação"? | ? | ? |
| Você confiaria nele o suficiente para começar a construir? | ? | ? |
| Total de tokens | ? | ? |

### O que observar

O modelo básico tende a **seguir em frente sem parar**: ele presume o que é a aplicação, produz um plano plausível, porém genérico, e lista riscos genéricos (orçamento, cronograma, aumento descontrolado de escopo). Raramente para para perguntar o que você está realmente construindo.

O modelo premium tem maior probabilidade de **fazer perguntas pertinentes de esclarecimento primeiro** (reserva de quadras? combinação de jogadores/ranking? acompanhamento de placares? agendamento de ligas? quem são os usuários?) e de revelar **riscos mais profundos e específicos do domínio** — reservas duplicadas / concorrência nas reservas de quadras, justiça do ranking, sincronização de placares em tempo real, privacidade da geolocalização, tratamento de ausências e cancelamentos. Esses são exatamente os riscos que comprometem um projeto silenciosamente.

> **A relação com o custo:** o plano premium custa mais tokens inicialmente. Mas um plano superficial não é barato — é um **custo adiado.** Cada risco que o modelo básico *não* sinalizou se torna retrabalho, uma reescrita ou um bug pelo qual você paga na execução — mais *tentativas* para chegar a algo que realmente possa construir. Em trabalhos abertos de alto impacto, pagar mais por um *pensamento mais profundo* costuma ser a escolha econômica — o inverso da Parte 1, em que pagar mais não trouxe nenhum benefício.

### Perguntas a responder

1. No plano de qual modelo você realmente confiaria o suficiente para começar a construir — e por quê?
2. Os tokens extras gastos pelo modelo premium trouxeram valor real aqui (ao contrário da Parte 1)? O que, especificamente?
3. Esta tarefa não tem uma "resposta certa". Como você decidiu qual saída era *melhor*? O que fez a diferença?

---

## Parte 3 — Compare os resultados e decida

Reúna suas medições em uma tabela:

| Tarefa | Básico: resultado | Básico: tokens | Premium: resultado | Premium: tokens | Qual modelo você deve usar? |
|------|---------------|--------------|------------------|-----------------|-----------------------------|
| Parte 1 (fácil, verificável) | correto? | ? | correto? | ? | ? |
| Parte 2 (aberta) | avalie a qualidade | ? | avalie a qualidade | ? | ? |

### Perguntas a responder

1. Na tarefa **fácil**, qual modelo ofereceu o melhor *custo-benefício* (resposta correta, menos tokens)?
2. Na tarefa **aberta**, os tokens extras do modelo premium trouxeram algo real — profundidade, perguntas de esclarecimento, riscos que o modelo básico não percebeu?
3. Se você executasse a tarefa **fácil** **10,000 vezes por dia**, qual modelo escolheria e quanto a escolha errada custaria?
4. Como você decidiria, *antes* de executar uma tarefa, se ela é uma tarefa da "Parte 1" (bem definida → básico) ou da "Parte 2" (aberta, exige muito discernimento → premium)?

---

## Parte 4 — Classifique suas próprias tarefas

A habilidade que este desafio desenvolve é a *previsão*: saber de qual nível uma tarefa precisa **antes** de gastar qualquer coisa.

1. Anote **duas tarefas reais** do seu próprio trabalho — uma que você acha que um modelo básico consegue realizar e outra que você acha que precisa de um modelo premium.
2. Para cada uma, preveja o nível e **por quê** (Ela é bem definida ou precisa de raciocínio em várias etapas / discernimento?).
3. Execute cada tarefa em **ambos** os níveis e verifique sua previsão. Você acertou? Anote quaisquer surpresas.

| Sua tarefa | Nível previsto | Melhor nível observado | Sua previsão estava certa? |
|---|---|---|---|
| 1. | | | |
| 2. | | | |

---

## Opcional — Restrições de saída

Tokens de saída geralmente custam mais que tokens de entrada, e restringir o que um modelo *produz* é uma alavanca que você controla em **todos** os modelos.

Escolha uma tarefa em que o modelo seja **detalhado por padrão** — por exemplo, pedir uma pequena função:

```
Escreva uma função Python que verifique se uma string é um palíndromo.
```

Execute-a no modelo básico e, em seguida, execute-a novamente com uma restrição de saída adicionada:

```
Escreva uma função Python que verifique se uma string é um palíndromo.
Retorne apenas o código. Sem explicação, sem blocos delimitados de Markdown.
```

Registre a diferença de tokens. Restringir a saída — "apenas código", "apenas a resposta", "explique em menos de 50 palavras", um schema JSON — reduz o custo mantendo o resultado correto.

> Observação: as restrições reduzem os tokens de **saída**. Elas ajudam mais quando o modelo, sem elas, encheria a resposta de explicações. Elas **não** transformam uma resposta superficial em uma boa resposta (veja a Parte 2) e têm pouco efeito quando a saída já é concisa ou quando os tokens ocultos de "pensamento" de um modelo de raciocínio predominam.

## Critérios de sucesso

Para concluir este desafio com sucesso, você deve ser capaz de:

- Executar o mesmo prompt em um modelo básico e em um modelo premium para ambas as tarefas
- Registrar o resultado (correto/incorreto ou nota de qualidade) e o uso de tokens das quatro execuções
- Mostrar que, na tarefa fácil, o modelo básico acertou **e** usou menos tokens
- Na tarefa aberta de planejamento, avaliar a *qualidade* de cada modelo segundo os critérios (perguntas de esclarecimento, profundidade dos 5 principais riscos, especificidade, confiança para começar) e explicar a partir de qual plano você construiria
- Classificar duas tarefas reais do seu próprio trabalho por nível e verificar sua previsão
- (Opcional) Demonstrar uma redução de tokens adicionando uma restrição de saída a uma tarefa com resposta detalhada

## Recursos de aprendizagem

- [Guia de seleção de modelos do GitHub Copilot](https://docs.github.com/en/copilot)
- [Engenharia de prompts: técnicas de formatação de saída](https://www.promptingguide.ai/)
- [Cobrança baseada em uso do GitHub Copilot](https://docs.github.com/en/copilot/concepts/billing/usage-based-billing-for-organizations-and-enterprises)

## Dicas

- Custo = tarifa por token × tokens × **tentativas**. Uma resposta *errada* cujo erro você precisa investigar é a opção mais cara.
- O modelo básico é ótimo para trabalhos bem definidos e com pouca ambiguidade — e é um desperdício *evitá-lo* nesses casos.
- O modelo premium justifica seu multiplicador em tarefas que precisam de raciocínio real, nas quais uma primeira resposta errada custa caro.
- Restrições de saída reduzem o custo em *qualquer* modelo — peça apenas a resposta quando não precisar de explicações.
- O melhor modelo não é o mais inteligente — é aquele que retorna uma resposta *correta* pelo menor custo total.

## Perguntas para reflexão

1. Descreva uma tarefa real do seu próprio trabalho que seja uma tarefa da "Parte 1". Qual modelo você usaria e por quê?
2. Descreva uma tarefa real da "Parte 2" — aberta, que exige muito discernimento. Como você justificaria o multiplicador premium para sua equipe?
3. Como você poderia combinar modelos básicos e premium em um único fluxo de trabalho para minimizar o custo total (por exemplo, o modelo básico cria rascunhos e o premium revisa)?
