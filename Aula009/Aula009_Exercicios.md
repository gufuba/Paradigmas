# Aula 009 – TADs e OO

## 1 · Java
**(a) Saída:** `au`

**(b) Execução.** A variável é do tipo `Animal`, mas o objeto é um `Cachorro`. Em Java os métodos de instância são despachados dinamicamente, pelo tipo real do objeto (vinculação dinâmica, via vtable).

## 2 · C++
**(a) Saída:** `A`

**(b) Compilação.** O método `f` não é `virtual`, então a chamada é resolvida pelo tipo do ponteiro (`A*`), e não pelo tipo do objeto. Com `virtual void f()` a saída seria `B`.

## 3 · Java
**(a) Saída:** `A B`

**(b)** `x.nome` é decidido na **compilação**, porque campos não são polimórficos e valem pelo tipo da referência (`A`). `x.getNome()` é decidido na **execução**, porque o método é sobrescrito e roda o de `B`, que devolve o `nome` de `B`.

## 4 · Python
**(a) Saída:** `1 2 2`

**(b)** Não há despacho polimórfico aqui. `total` é um atributo da **classe**, compartilhado, e `id` é da instância. Em Python a busca dos atributos acontece em **execução** (primeiro na instância, depois na classe).

## 5 · Java
**(a) Saída:** `A`

**(b) Compilação.** Métodos `static` não são sobrescritos, só ocultados (*hiding*). A chamada é resolvida pelo tipo declarado da variável (`A`), e não pelo objeto.

## 6 · Go
**(a) Saída:** `faz ... au`

**(b) Compilação.** Embutir `Animal` em `Cao` é composição, não herança. Dentro de `Falar`, o receptor `a` é um `Animal`, então `a.Som()` chama sempre `Animal.Som` (não há *virtual*). Já `Cao{}.Som()` chama o `Som` do próprio `Cao`, que "esconde" o do `Animal`.
