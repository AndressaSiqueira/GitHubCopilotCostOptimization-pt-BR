# Desafio 03 - Seleção de modelos e restrições de saída - Guia do instrutor

[< Solução anterior](./Solution-02.md) - **[Início](./README.md)** - [Próxima solução >](./Solution-04.md)

## Notas e orientações

Este desafio ensina uma ideia duradoura: **custo total = tarifa por token × tokens × tentativas**, portanto
*um custo menor por requisição não significa um custo menor por resultado.* Os alunos comprovam isso executando o mesmo
prompt em um **modelo base** e em um **modelo premium** para uma tarefa **fácil** e uma tarefa **difícil**,
medindo o resultado e os tokens. O segredo está no contraste: vencedores opostos nas duas tarefas.

> **Terminologia:** usamos **modelo base** (incluído, sem multiplicador de requisições premium — por exemplo,
> GPT-4.1, GPT-4o) e **modelo premium** (modelo de fronteira/raciocínio cobrado como uma requisição premium
> com um multiplicador — por exemplo, GPT-5, Claude Sonnet, o-series). Evite "barato/caro" com
> os alunos — é impreciso, e o ponto central é que "barato" pode ser a escolha mais custosa.

### A dinâmica central

| | Tarefa fácil (ordenação de versões) | Tarefa difícil (o lava-rápido) |
|---|---|---|
| Modelo base | ✅ correto, **menos tokens** | ❌ errado com confiança ("vá a pé"), parece de baixo custo (uma armadilha) |
| Modelo premium | ✅ correto, mais tokens | ✅ correto ("vá de carro"), mais tokens |
| **Lição** | Use o modelo base → economize créditos | A resposta errada do modelo base é a opção mais custosa → pague pela capacidade |

### Gabarito de referência (medido)

Medido pela API de inferência do GitHub Models, em uma única tentativa, **n=4 por célula** (consulte
[`Solutions/Challenge-03-ModelSelection-Solutions/`](./Solutions/Challenge-03-ModelSelection-Solutions/)). Os números exatos variam conforme o modelo/versão; o
**padrão** é o que importa.

| Modelo | Fácil: taxa de acerto | Fácil: média de tokens | Difícil: taxa de acerto | Difícil: média de tokens |
|---|---|---|---|---|
| `gpt-4.1` (base) | **4/4 (100%)** | ~106 | **0/4 (0%)** — responde "vá a pé" | ~166 |
| `gpt-5` (premium) | **4/4 (100%)** | ~293 | **4/4 (100%)** — responde "vá de carro" | ~1000 |

Conclusões a destacar:
- Tarefa fácil: resposta correta idêntica, mas o modelo base usou **~2,8× menos tokens.**
- Tarefa difícil: o modelo base errou **todas** as vezes (recomenda ir a pé, deixando o carro em
  casa). Nem sequer foi mais barato errar aqui — e nenhuma quantidade de novas tentativas corrige de forma confiável uma
  falha causada pelo limite de capacidade de raciocínio. O modelo premium foi a única opção correta.

### Por que estas tarefas específicas

- **Ordenação de versões (fácil):** real, prática, e ambos os níveis acertam — portanto o único
  diferencial é o custo em tokens. Demonstração clara de que "o modelo base vence".
- **O lava-rápido (difícil):** uma armadilha de raciocínio pragmático. A isca dos "40 metros" faz os modelos base
  se fixarem na distância ("vá a pé, é mais ecológico") e ignorarem que *o carro precisa estar presente para ser
  lavado.* A resposta certa (**vá de carro**) é óbvia para qualquer pessoa em um segundo — assim os alunos podem
  *ver* que o modelo base está errado sem precisar confiar em nós. Crucialmente, isso acompanha a **capacidade**, portanto
  os resultados melhoram de forma monotônica conforme a força do modelo.
- **Rejeitadas — tarefas de contagem de letras / "pegadinhas"** (por exemplo, "conte os 'l'"): elas são
  **artefatos da tokenização, não testes de raciocínio.** Nós as medimos, e os resultados **não** acompanham
  o preço — um modelo base pode acertar enquanto um premium erra (observamos Claude Haiku acertar
  e Claude Opus errar na mesma contagem de letras). Isso ensinaria o *oposto* da
  lição. Não use contagens de letras, comparações de decimais ou armadilhas do tipo "strawberry".
- **Rejeitada — "armadilha do algoritmo guloso" no problema do troco:** modelos pequenos modernos acertam; ela já não diferencia os modelos.

### A regra de "não tentar novamente" e o raciocínio sobre o custo de novas tentativas (Parte 2)

Diga explicitamente aos alunos: quando o modelo base falhar na Parte 2, **não o oriente nem repita a tentativa** para a
medição. Depois, peça que raciocinem sobre novas tentativas:
- *Quantas tentativas do modelo base custariam mais do que uma chamada premium?* (Use as contagens de tokens ou
  os multiplicadores da sua organização.)
- *Alguma quantidade de tentativas chegaria à resposta certa de forma confiável aqui?* (Não — é um limite de
  capacidade. Esta é a percepção central: insistir no modelo de menor custo é gastar mais dinheiro
  em uma escolha ruim, em tarefas que ele não consegue resolver por raciocínio.)

### Parte 4 — classifique suas próprias tarefas

É aqui que a habilidade se torna transferível. Os alunos escrevem duas tarefas reais do seu trabalho,
preveem o nível, executam ambos os modelos e verificam. Incentive-os a explicar *por que* uma tarefa pertence ao nível base ou
premium (bem definida/baixa ambiguidade versus raciocínio em várias etapas/julgamento) — essa regra
prática de previsão é a verdadeira entrega.

## Como os alunos executam

Sem base de código. Os alunos usam o **seletor de modelos do Copilot Chat no VS Code** para alternar entre um
modelo de nível base e um premium, colam os dois prompts de
[`Student/Resources/Challenge-03-ModelSelection/prompts.md`](../Student/Resources/Challenge-03-ModelSelection/prompts.md) e leem os tokens no painel
Output / visualização de uso. Eles preenchem [`measurements-template.md`](../Student/Resources/Challenge-03-ModelSelection/measurements-template.md).

> Organizações disponibilizam modelos diferentes. Oriente os alunos a escolher *qualquer* par de nível base e premium
> oferecido pelo seletor — o padrão se mantém. Se a organização disponibilizar apenas um nível, use o
> gabarito do instrutor acima como demonstração ou execute o harness ao vivo.

> **Ressalva sobre a visibilidade dos tokens:** dependendo da versão/organização do Copilot, o painel Output pode não mostrar uma
> contagem clara de tokens por requisição. Nesse caso, os alunos ainda podem observar o *padrão* (o modelo premium
> gera muito mais texto). Para contagens exatas, o harness do instrutor (ou o playground do GitHub Models)
> informa `usage.total_tokens` diretamente. Consulte [`TODO.md`](./Solutions/Challenge-03-ModelSelection-Solutions/TODO.md) — o alinhamento das instruções de medição de tokens
> em todo o hack (o Desafio 00 prepara isso) está sendo acompanhado ali.

## Tempo esperado

~45 minutos:
- 10 minutos: Parte 1 (fácil) em ambos os modelos
- 10 minutos: Parte 2 (difícil) em ambos os modelos + raciocínio sobre o custo de novas tentativas
- 10 minutos: Parte 3, comparação + discussão
- 10 minutos: Parte 4, classificação das próprias tarefas
- 5 minutos: execução opcional com restrição de saída

## Validação dos critérios de sucesso

Os alunos devem produzir uma tabela preenchida da Parte 3 mostrando **vencedores opostos**: o modelo base vence
a tarefa fácil em tokens; o premium é a única opção correta na tarefa difícil. Eles devem
explicar a matemática das novas tentativas (tentativas até o ponto de equilíbrio) e a questão do limite de capacidade, além de
classificar duas tarefas próprias por nível. Bônus: uma queda mensurável de tokens decorrente de uma restrição de
saída em uma tarefa prolixa.

## Obstáculos comuns

- **O aluno repete o modelo base até ele acertar.** Interrompa-o — isso contraria a lição.
  Redirecione para o raciocínio sobre o custo de novas tentativas.
- **O modelo base responde "vá de carro" uma vez por acaso.** É estocástico; peça que o execute 2–3×. Ele
  recomenda ir a pé na grande maioria das vezes. (Se o modelo base de um aluno acertar de forma confiável,
  seu modelo "base" pode ser bastante forte — peça que use o menor modelo
  oferecido pelo seletor.)
- **A organização disponibiliza apenas um nível de modelos.** Recorra ao gabarito ou use o harness do instrutor.
- **As contagens de tokens não estão visíveis.** O modelo premium ainda produz visivelmente muito mais texto — registre o
  padrão. Para números exatos, use o harness. (Consulte a ressalva sobre a visibilidade dos tokens acima.)
- **As contagens de tokens do modelo premium variam muito.** Modelos de raciocínio têm uso variável de tokens ocultos;
  enfatize a proporção/o padrão em vez dos números absolutos.

## Dicas para compartilhar

- "Base" versus "premium" diz respeito ao custo *total*, não ao preço por requisição. Uma resposta errada que você precisa
  refazer é o resultado mais custoso.
- Adeque o modelo à tarefa: base para trabalho bem definido/de baixa ambiguidade, premium para qualquer coisa
  que exija raciocínio ou julgamento real.
- Restrições de saída reduzem o custo em qualquer modelo — mas não fazem um modelo errado acertar.
- A distância até o lava-rápido é uma isca. A tarefa testa se o modelo raciocina sobre o *objetivo*.

## Dados de referência e reprodução

Consulte [`Solutions/Challenge-03-ModelSelection-Solutions/`](./Solutions/Challenge-03-ModelSelection-Solutions/):
- [`harness.py`](./Solutions/Challenge-03-ModelSelection-Solutions/harness.py) — harness de medição (conta acertos/falhas + tokens, com espera progressiva em caso de limite de requisições)
- [`results.md`](./Solutions/Challenge-03-ModelSelection-Solutions/results.md) — as tabelas medidas acima
- [`TODO.md`](./Solutions/Challenge-03-ModelSelection-Solutions/TODO.md) — pendências dos autores (alinhamento da medição de tokens, escopo avançado/do modo Auto)
