# Desafio 06 - Competição de golfe de tokens 🏌️

[< Desafio anterior](./Challenge-05.md) - **[Início](../README.md)**

## Introdução

Golfe de tokens é a arte de obter código de alta qualidade com o mínimo gasto de créditos. Neste desafio final, as equipes competem para concluir a mesma tarefa de programação com o menor consumo de créditos, atendendo a todos os critérios de aceitação. É aqui que você aplica tudo o que aprendeu: engenharia de contexto, seleção de modelos, higiene da sessão e desenvolvimento orientado por especificação.

Seu instrutor já concluiu esta tarefa e estabeleceu uma pontuação "par" — o custo em créditos de uma solução bem otimizada. Você consegue ficar abaixo do par?

## Descrição

Cada equipe constrói a mesma aplicação do zero: um painel de condições meteorológicas. Não há uma base de código inicial nem uma especificação pronta entregue a você — você decide a estrutura do projeto, a abordagem dos prompts, a escolha do modelo e quaisquer instruções do Copilot ou arquivos de contexto que configurar. Vários vencedores serão selecionados com base no menor uso de tokens, mas também no melhor retorno sobre o investimento (ROI) em tokens.

### Requisitos da aplicação

Construa um painel de condições meteorológicas. Um usuário deve ser capaz de pesquisar uma cidade e ver suas condições meteorológicas atuais, e o painel também deve mostrar as últimas cinco cidades pesquisadas pelo usuário.

- Permita que um usuário pesquise uma cidade e exiba suas condições meteorológicas: nome da cidade, temperatura, condição do tempo, umidade e velocidade do vento
- Mostre as últimas cinco cidades pesquisadas pelo usuário
- Use a stack de frontend, a fonte de dados meteorológicos, a abordagem de estilização e a estrutura de componentes que você considerar mais econômicas para construir


## Critérios de sucesso

Para concluir este desafio com sucesso, você deve ser capaz de:

- Demonstrar um painel de condições meteorológicas funcional, sem backend
- Verificar que a pesquisa de uma cidade exibe seu nome, temperatura, condição do tempo, umidade e velocidade do vento
- Mostrar que as últimas cinco cidades pesquisadas são exibidas e persistem após a atualização da página usando armazenamento local
- Demonstrar as técnicas utilizadas para alcançar sua pontuação final de uso de créditos
- Mostrar uma captura de tela do painel funcionando junto com seu uso final de créditos

## Recursos de aprendizagem

- [Boas práticas do GitHub Copilot](https://docs.github.com/en/copilot/using-github-copilot/best-practices-for-using-github-copilot)
- [Guia de engenharia de prompts](https://www.promptingguide.ai/)
- [Fundamentos do desenvolvimento orientado por testes](https://martinfowler.com/bliki/TestDrivenDevelopment.html)

## Dicas

- Comece pela especificação, não pelo código — quais são os critérios de aceitação?
- Escreva primeiro testes que falhem para estabelecer seu ciclo determinístico de feedback
- Escolha seu modelo com base na complexidade de cada subtarefa
- Acompanhe os créditos ao longo do processo, não apenas no final
- Se ficar preso em um ciclo de alto custo, reinicie: use `/clear` e tente uma abordagem diferente
- Lembre-se de que o caminho mais rápido nem sempre é o mais barato — um minuto extra de planejamento pode economizar 20 créditos na execução