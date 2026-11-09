# Desafio 03 — Resultados medidos (gabarito)

Fonte: API de inferência do GitHub Models. Método: `harness.py`, **n=4 tentativas por
(modelo, tarefa)**, uma única resposta por tentativa (sem novas tentativas). A contagem exata
de tokens varia conforme a versão do modelo; o **padrão é estável.**

**Nota da tradução:** estas são as medições originais com prompts em inglês. Traduzir os
prompts pode alterar respostas, taxas de acerto e consumo de tokens; os valores abaixo não
foram medidos novamente em português.

Modelos usados como par de demonstração:
- **Base:** `openai/gpt-4.1` (nível incluído, sem multiplicador premium — selecionável no Copilot Chat)
- **Premium:** `openai/gpt-5` (nível de fronteira/raciocínio)

## Resumo

| Modelo | Tarefa | Taxa de acerto | Média total de tokens |
|---|---|---|---|
| `openai/gpt-4.1` (base) | ordenação (fácil) | **4/4 — 100%** | ~106 |
| `openai/gpt-4.1` (base) | lava-rápido (difícil) | **0/4 — 0%** (responde "ir a pé") | ~166 |
| `openai/gpt-5` (premium) | ordenação (fácil) | **4/4 — 100%** | ~293 |
| `openai/gpt-5` (premium) | lava-rápido (difícil) | **4/4 — 100%** (responde "dirigir") | ~1000 |

## Interpretação

- **Tarefa fácil (ordenação de versões):** ambos os modelos acertaram 100%. O modelo base
  produziu a mesma resposta usando **~2,8× menos tokens** (106 contra 293). Pagar pelo modelo
  premium aqui não traz benefício → **use o modelo base.**
- **Tarefa difícil (lava-rápido):** o modelo base recomendou **caminhar** em todas as tentativas —
  fixou-se nos "40 metros" e ignorou que o carro precisa estar *no* lava-rápido. O modelo premium
  raciocinou sobre o objetivo e respondeu **dirigir** todas as vezes. Repetir a chamada ao
  modelo base não resolve isso — é um limite de capacidade de raciocínio → **pague pela capacidade.**

## Verificação de monotonicidade (por que o lava-rápido, e não a contagem de letras)

Precisamos de uma tarefa cujo sucesso acompanhe a **capacidade** (e, portanto, o preço).
A tarefa do lava-rápido atende a isso; as "pegadinhas" de tokenização não. Exemplos medidos:

| Tarefa | gpt-4o-mini (base) | gpt-4.1 (base) | gpt-5 (premium) | Acompanha a capacidade? |
|---|---|---|---|---|
| Lava-rápido (caminhar/dirigir) | ❌ caminhar | ❌ caminhar | ✅ dirigir | ✅ sim — monotônico |
| Contagem de letras ("l" em "parallel lullaby") | variável | ✅ 6 | ✅ 6 | ❌ não — o base acerta |
| Contagem de letras (Claude, observado no Copilot) | Haiku ✅ | — | Opus ❌ | ❌ não — **inverte** |

A linha de contagem de letras explica por que a descartamos: um modelo base (Haiku) acertou
enquanto um modelo premium (Opus) errou — o oposto da lição. Contagem de letras, comparação
de decimais e tarefas do tipo "strawberry" são artefatos de tokenização e não devem ser usados aqui.

## Restrição de saída (seção opcional)

Restrições reduzem tokens de **saída**, então funcionam melhor em uma tarefa **normalmente
verbosa**, com um modelo sem raciocínio (base). Medições com `openai/gpt-4.1`:

| Prompt (traduzido para consulta) | Média total de tokens |
|---|---|
| "Escreva uma função Python que verifique se uma string é um palíndromo." | ~190 |
| o mesmo + "Retorne apenas o código. Sem explicação e sem blocos Markdown." | ~66 |

→ **~65% menos tokens** para a mesma função.

Observação: a restrição **não** ajudou na tarefa de ordenação de versões, que já é concisa
(~103 → ~104 no gpt-4.1), e não reduziu o total de tokens do `gpt-5`, pois os tokens de
raciocínio predominam e não são restringidos. Escolha uma tarefa verbosa
para demonstrar esse fator.

## Modelos e tarefas avaliados e descartados

| Candidato | Motivo do descarte |
|---|---|
| `mistral-ai/ministral-3b` como modelo base | Fraco demais — também falhou na tarefa **fácil**, invalidando a ideia de que "o base vence na Parte 1" |
| `gpt-4.1-nano` como modelo base | Falha consistentemente na tarefa difícil, **mas não é selecionável no seletor de modelos do Copilot** — os alunos não podem usá-lo |
| Contagem de letras / decimais / tarefas "strawberry" | Artefatos de tokenização — os resultados não acompanham o preço (o base pode superar o premium); veja a tabela de monotonicidade |
| "Armadilha gulosa" do problema de troco | Modelos pequenos modernos acertam — já não diferencia os modelos |

## Reprodução

```bash
# tarefas fácil e difícil, base versus premium, n=4
python harness.py --models "openai/gpt-4.1" "openai/gpt-5" --tasks sort carwash -n 4 --sleep 2
```
