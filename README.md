# Bookworm
🐛 Bookworm is new experimental typechecker for `Watt`.

## Proposal
Bookworm needs to be as simple as possible solution for `Watt`
typechecking, but powerful too.

## Pipeline
Pipeline of the bookworm can be represented like this:
`Hir` -> `Bookworm` -> `TyCx` + `Thir`

## Design
Here's an explanation of the bookworm design.

Bookworm analysis separates to three stages:
1. `early`: registers types by name with generic parameters in arena.
2. `mid`: registers functions by signature, type fields.
3. `late`: analyses function bodies.

Bookworm stores `Struct` and `Enum` adt in arena. Arena located in `TyCx`

During inference process, bookworm uses `InferCx` that contains arena of the type variables and
`FresheningCx` that operates types instatiation.

Variables storage `ResolveCx` contains scopes stack (`RibStack`), module definitions (`ModuleDef`), imports.
Ribs stack is stack of the scopes (`Rib`). `Rib` contains rigid generic variables and local variables (`Variable`).

`Variable` type contains fields: `ty`, `publicity`, `mutability`. 

Fields of structures also got represented with `Field`.
`Field` type contains fields: `ty`, `mutability`

## Code quality
Bookworm will use `Code Rabbit` (`https://www.coderabbit.ai/`) for code quality control.
