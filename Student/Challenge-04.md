# Desafio 04 - Configuração da sessão (ferramentas + cache)

[< Desafio anterior](./Challenge-03.md) - **[Início](../README.md)** - [Próximo desafio >](./Challenge-05.md)

## Introdução

Cada ferramenta MCP e skill que você habilita adiciona uma sobrecarga de tokens a cada etapa do agente. O nome, a descrição e o schema dos parâmetros de cada ferramenta são apresentados ao modelo em cada solicitação — mesmo que a ferramenta nunca seja invocada. Uma sessão com muitas ferramentas não utilizadas consome créditos antes que você escreva uma linha de código.

Enquanto isso, alterar a configuração durante a sessão pode provocar a invalidação do cache, forçando reinicializações a frio caras, nas quais o contexto anteriormente armazenado em cache precisa ser reprocessado.

Neste desafio, você medirá o custo real da proliferação de ferramentas e observará como a higiene da sessão afeta seu gasto de créditos.

## Descrição

Este desafio tem duas partes: medir a sobrecarga das ferramentas MCP e observar o comportamento de invalidação do cache.

### Parte 1: Meça a sobrecarga das ferramentas MCP e skills

Use o GitHub Copilot para analisar/encontrar algo no repositório `microsoft/TypeScript` e apresentar um relatório.

Se você ainda não tiver servidores MCP habilitados, experimente o servidor MCP do GitHub com todas as suas ferramentas. Conclua a tarefa com todas as ferramentas habilitadas e registre seu gasto de créditos.

Em seguida, identifique quais ferramentas MCP e skills foram realmente utilizadas.

Desabilite as ferramentas e skills não utilizadas, repita a análise e meça a diferença de créditos. Cada ferramenta não utilizada adiciona uma sobrecarga de tokens em cada etapa do agente porque seu schema está incluído no prompt de sistema.

### Parte 2: Observe a invalidação do cache

Conclua a análise do repositório mais duas vezes sob condições diferentes:

**Sessão limpa:** Configure suas ferramentas uma vez e conclua toda a análise sem fazer nenhuma alteração de configuração. Registre o total de créditos.

**Sessão desorganizada:** Inicie a análise, mas, no meio dela, faça alterações de configuração deliberadamente — desabilite uma ferramenta, edite seu arquivo `.github/copilot-instructions.md` ou mude para outro nível de esforço de raciocínio. Termine a análise e registre o total de créditos.

Observe quais alterações de configuração causam picos mensuráveis de créditos. Esses picos indicam a invalidação do cache — quando o GitHub Copilot precisa reprocessar o contexto anteriormente armazenado em cache.

## Critérios de sucesso

Para concluir este desafio com sucesso, você deve ser capaz de:

- Mostrar quais ferramentas MCP estavam habilitadas no início
- Concluir a análise do repositório TypeScript e gerar um relatório com caminhos de arquivos e dependências
- Identificar quais ferramentas foram realmente invocadas examinando os logs do painel Saída do VS Code
- Demonstrar uma economia mensurável de créditos ao desabilitar ferramentas não utilizadas na mesma tarefa de análise
- Mostrar os custos comparativos de créditos entre as abordagens de sessão limpa e sessão desorganizada
- Explicar quais alterações de configuração você observou causando a invalidação do cache
- Documentar suas descobertas: quantidade de ferramentas antes/depois, créditos antes/depois e diferença de créditos entre sessões limpas/desorganizadas

## Recursos de aprendizagem

- [Gerenciamento de contexto no GitHub Copilot CLI](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/context-management)
- [Especificação de ferramentas do Model Context Protocol](https://modelcontextprotocol.io/specification/2025-06-18/server/tools.md)
- [Cache de prompts da Anthropic](https://claude.com/blog/prompt-caching)
- [Cobrança baseada em uso do GitHub Copilot](https://docs.github.com/en/copilot/concepts/billing/usage-based-billing-for-organizations-and-enterprises)

## Dicas

- O painel Saída do VS Code (Exibir → Saída → "GitHub Copilot"; View → Output na interface em inglês) mostra as invocações reais de ferramentas
- O schema de cada ferramenta MCP (nome, descrição, parâmetros) é enviado ao modelo em cada solicitação
- Alterações no prompt de sistema (como editar arquivos de instruções ou habilitar/desabilitar ferramentas) podem invalidar o contexto armazenado em cache
- O servidor MCP do GitHub normalmente inclui ferramentas como: search_code, get_file_contents, create_issue, search_users, list_pull_requests
- Para esta tarefa de análise, você provavelmente precisa apenas de search_code e get_file_contents
