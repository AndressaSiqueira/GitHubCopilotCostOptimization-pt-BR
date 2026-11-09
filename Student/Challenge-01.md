# Desafio 01 - Prompt direto vs. desenvolvimento orientado por especificação

[< Desafio anterior](./Challenge-00.md) - **[Início](../README.md)** - [Próximo desafio >](./Challenge-02.md)

## Introdução

Neste desafio, você construirá a mesma aplicação duas vezes com o GitHub Copilot:

1. Usando apenas um prompt direto
2. Usando uma especificação estruturada em um arquivo Markdown

O objetivo não é provar antecipadamente que uma abordagem é sempre melhor. O objetivo é observar como o nível de detalhamento do contexto afeta o tempo, o consumo de créditos, o número de interrupções e o resultado entregue.

Esta atividade usa **desenvolvimento orientado por especificação (Spec-Driven Development, SDD)**. A especificação será fornecida em um único arquivo `sdd.md`, sem uma constituição, comandos especiais, um plano separado ou uma lista de tarefas.

> **Conceito-chave:** no SDD, a especificação se torna a fonte de contexto para a implementação.

## Objetivo do experimento

Ambas as abordagens devem construir a mesma aplicação com a mesma tecnologia, modelo e escopo.

### Aplicação

Uma aplicação simples de notas construída com React e TypeScript.

Requisitos:

1. Criar, ler, atualizar e excluir notas (CRUD)
2. Cada nota deve ter um título obrigatório e conteúdo opcional
3. As notas devem existir apenas no estado em memória da aplicação
4. Não usar backend, banco de dados, armazenamento persistente ou testes automatizados
5. A aplicação deve ser implementada e executada localmente

## Preparação

Para tornar a comparação mais consistente:

- Use o mesmo computador e ambiente
- Use as mesmas versões do VS Code e do GitHub Copilot
- Use o mesmo modelo em ambas as execuções
- Inicie cada abordagem em uma pasta vazia e em uma nova conversa
- Não reutilize em uma abordagem os arquivos gerados pela outra
- Comece a medir quando enviar a instrução de implementação
- Pare de medir quando a aplicação estiver em execução e as operações CRUD tiverem sido verificadas manualmente

Registre também o tempo e o custo necessários para preparar a especificação. Eles serão analisados separadamente do tempo de implementação.

---

## Parte 1 - Implementação com um prompt direto

### Etapa 1 - Crie uma pasta vazia

```bash
mkdir notes-app-prompt
cd notes-app-prompt
code .
```

### Etapa 2 - Inicie uma nova conversa

Selecione o modelo escolhido para o experimento e envie apenas o prompt abaixo:

```text
Construa uma aplicação simples de notas usando React e TypeScript.

Requisitos:

1. Crie, leia, atualize e exclua notas.
2. Cada nota deve ter um título obrigatório e conteúdo opcional.
3. Armazene as notas apenas no estado em memória da aplicação.
4. Não use backend, banco de dados, armazenamento persistente ou testes automatizados.

Implemente a aplicação completa na máquina local.
```

### Etapa 3 - Registre a execução

Registre os horários de início e término, os créditos consumidos, as perguntas feitas pelo Copilot, as decisões sobre dependências solicitadas, as intervenções necessárias e quaisquer erros ou retrabalho.

Responda às perguntas necessárias para permitir que o processo continue, mas registre cada interrupção.

### Etapa 4 - Verifique manualmente

Confirme que você consegue:

- Criar uma nota com título e conteúdo
- Criar uma nota sem conteúdo
- Impedir a criação de uma nota sem título
- Visualizar as notas criadas
- Atualizar o título e o conteúdo de uma nota
- Excluir uma nota
- Recarregar a página e observar que os dados podem ser perdidos

Mantenha o projeto para a comparação final.

---

## Parte 2 - Implementação com SDD

Nesta parte, a mesma aplicação será construída a partir de uma especificação preparada anteriormente.

### Etapa 1 - Crie uma nova pasta vazia

```bash
mkdir notes-app-sdd
cd notes-app-sdd
code .
```

### Etapa 2 - Crie o arquivo de especificação

Na raiz da pasta, crie um arquivo chamado `sdd.md` com o seguinte conteúdo:

```markdown
# Especificação: aplicação simples de notas

## Objetivo

Construa uma aplicação completa de notas usando React e TypeScript que seja executada
na máquina local. A aplicação deve permitir que os usuários criem, leiam,
atualizem e excluam notas.

## Tecnologia

- React
- TypeScript
- Ambiente de desenvolvimento local

## Modelo de dados da nota

Cada nota deve conter:

| Campo | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| id | string ou number | Sim | Identificador único gerado pela aplicação |
| title | string | Sim | Título da nota |
| content | string | Não | Conteúdo opcional da nota |

## Requisitos funcionais

### REQ-001: Criar notas

O usuário deve ser capaz de criar uma nota com um título obrigatório e conteúdo
opcional. Uma nota válida deve ser adicionada ao estado em memória e exibida.

### REQ-002: Ler notas

A aplicação deve exibir as notas criadas durante a sessão atual,
incluindo o título de cada nota e seu conteúdo, quando presente.

### REQ-003: Atualizar notas

O usuário deve ser capaz de atualizar o título e o conteúdo de uma nota existente.
A atualização deve substituir a nota existente sem criar uma duplicata.

### REQ-004: Excluir notas

O usuário deve ser capaz de excluir uma nota existente. A nota excluída deve ser
removida da memória e não ser mais exibida.

### REQ-005: Título obrigatório

A aplicação não deve criar nem atualizar uma nota com título vazio. O
conteúdo pode estar vazio.

### REQ-006: Estado em memória

As notas devem ser gerenciadas apenas no estado da aplicação do lado do cliente. As notas podem ser
perdidas quando a página for atualizada ou a aplicação for reiniciada.

## Restrições

- Use React e TypeScript
- Execute na máquina local
- Não use backend
- Não use banco de dados
- Não use localStorage, IndexedDB, arquivos ou outro armazenamento persistente
- Não inclua testes automatizados

## Definição de pronto

A aplicação está completa quando é executada localmente e o usuário consegue criar,
ler, atualizar e excluir notas, respeitando todas as restrições acima.
```

### Etapa 3 - Inicie uma nova conversa

Selecione o mesmo modelo usado na Parte 1 e envie:

```text
Leia o arquivo sdd.md deste projeto e implemente a aplicação completa
descrita nele na máquina local.

Siga a especificação exatamente. Não adicione requisitos ou funcionalidades
fora do escopo definido.
```

### Etapa 4 - Registre e verifique

Registre as mesmas medições da Parte 1 e use exatamente a mesma lista de verificação manual. Não dê vantagem ao SDD por funcionalidades que não foram incluídas na especificação.

---

## Parte 3 - Compare os resultados

Preencha a tabela com os dados de ambas as execuções:

| Aspecto | Prompt direto | SDD com uma especificação pronta |
|---|---:|---:|
| Modelo utilizado | | |
| Tempo de implementação | | |
| Créditos consumidos durante a implementação | | |
| Perguntas durante a execução | | |
| Intervenções do usuário | | |
| Requisitos atendidos | | |
| Erros ou retrabalho | | |
| Avaliação qualitativa da UX | | |

### Três dimensões de análise

1. **Eficácia:** ambas as aplicações atenderam aos mesmos requisitos?
2. **Eficiência de implementação:** qual abordagem exigiu menos tempo, menos créditos e menos intervenções depois que sua entrada estava pronta?
3. **Eficiência do ciclo completo:** o resultado muda quando o custo de preparar a especificação é incluído?

O tempo e o custo totais do SDD devem ser calculados como:

$$
T_{SDD\ total} = T_{specification} + T_{implementation}
$$

$$
C_{SDD\ total} = C_{specification} + C_{implementation}
$$

Não misture essas duas perspectivas. Uma especificação pronta pode acelerar a implementação, mas prepará-la também tem um custo.


## Critérios de sucesso

Após concluir o desafio, você deve ser capaz de:

- Construir a mesma aplicação com um prompt direto e uma especificação Markdown
- Manter a tecnologia, o modelo e o escopo equivalentes em ambas as execuções
- Verificar manualmente as operações CRUD e as restrições
- Comparar tempo, créditos, perguntas e intervenções
- Separar o custo de implementação do custo de preparação
- Explicar por que um empate funcional ainda pode mostrar diferenças de eficiência
- Reconhecer que uma única execução é uma observação, não uma prova universal

## Perguntas para reflexão

1. Ambas as abordagens atenderam aos mesmos requisitos funcionais?
2. Qual abordagem exigiu mais decisões durante a implementação?
3. A especificação reduziu a ambiguidade ou apenas transferiu as decisões para uma etapa anterior?
4. Quanto tempo e quantos créditos foram usados para preparar a especificação?
5. O resultado muda quando esse custo é incluído?
6. Em quais situações a especificação poderia ser reutilizada e compensar seu custo inicial?
7. Uma aplicação maior ou uma alteração posterior nos requisitos produziria o mesmo resultado?

## Limitações do experimento

- Uma única execução não controla a variação natural nas respostas dos modelos
- A aplicação é pequena e pode favorecer o prompt direto em relação ao ciclo completo
- A avaliação visual é subjetiva sem critérios predefinidos
- O tempo pode ser afetado por instalações, condições de rede e familiaridade com as ferramentas
- Os resultados não demonstram que o SDD é sempre melhor ou pior
