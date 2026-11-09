# Desafio 05 - Gerenciamento da janela de contexto - Guia do instrutor

[< Solução anterior](./Solution-04.md) - **[Início](./README.md)** - [Próxima solução >](./Solution-06.md)

## Notas e orientações

Este desafio ensina o gerenciamento proativo do contexto em oposição à recuperação reativa. O maior custo evitável é deixar de executar `/compact` até que a deterioração do contexto já tenha degradado a qualidade.

### Conceitos principais a explicar

**Evolução da deterioração do contexto:**
- 0–60% da capacidade: a qualidade permanece alta
- 60–70% da capacidade: primeiros sinais de degradação (inconsistências)
- 70–85% da capacidade: perda perceptível de qualidade, requisitos esquecidos
- 85–100% da capacidade: degradação grave, ciclos de recuperação caros

**Dois comandos, objetivos diferentes:**
- `/compact`: resume o trabalho anterior, preserva o estado e preserva o cache (volante)
- `/clear`: apaga tudo, reinicia com cache frio (botão de reinicialização)

**Pontos naturais para compactação:**
- Funcionalidade concluída e testes passando
- Decisão de arquitetura tomada
- Mudança para um novo assunto/módulo
- Antes de o contexto atingir 60% de utilização

### Tempo esperado

45 minutos:
- 15 minutos: observação da deterioração do contexto (Parte A)
- 20 minutos: demonstração da compactação proativa (Parte B)
- 10 minutos: documentação das descobertas

### Validação dos critérios de sucesso

Os alunos devem demonstrar degradação mensurável da qualidade após 70% de utilização do contexto e mostrar economia de créditos com `/compact` proativo versus deixar o contexto se deteriorar.

### Dicas para compartilhar

- A utilização da janela de contexto fica visível na barra de status do VS Code ou no painel Output
- Execute `/compact` antes de sentir o problema, não depois
- Pontos naturais: "Acabei de concluir X, agora vou começar Y" — compacte na transição
- `/compact` preserva o cache; `/clear` força uma reinicialização a frio
- O custo não está em executar `/compact` com frequência demais — está em executá-lo tarde demais
