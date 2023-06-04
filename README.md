# expr

Expr is a simple, dynamically-typed, functional programming language.

![](https://github.com/sdingcn/expr/actions/workflows/auto-test.yml/badge.svg)

## dependencies

Python >= 3.9

## example

```
letrec (
  f = lambda (x) {
    if (lt x 0) then (void)
    else [(put x) (g (sub x 1))]
  }
  g = lambda (x) {
    if (lt x 0) then (void)
    else [(put x) (f (sub x 1))]
  }
) {
  (f 10)
}
```

For more examples, see `test/`.

## feature summary

| feature | status |
| --- | --- |
| first-class functions | complete |
| lexically scoped variables and closures | complete |
| dynamically scoped variables | complete |
| letrec and (mutual) recursion | complete |
| first-class continuations | complete |
| dynamic type check | complete |
| mark-and-sweep garbage collection | complete |

## syntax and semantics

```
<int> := [+-]?0 | [+-]?[1-9][0-9]*
<str> := Python double-quote str literal
<lex-var> := [a-z][a-zA-Z]*
<dyn-var> := [A-Z][a-zA-Z]*
<var> := <lex-var> | <dyn-var> ; except for keywords and intrinsic function names
```

```
<intrinsic> := void
             | add | sub | mul | div | mod | lt
             | strlen | strslice | strcat | strlt | strint
             | getline
             | put
             | callcc
             | type
             | exit
<var-list> := epsilon | <var> <var-list>
<binding-list> := epsilon | <var> = <expr> <binding-list>
<expr-list> := epsilon | <expr> <expr-list>
<expr> := <int>
        | lambda ( <var-list> ) { <expr> }
        | letrec ( <binding-list> ) { <expr> }
        | if <expr> then <expr> else <expr>
        | <var> ; can hold void, integers, closures, continuations, but cannot hold intrinsics
        | ( <expr> <expr-list> ) ; intrinsic / closure / continuation call
        | [ <expr> <expr-list> ] ; sequence
```

The full semantic reference is the interpreter itself.

## usage

+ `python3 src/interpreter.py run <file>` runs the code in `<file>`.

+ `python3 src/interpreter.py debug <file>` runs the code in `<file>` and prints (to `stderr`) interpretation steps.

+ `python3 src/interpreter.py dump-ast <file>` dumps the AST of the code in `<file>`.

+ `python3 test.py` runs all tests.
