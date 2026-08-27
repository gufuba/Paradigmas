# Exemplo de derivação sintática: comando `if` em Java

**Objetivo:** mostrar como um pequeno trecho de código pode ser construído a partir de regras gramaticais de uma linguagem real.

**Fonte de referência:** *The Java Language Specification (JLS)*, Capítulo 14 – "Blocks, Statements, and Patterns" (define `IfThenStatement`, `Block`, `BlockStatements` etc.) e Capítulo 2 – "Grammars" (define a notação usada). Disponível em: https://docs.oracle.com/javase/specs/jls/se21/html/jls-14.html

A gramática abaixo foi simplificada para fins didáticos, preservando a estrutura sintática essencial do comando `if`.

**Notação:** BNF, no estilo `::=` / `|`, adaptada da notação própria da JLS (descrita no Capítulo 2, que usa `{}` para repetição zero-ou-mais e `[]` para opcional).

## 1. Código gerado

```java
if (x > 0) {
    System.out.println(x);
}
```

## 2. Regras gramaticais utilizadas

Os símbolos entre `< >` são não terminais; os demais representam terminais da linguagem.

```
<if_statement>        ::= if ( <expression> ) <block>
<expression>          ::= <identifier> <relational_operator> <integer_literal>
<relational_operator> ::= > | < | ==
<block>                ::= { <block_statements> }
<block_statements>     ::= <block_statement>
<block_statement>      ::= <expression_statement>
<expression_statement> ::= <statement_expression> ;
<statement_expression> ::= <method_invocation>
<method_invocation>    ::= <method_name> ( <argument_list> )
<method_name>          ::= System.out.println
<argument_list>        ::= <identifier>
<identifier>           ::= x
<integer_literal>      ::= 0
```

Correspondência com os nomes reais da JLS: `<if_statement>` ≈ `IfThenStatement`, `<block>` ≈ `Block`, `<block_statements>` ≈ `BlockStatements`, `<block_statement>` ≈ `BlockStatement`, `<expression_statement>` ≈ `ExpressionStatement`, `<statement_expression>` ≈ `StatementExpression`, `<method_invocation>` ≈ `MethodInvocation`. A gramática real da JLS trata expressões, operadores e listas de argumentos de forma muito mais geral; aqui ela foi reduzida ao subconjunto necessário para esta derivação.

## 3. Derivação

A derivação abaixo começa no símbolo não terminal `<if_statement>` e substitui, passo a passo, cada não terminal até obter a sequência de terminais correspondente ao trecho desejado.

```
<if_statement>
⇒ if ( <expression> ) <block>
⇒ if ( <identifier> <relational_operator> <integer_literal> ) <block>
⇒ if ( x <relational_operator> <integer_literal> ) <block>
⇒ if ( x > <integer_literal> ) <block>
⇒ if ( x > 0 ) <block>
⇒ if ( x > 0 ) { <block_statements> }
⇒ if ( x > 0 ) { <block_statement> }
⇒ if ( x > 0 ) { <expression_statement> }
⇒ if ( x > 0 ) { <statement_expression> ; }
⇒ if ( x > 0 ) { <method_invocation> ; }
⇒ if ( x > 0 ) { <method_name> ( <argument_list> ) ; }
⇒ if ( x > 0 ) { System.out.println ( <argument_list> ) ; }
⇒ if ( x > 0 ) { System.out.println ( <identifier> ) ; }
⇒ if ( x > 0 ) { System.out.println ( x ) ; }
```

Forma concreta em Java, com formatação:

```java
if (x > 0) {
    System.out.println(x);
}
```

## 4. Breve explicação textual

O comando `if` em Java testa uma condição booleana entre parênteses e, se verdadeira, executa o comando seguinte — neste exemplo, um bloco (`<block>`) delimitado por `{ }`. Dentro do bloco, a derivação expande `<block_statements>` até chegar a um único `<block_statement>`, que é uma `<expression_statement>`: uma chamada de método (`<method_invocation>`) seguida de `;`. A chamada `System.out.println(x)` é derivada substituindo `<method_name>` pelo nome literal do método e `<argument_list>` pelo identificador `x`. Cada seta (⇒) representa a aplicação de uma produção, até restarem apenas terminais — nesse ponto a derivação termina e temos o código-fonte válido.

**Terminais:** `if`, `(`, `)`, `{`, `}`, `;`, `>`, `<`, `==`, `x`, `0`, `System.out.println`

**Não terminais:** `<if_statement>`, `<expression>`, `<relational_operator>`, `<block>`, `<block_statements>`, `<block_statement>`, `<expression_statement>`, `<statement_expression>`, `<method_invocation>`, `<method_name>`, `<argument_list>`, `<identifier>`, `<integer_literal>`

---

**Referência:** Oracle. *The Java Language Specification, SE 21*, Capítulos 2 e 14. Disponível em: https://docs.oracle.com/javase/specs/jls/se21/html/jls-14.html
