# Desafio 03 — Pendências de autoria e itens adiados

Notas para instrutores/autores. O desafio está completo e pode ser executado. Este documento
acompanha os próximos passos.

## Concluído (nesta revisão)
- [x] **Substituímos a tarefa difícil** de contagem de letras → **lava-rápido** ("caminhar
      ou dirigir 40 m para lavar meu carro"). A contagem de letras era um artefato de
      tokenização cujos resultados **não** acompanhavam o preço (o modelo base podia
      superar o premium — observamos Haiku acertar / Opus errar). O lava-rápido acompanha
      a capacidade e é monotônico. Veja `results.md`.
- [x] **Trocamos o par base/premium** por modelos selecionáveis no Copilot. O antigo
      `gpt-4.1-nano` falhava consistentemente na tarefa difícil, mas **não é selecionável
      no seletor de modelos do Copilot**, então os alunos não podiam usá-lo. Novo par:
      base `gpt-4.1`, premium `gpt-5`.
- [x] **Terminologia:** removemos "barato/caro"; agora usamos **modelo base** /
      **modelo premium** (compatível com a linguagem de cobrança do Copilot para
      requisições incluídas versus premium).
- [x] **Aprofundamento:** raciocínio sobre custo de novas tentativas na Parte 2 ("quantas
      tentativas base superam uma chamada premium?" + limite de capacidade); Parte 4
      "classifique suas próprias tarefas"; um parágrafo sobre "por que isso importa
      para programação"; uma observação sobre variação de tokens.
- [x] **Seção de restrição de saída** refeita com uma tarefa verbosa (função de palíndromo,
      190→66 tokens no gpt-4.1) — o antigo exemplo de ordenação de versões não mostrava redução.

## Em aberto
- [ ] **Alinhamento da medição de tokens (todo o workshop).** Os documentos dos alunos
      apontam para `View → Output → "GitHub Copilot Chat"` / visualização de uso para
      contagem de tokens, conforme a configuração do Desafio 00. Verificar se o Copilot
      Chat realmente exibe uma contagem clara por requisição na versão-alvo do VS Code/Copilot.
      Caso **não** exiba, isso é um problema do **Desafio 00**, que afeta todos os desafios —
      corrigir ali (ou padronizar uma fonte de tokens), não apenas no Desafio 03.
      A ferramenta de medição dos instrutores e o playground do GitHub Models são alternativas confiáveis.
- [ ] **Seção avançada (opcional).** Adicionar um bloco de "Desafios avançados": testar
      um modelo intermediário / de raciocínio na tarefa difícil (onde está o melhor
      equilíbrio preço/capacidade?); criar um fluxo com dois modelos, "base cria rascunho →
      premium revisa", e medir o custo total.
- [ ] **Decisão de escopo — níveis de raciocínio e modo Auto.** O Desafio 03 *original*
      incluía comparar níveis de esforço de raciocínio e explicar quando o **modo Auto**
      supera a seleção manual. Decidir se isso deve voltar como opcional/avançado.
      Exige aprovação do responsável.

## Dados validados (base do gabarito)

Medidos pela API do GitHub Models (`harness.py`), uma única resposta por tentativa,
sem novas tentativas, n=4:

| Modelo | Fácil (ordenação de versões) | Difícil (lava-rápido) |
|---|---|---|
| gpt-4.1 (base) | ✅ 4/4, ~106 tokens | ❌ 0/4 — diz "ir a pé", ~166 tokens |
| gpt-5 (premium) | ✅ 4/4, ~293 tokens | ✅ 4/4 — diz "dirigir", ~1000 tokens |

Restrição de saída (gpt-4.1, função de palíndromo): ~190 → ~66 tokens = **−65%**, código idêntico.
A restrição **não** teve efeito na tarefa concisa de ordenação nem no gpt-5 (tokens de
raciocínio predominam).

Descartados: contagem de letras/decimais/"strawberry" (artefatos de tokenização — não
acompanham o preço); `ministral-3b` (também falha na tarefa fácil); `gpt-4.1-nano`
(não está no seletor do Copilot); armadilha gulosa do troco (modelos pequenos modernos acertam).

**Nota da tradução:** os dados acima foram preservados da versão original em inglês;
não foram medidos novamente com os prompts em português.
