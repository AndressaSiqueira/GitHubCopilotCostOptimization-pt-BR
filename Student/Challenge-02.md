# Desafio 02 - Engenharia de contexto (aplicação NYC)

[< Desafio anterior](./Challenge-01.md) - **[Início](../README.md)** - [Próximo desafio >](./Challenge-03.md)

## Introdução

Neste desafio, você otimizará o contexto do Copilot usando uma tarefa real de código na aplicação inicial NYC em Resources/Challenge-02-NYCApp.

A aplicação inclui intencionalmente um arquivo global `.github/copilot-instructions.md` superdimensionado e várias rotas (`events`, `restaurants`, `neighborhoods`) para que você possa comparar o contexto amplo (`#Codebase`) com anexos precisos, focados na tarefa.

Cada token enviado ao GitHub Copilot tem um custo. O contexto que persiste entre interações, como arquivos de instruções globais ou referências amplas ao espaço de trabalho, pode aumentar o gasto recorrente ao adicionar tokens que não são necessários para a tarefa atual.

Você auditará o arquivo de instruções globais sobrecarregado, o reestruturará em arquivos com escopo específico por caminho e substituirá referências amplas por anexos fixados para reduzir o custo básico de cada interação com o Copilot, mantendo a qualidade da saída.

## Descrição

Use o projeto em:

`Resources/Challenge-02-NYCApp`

### Parte 1 - Defina o escopo das instruções

1. Audite `.github/copilot-instructions.md` e identifique o que é:
	 - universalmente útil
	 - específico de eventos
	 - irrelevante para esta tarefa (por exemplo, regras de restaurantes/bairros/frontend/testes)
2. Reduza o arquivo global para conter apenas orientações verdadeiramente globais.
3. Crie arquivos de instruções com escopo em `.github/instructions/` para regras que devem se aplicar apenas a caminhos/tarefas específicos. Por exemplo, crie um arquivo `api.instructions.md` e um arquivo `events.instructions.md`.
4. Mantenha a lógica específica de eventos fácil de encontrar para o trabalho em `src/routes/events.ts`.
5. Crie uma skill reutilizável do Copilot em `.github/skills/free-events-endpoint/SKILL.md` que registre o padrão de implementação de um endpoint de eventos gratuitos. Essa skill deve ser carregada apenas quando invocada explicitamente, tornando-se um custo condicional em vez de recorrente.

### Parte 2 - Implemente a tarefa de rota de referência

Implemente `GET /events/free-this-week` em `src/routes/events.ts` com este comportamento:

- inclua eventos em que `price === 0`
- inclua apenas eventos nos próximos 7 dias
- ordene por data em ordem crescente
- retorne JSON no formato `{ count, events }`

Importante:

- modifique `src/routes/events.ts`
- não modifique `src/routes/restaurants.ts`
- não modifique `src/routes/neighborhoods.ts`

### Parte 3 - Precisão dos anexos e verificação do uso de tokens

Na interface do GitHub Copilot Chat, execute esta consulta exata duas vezes e compare os resultados:

"Quais dados ou funcionalidades esta aplicação oferece?"

Execute-a duas vezes e registre o uso de tokens em cada execução:

1. Sem arquivos com escopo (contexto amplo, como `#Codebase`)
2. Com arquivos com escopo fixados (apenas arquivos relevantes para a tarefa, por exemplo: `src/routes/events.ts`, `src/data/events.ts` e arquivos de instruções relevantes)

Registre ambas as contagens de tokens nos detalhes de uso/saída do Copilot Chat, compare a qualidade das respostas e calcule a diferença.

Para cada execução, registre as estatísticas da janela de contexto neste formato:

- Tokens utilizados / Total de tokens da janela de contexto
- Porcentagem de utilização da janela de contexto

Exemplo de formato:

- Execução A (ampla): 8,200 / 32,000 (25.6%)
- Execução B (com escopo): 2,100 / 32,000 (6.6%)

Em seguida, calcule:

- Diferença de tokens utilizados (A - B)
- Diferença de utilização em pontos percentuais

Use esta tabela para registrar suas medições:

| Execução | Estratégia de contexto | Consulta | Tokens utilizados | Total de tokens da janela de contexto | Utilização % | Observações |
|-----|------------------|-------|-------------|-----------------------------|---------------|-------|
| A | Ampla (`#Codebase` ou equivalente) | Quais dados ou funcionalidades esta aplicação oferece? | | | | |
| B | Arquivos com escopo fixados | Quais dados ou funcionalidades esta aplicação oferece? | | | | |

| Métrica de comparação | Valor |
|-------------------|-------|
| Diferença de tokens utilizados (A - B) | |
| Diferença de utilização em pontos percentuais (A - B) | |


## Critérios de sucesso

Para concluir este desafio com sucesso, você deve ser capaz de:

- Mostrar que `.github/copilot-instructions.md` é significativamente menor que o original
- Mostrar os arquivos de instruções com escopo criados em `.github/instructions/`
- Mostrar uma skill reutilizável criada em `.github/skills/free-events-endpoint/SKILL.md`
- Demonstrar uma implementação correta de `/events/free-this-week` em `src/routes/events.ts`
- Demonstrar que `src/routes/restaurants.ts` e `src/routes/neighborhoods.ts` permaneceram inalterados
- Mostrar a comparação de tokens entre `#Codebase` e anexos fixados para a mesma tarefa
- Mostrar a comparação de tokens e janela de contexto da Parte 3 para a consulta "Quais dados ou funcionalidades esta aplicação oferece?" no Copilot Chat:
	- sem arquivos com escopo
	- com arquivos com escopo fixados
	- com estatísticas documentadas da janela de contexto (utilizados / total)
	- com a porcentagem de utilização documentada para ambas as execuções
	- com as diferenças de tokens e utilização documentadas
- Mostrar uma redução mensurável de créditos preservando a qualidade da saída

## Recursos de aprendizagem

- [Documentação de instruções do GitHub Copilot](https://docs.github.com/en/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot)
- [Arquivos de prompt e anexos do GitHub Copilot](https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide#reference-files-in-your-prompts)
- [Visão geral das skills do GitHub Copilot](https://docs.github.com/en/copilot/using-github-copilot/using-github-copilot-skills)

## Dicas

- Instruções persistentes são custos recorrentes — elas são carregadas em cada chamada
- Skills são custos condicionais — elas só são carregadas quando invocadas
- Anexos são custos por chamada — você controla exatamente o que é incluído
- A meta de engenharia: mantenha as instruções globais sempre ativas abaixo de 1000 tokens
- Instruções com escopo devem ser fáceis de encontrar: se uma regra se aplica apenas a `/api`, coloque o arquivo de instruções em `/api/.github/`
