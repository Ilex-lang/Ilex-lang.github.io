---
title: Variables & Constants
description: Variable declaration, mutability, and constants in Ilex.
sidebar:
  order: 1
---

Ilex requires you to be explicit about mutability.

## Mutable Variables

Use `mut` to declare a variable you intend to change:

```ilex
mut x: int = 10;
mut name: string = "Ilex";
```

The shorthand `:=` also declares a mutable variable with type inference:

```ilex
x := 10;
name := "Ilex";
```

## Immutable Variables

Use `const` for values that shouldn't change after initialization:

```ilex
const y = 20;
const pi: f64 = 3.14159;
```

The shorthand `::=` declares an immutable variable:

```ilex
y ::= 20;
pi ::= 3.14159;
```

## Compile-Time Constants

When a `const` is assigned a literal or an expression that can be fully evaluated at compile time, it becomes a compile-time constant automatically:

```ilex
const MAX_SIZE = 1024;        // compile-time constant
const GREETING = "hello";     // compile-time constant
const DOUBLED = MAX_SIZE * 2; // also compile-time
```

## Type Inference

Ilex infers types when possible, but you can always be explicit:

```ilex
x := 42;          // inferred as s32 (int)
y := 3.14;        // inferred as f64 (double)
mut z: u64 = 100; // explicit type
```

## Auto-Initialization

Variables are initialized to their zero values by default:

```ilex
mut n: int;    // 0
mut b: bool;   // false
mut s: string; // ""
mut p: ^int;   // null
```

If you explicitly don't want initialization (for performance), use `undefined`:

```ilex
mut buffer: [1024]u8 = undefined; // no initialization
```

Note that this is not like `undefined` in Typescript, you can't check for it:

```ilex
if x == undefined {
    fmt::println("This code is invalid!");
}
```

## Discarding Values

Use `_` to discard a return value you don't need:

```ilex
_ = some_function_with_return();
```

## Visibility

Variable naming controls visibility across namespaces:

- `count` — exported (public)
- `_count` — private to the namespace
- `count_` — private to the file
- `_count_` — private to the file (most private wins)
