# Desafio 05 - Gerenciamento da janela de contexto

[< Desafio anterior](./Challenge-04.md) - **[Início](../README.md)** - [Próximo desafio >](./Challenge-06.md)

## Pré-requisitos

- Conclua o Desafio 02 (Engenharia de contexto) — você ampliará a aplicação CityScout NYC daquele desafio
- Conclua o Desafio 04 (Configuração da sessão: ferramentas + cache)

## Introdução

As janelas de contexto crescem a cada interação. À medida que uma sessão acumula mensagens, anexos e código gerado, o modelo tem mais histórico para processar a cada turno.

Quando o contexto cresce demais, a qualidade frequentemente cai: requisitos ignorados, perguntas repetidas, edições inconsistentes e maior gasto de créditos. Neste desafio, você comparará o crescimento não gerenciado do contexto com o gerenciamento proativo do contexto e medirá a diferença de créditos.

## Descrição

Você ampliará a **aplicação CityScout NYC** (do Desafio 02) com quatro novas funcionalidades e comparará duas estratégias de sessão lado a lado: uma em que você deixa o contexto crescer sem controle e outra em que o gerencia ativamente. As funcionalidades abrangem deliberadamente as três rotas e forçam mudanças de assunto — exatamente as condições que fazem o contexto crescer rapidamente.

### A tarefa: sprint de funcionalidades do CityScout

Usando a aplicação NYC com a qual você trabalhou no Desafio 02 (em `Resources/Challenge-02-NYCApp`), implemente estas quatro funcionalidades em ordem:

- **Funcionalidade 1 – Filtragem de restaurantes:** Adicione suporte a parâmetros de consulta a `GET /restaurants` para que os clientes possam filtrar por `borough` e/ou `cuisine` (por exemplo, `/restaurants?borough=Brooklyn&cuisine=Mexican`). Retorne a lista completa quando nenhum filtro for fornecido.
- **Funcionalidade 2 – Detalhes do bairro com restaurantes:** Adicione `GET /neighborhoods/:name`, que retorna o objeto do bairro correspondente mais um array incorporado de restaurantes desse bairro (uma junção entre os dados dos arquivos `neighborhoods.ts` e `restaurants.ts`).
- **Funcionalidade 3 – Paginação (transversal):** Adicione suporte a `?page=N&limit=N` aos três endpoints de listagem (`/events/free-this-week`, `/restaurants`, `/neighborhoods`). Use a página 1 e o limite 10 como padrão. Retorne `{ page, limit, total, data }`.
- **Funcionalidade 4 – Validação de entrada e tratamento de erros:** Adicione respostas adequadas `400 Bad Request` para parâmetros de consulta inválidos e `404 Not Found` para recursos ausentes em todas as rotas.

Essas quatro funcionalidades afetam vários arquivos, exigem referências entre arquivos e criam pontos de parada naturais entre cada funcionalidade — ideais para testar estratégias de gerenciamento de contexto. Recomendamos não fazer commit desses arquivos para facilitar a reversão.

### Execução A – Crescimento não gerenciado do contexto

Implemente as quatro funcionalidades em uma única sessão sem usar `/compact` em nenhum momento:

- Deixe o contexto acumular naturalmente à medida que passa de uma funcionalidade para outra
- Não inicie novas sessões entre funcionalidades
- Acompanhe o uso de créditos após a conclusão de cada funcionalidade
- Observe sinais de degradação de qualidade à medida que o contexto cresce:
  - O Copilot esquece requisitos anteriores (por exemplo, o formato de paginação difere entre as rotas)
  - Sugestões contraditórias (por exemplo, formatos de erro diferentes em rotas diferentes)
  - Repetição de perguntas de esclarecimento que você já respondeu
  - Aumento de retrabalho ou correções manuais

Registre uma breve observação de evidência após cada funcionalidade: o que funcionou e o que piorou.

### Execução B – Gerenciamento proativo do contexto

Implemente as mesmas quatro funcionalidades, mas gerencie ativamente o contexto durante todo o processo. Você escolhe sua própria estratégia:

- `/compact` para resumir e continuar na mesma sessão
- `/clear` para limpar e reiniciar com um novo prompt
- Inicie uma nova sessão (`/new`) em qualquer ponto de parada que escolher

O objetivo é manter o contexto enxuto e o gasto de créditos baixo. Acompanhe o total de créditos de todo o sprint (incluindo quaisquer novas sessões que você iniciar) e compare com a Execução A. Documente quais ações de gerenciamento de contexto você realizou e por quê.

## Critérios de sucesso

Para concluir este desafio com sucesso, você deve ser capaz de:

- Demonstrar pelo menos dois sinais concretos de degradação de qualidade na Execução A
- Mostrar uma comparação de créditos lado a lado entre a Execução A e a Execução B para as mesmas quatro funcionalidades
- Verificar que sua estratégia de gerenciamento de contexto da Execução B reduziu o gasto total de créditos em comparação com a Execução A
- Explicar as vantagens e desvantagens de `/compact`, `/clear` e iniciar uma nova sessão
- Mostrar um registro conciso de evidências para ambas as execuções (ações de gerenciamento de contexto realizadas, créditos por funcionalidade, total de créditos)

## Recursos de aprendizagem

- [Entendendo janelas de contexto e limites de tokens](https://www.anthropic.com/index/prompting-long-context)
- [Documentação de comandos do GitHub Copilot Chat](https://docs.github.com/en/copilot/using-github-copilot/using-github-copilot-chat)
- [Gerenciamento de conversas longas com assistentes de IA](https://www.promptingguide.ai/)

## Dicas

- Não otimize primeiro pela velocidade; otimize para comparações claras de créditos entre as execuções
- Mantenha as quatro funcionalidades idênticas entre a Execução A e a Execução B para que a comparação de créditos seja significativa
- Registre os créditos após cada funcionalidade, não apenas no final — isso mostra onde os custos aceleram
- Não há uma única estratégia "certa" para a Execução B; `/compact`, `/clear` e `/new` têm vantagens e desvantagens
- `/compact` preserva alguma continuidade de contexto, mas consome tokens para resumir
- `/clear` e `/new` oferecem um início a frio — barato por turno, mas você restabelece o contexto do zero
- A melhor estratégia frequentemente combina abordagens, dependendo de quanto contexto anterior a próxima funcionalidade precisa
