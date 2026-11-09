# What The Hack - Otimização de custos do GitHub Copilot - Guia do instrutor

## Introdução

Boas-vindas ao guia do instrutor do What The Hack sobre otimização de custos do GitHub Copilot. Aqui você encontrará links para orientações específicas para instrutores em cada desafio.

Este hack ensina as equipes a maximizar a qualidade do código enquanto minimizam o gasto de créditos do GitHub Copilot na cobrança baseada em uso (UBB). O foco são técnicas práticas de engenharia: engenharia de contexto, seleção de modelos, higiene de sessões e desenvolvimento orientado por especificações.

**OBSERVAÇÃO:** Se você participa do hackathon, este é o guia de respostas. Não prejudique seu aprendizado consultando estas respostas durante o hack! Vá aprender algo. :)

## Guias do instrutor

- Desafio 00: **[Pré-requisitos e linha de base](./Solution-00.md)**
   - Configure o ambiente do hack e estabeleça medições do gasto de créditos da linha de base
- Desafio 01: **[Desenvolvimento orientado por especificações](./Solution-01.md)**
   - Aproveite controles determinísticos como controles de tokens
- Desafio 02: **[Engenharia de contexto](./Solution-02.md)**
   - Otimize a arquitetura de instruções e a precisão dos anexos
- Desafio 03: **[Seleção de modelos e restrições de saída](./Solution-03.md)**
   - Compare modelos e aplique restrições de saída para reduzir custos
- Desafio 04: **[Configuração da sessão (ferramentas + cache)](./Solution-04.md)**
   - Gerencie a proliferação de ferramentas MCP e entenda a invalidação do cache
- Desafio 05: **[Gerenciamento da janela de contexto](./Solution-05.md)**
   - Use /compact proativamente para manter a qualidade e controlar custos
- Desafio 06: **[Competição de Token Golf](./Solution-06.md)**
   - Desafio competitivo de programação que busca o menor gasto de créditos

## Pré-requisitos do instrutor

Este hack tem pré-requisitos que o instrutor é responsável por entender e/ou configurar ANTES de organizar um evento. Consulte o [guia de organização do What The Hack](https://aka.ms/wthhost) para obter informações sobre como organizar um evento de hack.

O guia aborda as etapas comuns de preparação que um instrutor precisa realizar antes de qualquer evento What The Hack, incluindo como configurar corretamente o Microsoft Teams.

### Recursos dos alunos

Antes do hack, é responsabilidade do instrutor baixar e empacotar o conteúdo da pasta `/Student/Resources` deste hack em um arquivo "Resources.zip". O instrutor deve então fornecer uma cópia do arquivo Resources.zip a todos os alunos no início do hack.

A pasta Student/Resources deve conter:

- **Base de código inicial** com uma configuração do GitHub Copilot intencionalmente abaixo do ideal:
  - `.github/copilot-instructions.md` inchado (~1500 tokens) para o Desafio 02
  - Várias ferramentas MCP habilitadas (algumas desnecessárias) para o Desafio 04
  - Código de exemplo com oportunidades para comparar a abordagem de especificação primeiro com a de tentativa e erro
- **Tarefa de programação da linha de base** (baseline-task.md) para o Desafio 00
- **Prompts de seleção de modelos + modelo de medição** (`Challenge-03-ModelSelection/`) para o Desafio 03

O Desafio 06 (Token Golf) não exige uma base de código inicial nem um arquivo de especificação — a tarefa do painel meteorológico e seus critérios de aceitação são descritos diretamente no guia do Desafio 06 do aluno.

Sempre encaminhe os alunos ao [site do What The Hack](https://aka.ms/wth) para acessar o guia do aluno: [https://aka.ms/wth](https://aka.ms/wth)

**OBSERVAÇÃO:** Os alunos **não** devem receber um link para o repositório do What The Hack antes ou durante um hack. O guia do aluno **NÃO** contém links para o guia do instrutor nem para o repositório do What The Hack no GitHub.

### Pré-requisitos adicionais do instrutor

**O instrutor deve concluir o Desafio 06 (Token Golf) antes do hack:**

- Conclua você mesmo a tarefa de programação do Token Golf para estabelecer a pontuação "par"
- Documente seu gasto de créditos e as técnicas utilizadas
- Esse "par" se torna a referência que as equipes tentarão superar

**Prepare as ferramentas de medição:**

- Verifique a visibilidade dos tokens no painel Output do VS Code (GitHub Copilot Chat)
- Teste o acesso ao painel de uso do GitHub Copilot

## Requisitos do Azure

Este hack não exige recursos do Azure. Todo o trabalho é feito localmente com o GitHub Copilot no Visual Studio Code.

## Agenda sugerida para o hack

Este hack pode ser realizado como um evento de meio dia ou de um dia inteiro:

### Formato de meio dia (4 horas)
- Desafio 00: Pré-requisitos e linha de base (30 minutos)
- Desafio 01: Desenvolvimento orientado por especificações (45 minutos)
- Desafio 02: Engenharia de contexto (45 minutos)
- Desafio 03: Seleção de modelos e restrições de saída (45 minutos)
- Desafio 04: Configuração da sessão (30 minutos)
- Desafio 06: Competição de Token Golf (45 minutos)

### Formato de dia inteiro (6–7 horas)
- Desafio 00: Pré-requisitos e linha de base (45 minutos)
- Desafio 01: Desenvolvimento orientado por especificações (60 minutos)
- Desafio 02: Engenharia de contexto (60 minutos)
- Intervalo (15 minutos)
- Desafio 03: Seleção de modelos e restrições de saída (60 minutos)
- Desafio 04: Configuração da sessão (45 minutos)
- Desafio 05: Gerenciamento da janela de contexto (45 minutos)
- Intervalo (15 minutos)
- Desafio 06: Competição de Token Golf (60 minutos)
- Discussão final e estratégias vencedoras (30 minutos)

## Conteúdo do repositório

- `./Coach`
  - Guia do instrutor e arquivos relacionados
- `./Coach/Solutions`
  - Arquivos de solução com exemplos de medições e técnicas para cada desafio
- `./Student`
  - Guia de desafios do aluno
- `./Student/Resources`
  - Base de código inicial, tarefa da linha de base e especificação do Token Golf (devem ser empacotadas pelo instrutor e fornecidas aos alunos no início do evento)

- Recursos do Azure que serão consumidos por um aluno ao implementar os desafios do hack
- Permissões do Azure necessárias para que um aluno conclua os desafios do hack.

## Agenda sugerida para o hack (opcional)

_Esta seção é opcional. Você pode fornecer uma estimativa de quanto tempo cada desafio deve levar para um grupo médio de alunos concluir e/ou uma proposta de quantos desafios um instrutor deve incluir em cada sessão de um evento de hack com várias sessões. Por exemplo:_

- Exemplo de dia 1
  - Desafio 1 (1 hora)
  - Desafio 2 (30 minutos)
  - Desafio 3 (2 horas)
- Exemplo de dia 2
  - Desafio 4 (45 minutos)
  - Desafio 5 (1 hora)
  - Desafio 6 (45 minutos)

## Conteúdo do repositório

_Os arquivos e pastas padrão estão listados abaixo. Você pode ampliar esta lista se quiser especificar o conteúdo de subpastas adicionais que criar._

- `./Coach`
  - Guia do instrutor e arquivos relacionados
- `./Coach/Solutions`
  - Arquivos de solução com exemplos completos de respostas a um desafio
- `./Student`
  - Guia de desafios do aluno
- `./Student/Resources`
  - Arquivos de recursos, código de exemplo, scripts etc. destinados aos alunos. (Devem ser empacotados pelo instrutor e fornecidos aos alunos no início do evento)
