# Desafio 05 - Gerencie o contexto durante uma sequência de funcionalidades

[< Desafio anterior](./Challenge-04.md) - **[Início](../README.md)** - [Próximo desafio >](./Challenge-06.md)

## O que você vai aprender

Uma conversa de desenvolvimento acumula requisitos, decisões, código e resultados de ferramentas. Parte desse histórico continua útil; outra parte pode deixar de contribuir para a próxima tarefa.

Neste desafio, você vai implementar a mesma sequência de funcionalidades do CityScout NYC de duas formas: mantendo uma conversa contínua e gerenciando ativamente o contexto.

Ao final, você deverá conseguir:

- Escolher pontos de parada entre funcionalidades.
- Preservar decisões importantes ao resumir ou iniciar outra conversa.
- Comparar consumo e retrabalho sem reutilizar a implementação de uma execução na outra.
- Verificar se uma mudança de contexto preservou os contratos da aplicação.

> **Ideia central:** contexto menor só é uma vantagem quando a próxima etapa continua recebendo os requisitos e as evidências de que precisa.

## Antes de começar

1. Conclua o [Desafio 02](./Challenge-02.md) e o [Desafio 04](./Challenge-04.md).
2. Use a aplicação em [Resources/Challenge-02-NYCApp](./Resources/Challenge-02-NYCApp), com a rota de eventos do Desafio 02 implementada.
3. Tenha um ambiente de validação comum às duas execuções.

O material inicial contém dados e rotas, mas não inclui manifesto de dependências nem servidor completo. Antes de medir, peça ao instrutor a base executável ou prepare uma única base com as dependências, a montagem das três rotas e os comandos de execução e testes documentados.

Essa preparação não deve implementar as funcionalidades abaixo. Registre seu consumo separadamente e use a mesma base pronta nas duas execuções.

### Preserve um ponto de partida comum

- Guarde uma cópia da base concluída, incluindo instruções e dependências.
- Crie duas cópias independentes: **A** e **B**.
- Não copie código, resumos de implementação ou correções de A para B.
- Use o mesmo modelo, ferramentas, instruções iniciais e critérios de aceitação.
- Mantenha o código de cada execução separado; iniciar uma conversa nova não desfaz arquivos.

> Ao contrário do Desafio 02, agora você **pode alterar as três rotas**. Também poderá acrescentar o campo de associação aos dados de restaurantes e atualizar as instruções afetadas pelos novos contratos. Não descarte seu trabalho anterior para reiniciar o experimento.

---

## Parte 1 - Entenda a sequência de funcionalidades

Implemente as quatro funcionalidades abaixo, na mesma ordem, em A e em B. As regras já estão definidas para reduzir diferenças causadas por decisões de produto.

### Funcionalidade 1 - Filtre restaurantes

Adicione filtros a `GET /restaurants`:

- Aceite `borough` e `cuisine`.
- Compare os valores completos, ignorando diferenças entre maiúsculas e minúsculas e espaços nas extremidades.
- Quando ambos forem enviados, aplique os dois filtros.
- Sem filtros, retorne todos os restaurantes.
- Sem correspondências, retorne uma lista vazia, não `404`.

Exemplo:

```text
/restaurants?borough=Brooklyn&cuisine=Mexican
```

Com os dados originais, esse filtro deve selecionar apenas `Williamsburg Tacos`.

### Funcionalidade 2 - Consulte um bairro e seus restaurantes

Adicione `GET /neighborhoods/:name`.

- Busque o nome completo do bairro com a mesma normalização de texto dos filtros.
- Retorne `{ neighborhood, restaurants }`, em que `neighborhood` é o objeto encontrado.
- Se o bairro não existir, retorne `404`.
- Se existir sem restaurantes associados, retorne `200` com `restaurants: []`.

**Atenção à associação:** os restaurantes originais têm apenas `borough`, que representa uma região maior, não o bairro. Não associe todos os restaurantes de Manhattan a West Village.

Acrescente o campo `neighborhood` aos dois restaurantes:

| Restaurante | Valor de `neighborhood` |
|---|---|
| West Village Pasta | West Village |
| Williamsburg Tacos | Williamsburg |

Use esse campo para relacionar restaurantes e bairros, preservando os demais dados.

### Funcionalidade 3 - Padronize a paginação das listagens

Adicione `page` e `limit` a:

- `GET /events/free-this-week`
- `GET /restaurants`
- `GET /neighborhoods`

Regras:

- Use `page=1` e `limit=10` quando os parâmetros estiverem ausentes.
- Aceite apenas inteiros positivos representados por dígitos, dentro do intervalo seguro de inteiros do JavaScript.
- Aplique filtros e ordenação **antes** da paginação.
- Preserve a ordem original dos dados nas listagens de restaurantes e bairros.
- Preserve a filtragem de eventos gratuitos, o intervalo de datas e a ordem cronológica do Desafio 02.
- `total` deve contar todos os resultados filtrados, antes do recorte da página.
- Uma página além dos resultados deve retornar `200` com `data: []`.

Todas as listagens devem retornar:

```json
{
  "page": 1,
  "limit": 10,
  "total": 2,
  "data": []
}
```

O exemplo ilustra o formato; os itens de `data` dependem da consulta.

> **Mudança intencional de contrato:** a rota de eventos passa de `{ count, events }` para `{ page, limit, total, data }`. Atualize instruções e testes que ainda exijam o formato antigo. A rota de detalhe do bairro mantém `{ neighborhood, restaurants }` e não recebe paginação.

### Funcionalidade 4 - Valide entradas e padronize erros

Use estas regras em todas as rotas do exercício:

- `page` e `limit` inválidos, vazios ou repetidos: `400`.
- `borough` e `cuisine` vazios ou que não sejam valores de texto únicos: `400`.
- Parâmetros de consulta não suportados pela rota: `400`.
- Nome de bairro inexistente: `404`.
- Rota inexistente: `404`.
- Listagem válida sem resultados: `200`, nunca `404`.

Os parâmetros permitidos são `page` e `limit` nas três listagens, mais `borough` e `cuisine` na listagem de restaurantes. A rota de detalhe não aceita parâmetros de consulta.

Padronize os erros:

```json
{
  "error": {
    "code": "INVALID_QUERY",
    "message": "Descrição clara do parâmetro inválido."
  }
}
```

Use `NOT_FOUND` para os erros `404`. Não exponha stack traces. O tratamento de rota inexistente deve ficar depois da montagem das rotas no servidor preparado.

---

## Parte 2 - Defina como verificar cada entrega

Use a mesma lista em A e B. Execute a validação após cada funcionalidade e repita os casos anteriores para detectar regressões.

| Caso | Resultado esperado |
|---|---|
| `/restaurants?borough=brooklyn&cuisine=Mexican` | Apenas Williamsburg Tacos |
| `/restaurants?cuisine=Thai` | Lista vazia, com status `200` |
| `/neighborhoods/West%20Village` | Bairro West Village e apenas seu restaurante associado |
| `/neighborhoods/BairroInexistente` | `404` com `NOT_FOUND` |
| `/restaurants?page=1&limit=1` | `page: 1`, `limit: 1`, `total: 2` e um item em `data` |
| `/restaurants?borough=Brooklyn&page=1&limit=1` | `total: 1` e Williamsburg Tacos |
| `/neighborhoods?page=99&limit=10` | `200`, `total: 2` e `data: []` |
| `/events/free-this-week?page=1&limit=1` | `total: 2` e Central Park Yoga na primeira página, com os dados originais |
| `/restaurants?page=0`, `?page=abc` ou `?limit=` | `400` com `INVALID_QUERY` |
| `/restaurants?page=1&page=2` ou `?borough=` | `400` com `INVALID_QUERY` |
| `/neighborhoods?cuisine=Mexican` | `400` com `INVALID_QUERY` |
| Uma rota inexistente | `404` com `NOT_FOUND` |

Nos casos sem parâmetros de paginação, use o formato vigente na etapa: a partir da Funcionalidade 3, as listagens retornam o envelope paginado.

Registre os comandos reais de execução e testes da sua base. Uma revisão de código sem execução pode ser útil, mas não deve ser apresentada como evidência de que os endpoints responderam corretamente.

---

## Parte 3 - Execute A: uma conversa contínua

1. Abra a cópia A e comece uma conversa nova.
2. Forneça a especificação das quatro funcionalidades e a lista de verificação.
3. Peça a implementação de uma funcionalidade por vez.
4. Ao final de cada uma, valide, corrija os problemas necessários e registre o consumo.
5. Continue na mesma conversa, sem solicitar compactação manual ou limpar o histórico.

Não provoque falhas nem acrescente mensagens inúteis para aumentar o contexto. Se o cliente compactar automaticamente, registre o ocorrido: “sem compactação manual” não significa “sem gerenciamento automático”.

Observe possíveis sinais de perda de continuidade:

- Esquecimento do contrato de paginação.
- Associação incorreta entre bairro e região.
- Reintrodução de um erro já corrigido.
- Perguntas sobre decisões que já estavam definidas.

Esses sinais podem não ocorrer. Registre o comportamento real, inclusive quando a qualidade permanecer estável.

## Parte 4 - Execute B: gerenciamento proativo

1. Abra a cópia B, ainda no ponto de partida comum.
2. Comece uma conversa nova com a mesma especificação e lista de verificação.
3. Implemente e valide as funcionalidades na mesma ordem.
4. Nos pontos de parada, escolha se vale manter, compactar ou iniciar outra conversa.
5. Registre cada ação e inclua seu consumo no total de B.

### Escolha a ação pelo que você precisa preservar

| Ação | Quando pode ajudar | Cuidado |
|---|---|---|
| Continuar na conversa | A próxima mudança depende de detalhes recentes | O histórico continua crescendo |
| Compactar, se disponível | Há decisões importantes a preservar e histórico excessivo | O resumo pode perder detalhes e sua geração tem consumo |
| Iniciar outra conversa | Há uma entrega concluída e verificável | É preciso reapresentar decisões e localizar o estado do código |
| Limpar o histórico, se disponível | Você quer descartar o contexto da conversa atual | Isso não restaura arquivos nem garante menor custo total |

Comandos como `/compact`, `/clear` ou `/new` dependem do cliente, modo e versão. Confira os comandos disponíveis ao digitar `/` e use o controle equivalente da interface quando necessário.

### Faça uma passagem de contexto curta e verificável

Antes de trocar de conversa, prepare um resumo com:

```text
Concluído e validado:
- Funcionalidade:
- Arquivos alterados:
- Comando de teste e resultado:

Contratos e decisões que continuam obrigatórios:
- Formato das respostas:
- Associação entre bairros e restaurantes:
- Regras de validação:

Próxima tarefa:
- Funcionalidade:
- Arquivos que precisam ser consultados:
- Pendências conhecidas:
```

Use apenas informações da própria execução B. Anexe os arquivos necessários para que a nova conversa confira o resumo no código.

---

## Parte 5 - Compare consumo, qualidade e retrabalho

Registre os dados após cada funcionalidade, incluindo as correções necessárias:

| Execução | Funcionalidade | Ação de contexto | Consumo da etapa e unidade | Testes passaram? | Correções ou regressões observadas |
|---|---|---|---|---|---|
| A | 1 | Conversa contínua | | | |
| A | 2 | Conversa contínua | | | |
| A | 3 | Conversa contínua | | | |
| A | 4 | Conversa contínua | | | |
| B | 1 | | | | |
| B | 2 | | | | |
| B | 3 | | | | |
| B | 4 | | | | |

Some todas as sessões, resumos e tentativas de cada execução. Se registrar valores acumulados na interface, calcule o consumo de cada etapa pela diferença entre os valores inicial e final; não some os acumulados.

| Comparação | A | B |
|---|---|---|
| Créditos totais atribuíveis ao experimento, se disponíveis | | |
| Tempo total, incluindo validação e correções | | |
| Quantidade de correções ou regressões | | |
| Todos os critérios passaram? | | |

Não confunda ocupação da janela de contexto com créditos ou tokens faturados. Se não houver métricas individualizadas, registre **“não disponível”** e analise qualidade, continuidade e retrabalho.

B pode consumir menos, igual ou mais que A. Explique o resultado, sem exigir uma economia que não foi observada. Uma única comparação também não demonstra que o tamanho do histórico causou os problemas encontrados.

## Critérios de sucesso

- [ ] Usei duas cópias da mesma base executável, sem transferir a implementação entre elas.
- [ ] Implementei as quatro funcionalidades na mesma ordem.
- [ ] Criei a associação explícita por bairro, sem usar apenas `borough`.
- [ ] Atualizei o contrato de paginação e as instruções afetadas.
- [ ] Validei os mesmos casos em A e B, incluindo erros e regressões.
- [ ] Registrei ações de contexto, correções, consumo disponível e limitações.
- [ ] Incluí resumos e novas sessões no total da execução B.
- [ ] Comparei os resultados sem exigir degradação em A ou economia em B.

## Perguntas para reflexão

1. Em que ponto mudar de conversa ajudou ou atrapalhou?
2. Qual informação importante quase se perdeu na passagem de contexto?
3. O custo de resumir compensou a redução de histórico?
4. Que estratégia você adotaria em uma próxima sequência de funcionalidades?

## Recursos de aprendizagem

- [Conceitos de contexto em agentes](https://code.visualstudio.com/docs/agents/concepts/context)
- [Gerenciamento de sessões no VS Code](https://code.visualstudio.com/docs/agents/run/sessions/manage-sessions)
- [Adição de contexto ao chat](https://code.visualstudio.com/docs/chat/copilot-chat-context)
