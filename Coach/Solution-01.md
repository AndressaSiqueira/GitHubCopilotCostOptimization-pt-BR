# Desafio 01 - Desenvolvimento orientado por especificações com Spec Kit - Guia do instrutor

[< Solução anterior](./Solution-00.md) - **[Início](./README.md)** - [Próxima solução >](./Solution-02.md)

# Guia do instrutor: prompt direto versus desenvolvimento orientado por especificações

## Objetivo

Este guia ajuda os instrutores a conduzir um experimento que compara duas maneiras de criar a mesma aplicação React e TypeScript com o GitHub Copilot:

1. Um prompt direto de implementação.
2. Uma especificação estruturada em Markdown usando desenvolvimento orientado por especificações (SDD).

O objetivo não é provar que uma abordagem é universalmente melhor. Os participantes devem observar como o contexto influencia o tempo de implementação, o consumo de créditos, as interrupções, as intervenções, o retrabalho e a aplicação entregue.

## Resultados de aprendizagem

Ao final da atividade, os participantes devem ser capazes de:

- Explicar o papel de uma especificação como contexto de implementação.
- Comparar o uso de prompts diretos e o SDD em condições equivalentes.
- Distinguir eficácia funcional de eficiência de implementação.
- Incluir a preparação da especificação ao avaliar a eficiência do ciclo completo.
- Discutir resultados experimentais sem generalizar a partir de uma única execução.

## Duração recomendada

| Atividade | Tempo sugerido |
|---|---:|
| Introdução e verificação do ambiente | 10 minutos |
| Implementação com prompt direto | 20–30 minutos |
| Implementação com SDD | 20–30 minutos |
| Comparação e discussão | 20 minutos |
| Total | 70–90 minutos |

Não imponha um limite de tempo de implementação se isso impedir os participantes de concluir e verificar manualmente a aplicação.

## Preparação do instrutor

Antes da sessão:

- Confirme que VS Code, Node.js, npm e GitHub Copilot estão disponíveis.
- Selecione um modelo do GitHub Copilot para usar nas duas execuções.
- Mantenha disponível o conteúdo fornecido de `sdd.md`.
- Prepare um cronômetro e uma planilha de medição.
- Garanta que os participantes possam consultar o consumo de créditos do Copilot.
- Peça aos participantes que fechem conversas e projetos não relacionados.
- Explique que arquivos gerados não podem ser reutilizados entre as execuções.

As pastas devem começar vazias. Estruturas iniciais, modelos ou arquivos existentes podem afetar a comparação e devem ser registrados caso sejam utilizados.

## Regras de equidade

O instrutor deve garantir os seguintes controles:

- Mesmo computador e ambiente.
- Mesmas versões do VS Code e do GitHub Copilot.
- Mesmo modelo do Copilot.
- Mesmo escopo da aplicação e checklist de verificação manual.
- Pastas vazias separadas e conversas novas.
- Nenhuma reutilização de código gerado entre as execuções.
- Nenhuma instrução adicional de implementação, a menos que seja necessária para desbloquear o progresso.
- Todo esclarecimento, correção ou intervenção deve ser registrado.

Não direcione o Copilot para uma escolha específica de framework, pacote, design de UI ou solução, a menos que o participante esteja travado. Qualquer ajuda desse tipo conta como uma intervenção.

## Fluxo de condução

### 1. Apresente o experimento

Explique que o experimento avalia três dimensões:

- **Eficácia:** se a aplicação atende aos requisitos.
- **Eficiência de implementação:** esforço após o prompt ou a especificação estar pronto.
- **Eficiência do ciclo completo:** esforço de implementação mais preparação da especificação.

Lembre aos participantes que um empate funcional ainda pode revelar diferenças de tempo, custo, ambiguidade e retrabalho.

### 2. Execute a abordagem de prompt direto

Antes de o participante enviar o prompt:

- Confirme que a pasta está vazia.
- Confirme que uma nova conversa do Copilot está aberta.
- Registre o modelo selecionado.
- Prepare o cronômetro.

Comece a cronometrar quando o prompt de implementação for enviado. Durante a execução, observe sem direcionar o participante.

Registre:

- Horários de início e término.
- Créditos consumidos.
- Perguntas feitas pelo Copilot.
- Decisões solicitadas sobre dependências ou ferramentas.
- Intervenções do participante.
- Erros, comandos que falharam e retrabalho.
- Qualquer funcionalidade adicionada além do escopo solicitado.

Pare de cronometrar somente depois que a aplicação estiver em execução e todo o checklist manual tiver sido concluído.

### 3. Execute a abordagem SDD

Antes da segunda execução:

- Confirme que está sendo usada outra pasta vazia.
- Crie o `sdd.md` fornecido na raiz do projeto.
- Abra uma nova conversa do Copilot.
- Selecione o mesmo modelo.
- Verifique que nenhum arquivo da primeira implementação foi reutilizado.

Comece a cronometrar quando o participante enviar a instrução para ler e implementar `sdd.md`.

Aplique as mesmas regras de observação e encerramento utilizadas na execução com prompt direto. Não atribua mérito à implementação SDD por funcionalidades adicionais que não foram exigidas pela especificação.

### 4. Realize a verificação manual

Use exatamente o mesmo checklist para ambas as aplicações:

- [ ] Crie uma nota com título e conteúdo.
- [ ] Crie uma nota sem conteúdo.
- [ ] Rejeite a criação quando o título estiver vazio ou contiver apenas espaços em branco.
- [ ] Exiba todas as notas criadas durante a sessão.
- [ ] Atualize o título e o conteúdo de uma nota existente.
- [ ] Rejeite uma atualização com título vazio.
- [ ] Atualize sem criar uma nota duplicada.
- [ ] Exclua uma nota existente.
- [ ] Confirme que a nota excluída desaparece.
- [ ] Recarregue a página e confirme que as notas podem ser perdidas.
- [ ] Confirme que nenhum backend, banco de dados ou armazenamento persistente é utilizado.
- [ ] Confirme que nenhum teste automatizado foi adicionado.

Registre falhas e correções em vez de corrigi-las silenciosamente.

## Definições de medição

Use definições consistentes nas duas execuções:

- **Pergunta:** o Copilot solicita explicitamente uma informação ou decisão.
- **Interrupção:** o progresso é pausado porque uma contribuição do participante é necessária.
- **Intervenção:** o participante fornece uma correção, instrução adicional, comando ou alteração de código.
- **Erro:** uma falha de build, execução, dependência ou funcionalidade.
- **Retrabalho:** trabalho necessário para corrigir um resultado ausente ou incorreto.
- **Tempo de implementação:** tempo entre o envio da instrução de implementação e o momento em que a aplicação está em execução e passa na verificação manual.
- **Custo de preparação da especificação:** tempo e créditos utilizados para escrever ou refinar a especificação, excluindo a implementação.

Se a especificação foi fornecida pronta, registre separadamente seu custo conhecido de preparação. Se esse custo não estiver disponível, marque-o como “não medido” em vez de tratá-lo como zero.

## Planilha de resultados

| Aspecto | Prompt direto | SDD com especificação pronta |
|---|---:|---:|
| Modelo utilizado | | |
| Tempo de implementação | | |
| Créditos de implementação | | |
| Perguntas feitas | | |
| Interrupções | | |
| Intervenções do usuário | | |
| Erros | | |
| Ações de retrabalho | | |
| Requisitos atendidos | /12 | /12 |
| Funcionalidades fora do escopo | | |
| Pontuação qualitativa de UX | /5 | /5 |

Registre a preparação do SDD separadamente:

| Métrica da especificação | Resultado |
|---|---:|
| Tempo de preparação | |
| Créditos de preparação | |
| Número de revisões | |

Calcule os valores do ciclo completo do SDD como:

$$
T_{\mathrm{SDD\ total}}
=
T_{\mathrm{especificação}}
+
T_{\mathrm{implementação}}
$$

$$
C_{\mathrm{SDD\ total}}
=
C_{\mathrm{especificação}}
+
C_{\mathrm{implementação}}
$$

## Orientações qualitativas de UX

Para reduzir a subjetividade, pontue ambas as aplicações de 1 a 5 usando os mesmos critérios:

- Clareza do formulário e das ações.
- Feedback de validação.
- Legibilidade das notas.
- Facilidade de encontrar as ações de editar e excluir.
- Consistência e usabilidade gerais.

O refinamento visual é secundário. Ele não deve compensar requisitos funcionais ausentes.

## Perguntas para a discussão final

Pergunte aos participantes:

1. Ambas as aplicações atenderam aos mesmos requisitos?
2. Qual abordagem exigiu mais decisões durante a implementação?
3. Quais ambiguidades apareceram na execução com prompt direto?
4. O SDD eliminou a ambiguidade ou transferiu as decisões para a preparação da especificação?
5. Qual abordagem usou menos tempo de implementação e menos créditos?
6. A conclusão muda quando a preparação da especificação é incluída?
7. Qual conteúdo da especificação teve o maior impacto na implementação?
8. Quais partes da especificação poderiam ser reutilizadas?
9. Como uma aplicação maior poderia mudar o resultado?
10. Como alterações posteriores nos requisitos poderiam afetar cada abordagem?

## Notas para o instrutor

Evite anunciar um vencedor esperado. Resultados válidos comuns incluem:

- Ambas as abordagens entregam aplicações equivalentes.
- O SDD reduz interrupções, mas custa mais no total para uma aplicação pequena.
- O prompt direto é mais rápido, mas exige mais decisões ou correções.
- A especificação estruturada melhora a consistência sem reduzir créditos.
- A variação natural do modelo supera a diferença entre as abordagens.

Trate cada resultado como uma observação, não como prova. Incentive os participantes a descrever o que aconteceu, identificar fatores que contribuíram e declarar as limitações do experimento.

## Critérios de conclusão

O desafio está concluído quando:

- Ambas as aplicações foram criadas de forma independente.
- Ambas foram avaliadas com o mesmo checklist.
- Todas as medições e intervenções foram registradas.
- Os custos de implementação e de preparação da especificação permanecem separados.
- Os participantes conseguem explicar as vantagens, desvantagens e limitações observadas.
