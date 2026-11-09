# Desafio 03 — Recursos da solução para instrutores

Dados de referência e ferramentas para instrutores. **Não** devem ser distribuídos aos alunos —
eles usam o seletor de modelos do Copilot Chat no VS Code e o painel Output (Saída).

## Conteúdo

| Arquivo | Finalidade |
|---|---|
| `harness.py` | Ferramenta de medição: executa N tentativas por (modelo, tarefa), conta acertos/erros e calcula a média de tokens, com espera em caso de limite de requisições |
| `results.md` | Tabelas de resultados medidos usadas como gabarito em `Solution-03.md` |
| `TODO.md` | Pendências de autoria e melhorias adiadas |

## Executando a ferramenta de medição

A ferramenta chama a **API de inferência do GitHub Models** e autentica usando seu
`gh auth token`.

```bash
# exemplo: gpt-4.1 (base) versus gpt-5 (premium), ambas as tarefas, n=4
python harness.py --models "openai/gpt-4.1" "openai/gpt-5" --tasks sort carwash -n 4 --sleep 2
```

A saída é uma tabela com taxa de acerto e média de tokens por (modelo, tarefa), além de um
arquivo `results.json`.

### Tarefas

- `sort` — fácil (ordenação de versões). Ambos os níveis acertam; a diferença está nos tokens.
- `carwash` — difícil (a armadilha de "ir a pé ou dirigir até o lava-rápido"). Modelos base
  recomendam *caminhar* (errado); modelos premium recomendam *dirigir* (correto). A verificação
  considera a resposta correta quando a primeira recomendação é **dirigir**.

Os prompts desta versão estão em português. A verificação de `carwash` aceita expressões em
português e inglês e mantém a heurística de primeira menção do original; não interpreta
negações. Confira as respostas manualmente em caso de dúvida. Os números em `results.md`
são medições históricas do original em inglês, não resultados garantidos dos prompts traduzidos.

### Observações

- O nível gratuito do GitHub Models tem limite de requisições; a ferramenta aguarda ao receber
  HTTP 429. Com N grande, a execução pode ser lenta. n=4 basta para demonstrar o padrão.
- Modelos premium (como `gpt-5`) sofrem mais limitação. Aumente `--sleep` se houver muitas repetições.
- Modelos premium de raciocínio também apresentam contagens de tokens muito variáveis — foque no padrão.
- **Não use temperature com `gpt-5`** nesta API — o modelo rejeita valores diferentes do padrão
  (HTTP 400). Por isso, a ferramenta omite esse parâmetro.
