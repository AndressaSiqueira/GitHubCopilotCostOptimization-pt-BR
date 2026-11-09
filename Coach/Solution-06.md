# Desafio 06 - Competição de Token Golf - Guia do instrutor

[< Solução anterior](./Solution-05.md) - **[Início](./README.md)**

## Notas e orientações

Token Golf é o desafio final em que as equipes aplicam competitivamente todas as técnicas de otimização. Ele é tanto uma validação do aprendizado quanto uma atividade motivadora em equipe.

### Preparação prévia do instrutor (CRÍTICA)

**Você deve concluir a tarefa do Token Golf antes do hack:**

1. Crie a aplicação de painel meteorológico descrita no Desafio 06 do aluno (somente frontend, sem backend, busca por cidade com temperatura/condição/umidade/velocidade do vento, últimas cinco cidades pesquisadas persistidas no local storage)
2. Use as técnicas de otimização dos Desafios 1–5
3. Registre seu consumo total de créditos — isso se torna o "par"
4. Documente sua abordagem: sequência de prompts, escolhas de modelos e técnicas utilizadas
5. Prepare-se para compartilhar sua "pontuação par" no início do Desafio 06

**Definição do par:**

Sua "pontuação par" deve representar uma solução bem otimizada — não perfeita, mas competente. Busque:
- Instruções globais com escopo adequadamente definido (Desafio 01)
- Seleção eficiente de modelos (Desafio 02)
- Boa higiene de sessões (Desafio 03)
- Compactação proativa (Desafio 04)
- Abordagem de especificação primeiro (Desafio 05)

Pontuações par típicas para uma tarefa de complexidade moderada: 15–25 créditos (versus 60–100 sem otimização).

### Conceitos principais a explicar

**Requisitos da ficha de pontuação:**

As equipes devem documentar sua abordagem completa, não apenas os créditos finais. Isso evita vitórias por "sorte" e garante a transferência do aprendizado. Elementos obrigatórios da ficha de pontuação:

- Total de créditos consumidos (do painel Output do VS Code)
- Sequência de prompts (quais prompts, em qual ordem)
- Modelos selecionados para cada subtarefa (por exemplo, Haiku para boilerplate, Sonnet para lógica complexa)
- Técnicas dos desafios anteriores aplicadas:
  - Qual estratégia de definição de escopo das instruções (Desafio 01)
  - Restrições de saída utilizadas (Desafio 02)
  - Ferramentas removidas (Desafio 03)
  - Pontos de compactação (Desafio 04)
  - Abordagem de especificação primeiro (Desafio 05)
- Quaisquer técnicas ou estratégias próprias

**O que conta para a pontuação:**

- Todas as interações com o GitHub Copilot: conclusões inline, chat, edições e consultas ao workspace
- Custos de tokens visíveis no painel Output do VS Code
- Do início da tarefa até o cumprimento dos critérios de aceitação (testes passando, documentação existente, padrões de qualidade atendidos)

**O que não conta:**

- Digitação manual (custo zero)
- Linters/verificadores de tipos/testes executados localmente (custo zero)
- Tempo gasto (não é medido, apenas créditos)

### Orientações para o desenho da tarefa

Todas as equipes criam o mesmo painel meteorológico, uma aplicação somente frontend, sem backend nem base de código inicial. Ela foi projetada para ser:
- Concluída em 45–60 minutos por um desenvolvedor experiente
- Avaliada pela completude em relação aos requisitos abaixo, além de uma captura de tela e do uso de créditos, em vez de passar em testes previamente escritos
- Aberta a várias abordagens de solução (fonte de dados meteorológicos, estilização, estrutura de componentes, estratégia de prompts e escolha de modelo)
- Complexa o suficiente para que as técnicas de otimização façam diferença (gerenciamento de estado, dados externos e persistência)

**Requisitos da tarefa:**

```markdown
# Tarefa do Token Golf: crie um painel meteorológico

## Requisitos funcionais
- Permita que o usuário pesquise uma cidade e veja suas informações meteorológicas
- Exiba o nome da cidade, a temperatura, a condição meteorológica, a umidade e a velocidade do vento
- Mostre as últimas cinco cidades pesquisadas pelo usuário
- Persista as pesquisas recentes usando local storage (sem backend)

## Critérios de aceitação
- Somente frontend, sem backend
- A pesquisa de uma cidade exibe todos os campos meteorológicos obrigatórios
- As pesquisas recentes (últimas cinco) persistem após atualizar a página
- O código passa no linting e na verificação de tipos
- Captura de tela do painel funcionando e uso final de créditos enviados
```

### Opções de formato da competição

**Opção 1: todas as equipes com a mesma tarefa (padrão)**
- Todos implementam a mesma funcionalidade
- Comparação direta dos custos em créditos
- Mais simples de avaliar

**Opção 2: as equipes escolhem a tarefa (avançado)**
- Forneça 2–3 tarefas de complexidade semelhante
- As equipes escolhem qual implementar
- Compensa diferenças de habilidade/interesse

**Opção 3: classificação ao vivo (alta energia)**
- As equipes enviam as pontuações conforme concluem
- Exiba na tela a classificação atualizada
- Cria um clima competitivo

### Obstáculos comuns

**As equipes não sabem por onde começar:**

Dica: aplique o ciclo pesquisar → planejar → implementar:
1. Pesquisar: leia os requisitos, escolha uma fonte de dados meteorológicos e entenda os critérios de aceitação
2. Planejar: defina os tipos e a estrutura de componentes, estabeleça uma especificação
3. Implementar: use o GitHub Copilot para programar conforme a especificação

**As equipes otimizam a velocidade, não o custo:**

Lembre: isto é Token Golf, não golfe de velocidade. Gastar 2 minutos extras para escrever os testes primeiro pode economizar 20 créditos em tentativa e erro.

**As equipes chegam a becos sem saída e queimam créditos na recuperação:**

Incentive `/clear` quando estiverem travadas — recomece em vez de gastar créditos tentando sair de uma abordagem errada.

### Tempo esperado

60 minutos no total:
- 5 minutos: explicação da tarefa e das regras, anúncio da "pontuação par"
- 45 minutos: implementação e medição pelas equipes
- 10 minutos: discussão final e estratégias vencedoras

### Critérios de avaliação

**Principal:** a solução mais completa (todos os requisitos funcionais atendidos) pelo menor custo em créditos — uma UI básica que tecnicamente atende aos critérios não deve superar uma refinada com custo semelhante

**Desempates (na ordem):**
1. Tempo de conclusão (envio mais cedo)
2. Qualidade do código (avaliação subjetiva do instrutor)

**Desclassificações:**
- Requisitos funcionais ausentes (busca por cidade, todos os campos obrigatórios, últimas cinco pesquisas, persistência no local storage)
- Nenhuma captura de tela ou informação de uso de créditos enviada
- Ficha de pontuação não documentada (não é possível verificar as técnicas utilizadas)

### Pontos para a discussão final

Depois de anunciar o vencedor, discuta:

**Estratégias vencedoras:**
- Quais técnicas dos Desafios 1–5 o vencedor aplicou?
- Onde as outras equipes gastaram créditos desnecessários?
- O que você faria de forma diferente na próxima vez?

**Lições principais:**
- "Escreva o teste primeiro" é tanto uma boa prática de TDD quanto uma boa prática de economia de tokens
- Modelos mais baratos com restrições rígidas frequentemente superam modelos caros com saída prolixa
- Os maiores desperdícios de créditos são os ciclos de recuperação — evite-os com especificações antecipadas
- A higiene do cache importa — a deterioração do contexto força recuperações caras

### Variações para eventos futuros

**Sistema de compensação:**
- Dê às equipes menos experientes um bônus de créditos (por exemplo, +10 créditos)
- Equilibra a competição sem deixar de recompensar a otimização

**Formato de revezamento:**
- As equipes implementam funcionalidades diferentes em sequência
- Cada equipe herda a base de código da equipe anterior
- Testa estratégias de gerenciamento do cache e de transferência de contexto

**Restrições do mundo real:**
- Limite a seleção de modelos (por exemplo, somente Haiku — força eficiência máxima)
- Introduza alterações de requisitos no meio da tarefa (testa o tratamento da invalidação do cache)

### Pontuações par de referência

Pontuações par típicas para tarefas bem projetadas:
- Tarefa simples (15–20 minutos): 10–15 créditos
- Tarefa moderada (30–45 minutos): 15–25 créditos
- Tarefa complexa (60 minutos): 25–40 créditos

Se todas as pontuações dos alunos estiverem dentro de 10% do par, a tarefa está bem calibrada. Se a dispersão for grande (algumas com 2x o par, outras abaixo do par), a tarefa pode ter caminhos-armadilha que queimam créditos desnecessariamente.

### Acompanhamento após o evento

Incentive as equipes a:
- Documentar as "diretrizes de Token Golf" da organização com base no aprendizado
- Compartilhar internamente as estratégias vencedoras
- Aplicar estas técnicas ao trabalho real (medir antes/depois em tarefas de produção)
- Acompanhar a redução do gasto de créditos de toda a equipe nos próximos 30 dias
