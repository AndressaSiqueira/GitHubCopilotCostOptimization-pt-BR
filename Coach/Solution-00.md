# Desafio 00 - Pré-requisitos e linha de base - Guia do instrutor

**[Início](./README.md)** - [Próxima solução >](./Solution-01.md)

## Notas e orientações

Este desafio estabelece a linha de base de medição com a qual todos os desafios seguintes serão comparados. Os alunos devem ser capazes de acompanhar o consumo de créditos com precisão antes de otimizar.

### Conceitos principais a explicar

**Fundamentos da cobrança baseada em uso (UBB):**
- Custo em créditos = (tokens de entrada × tarifa de entrada) + (tokens de saída × tarifa de saída)
- Modelos diferentes têm tarifas diferentes (a diferença entre a classe Sonnet/GPT-4 e a classe Haiku pode ser de 10x)
- O painel Output do VS Code mostra o detalhamento dos tokens por interação
- O painel de uso do GitHub Copilot mostra o gasto acumulado

**Objetivo da linha de base:**
- Estabelece a medição do "antes" para todas as técnicas de otimização
- Os alunos devem usar seu fluxo de trabalho natural — sem otimização ainda
- Documente a abordagem (conclusões inline, frequência do chat, referências do workspace utilizadas)
- Esta linha de base provavelmente será ineficiente — isso é intencional

### Obstáculos comuns

**UBB não habilitada:**
- Algumas organizações ainda podem usar cobrança por assento
- Os alunos precisam de acesso de administrador ou devem coordenar com o administrador de cobrança
- Alternativa: o instrutor pode fornecer dados de exemplo da linha de base se a UBB não estiver disponível

**Problemas de visibilidade dos tokens:**
- O painel Output do VS Code deve ser configurado para mostrar os logs do GitHub Copilot Chat
- Alguns alunos podem não ver as contagens de tokens se estiverem usando uma versão antiga da extensão do Copilot
- Solução: atualize a extensão do GitHub Copilot para a versão mais recente

**Seleção da tarefa da linha de base:**
- A tarefa não deve ser trivial (10–20 minutos de desenvolvimento)
- A tarefa deve poder ser concluída de várias maneiras (deixa espaço para otimização)
- Tarefas sugeridas para a linha de base:
  - Implemente um endpoint de API REST com validação e tratamento de erros
  - Adicione um middleware de autenticação a um serviço existente
  - Refatore um módulo para usar injeção de dependência

### Tempo esperado

45 minutos no total:
- 15 minutos: configuração do ambiente e verificação da UBB
- 20 minutos: conclusão da tarefa de programação da linha de base
- 10 minutos: documentação das medições e da abordagem

### Validação dos critérios de sucesso

Os alunos devem demonstrar:
- Captura de tela ou compartilhamento de tela do painel Output do VS Code mostrando as contagens de tokens
- Captura de tela do painel de uso do GitHub Copilot mostrando o saldo atual de créditos
- Código da tarefa da linha de base concluído (não precisa ser perfeito)
- Documentação escrita: total de créditos consumidos, funcionalidades utilizadas e abordagem adotada

### Dicas para compartilhar

- Não otimize ainda! Use seu fluxo de trabalho natural
- Documente tudo — esta é a sua fotografia do "antes"
- Se os créditos parecerem surpreendentemente altos, isso é normal e esperado
- Acompanhe não apenas o total de créditos, mas também quais interações custaram mais
- Observação: conclusões inline normalmente são muito mais baratas por interação do que chat/edições

### Medições de referência

Medições típicas da linha de base para uma tarefa de programação de 15–20 minutos:
- Sem otimização: 50–80 créditos (usando um modelo da classe GPT-4, chat prolixo e referências amplas)
- Esperado após a otimização: 10–20 créditos (instruções direcionadas, modelo eficiente e anexos fixados)

### Recursos adicionais para o instrutor

- Garanta que Resources.zip contenha `baseline-task.md` com requisitos claros
- Considere fornecer uma implementação de referência para equipes que ficarem travadas
- Tenha exemplos de detalhamento de tokens prontos para compartilhar caso os alunos não consigam ver os próprios
