<!--
# Instruções do Copilot (INTENCIONALMENTE EXCESSIVAS)

- Sempre valide as entradas
- Sempre trate os erros
- Sempre use APIs REST
- Sempre use hooks do React
- Sempre otimize o desempenho
- Sempre escreva testes
- Sempre garanta a acessibilidade
- Sempre normalize o JSON
- Restaurantes devem incluir cuisine e borough
- Bairros devem incluir transit e vibe
- Eventos devem incluir filtragem por preço e data

# GRANDE DEMAIS DE PROPÓSITO -->
# Instruções do Copilot (INTENCIONALMENTE EXCESSIVAS)

## Regras gerais de engenharia
- Sempre escreva código limpo, de fácil manutenção, escalável e pronto para produção
- Sempre valide todas as entradas em cada camada da aplicação
- Sempre trate os erros adequadamente com mensagens de erro significativas
- Sempre use nomes descritivos para variáveis e funções
- Sempre inclua comentários explicando a lógica de negócio
- Evite lógica com muitos níveis de aninhamento sempre que possível
- Prefira componentes modulares e reutilizáveis
- Garanta que todo o código esteja otimizado para desempenho
- Evite cálculos e loops desnecessários
- Minimize o uso de memória e as chamadas de API

## Regras de design de APIs
- Use convenções RESTful para todos os endpoints
- Garanta nomes consistentes para os endpoints (substantivos no plural)
- Sempre retorne respostas JSON
- Sempre inclua códigos de status HTTP
- Valide todos os parâmetros de consulta e corpos de solicitação
- Use middleware para validação e tratamento de erros
- Retorne as respostas no formato:
  {
    "count": number,
    "data": []
  }
- Nunca exponha detalhes internos de implementação nas respostas

## Regras de frontend (NÃO RELEVANTES, MAS INCLUÍDAS)
- Use apenas componentes funcionais do React
- Prefira hooks a componentes de classe
- Use useEffect e useState adequadamente
- Garanta a acessibilidade (rótulos ARIA, navegação por teclado)
- Otimize o desempenho da renderização
- Use princípios de design responsivo
- Evite novas renderizações desnecessárias
- Garanta padrões de design de UI/UX limpos

## Regras de modelagem de dados
- Normalize as estruturas JSON
- Evite dados duplicados
- Use nomes consistentes de campos em todos os conjuntos de dados
- Prefira arrays de objetos para coleções
- Sempre use formatos de data ISO (YYYY-MM-DD)
- Evite valores null quando possível
- Garanta a compatibilidade retroativa das alterações de schema

## Regras do domínio de restaurantes (NÃO NECESSÁRIAS PARA EVENTOS)
- Restaurantes devem incluir:
  - name
  - borough
  - cuisine
  - rating
  - priceLevel
- Inclua indicadores de opções adequadas para vegetarianos
- Inclua informações sobre o bairro
- Inclua descrições da atmosfera (por exemplo, aconchegante, animada, romântica)
- Inclua estimativas de tempo de espera para locais populares

## Regras do domínio de bairros (NÃO NECESSÁRIAS PARA EVENTOS)
- Bairros devem incluir:
  - borough
  - vibe
  - opções de transporte
  - faixa média de aluguel
  - categorias bestFor
- Inclua informações sobre a facilidade de se locomover a pé
- Inclua a proximidade de parques, restaurantes e vida noturna
- Inclua considerações sobre segurança
- Use uma linguagem envolvente e descritiva

## Regras do domínio de eventos (REALMENTE RELEVANTES)
- Eventos devem incluir:
  - name
  - date
  - location
  - borough
  - price
- Eventos gratuitos devem ter price === 0
- Eventos devem ser filtrados por data quando necessário
- Eventos devem ser ordenados por data em ordem crescente
- Exclua eventos passados
- Garanta que os dados dos eventos estejam completos e válidos

## Regras de testes (NÃO UTILIZADAS NESTA TAREFA)
- Escreva testes unitários para a lógica de negócio
- Escreva testes de integração para os endpoints
- Simule dependências quando necessário
- Garanta uma cobertura de testes adequada (pelo menos 80%)
- Teste os casos extremos minuciosamente
- Valide os fluxos de tratamento de erros

## Regras de registro de logs e monitoramento
- Registre todas as ações importantes
- Registre os erros com rastreamentos de pilha (mas não nas respostas)
- Garanta que os logs sejam estruturados
- Inclua marcas de tempo nos logs
- Evite registrar dados sensíveis

## Regras de segurança
- Valide todas as entradas para prevenir ataques de injeção
- Higienize as entradas do usuário
- Evite expor segredos ou chaves
- Use variáveis de ambiente para a configuração
- Siga o princípio do menor privilégio

## Regras de conteúdo e tom de NYC
- Mantenha os exemplos divertidos e específicos de NYC
- Faça referência a locais como Central Park, Brooklyn, SoHo, Williamsburg
- Use descrições locais com as quais as pessoas possam se identificar
- Evite uma redação genérica ou sem graça
- Faça a aplicação parecer construída para um morador real de NYC

## Regras de otimização de desempenho
- Otimize os loops e a lógica de filtragem
- Evite cálculos redundantes
- Armazene os resultados em cache quando possível
- Minimize o consumo de memória
- Reduza chamadas de API desnecessárias

---

# ⚠️ ESTE ARQUIVO ESTÁ INTENCIONALMENTE SOBRECARREGADO

Ele inclui:
- ✅ regras relevantes (eventos)
- ❌ domínios irrelevantes (restaurantes, bairros)
- ❌ camadas não relacionadas (frontend, segurança, registro de logs, testes)

👉 Os alunos devem REDUZIR este arquivo drasticamente.
