# Desafio 03 — Prompts

Execute cada prompt **exatamente como está escrito**. Não adicione contexto, anexos ou instruções — manter a
entrada idêntica entre os modelos é o que torna justa a comparação de tokens.

---

## Parte 1 — Tarefa fácil (ordenação de versões)

```
Ordene estes números de versão de software do mais antigo para o mais recente e liste-os
em ordem, separados por vírgulas: 1.9.0, 1.10.0, 1.2.0, 1.11.0, 1.9.5
```

✅ **Resposta correta:** `1.2.0, 1.9.0, 1.9.5, 1.10.0, 1.11.0`

Uma resposta errada geralmente ordena as versões como texto (assim, `1.10.0` e `1.11.0` ficam antes de
`1.9.0`). Modelos modernos — básicos ou premium — quase sempre acertam. O diferencial
aqui é o **custo de tokens**, não a correção da resposta.

---

## Parte 2 — Tarefa difícil (o lava-rápido)

```
O lava-rápido fica a 40 metros da minha casa. Quero lavar meu carro.
Devo ir a pé ou de carro?
```

✅ **Resposta correta:** **Vá de carro.** Você não pode lavar um carro que não está lá — o carro precisa estar
*no* lava-rápido. Os "40 metros" são uma distração deliberada; o modelo básico tende a se fixar
na curta distância e dizer para você **ir a pé** (deixando seu carro, e todo o propósito da ida, em casa).

Um modelo premium raciocina sobre o objetivo real — *o carro precisa estar presente para ser lavado* — e
responde **vá de carro**. A resposta errada é óbvia para qualquer pessoa em um segundo: é exatamente por isso que
esta tarefa funciona.

---

## Opcional — Variante com restrição de saída (tarefa de programação com resposta detalhada)

Escolha uma tarefa sobre a qual o modelo é detalhado por padrão e, em seguida, restrinja a saída:

```
Escreva uma função Python que verifique se uma string é um palíndromo.
```

depois

```
Escreva uma função Python que verifique se uma string é um palíndromo.
Retorne apenas o código. Sem explicação, sem blocos delimitados de Markdown.
```

Execute ambos no **modelo básico** e compare o total de tokens. O código é o mesmo; a execução
com restrição elimina a explicação ao redor, reduzindo o custo.
