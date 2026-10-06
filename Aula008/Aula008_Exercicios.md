# Aula 008 – Subprogramas

## 1 · Python
**Saída:**
```
[1]
[1, 2]
```
**Conceito:** valor padrão mutável. O `lista=[]` é criado uma única vez, na definição da função, e é reaproveitado entre as chamadas. Por isso a segunda chamada enxerga o `1` da primeira. A correção usual é `lista=None` e criar a lista dentro da função.

## 2 · Java
**Saída:** `0 5`

**Conceito:** passagem por valor. O `v` é uma referência copiada, então `v[0] = 0` altera o mesmo array do chamador. O `n` é um primitivo copiado, então `n = 0` muda só a cópia local.

## 3 · Python
**Saída:** `[2, 2, 2]`

**Conceito:** fechamento com ligação tardia (*late binding*). As três lambdas capturam a **variável** `i`, não o valor dela. Quando são chamadas, o laço já terminou e `i` vale 2. Para obter `[0, 1, 2]`, use `lambda i=i: i`.

## 4 · C
**Saída:** `3`

**Conceito:** variável local `static`. Ela fica em memória estática, e não no registro de ativação, então mantém o valor entre as chamadas. É inicializada só uma vez, e a terceira chamada retorna `++n` = 3.

## 5 · Rust
**Saída:** erro de compilação, `borrow of moved value: v` (E0382).

**Conceito:** posse (*ownership*) e *move*. `dobra(v)` transfere a posse do vetor para a função. Depois disso o `v` não pode mais ser usado no `println!`. Correções: passar `&v` (empréstimo, com a função recebendo `&Vec<i32>`) ou `dobra(v.clone())`.

## 6 · Python
**Saída:** erro `UnboundLocalError: cannot access local variable 'total' where it is not associated with a value`.

**Conceito:** escopo de variáveis. Como há uma atribuição a `total` dentro da função, o Python trata `total` como **local** em toda a função. A leitura em `total + x` acontece antes de a variável local existir. Correção: declarar `global total`, ou, melhor, usar uma variável local ou um parâmetro (`nonlocal` serve se a função estiver aninhada).
