# Desafio 04 - Configure as ferramentas e observe o comportamento da sessão

[< Desafio anterior](./Challenge-03.md) - **[Início](../README.md)** - [Próximo desafio >](./Challenge-05.md)

## O que você vai aprender

Ferramentas permitem que o Copilot consulte arquivos, pesquise repositórios e acesse serviços externos. Essas capacidades são úteis, mas uma sessão não precisa oferecer todas as ferramentas para qualquer tarefa.

Neste desafio, você vai analisar um trecho do repositório público `microsoft/TypeScript`, identificar quais ferramentas foram usadas e comparar configurações de sessão.

Ao final, você deverá conseguir:

- Diferenciar ferramentas disponíveis de ferramentas realmente invocadas.
- Preparar uma configuração suficiente para uma tarefa de leitura.
- Comparar consumo e qualidade sem mudar várias condições ao mesmo tempo.
- Distinguir uma evidência de uso de cache de uma hipótese sobre seu comportamento.

> **Ideia central:** ofereça as capacidades necessárias, mantenha a configuração estável quando fizer sentido e interprete apenas as métricas que você consegue observar.

## Antes de começar

1. Use o GitHub Copilot Chat com um modelo e um modo que possam permanecer iguais durante o experimento.
2. Tenha acesso de leitura ao repositório [microsoft/TypeScript](https://github.com/microsoft/TypeScript).
3. Use uma integração GitHub MCP aprovada pela sua organização, caso esteja disponível. Se não estiver, acompanhe a demonstração do instrutor; não contorne políticas de acesso.
4. Escolha e registre um **SHA de commit** do TypeScript. Todas as execuções devem consultar essa mesma versão.
5. Localize o seletor de ferramentas e as informações de uso disponíveis na sua versão do VS Code.

Não é necessário clonar nem compilar o TypeScript. A tarefa é somente de leitura.

> **Segurança:** revise a origem e as permissões de qualquer servidor MCP. Não habilite ferramentas de escrita, administração ou acesso a dados privados apenas para aumentar a quantidade de ferramentas do experimento. Não inclua credenciais nos prompts ou registros.

## Entenda o que será observado

| Conceito | Significado |
|---|---|
| Ferramenta habilitada | Pode ser disponibilizada para a sessão |
| Ferramenta invocada | Foi chamada de fato durante a tarefa |
| Descoberta de ferramentas | O cliente pode selecionar ou carregar ferramentas conforme a necessidade |
| Cache de contexto | Reutilização de conteúdo processado anteriormente, quando suportada |
| Consumo medido | Tokens ou créditos informados pela interface, com sua unidade e seu escopo |

A forma de apresentar ferramentas ao modelo varia entre clientes e versões. Não presuma que o schema completo de toda ferramenta habilitada seja enviado em todas as chamadas.

Skills também não equivalem a ferramentas MCP: possuem mecanismos próprios de descoberta e carregamento. Neste experimento, mantenha o conjunto de skills e as instruções iguais para isolar a configuração das ferramentas.

---

## Parte 1 - Compare duas configurações de ferramentas

### Etapa 1 - Defina a tarefa de análise

Substitua `<SHA>` pelo commit escolhido e guarde o prompt final. Use exatamente esse texto nas duas execuções:

```text
Analise o repositório público microsoft/TypeScript no commit <SHA>.
Faça apenas operações de leitura.

Localize a implementação de createProgram e produza um relatório com:
1. O caminho do arquivo e o símbolo encontrado.
2. A responsabilidade da função, em até 100 palavras.
3. Até 3 dependências diretas que ela usa, indicando os símbolos e onde
   são definidos ou importados.
4. Referências para o código no commit informado.

Não analise o repositório inteiro. Se uma informação não puder ser
confirmada no código consultado, indique a limitação.
```

Aqui, “dependência direta” significa uma função, tipo ou módulo usado pela implementação, não necessariamente um pacote externo.

### Etapa 2 - Execute com a configuração inicial

Na **execução A**:

1. Mantenha seu conjunto inicial de ferramentas de leitura aprovadas.
2. Registre os nomes e a quantidade das ferramentas habilitadas.
3. Abra uma conversa nova e envie o prompt.
4. Preserve o relatório, as chamadas de ferramentas e as métricas disponíveis.

Confira a implementação e as referências citadas. Um relatório convincente, mas sem suporte no código, não satisfaz a tarefa.

### Etapa 3 - Identifique o conjunto necessário

Examine as chamadas exibidas no chat e, quando disponíveis, os logs da sessão no painel **Saída / Output**.

Classifique as ferramentas:

| Ferramenta | Habilitada em A? | Foi invocada? | Necessária para repetir a tarefa? |
|---|---|---|---|
| | | | |

Um conjunto suficiente costuma incluir capacidades de pesquisa e leitura de arquivos, mas os nomes exatos dependem da integração. Pode ser necessário manter uma ferramenta de descoberta para encontrar as demais.

### Etapa 4 - Execute com uma configuração focada

Na **execução B**:

1. Antes de iniciar a conversa, desabilite apenas ferramentas que não sejam necessárias para a tarefa.
2. Mantenha modelo, instruções, skills, prompt e SHA iguais aos da execução A.
3. Abra uma conversa nova e repita a análise.
4. Registre relatório, ferramentas invocadas e métricas.

Se A e B já tiverem o mesmo conjunto mínimo, registre essa condição. Não habilite ferramentas desnecessárias apenas para fabricar uma diferença.

### Etapa 5 - Compare

| Execução | Ferramentas habilitadas | Chamadas realizadas | Créditos, se disponíveis | Tokens, se disponíveis | Relatório atende aos 4 itens? |
|---|---|---|---|---|---|
| A - Inicial | | | | | |
| B - Focada | | | | | |

Se houver créditos atribuíveis às execuções:

```text
Diferença de créditos = créditos de A − créditos de B
Redução relativa (%) = (créditos de A − créditos de B) / créditos de A × 100
```

Calcule a redução relativa apenas se A for maior que zero. Valores negativos indicam aumento, não economia.

Não trate a contagem de ferramentas como uma medição de tokens. Se o consumo não estiver disponível, registre **“não disponível”** e limite a conclusão à configuração e ao comportamento observados.

---

## Parte 2 - Compare uma sessão estável com uma alteração controlada

Agora o objetivo é observar o efeito de **uma mudança de configuração**, não reproduzir vários tipos de interrupção ao mesmo tempo.

### Etapa 1 - Prepare uma análise em dois turnos

Use a configuração focada da Parte 1 e escolha uma ferramenta de leitura não necessária para os dois turnos. Ela deve começar habilitada tanto em C quanto em D.

Se não houver uma ferramenta dispensável, não desabilite uma necessária. Registre a limitação e faça esta parte como demonstração com o instrutor.

Em cada sessão, execute:

**Turno 1:** o mesmo prompt de análise de `createProgram` usado na Parte 1.

**Turno 2:**

```text
Revise o relatório anterior usando o mesmo commit.
Confira no código uma das dependências diretas citadas.
Apresente a evidência e corrija o relatório apenas se necessário.
Não amplie o escopo.
```

### Etapa 2 - Execute a sessão estável

Na **execução C**, comece uma conversa nova e complete os dois turnos sem mudar ferramentas, instruções, modelo ou configuração de raciocínio.

Registre o consumo de cada turno, se disponível.

### Etapa 3 - Execute a sessão com alteração

Na **execução D**, comece outra conversa nova com a mesma configuração inicial de C.

1. Envie o primeiro prompt.
2. Antes do segundo turno, desabilite somente a ferramenta dispensável escolhida.
3. Registre a ferramenta alterada e se a interface indicou que a mudança entrou em vigor.
4. Envie o segundo prompt sem mudar nenhuma outra condição.

Se a alteração só valer em uma nova sessão, esta execução não testa uma mudança no meio da conversa. Documente isso em vez de tratá-la como se tivesse surtido efeito.

### Etapa 4 - Interprete as evidências

| Execução | Alteração entre turnos | Consumo do turno 1 | Consumo do turno 2 | Cache informado pela interface | Qualidade e observações |
|---|---|---|---|---|---|
| C - Estável | Nenhuma | | | | |
| D - Alterada | | | | | |

Indique a unidade e a fonte de cada métrica. Se o total for agregado e não puder ser atribuído à sessão, deixe essa limitação explícita.

> **Cuidado com a conclusão:** um aumento de créditos ou de latência não prova invalidação de cache. Diferenças no tamanho das respostas, nas buscas, no processamento interno e na sequência de chamadas também podem alterar o consumo. Só afirme um comportamento de cache quando houver métricas que o sustentem; mesmo assim, uma comparação isolada não estabelece causalidade.

Uma repetição opcional pode inverter a ordem de C e D. Registre todas as tentativas e considere que cache entre sessões e variações do serviço também podem afetar o resultado.

## Critérios de sucesso

- [ ] Registrei o SHA do TypeScript e mantive a análise somente de leitura.
- [ ] Listei ferramentas habilitadas e distingui as chamadas efetivas.
- [ ] Produzi relatórios verificáveis, com caminhos, símbolos e referências.
- [ ] Comparei a configuração inicial e a focada sem alterar modelo, skills ou instruções.
- [ ] Registrei métricas disponíveis e limitações de observação.
- [ ] Comparei sessões estável e alterada, ou documentei por que a etapa não pôde ser executada.
- [ ] Não apresentei uma diferença de consumo como prova automática de invalidação de cache.
- [ ] Expliquei quando reduzir ferramentas ajudou, não ajudou ou não pôde ser medido.

## Perguntas para reflexão

1. Quais capacidades eram realmente necessárias para a análise?
2. A descoberta de ferramentas influenciou o conjunto disponibilizado ao modelo?
3. O que você mediu diretamente e o que permanece uma hipótese?
4. Qual configuração você manteria para repetir essa tarefa?

## Recursos de aprendizagem

- [Configuração de servidores MCP no VS Code](https://code.visualstudio.com/docs/agent-customization/mcp-servers)
- [Conceitos de contexto em agentes](https://code.visualstudio.com/docs/agents/concepts/context)
- [Especificação de ferramentas MCP](https://modelcontextprotocol.io/specification/2025-06-18/server/tools)
- [Cobrança baseada em uso para organizações e empresas](https://docs.github.com/en/copilot/concepts/billing-and-usage/organizations-and-enterprises/billing)
