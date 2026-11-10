# Desafio 06 - Golfe de tokens: entregue um painel meteorológico com eficiência

[< Desafio anterior](./Challenge-05.md) - **[Início](../README.md)**

## O que você vai aprender

Neste desafio final, você vai combinar o que praticou: especificação clara, seleção de modelos, contexto focado, configuração de ferramentas e validação.

As equipes construirão a mesma aplicação e compararão o consumo necessário para entregar uma solução correta.

O nome “golfe de tokens” faz referência a concluir uma tarefa com menos recursos. A competição, porém, deve usar uma **métrica principal definida antes do início**, sem confundir tokens, créditos e tamanho do código.

> **Ideia central:** uma aplicação incompleta com consumo baixo não vence uma aplicação que atende aos critérios. Primeiro, valide a entrega; depois, compare eficiência.

## Antes de começar

Combine com o instrutor:

| Item | Regra a definir |
|---|---|
| Métrica principal | Preferencialmente créditos atribuíveis à execução; tokens somente se houver uma medição comparável |
| Fonte da medição | Tela, relatório ou log disponível para todas as equipes |
| Início e término | Do primeiro uso de IA para planejar a solução até a última correção e validação |
| Limite de tempo e consumo | Mesmo limite para todas as equipes |
| Modelos e ferramentas | Opções permitidas pela organização |
| Dependências e templates | Mesmas regras de acesso para todas as equipes |
| Desempate | Menor tempo total após atender aos mesmos critérios |
| Referência do instrutor | Valor “par”, se houver, medido sob as mesmas regras |

Se não houver métricas comparáveis, faça o desafio como uma demonstração de eficiência, sem declarar um vencedor financeiro.

Use uma pasta vazia para sua aplicação. Não há base de código inicial. Não reutilize uma solução pronta para evitar a construção, mas use bibliotecas e ferramentas permitidas pelas regras.

## A aplicação: painel de condições meteorológicas

O usuário deverá pesquisar uma cidade, consultar suas condições atuais e acessar as cinco cidades mais recentes do histórico.

### Requisitos funcionais

| Área | Comportamento obrigatório |
|---|---|
| Pesquisa | Aceitar o nome de uma cidade e iniciar uma consulta |
| Identificação | Exibir cidade e país ou região, para reduzir ambiguidades |
| Condições atuais | Exibir temperatura, condição do tempo, umidade e velocidade do vento |
| Unidades | Identificar temperatura em °C, umidade em % e vento em km/h |
| Histórico | Mostrar até 5 cidades distintas consultadas com sucesso, da mais recente para a mais antiga |
| Repetição | Uma nova consulta da mesma cidade a move para o início, sem duplicá-la |
| Persistência | Preservar o histórico após atualizar a página, usando `localStorage` |
| Reconsulta | Permitir selecionar uma cidade do histórico e atualizar suas condições |
| Estados da interface | Exibir carregamento, cidade não encontrada e falha de consulta |

### Restrições técnicas

- A aplicação deve funcionar no navegador, **sem backend próprio**.
- A stack de frontend, a estilização e a estrutura de componentes ficam a critério da equipe.
- Use uma fonte de dados meteorológicos reais que permita chamadas pelo navegador.
- Se a busca retornar cidades homônimas, permita selecionar a localização ou apresente claramente qual foi escolhida.
- Use uma identidade estável, como identificador do provedor ou coordenadas, para distinguir cidades no histórico.
- Consultas sem resultado ou com falha não devem acrescentar itens ao histórico.
- Não é necessário persistir os dados meteorológicos: ao selecionar uma cidade salva, consulte as condições novamente.

> **Credenciais:** não coloque segredos no código do frontend, no `localStorage` ou no repositório. Variáveis de ambiente incorporadas ao frontend também ficam expostas no navegador. Prefira um serviço que não exija segredo; se usar uma chave pública de cliente, confira as permissões e restrições previstas pelo provedor.

### Fora do escopo

Não implemente autenticação, previsão de vários dias, mapas, geolocalização automática, banco de dados ou deploy em nuvem. Essas funcionalidades não contam pontos e podem aumentar o consumo sem melhorar a entrega obrigatória.

---

## Parte 1 - Planeje uma entrega pequena e verificável

Antes de pedir código, registre uma especificação curta com:

1. Stack escolhida e comando para iniciar a aplicação.
2. Fonte dos dados, processo de busca da cidade e campos que serão exibidos.
3. Regras de histórico e persistência.
4. Estados de carregamento e erro.
5. Casos de validação da Parte 3.

Você pode escrever a especificação manualmente ou com o Copilot. Se usar IA, inclua esse consumo na pontuação.

Um prompt inicial possível:

```text
Vamos construir um painel meteorológico frontend, sem backend.
Use os requisitos e critérios de aceitação anexados.

Antes de implementar, proponha uma solução pequena e confirme a fonte
de dados, as unidades e a persistência das 5 cidades distintas mais recentes.
Não acrescente funcionalidades fora do escopo.
Depois, implemente em etapas verificáveis, usando as ferramentas necessárias
e evitando alterações sem relação com a tarefa.
```

Anexe sua especificação completa. O prompt é um ponto de partida, não substitui os requisitos.

## Parte 2 - Implemente com pontos de verificação

Uma sequência recomendada é:

1. Criar a interface mínima e a pesquisa.
2. Integrar os dados reais e conferir as unidades.
3. Implementar histórico, reconsulta e persistência.
4. Tratar carregamento e erros.
5. Executar os casos de aceitação e corrigir as falhas.

Use as técnicas que fizerem sentido:

- Selecionar o modelo conforme a subtarefa.
- Anexar apenas os arquivos relevantes.
- Manter instruções curtas e ferramentas suficientes.
- Pedir respostas concisas quando a explicação não for necessária.
- Resumir ou iniciar outra conversa em um ponto de parada verificado.
- Usar testes automatizados para as regras de histórico e validação, quando forem úteis.

Não troque de modelo ou de conversa apenas por hábito. Cada mudança pode exigir restabelecer contexto. Registre todas as sessões e tentativas, inclusive abordagens abandonadas.

Mocks podem ajudar nos testes, mas não substituem a demonstração final com dados reais.

---

## Parte 3 - Valide antes de contar a pontuação

Execute os mesmos casos em todas as equipes:

| Caso | Evidência esperada |
|---|---|
| Pesquisar uma cidade válida | Nome, localização, temperatura, condição, umidade e vento visíveis, com unidades |
| Pesquisar uma cidade inexistente | Mensagem clara, sem acrescentar item ao histórico |
| Enviar uma pesquisa vazia | Orientação para informar uma cidade, sem consulta desnecessária |
| Consultar 6 cidades distintas com sucesso | Apenas as 5 mais recentes no histórico, na ordem correta |
| Consultar novamente uma das 5 cidades | Cidade movida para o início, sem duplicação |
| Atualizar a página | Histórico preservado |
| Selecionar uma cidade do histórico | Nova consulta e atualização das condições atuais |
| Simular indisponibilidade da rede | Erro visível, fim do carregamento e possibilidade de tentar novamente |

Verifique também que respostas atrasadas não substituem a cidade mais recentemente selecionada e que campos ausentes não são exibidos como números ou condições inventados.

Para simular falhas, você pode usar os recursos de rede do navegador. Na demonstração de sucesso, restaure a conexão.

Não há valores meteorológicos fixos no gabarito: eles mudam com o horário e a fonte. Compare a localização, as unidades e os campos retornados pelo serviço.

## Parte 4 - Registre o consumo completo

Anote o consumo por etapa, quando a interface permitir:

| Etapa | Modelo(s) | Créditos | Tokens e tipo, se disponíveis | Correções e decisões |
|---|---|---|---|---|
| Planejamento | | | | |
| Interface e pesquisa | | | | |
| Integração meteorológica | | | | |
| Histórico e persistência | | | | |
| Validação e correções | | | | |
| **Total** | | | | |

- Some todas as interações de IA usadas para concluir a tarefa.
- Inclua prompts de revisão, resumos, testes gerados e tentativas descartadas.
- Se usar valores acumulados, calcule a diferença final menos inicial; não some os acumulados.
- Registre separadamente tempo total e eventuais custos do serviço meteorológico.
- Se uma métrica não estiver disponível, escreva **“não disponível”**, sem inferi-la pela quantidade de texto.
- A ocupação da janela de contexto não é o total de tokens consumidos.

### Como determinar o resultado

1. Confirme que a equipe passou em todos os casos obrigatórios.
2. Compare somente equipes com medição válida sob as mesmas regras.
3. Ordene pela métrica principal acordada, do menor para o maior consumo.
4. Aplique o desempate previamente definido.

Se houver um “par” do instrutor, informe a diferença na mesma unidade. Ficar acima do par não invalida a entrega; serve para discutir decisões e oportunidades de melhoria.

Premiações adicionais, como clareza de código ou experiência de uso, podem existir, mas precisam ter critérios próprios definidos antes da competição. Não use “ROI de tokens” como uma pontuação sem fórmula ou evidência.

## Entrega final

Apresente:

- A aplicação funcionando e os comandos para executá-la.
- Uma captura de tela de uma consulta bem-sucedida e do histórico.
- O registro dos testes ou a lista de verificação preenchida.
- A medição final de consumo, com fonte, unidade e período.
- Uma explicação curta das duas decisões que mais contribuíram para a eficiência.

Não exponha dados da conta, credenciais ou informações de outras pessoas nas capturas de uso.

## Critérios de sucesso

- [ ] Entreguei uma aplicação frontend funcional com dados meteorológicos reais.
- [ ] Exibi todos os campos obrigatórios e suas unidades.
- [ ] Mantive até 5 cidades distintas, com ordem, reconsulta e persistência corretas.
- [ ] Tratei entrada vazia, cidade inexistente e falha de rede.
- [ ] Executei os mesmos casos de aceitação usados pelas demais equipes.
- [ ] Registrei todo o consumo atribuível à tarefa, incluindo planejamento e correções.
- [ ] Apresentei evidências de funcionamento e expliquei minhas escolhas de otimização.

## Perguntas para reflexão

1. Qual decisão reduziu consumo sem reduzir a qualidade?
2. Qual tentativa gerou mais retrabalho e por quê?
3. O que você faria diferente antes de escrever a primeira linha de código?
4. Qual técnica dos desafios anteriores vale incorporar ao seu fluxo diário?

## Recursos de aprendizagem

- [Boas práticas do GitHub Copilot](https://docs.github.com/en/copilot/using-github-copilot/best-practices-for-using-github-copilot)
- [Adição de contexto ao chat](https://code.visualstudio.com/docs/chat/copilot-chat-context)
- [Armazenamento local no navegador](https://developer.mozilla.org/pt-BR/docs/Web/API/Window/localStorage)
