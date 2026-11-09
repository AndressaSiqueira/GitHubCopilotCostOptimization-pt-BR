# Desafio 04 - Configuração da sessão (ferramentas + cache) - Guia do instrutor

[< Solução anterior](./Solution-03.md) - **[Início](./README.md)** - [Próxima solução >](./Solution-05.md)

## Notas e orientações

Este desafio ensina aos alunos que ferramentas MCP adicionam sobrecarga de tokens a cada requisição e que alterações de configuração podem invalidar o contexto em cache. O cenário de varredura do repositório TypeScript fornece uma tarefa simples e mensurável para observar esses efeitos.

### Conceitos principais a explicar

**Sobrecarga das ferramentas MCP:**
- A definição de cada ferramenta MCP (nome, descrição, schema de parâmetros) é incluída no prompt de sistema
- Essa sobrecarga se aplica a toda requisição ao LLM, mesmo que a ferramenta nunca seja invocada
- O servidor MCP do GitHub normalmente habilita 6–8 ferramentas por padrão
- Para a tarefa de varredura do repositório, os alunos provavelmente só precisam de `search_code` e `get_file_contents`
- Ferramentas não utilizadas, como `create_issue`, `search_users` e `list_pull_requests`, adicionam sobrecarga desnecessária

**Invalidação do cache:**
- O GitHub Copilot CLI usa modelos Anthropic Claude com prompt caching
- A invalidação do cache ocorre quando o prompt de sistema muda (por exemplo, definições de ferramentas e instruções)
- Gatilhos comuns: habilitar/desabilitar ferramentas MCP, editar `.github/copilot-instructions.md` e trocar de modelo
- Sessões organizadas mantêm uma configuração estável = maior reutilização do cache = custos menores
- Sessões desorganizadas com alterações no meio da tarefa = invalidação do cache = sobrecarga de reprocessamento

**Observação importante sobre a documentação:**
A documentação oficial do GitHub não lista explicitamente os gatilhos de invalidação do cache. Os alunos os descobrem por meio de experimentação, observando picos de créditos após alterações de configuração. A tecnologia subjacente de prompt caching da Anthropic invalida o cache quando o prefixo do prompt muda.

### O cenário

Os alunos usam o GitHub Copilot CLI para fazer uma varredura do repositório `microsoft/TypeScript`:
- Encontrar todos os arquivos `package.json`
- Encontrar todos os arquivos `tsconfig.json`
- Ler o package.json principal para identificar dependências
- Gerar um relatório formatado

Esta é uma tarefa com vários turnos (5–10 etapas do agente) que oferece várias oportunidades de medição.

### Tempo esperado

60 minutos:
- 15 minutos: conclusão da varredura inicial com todas as ferramentas e registro da linha de base
- 10 minutos: identificação de ferramentas não utilizadas pelo painel Output do VS Code
- 15 minutos: desabilitação das ferramentas não utilizadas, repetição da varredura e medição da economia
- 15 minutos: comparação entre sessões organizadas e desorganizadas
- 5 minutos: documentação das descobertas

### Medições esperadas

**Economia na sobrecarga das ferramentas:**
- Linha de base: 6–8 ferramentas MCP do GitHub habilitadas
- Otimizado: 2 ferramentas habilitadas (search_code, get_file_contents)
- Removidas: 4–6 ferramentas não utilizadas
- Cada ferramenta não utilizada: ~100–300 tokens por etapa do agente
- Tarefa de varredura: ~5–10 etapas do agente
- **Economia esperada: 2.000–15.000 tokens (20–150 créditos)**

A economia real varia conforme:
- O modelo selecionado (Sonnet e Haiku têm custos base diferentes)
- O número de ferramentas inicialmente habilitadas
- A complexidade dos schemas das ferramentas
- O número de etapas executadas pelo agente

**Impacto da invalidação do cache:**
- Sessão organizada: configurar uma vez e concluir a varredura = cache estável
- Sessão desorganizada: habilitar/desabilitar ferramenta no meio da varredura + editar instruções = invalidações do cache
- **Diferença esperada: custo 10–30% maior para a sessão desorganizada**

A diferença pode ser sutil, pois a tarefa de varredura é relativamente curta. Tarefas mais longas mostram penalidades mais acentuadas de invalidação do cache.

### Obstáculos comuns

**Os alunos não conseguem encontrar a configuração de ferramentas MCP:**
- Os servidores MCP são configurados nas configurações do Copilot CLI (específicas de cada plataforma)
- No macOS/Linux: `~/.copilot/mcp.json` ou pelas configurações da CLI
- No Windows: `%USERPROFILE%\.copilot\mcp.json`
- Os alunos também podem usar o comando `copilot mcp` para gerenciar servidores

**Os alunos não veem as invocações de ferramentas:**
- Painel Output do VS Code: View → Output → selecione "GitHub Copilot" no menu suspenso
- As chamadas de ferramentas aparecem como mensagens JSON-RPC mostrando o nome e os parâmetros da ferramenta
- Se nenhuma ferramenta aparecer, talvez o servidor MCP do GitHub não esteja configurado
- Forneça uma saída de exemplo para que saibam o que procurar

**Os alunos não conseguem medir os créditos com precisão:**
- Use o comando `/usage` após cada tarefa para ver o detalhamento dos créditos
- O painel de uso do GitHub Copilot mostra o gasto acumulado (pode haver atraso)
- Incentive os alunos a registrar: nome da tarefa, data e hora, créditos utilizados
- Foque nas diferenças relativas (antes/depois), não nos números absolutos

**Os efeitos da invalidação do cache são sutis:**
- Tarefas curtas podem não mostrar diferenças acentuadas
- Incentive os alunos a fazer alterações claras: habilitar/desabilitar várias ferramentas, editar significativamente as instruções
- Os picos de créditos podem ser pequenos (10–30%), mas ainda mensuráveis
- O objetivo de aprendizagem é reconhecer o padrão, não atingir números específicos

### Dicas para compartilhar

**Se os alunos tiverem dificuldade em identificar ferramentas não utilizadas:**
- "Procure ferramentas que nunca aparecem no painel Output durante sua varredura"
- "Pergunte a si mesmo: criei alguma issue? Pesquisei usuários? Se não, você não precisa dessas ferramentas"
- "Para uma varredura de repositório somente leitura, você só precisa de ferramentas de busca e leitura"

**Se os alunos não conseguirem ver os efeitos da invalidação do cache:**
- "Tente fazer alterações mais expressivas no meio da sessão — edite significativamente as instruções, habilite/desabilite 2–3 ferramentas"
- "O efeito é mais visível em tarefas mais longas; sua varredura curta pode mostrar diferenças menores"
- "Concentre-se em observar o padrão, não em atingir uma porcentagem específica"

**Se os alunos questionarem por que isso importa:**
- "Em produção, os desenvolvedores realizam centenas de interações com o Copilot por dia"
- "Pequena sobrecarga por requisição × centenas de requisições = custo mensal significativo"
- "Uma boa higiene de sessões é como uma boa higiene do Git — evita desperdício acumulado"

### Aprofundamento técnico (se solicitado)

**Como as ferramentas MCP adicionam sobrecarga:**

Segundo a especificação do Model Context Protocol, cada ferramenta inclui:
```json
{
  "name": "get_weather",
  "description": "Obtenha informações meteorológicas atuais para uma localização",
  "inputSchema": {
    "type": "object",
    "properties": {
      "location": {
        "type": "string",
        "description": "Nome da cidade ou código postal"
      }
    },
    "required": ["location"]
  }
}
```

Esse schema completo é enviado ao LLM em cada requisição para que o modelo saiba:
- Quais ferramentas estão disponíveis
- O que cada ferramenta faz
- Como chamá-las corretamente

Uma ferramenta simples usa ~100–150 tokens; ferramentas complexas com muitos parâmetros usam 300–500 ou mais tokens.

**Por que ocorre a invalidação do cache:**

O GitHub Copilot CLI usa modelos Anthropic Claude. O prompt caching da Anthropic funciona armazenando em cache o "prefixo do prompt" (instruções de sistema + definições de ferramentas + histórico da conversa até um marcador de cache).

Se qualquer coisa nesse prefixo mudar — mesmo um único token — o cache é invalidado e precisa ser reconstruído. Isso significa:
- Habilitar/desabilitar uma ferramenta → o prompt de sistema muda → cache invalidado
- Editar instruções → o prompt de sistema muda → cache invalidado
- Trocar de modelo → o modelo diferente tem seu próprio espaço de cache

Referência: [Prompt caching da Anthropic](https://claude.com/blog/prompt-caching)

### Validação dos critérios de sucesso

Os alunos concluem com sucesso quando conseguem mostrar:

1. ✅ **Documentação da auditoria de ferramentas:**
   - Captura de tela ou saída de texto mostrando as ferramentas habilitadas antes da otimização
   - Evidência de quais ferramentas foram realmente invocadas (painel Output do VS Code)
   - Captura de tela mostrando a lista reduzida de ferramentas após a otimização

2. ✅ **Economia mensurável:**
   - Gasto de créditos na varredura da linha de base (todas as ferramentas habilitadas)
   - Gasto de créditos na varredura otimizada (ferramentas não utilizadas desabilitadas)
   - Economia calculada (mesmo que pequena)

3. ✅ **Observação da invalidação do cache:**
   - Gasto de créditos na sessão organizada
   - Gasto de créditos na sessão desorganizada
   - Descrição das alterações realizadas no meio da sessão
   - Observação de que a sessão desorganizada custou mais

4. ✅ **Explicação do aprendizado:**
   - Consegue explicar por que ferramentas não utilizadas custam tokens
   - Consegue citar pelo menos 2–3 alterações de configuração que invalidam o cache
   - Entende que configuração estável = melhor reutilização do cache

### Desafios adicionais

Para equipes que terminarem cedo:

**Auditoria avançada de ferramentas:**
- Configure 3–4 servidores MCP diferentes (GitHub, sistema de arquivos, HTTP, banco de dados)
- Conclua uma tarefa usando apenas um servidor
- Meça a sobrecarga de todos os servidores adicionais não utilizados

**Comparação de modelos:**
- Conclua a varredura com Sonnet (todas as ferramentas) versus Haiku (mínimo de ferramentas)
- Observe que modelo mais barato + configuração organizada pode superar modelo caro + configuração inchada

**Teste de sessão longa:**
- Use o Copilot CLI por mais de 30 minutos em tarefas variadas
- Observe o comportamento de compactação quando a janela de contexto se encher (~80% da capacidade)
- Meça se alterações frequentes de configuração acionam mais compactações

### Recursos adicionais para os alunos

Compartilhe depois que concluírem o desafio:

- [Gerenciamento de contexto no GitHub Copilot CLI](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/context-management) - Documentação oficial sobre janela de contexto e compactação
- [Especificação de ferramentas MCP](https://modelcontextprotocol.io/specification/2025-06-18/server/tools.md) - Detalhes sobre o que está incluído nos schemas das ferramentas
- Relatório de pesquisa salvo durante a preparação do hack, com citações detalhadas e validação técnica
