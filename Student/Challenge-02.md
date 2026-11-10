# Desafio 02 - Engenharia de contexto: forneça ao Copilot o que ele precisa

[< Desafio anterior](./Challenge-01.md) - **[Início](../README.md)** - [Próximo desafio >](./Challenge-03.md)

## O que você vai aprender

Uma boa resposta não depende apenas do prompt. Ela também depende do **contexto**: as instruções, os arquivos e o histórico que o Copilot recebe para realizar uma tarefa.

Neste desafio, você vai trabalhar com o CityScout NYC, uma aplicação de exemplo com dados e rotas de eventos, restaurantes e bairros. O projeto contém um arquivo de instruções globais propositalmente sobrecarregado.

Sua missão será organizar essas instruções, implementar uma funcionalidade de eventos e comparar duas estratégias de seleção de contexto.

Ao final, você deverá conseguir:

- Diferenciar instruções globais, instruções por caminho e skills.
- Selecionar arquivos relevantes sem omitir informações necessárias.
- Implementar uma tarefa com escopo bem definido.
- Medir o uso da janela de contexto e avaliar a qualidade da resposta.

> **Ideia central:** otimizar contexto não é simplesmente enviar menos informações. É fornecer as informações necessárias para obter uma resposta correta, com menos conteúdo desnecessário.

## Antes de começar

1. Localize o projeto em [Resources/Challenge-02-NYCApp](./Resources/Challenge-02-NYCApp).
2. Abra **essa pasta como raiz de uma janela do VS Code**. Isso facilita a descoberta das personalizações na pasta `.github` e mantém os padrões de caminho deste desafio relativos à aplicação.
3. Tenha o GitHub Copilot Chat disponível e selecione um modelo que você possa manter durante a comparação.
4. Guarde uma cópia do arquivo original `.github/copilot-instructions.md`, fora da pasta aberta no VS Code, para comparar seu tamanho ao final.

Os caminhos nas próximas etapas são relativos à raiz do CityScout NYC.

> O material inicial contém arquivos de exemplo, mas não inclui um projeto executável completo com manifesto de dependências e servidor. Não é necessário criar uma nova aplicação para este desafio: a validação pode ser feita pela revisão do código e dos casos de teste. Se você já tiver um ambiente executável preparado pelo instrutor, use-o também.

## Entenda os três tipos de contexto

| Recurso | Para que serve | Exemplo neste desafio |
|---|---|---|
| Instruções globais | Orientações aplicáveis ao projeto como um todo | Convenções gerais em `.github/copilot-instructions.md` |
| Instruções por caminho | Regras aplicáveis a determinados arquivos, selecionadas por `applyTo` | Regras de eventos para `src/routes/events.ts` |
| Skill | Procedimento reutilizável carregado sob demanda | Passos para implementar um endpoint de eventos gratuitos |

Arquivos anexados ao chat complementam esse contexto com o código necessário para a tarefa.

> Instruções globais podem acrescentar contexto às solicitações em que são aplicadas. Instruções por caminho restringem esse uso aos arquivos correspondentes. Skills podem ser descobertas automaticamente ou invocadas pelo usuário; neste exercício, você configurará uma skill para invocação apenas manual.

---

## Parte 1 - Organize as instruções

### Etapa 1 - Audite o arquivo original

Abra `.github/copilot-instructions.md` e classifique suas orientações:

| Categoria | Pergunta para decidir | Destino sugerido |
|---|---|---|
| Global | Esta regra é útil independentemente do domínio ou arquivo? | Arquivo global |
| API | Esta regra se aplica às rotas da aplicação? | `api.instructions.md` |
| Eventos | Esta regra trata especificamente de eventos? | `events.instructions.md` |
| Outro domínio ou camada | Esta regra trata de restaurantes, bairros, frontend ou testes? | Arquivo com escopo correspondente, se houver arquivos aos quais ela se aplique |
| Redundante ou sem aplicação | Esta regra repete outra ou não corresponde ao projeto atual? | Remover ou consolidar |

Não exclua uma regra importante apenas porque ela não é necessária para eventos. Se ela ainda for válida para outro domínio, preserve-a no escopo adequado.

Observe também os conflitos. Por exemplo, uma orientação genérica de API sugere `{ count, data }`, enquanto a tarefa deste desafio exige `{ count, events }`. A organização deve deixar esse contrato específico explícito, sem instruções contraditórias.

### Etapa 2 - Enxugue o arquivo global

Mantenha em `.github/copilot-instructions.md` apenas orientações curtas, úteis para todo o projeto.

Evite repetir recomendações genéricas sem uma ação clara, como “sempre otimize tudo”. Prefira regras verificáveis e aplicáveis ao código existente.

**Resultado esperado:** um arquivo global menor, sem regras exclusivas de eventos, restaurantes ou bairros.

### Etapa 3 - Crie instruções por caminho

Crie a pasta `.github/instructions/` e, no mínimo, estes arquivos:

```text
.github/
  copilot-instructions.md
  instructions/
    api.instructions.md
    events.instructions.md
```

Cada arquivo deve começar com um cabeçalho YAML que indique seu escopo. Por exemplo:

**`api.instructions.md`:**

```yaml
---
description: "Convenções das rotas HTTP da aplicação CityScout NYC."
applyTo: "src/routes/**/*.ts"
---
```

**`events.instructions.md`:**

```yaml
---
description: "Regras de filtragem, ordenação e resposta das rotas de eventos."
applyTo: "src/routes/events.ts"
---
```

Após o cabeçalho, escreva as instruções correspondentes.

- No arquivo de API, coloque as convenções compartilhadas pelas rotas.
- No arquivo de eventos, coloque as regras de preço, data, ordenação e formato da resposta.
- Se criar instruções para outros domínios, use padrões que correspondam aos arquivos existentes.
- Não use `applyTo: "**"` para regras que só fazem sentido em uma parte do projeto.

> **Verifique a configuração:** criar um arquivo de instruções não basta. Confira se o padrão de `applyTo` corresponde ao caminho que você pretende modificar e, quando a interface permitir, verifique quais instruções foram usadas pelo Copilot.

### Etapa 4 - Registre um procedimento reutilizável em uma skill

Crie `.github/skills/free-events-endpoint/SKILL.md` com este cabeçalho:

```yaml
---
name: free-events-endpoint
description: "Orienta a implementação e a validação de endpoints de eventos gratuitos."
disable-model-invocation: true
---
```

No corpo, descreva um procedimento para:

1. Identificar a rota e a fonte de dados.
2. Confirmar o contrato da resposta e o intervalo de datas.
3. Filtrar os eventos gratuitos dentro do intervalo.
4. Ordenar os resultados por data.
5. Conferir os casos de borda e os arquivos que não devem ser alterados.

Evite copiar todas as instruções de eventos para a skill. As instruções registram **regras**; a skill organiza **como executar o trabalho**.

O campo `disable-model-invocation: true` impede o acionamento automático pelo modelo. Quando for implementar a tarefa, invoque a skill explicitamente no chat, por exemplo com `/free-events-endpoint`, se disponível na sua versão.

---

## Parte 2 - Implemente a rota de eventos gratuitos

### Etapa 1 - Delimite o trabalho

A rota `GET /events/free-this-week` já tem um esqueleto em `src/routes/events.ts`, mas ainda retorna todos os eventos.

Você deverá completar sua lógica usando os dados de `src/data/events.ts`.

| Pode alterar ou criar | Não deve alterar |
|---|---|
| `.github/copilot-instructions.md` | `src/routes/restaurants.ts` |
| `.github/instructions/*.instructions.md` | `src/routes/neighborhoods.ts` |
| `.github/skills/free-events-endpoint/SKILL.md` | Os dados de exemplo, para fazer o resultado “passar” |
| `src/routes/events.ts` | Arquivos de código não relacionados à tarefa |

### Etapa 2 - Use um contexto focado

Inicie uma nova conversa, invoque a skill criada e anexe os arquivos necessários para esta tarefa:

- `src/routes/events.ts`
- `src/data/events.ts`

Confira também a aplicação das instruções de API e de eventos. Use **Adicionar contexto / Add Context**, ou o recurso equivalente da sua versão do Copilot Chat.

Você pode usar este prompt:

```text
Complete a implementação de GET /events/free-this-week em src/routes/events.ts.

Requisitos:
- Incluir somente eventos com price === 0.
- Excluir eventos anteriores a hoje e posteriores ao limite de 7 dias.
- Para esta atividade, comparar datas de calendário em UTC, incluindo hoje
  e a data correspondente a hoje + 7 dias.
- Ordenar os resultados por data crescente.
- Retornar JSON no formato { count, events }, com count igual ao tamanho
  da lista retornada.
- Se não houver resultados, retornar { count: 0, events: [] }.
- Não modificar os dados, as rotas de restaurantes ou as rotas de bairros.

Use os arquivos anexados e siga as instruções aplicáveis ao projeto.
```

> **Por que explicitar as datas?** “Nos próximos 7 dias” pode gerar interpretações diferentes sobre hoje, o último dia e o fuso horário. O contrato acima adota uma convenção explícita para tornar a implementação e a validação consistentes.

### Etapa 3 - Valide o resultado

Revise o código produzido. Não considere a tarefa concluída apenas porque o Copilot informou que terminou.

Nos dados fornecidos, a resposta deve conter:

| Evento | Deve aparecer? | Motivo |
|---|---|---|
| Central Park Yoga | Sim | Gratuito e ocorre em 1 dia |
| Brooklyn Flea Market Walk | Sim | Gratuito e ocorre em 2 dias |
| Rooftop Movie Night | Não | É pago |
| Jazz in Washington Square Park | Não | Ocorre em 10 dias |

Portanto, com os dados originais, o resultado esperado é `count: 2`, com os dois eventos gratuitos em ordem cronológica.

Confira também a lógica para eventos passados, eventos na data-limite e ausência de resultados. Você pode usar casos hipotéticos na revisão ou testes no ambiente preparado, sem alterar permanentemente os dados do exercício.

Por fim, confirme que as rotas de restaurantes e bairros permaneceram inalteradas.

---

## Parte 3 - Compare contexto amplo e arquivos selecionados

Agora você fará um experimento separado da implementação. O objetivo é observar o efeito da seleção de contexto sobre **a mesma pergunta**, mantendo a cobertura da resposta.

### Etapa 1 - Prepare uma comparação justa

- Faça as duas execuções depois de concluir as alterações das partes anteriores.
- Use o mesmo modelo, modo do chat e versão do projeto.
- Inicie uma nova conversa para cada execução, sem histórico anterior.
- Envie exatamente a mesma pergunta nas duas conversas.
- Registre as métricas no mesmo momento: após a resposta final.
- Se houver chamadas de ferramentas ou buscas adicionais, registre isso nas observações.

Assim, a principal diferença entre as execuções será a estratégia de seleção dos arquivos, e não o histórico ou uma mudança no código.

### Etapa 2 - Execute com contexto amplo

Na conversa A, use o recurso de pesquisa no workspace disponível na sua versão, como `#codebase` ou equivalente, e envie:

```text
Quais dados ou funcionalidades esta aplicação oferece?
```

Não selecione manualmente os arquivos de domínio nessa execução. Registre a resposta e as métricas disponíveis.

> Pesquisa no workspace não significa necessariamente enviar todos os arquivos ao modelo. O Copilot pode buscar e selecionar trechos. O experimento deve comparar o contexto efetivamente observado, não presumir que o contexto amplo sempre será maior.

### Etapa 3 - Execute com arquivos selecionados

Na conversa B, anexe os arquivos de rotas e dados de **eventos, restaurantes e bairros** e envie a mesma pergunta:

```text
Quais dados ou funcionalidades esta aplicação oferece?
```

Como a pergunta trata da aplicação inteira, selecionar apenas eventos produziria uma resposta incompleta. Para uma tarefa exclusiva de eventos, como na Parte 2, os dois arquivos desse domínio são um contexto mais adequado.

Mantenha as instruções aplicáveis iguais nas duas execuções e registre quaisquer referências adicionais usadas pelo Copilot.

### Etapa 4 - Registre as medições

Consulte o indicador da janela de contexto ou os detalhes de uso disponíveis na sua versão do Copilot Chat. Anote os valores exibidos, sem estimar medições ausentes.

| Execução | Estratégia | Tokens utilizados | Capacidade da janela | Utilização (%) | Qualidade e observações |
|---|---|---|---|---|---|
| A | Pesquisa ampla no workspace | | | | |
| B | Arquivos relevantes selecionados | | | | |

Se a interface não expuser uma métrica, registre **“não disponível”** e indique qual evidência você conseguiu obter.

Calcule, quando houver dados:

```text
Utilização (%) = tokens utilizados / capacidade da janela × 100
Diferença de tokens = tokens de A − tokens de B
Diferença de utilização = utilização de A − utilização de B
```

Expresse a última diferença em **pontos percentuais**, não em porcentagem de redução.

Por exemplo, se A usar 8.200 de 32.000 tokens e B usar 2.100 de 32.000 tokens:

- A utiliza aproximadamente 25,6% da janela.
- B utiliza aproximadamente 6,6% da janela.
- A diferença é de 6.100 tokens e aproximadamente 19,1 pontos percentuais, calculados antes do arredondamento.

Esses valores são ilustrativos; não são uma meta nem uma previsão do seu resultado.

| Métrica de comparação | Resultado |
|---|---|
| Diferença de tokens utilizados (A − B) | |
| Diferença de utilização em pontos percentuais (A − B) | |
| Ambas as respostas cobrem os três domínios? | |
| Houve informação incorreta, omissão ou busca adicional? | |

> **Contexto não é cobrança:** a ocupação da janela não representa, por si só, o total de tokens processados em todas as chamadas nem os créditos consumidos. Se sua interface disponibilizar dados de consumo, registre-os separadamente. Não converta redução de contexto diretamente em economia financeira.

### Etapa 5 - Interprete o resultado

Compare as respostas: ambas identificam eventos, restaurantes e bairros? Descrevem apenas funcionalidades presentes no código? Alguma precisou buscar informações que estavam faltando?

Se B usar menos contexto e mantiver a cobertura, você terá uma evidência de seleção mais eficiente para essa pergunta. Se não houver redução, documente o resultado e investigue as referências usadas. Uma resposta menor, mas incompleta, não é uma otimização bem-sucedida.

---

## Critérios de sucesso

Use esta lista para conferir sua entrega:

- [ ] Comparei o tamanho do arquivo global antes e depois e expliquei o que foi removido, consolidado ou realocado.
- [ ] Criei instruções de API e de eventos com padrões `applyTo` correspondentes aos arquivos.
- [ ] Eliminei conflitos entre as instruções gerais e o contrato `{ count, events }`.
- [ ] Criei a skill `free-events-endpoint` com invocação automática desabilitada e a invoquei explicitamente.
- [ ] Implementei a filtragem, o intervalo de datas, a ordenação e o formato da resposta.
- [ ] Conferi o resultado esperado de dois eventos com os dados originais e revisei os casos de borda.
- [ ] Mantive as rotas de restaurantes e bairros inalteradas.
- [ ] Fiz as duas consultas em conversas novas, com o mesmo modelo e a mesma versão do código.
- [ ] Registrei as métricas disponíveis, os cálculos possíveis e a qualidade das respostas.
- [ ] Expliquei se houve redução de contexto, sem confundi-la com redução comprovada de créditos.

## Perguntas para reflexão

1. Quais regras realmente precisam estar disponíveis em todo o projeto?
2. O que deve ficar em uma instrução por caminho e o que deve virar uma skill?
3. Quando selecionar poucos arquivos ajuda e quando isso pode esconder informações importantes?
4. Que evidências adicionais seriam necessárias para afirmar que houve economia de créditos?

## Recursos de aprendizagem

- [Instruções personalizadas no VS Code](https://code.visualstudio.com/docs/copilot/customization/custom-instructions)
- [Agent Skills no VS Code](https://code.visualstudio.com/docs/copilot/customization/agent-skills)
- [Gerenciamento de contexto no Copilot Chat](https://code.visualstudio.com/docs/copilot/chat/copilot-chat-context)
