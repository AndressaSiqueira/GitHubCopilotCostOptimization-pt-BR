# What The Hack - Otimização de custos com GitHub Copilot

## Introdução

O GitHub Copilot transforma a produtividade de quem desenvolve software, mas, com a cobrança baseada em uso (UBB), cada token conta. Este What The Hack ensina equipes de engenharia a maximizar a qualidade do código e minimizar o consumo de créditos de IA por meio de boas práticas de engenharia.

Você aprenderá a controlar três fatores de custo: o que entra no contexto (instruções, anexos e ferramentas MCP), o que o modelo produz (seleção do modelo e restrições de saída) e a eficiência no uso da sessão (gerenciamento de cache, organização da janela de contexto e ciclos de feedback determinísticos). Ao final, você entenderá que otimizar custos do Copilot não significa, em geral, restringir o uso, mas preparar entradas e fluxos de trabalho melhores que ajudem o agente a concluir as tarefas mais rapidamente.

## Objetivos de aprendizagem

Neste workshop, você aprenderá técnicas práticas para otimizar os custos de uso do GitHub Copilot:

- Reduzir a sobrecarga de instruções persistentes usando arquivos de configuração com escopo definido por caminho
- Escolher modelos adequados e aplicar restrições de saída para controlar os custos de geração
- Gerenciar o excesso de ferramentas MCP e compreender os gatilhos de invalidação do cache
- Gerenciar a janela de contexto de forma proativa para manter a qualidade e controlar os custos
- Usar ciclos de feedback determinísticos (testes, linters e verificações de tipos) para controlar o consumo de tokens
- Medir e comparar o consumo de créditos em diferentes fluxos de desenvolvimento

## Desafios

- Desafio 00: **[Pré-requisitos](Student/Challenge-00.md)**
   - Preparar o ambiente do workshop
- Desafio 01: **[Desenvolvimento orientado por especificações](Student/Challenge-01.md)**
   - Demonstrar que controles determinísticos (testes e especificações) reduzem o desperdício de tokens por tentativa e erro
- Desafio 02: **[Engenharia de contexto](Student/Challenge-02.md)**
   - Revisar e reorganizar instruções globais em arquivos com escopo definido e substituir referências amplas por anexos fixados
- Desafio 03: **[Seleção de modelos e restrições de saída](Student/Challenge-03.md)**
   - Comparar custos em créditos entre modelos e níveis de raciocínio e aplicar restrições de saída para reduzir o consumo de tokens
- Desafio 04: **[Configuração da sessão (ferramentas e cache)](Student/Challenge-04.md)**
   - Remover ferramentas MCP não utilizadas e compreender os padrões de invalidação do cache
- Desafio 05: **[Gerenciamento da janela de contexto](Student/Challenge-05.md)**
   - Usar /compact proativamente para gerenciar o crescimento do contexto e evitar sua degradação
- Desafio 06: **[Competição de Token Golf](Student/Challenge-06.md)**
   - Concluir uma tarefa de programação com o menor consumo de créditos, atendendo a todos os critérios de aceitação

## Pré-requisitos

- Assinatura do GitHub Copilot
- Conhecimento dos fundamentos do GitHub Copilot
- Visual Studio Code OU uma IDE de sua preferência com a extensão do GitHub Copilot instalada

## Conteúdo do repositório

- [Student/Resources/](Student/Resources/) - Código inicial com configuração do Copilot intencionalmente pouco otimizada para as equipes aprimorarem
- [Coach/Solutions/](Coach/Solutions/) - Implementações de referência e dados de medição dos desafios
- [Guia de instrutores](Coach/README.md) - Orientações e soluções dos desafios
- [Slides](Coach/Lectures.pptx) - Modelo de apresentação do material original, traduzido; contém espaços reservados e texto de exemplo, não uma aula pronta

## Origem e tradução

Esta é uma tradução para português do Brasil do workshop [076-GitHubCopilotCostOptimization](https://github.com/Whowong/WhatTheHack/tree/xxx-GitHubCopilotCostOptimization/076-GitHubCopilotCostOptimization), do projeto What The Hack, baseada na revisão [`2c07574ed16b2ef160628f401dab207974c27195`](https://github.com/Whowong/WhatTheHack/commit/2c07574ed16b2ef160628f401dab207974c27195).

O conteúdo completo dessa pasta foi preservado, incluindo desafios, soluções, recursos e slides. Os nomes de arquivos, comandos, identificadores técnicos e dados dos exemplos permanecem compatíveis com o original. Prompts e explicações foram traduzidos. Os resultados de medição publicados são os do material original, não medições repetidas em português; a tradução dos prompts pode alterar as respostas e o consumo de tokens.

A [licença MIT](LICENSE), em sua versão original, e os créditos foram mantidos. Links para recursos gerais do projeto What The Hack continuam apontando para a origem.

## Colaboradores do material original

- Andy Huang
- Andressa Siqueira
- Anastasia Nefedova
- Anahita Afshari
- Devanshi Thakar
