# Desafio 02 - Engenharia de contexto - Guia do instrutor

[< Solução anterior](./Solution-01.md) - **[Início](./README.md)** - [Próxima solução >](./Solution-03.md)

## Notas e orientações

Este desafio ensina aos alunos que o contexto persistente tem custos recorrentes. O objetivo é minimizar a sobrecarga permanente enquanto se mantém a qualidade por meio de instruções com escopo definido e anexos precisos.

### Conceitos principais a explicar

**Os três tipos de custos de contexto:**

1. **Instruções persistentes (custo recorrente):**
   - `.github/copilot-instructions.md` é carregado em TODA interação
   - Exemplo: arquivo global de 1500 tokens = 1500 tokens × cada chamada de chat/edição
   - Meta: manter as instruções globais abaixo de 500–1000 tokens

2. **Skills do GitHub Copilot (custo condicional):**
   - Só são carregadas quando invocadas explicitamente
   - Exemplo: `@workspace /new` só carrega modelos de criação quando chamado
   - Mais adequadas para: padrões específicos de tarefas que não se aplicam a todo o trabalho

3. **Anexos (custo por chamada):**
   - Você controla exatamente o que é incluído a cada vez
   - Exemplo: `#file:src/api/routes.ts` só é carregado quando você o anexa
   - `#Codebase` pode trazer milhares de tokens desnecessários

### Parte A: estratégia de definição de escopo das instruções

**Processo de auditoria:**

Ajude os alunos a categorizar suas instruções inchadas:

- **Manter globais (menos de 500 tokens):**
  - Preferências de estilo de código que se aplicam universalmente (por exemplo, "prefira padrões funcionais")
  - Padrões de qualidade (por exemplo, "sempre trate erros explicitamente")
  - Convenções de toda a organização

- **Mover para instruções específicas por linguagem:**
  - `.github/copilot-instructions-python.md` para regras exclusivas de Python
  - `.github/copilot-instructions-typescript.md` para regras exclusivas de TypeScript
  - Elas só são carregadas ao trabalhar nessa linguagem

- **Mover para instruções específicas por caminho:**
  - `src/api/.github/copilot-instructions.md` para padrões específicos de API
  - `tests/.github/copilot-instructions.md` para convenções de testes
  - Elas só são carregadas ao trabalhar nesse diretório

- **Converter em skills:**
  - Modelos específicos de tarefas (por exemplo, "como escrever uma migração")
  - Padrões condicionais (por exemplo, "ao adicionar um novo modelo, faça X")

**Economia esperada:**

- Antes: ~1500 tokens por interação (instruções globais)
- Depois: ~400 tokens globais + ~200 tokens com escopo definido (somente quando dentro do escopo)
- Resultado: redução de 60–70% na sobrecarga das instruções na maioria das interações

### Parte B: precisão dos anexos

**Antipadrão comum:**

```
Prompt: "Refatore a lógica de autenticação"
Anexos: #Codebase
```
Isso traz tudo — potencialmente mais de 50.000 tokens para um repositório grande.

**Padrão otimizado:**

```
Prompt: "Refatore a lógica de autenticação"
Anexos:
  - #file:src/auth/middleware.ts:1-50
  - #file:src/auth/types.ts
  - #file:tests/auth.test.ts
```
Isso traz exatamente o que é necessário — talvez 500 tokens.

**Exercício de demonstração:**

Peça aos alunos que concluam a mesma refatoração duas vezes:
1. Com `#Codebase` (registre a contagem de tokens do painel Output)
2. Com arquivos fixados (registre a contagem de tokens)

Resultados típicos: mais de 10.000 tokens → 800 tokens (redução superior a 90%)

### Obstáculos comuns

**Os alunos não sabem o que manter global:**

Regra prática: se uma regra só se aplica a 20% da sua base de código, ela não deve ser global.

**Instruções específicas por caminho não são carregadas:**

O GitHub Copilot percorre a árvore de diretórios em direção à raiz procurando arquivos `.github/copilot-instructions.md`. Garanta que:
- A estrutura de diretórios esteja correta
- O arquivo tenha exatamente o nome `.github/copilot-instructions.md` (não `.github/copilot-instructions-api.md` na pasta api)

**Não é possível medir a redução de tokens:**

- O painel Output do VS Code (View → Output → "GitHub Copilot Chat") mostra as contagens de tokens
- Se não estiverem visíveis, atualize a extensão do GitHub Copilot para a versão mais recente

### Tempo esperado

60 minutos no total:
- 20 minutos: auditoria e categorização das instruções globais
- 20 minutos: reestruturação em arquivos com escopo definido
- 20 minutos: teste da precisão dos anexos e medição da economia

### Validação dos critérios de sucesso

Os alunos devem demonstrar:
- `.github/copilot-instructions.md` global reduzido para menos de 500 tokens
- Pelo menos um arquivo de instruções específico por caminho ou linguagem criado
- Comparação de tokens mostrando a economia de anexos fixados versus `#Codebase`
- Mesma tarefa da linha de base concluída com custo reduzido em créditos

### Dicas para compartilhar

- Comece perguntando: "Esta regra se aplica a TODO código que escrevo?" Se não, defina seu escopo
- Use arquivos específicos por linguagem para regras de linting/formatação que variam conforme a linguagem
- Use arquivos específicos por caminho para padrões arquiteturais (por exemplo, convenções de API em `src/api/`)
- Fixe arquivos quando souber exatamente do que precisa; use `#Codebase` apenas para descoberta
- O objetivo não é ter zero instruções — é ter instruções do tamanho certo

### Soluções de referência

Reestruturação típica:

**Antes (1500 tokens globais):**
```
.github/copilot-instructions.md (todas as regras)
```

**Depois (400 tokens globais + instruções com escopo definido):**
```
.github/copilot-instructions.md (regras universais, ~400 tokens)
.github/copilot-instructions-python.md (específicas de Python, ~300 tokens)
.github/copilot-instructions-typescript.md (específicas de TypeScript, ~250 tokens)
src/api/.github/copilot-instructions.md (padrões de API, ~200 tokens)
```

Os alunos que trabalham em `src/api/*.ts` agora carregam: 400 + 250 + 200 = 850 tokens (versus 1500 antes)
