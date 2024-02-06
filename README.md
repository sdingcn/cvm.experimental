# cvm

![](https://github.com/sdingcn/closure/actions/workflows/auto-test.yml/badge.svg)

Closure virtual machine: a programming language, a shell, and a virtual machine.

## Programming language

```
<variable> := [a-zA-Z][a-zA-Z0-9_]*
<binding> :=
    <variable> = <expr>
<callee> :=
    <intrinsic>
  | <expr>
<expr> :=
    <integer>
  | <string>
  | <variable>
  | lambda ( <variable>* ) { <expr> }
  | letrec ( <binding>* ) { <expr> }
  | if <expr> then <expr> else <expr>
  | ( <callee> <expr>* )
  | [ <expr>+ ]
  | @ <variable> <expr>
  | & <variable> <expr>
<def> :=
    letrec ( <binding>* )
<intrinsic> :=
    .void
  | .+ | .- | .* | ./ | .% | .<
  | .slen | .ssub | .s+ | .squote | .s<
  | .i->s | .s->i
  | .v? | .i? | .s? | .c?
  | .get | .put
  | .eval
  | .exit
  | .send | .recv
```

## Shell

```
<def>          // foreground definition
/ls            // list all names defined by letrec
/co name       // examine the value of name
/dl name       // delete name
<expr>         // foreground evaluation
CTRL-D         // bring current process into background with pid = unused_rand()
/bg pid <expr> // background evaluation
/fg pid        // bring to foreground
/ki pid        // kill process
/ps            // list all background processes
/gc            // run garbage collection
/sd            // shutdown
```

## Dependency and usage

Python >= 3.9
