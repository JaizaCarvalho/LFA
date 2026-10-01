# Atividade — Máquinas de Turing

## Etapa 1 — Introdução

### 1. O que é uma Máquina de Turing?

Uma Máquina de Turing é um modelo matemático de computação capaz de realizar operações sobre uma fita de símbolos por meio de uma cabeça de leitura e escrita. Ela funciona seguindo um conjunto de estados e regras de transição, permitindo representar algoritmos e estudar quais problemas podem ou não ser resolvidos computacionalmente.

### 2. Quais são os principais componentes de uma Máquina de Turing?

Os principais componentes são:

- **Fita:** armazena os símbolos utilizados durante a execução.
- **Cabeça de leitura/escrita:** lê e altera os símbolos da fita e pode se movimentar para a esquerda ou para a direita.
- **Estados:** representam as diferentes situações em que a máquina pode estar durante a execução.
- **Alfabeto:** conjunto de símbolos que podem ser utilizados.
- **Regras de transição:** determinam qual ação deve ser realizada para cada símbolo lido em determinado estado.
- **Estado inicial:** estado em que a máquina começa.
- **Estados de aceitação e rejeição:** determinam se a entrada foi aceita ou rejeitada.

### 3. Qual é a importância das Máquinas de Turing para a computação?

As Máquinas de Turing são importantes porque fornecem um modelo matemático para representar a computação e os algoritmos. Elas permitem estudar como problemas podem ser resolvidos por processos computacionais e também ajudam a compreender os limites da computação, mostrando que existem problemas para os quais não existe algoritmo capaz de fornecer uma solução para todos os casos.

### 4. Qual é a relação entre Máquina de Turing e algoritmo?

Um algoritmo é uma sequência de passos utilizada para resolver um problema. Uma Máquina de Turing pode representar a execução desses passos por meio de estados, símbolos e regras de transição. Dessa forma, ela é um modelo utilizado para estudar formalmente o funcionamento dos algoritmos e a capacidade de resolução de problemas por computadores.

---

## Etapa 2 — Simulação

### Linguagem reconhecida

A Máquina de Turing reconhece palavras da forma:

**0ⁿ1ⁿ**

Ou seja, a palavra deve possuir uma quantidade igual de símbolos `0` e `1`, com todos os `0` aparecendo antes dos `1`.

### Exemplos aceitos

- `01`
- `0011`
- `000111`
- `00001111`

### Exemplos rejeitados

- `0`
- `1`
- `001`
- `011`
- `00111`

### Funcionamento da máquina

A máquina utiliza os símbolos auxiliares `X` e `Y`.

- `X` representa um `0` que já foi utilizado.
- `Y` representa um `1` que já foi utilizado.
- A máquina procura um `0` ainda não marcado e o transforma em `X`.
- Em seguida, procura um `1` correspondente e o transforma em `Y`.
- Esse processo continua até que todos os `0` tenham sido associados a um `1`.
- Ao final, a máquina aceita somente quando existir a mesma quantidade de `0` e `1` e os símbolos estiverem na ordem correta.

### Estados

- `q0` — procura o próximo `0` não marcado.
- `q1` — procura o `1` correspondente ao `0` marcado.
- `q2` — retorna para o início da fita.
- `q3` — verifica se não existem símbolos `0` não correspondidos.
- `qAceita` — aceita a palavra.
- `qRejeita` — rejeita a palavra.

### Regras principais de transição

| Estado | Lê | Escreve | Movimento | Próximo estado |
|---|---|---|---|---|
| `q0` | `X` | `X` | → | `q0` |
| `q0` | `0` | `X` | → | `q1` |
| `q0` | `Y` | `Y` | → | `q3` |
| `q1` | `0` | `0` | → | `q1` |
| `q1` | `Y` | `Y` | → | `q1` |
| `q1` | `1` | `Y` | ← | `q2` |
| `q1` | `□` | `□` | → | `qRejeita` |
| `q2` | `0` | `0` | ← | `q2` |
| `q2` | `X` | `X` | ← | `q2` |
| `q2` | `Y` | `Y` | ← | `q2` |
| `q2` | `□` | `□` | → | `q0` |
| `q3` | `Y` | `Y` | → | `q3` |
| `q3` | `1` | `1` | → | `qRejeita` |
| `q3` | `0` | `0` | → | `qRejeita` |
| `q3` | `□` | `□` | → | `qAceita` |

---

## Etapa 3 — Registro da simulação

### Teste 1

**Entrada:** `0011`

**Resultado esperado:** ACEITA

**Resultado obtido:** ACEITA

**Estados percorridos:**

`q0 → q1 → q2 → q0 → q1 → q2 → q0 → q3 → q3 → qAceita`

---

### Teste 2

**Entrada:** `000111`

**Resultado esperado:** ACEITA

**Resultado obtido:** ACEITA

**Estados percorridos:**

`q0 → q1 → q2 → q0 → q1 → q2 → q0 → q1 → q2 → q0 → q3 → q3 → q3 → qAceita`

---

### Teste 3

**Entrada:** `00111`

**Resultado esperado:** REJEITA

**Resultado obtido:** REJEITA

**Estados percorridos:**

`q0 → q1 → q2 → q0 → q1 → q2 → q0 → q3 → q3 → q3 → qRejeita`

---

## Descrição da Máquina de Turing criada

A Máquina de Turing criada verifica se uma palavra possui a mesma quantidade de `0` e `1`, mantendo os `0` antes dos `1`. Para isso, cada `0` encontrado é marcado com `X` e associado a um `1`, que é marcado com `Y`. A máquina repete esse processo até que todos os símbolos sejam verificados. Caso exista uma quantidade diferente de `0` e `1`, ou a ordem dos símbolos esteja incorreta, a palavra é rejeitada. Quando todos os símbolos são correspondentes e a estrutura da palavra está correta, a máquina aceita a entrada.

---

## Etapa 4 — Reflexão sobre os limites computacionais

Uma Máquina de Turing não consegue resolver qualquer problema computacional. Ela consegue representar algoritmos para problemas que são computáveis, mas existem problemas para os quais não existe um algoritmo capaz de produzir uma resposta correta para todos os casos possíveis. Esses problemas são chamados de indecidíveis. Portanto, existem limites para aquilo que pode ser realizado por meio de algoritmos. O estudo das Máquinas de Turing permite identificar esses limites e compreender a diferença entre um problema que é apenas difícil e um problema que não pode ser resolvido por um algoritmo em todos os casos.

---

## Questão final

Um problema pode ser considerado apenas difícil quando existe um algoritmo capaz de resolvê-lo, mesmo que esse algoritmo necessite de muito tempo ou muitos recursos. Já um problema indecidível é aquele para o qual não existe um algoritmo capaz de fornecer uma resposta correta para todos os casos. As Máquinas de Turing são utilizadas para estudar essa diferença dentro da teoria da computabilidade. Assim, a análise da existência de um algoritmo é fundamental para saber se estamos diante de um problema difícil de resolver ou de um problema que possui um limite computacional.
