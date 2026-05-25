# safe-expr-eval

Fast and lightweight expression evaluator for JavaScript and TypeScript.

A modern expression parser with a familiar API, zero dependencies, and full TypeScript support.

---

## Features

* Fast expression parsing and evaluation
* Lightweight and dependency-free
* Full TypeScript support
* Simple and familiar API
* Custom functions and constants
* ES2020+ compatible
* Well tested

---

## Installation

```bash
npm install safe-expr-eval
```

---

# Quick Start

## Basic Usage

```ts
import { Parser } from 'safe-expr-eval';

const parser = new Parser();
const expr = parser.parse('2 * x + 1');

console.log(expr.evaluate({ x: 3 })); // 7
console.log(expr.evaluate({ x: 10 })); // 21
```

---

## Direct Evaluation

```ts
import { evaluate } from 'safe-expr-eval';

const result = evaluate('10 + 5 * 2');

console.log(result); // 20
```

---

## Compiled Expressions

```ts
import { compile } from 'safe-expr-eval';

const fn = compile('price * quantity * (1 - discount)');

console.log(
  fn({
    price: 100,
    quantity: 2,
    discount: 0.1
  })
); // 180
```

---

# Supported Operations

## Arithmetic

```txt
+  -  *  /  %
```

## Comparison

```txt
==  !=  >  <  >=  <=
```

## Logical

```txt
and  or  not
&&   ||   !
```

---

# Data Types

```txt
Numbers   → 42, 3.14
Strings   → "hello"
Booleans  → true, false
Variables → price, user.name
```

---

# Custom Functions

```ts
const parser = new Parser();

parser.functions.max = Math.max;
parser.functions.min = Math.min;
parser.functions.round = Math.round;

const expr = parser.parse(
  'round(max(a, b) * 1.5)'
);

console.log(
  expr.evaluate({
    a: 10,
    b: 20
  })
); // 30
```

---

# Constants

```ts
const parser = new Parser();

parser.consts.PI = Math.PI;
parser.consts.TAX_RATE = 0.15;

const expr = parser.parse(
  'price * (1 + TAX_RATE)'
);

console.log(
  expr.evaluate({
    price: 100
  })
); // 115
```

---

# API

## Parser

### Create parser

```ts
new Parser()
```

### Parse expression

```ts
parser.parse(expression)
```

### Evaluate expression

```ts
parser.evaluate(expression, variables?)
```

### Functions registry

```ts
parser.functions
```

### Constants registry

```ts
parser.consts
```

---

# Standalone Functions

## evaluate

```ts
evaluate(expression, variables?)
```

## compile

```ts
compile(expression)
```

---

# Testing

```bash
npm test
```

```bash
npm run test:coverage
```

---

# License

MIT

See the LICENSE file for details.

---

# Contributing

Pull requests and contributions are welcome.

---

# Issues

Please open an issue if you find a bug or have a feature request.

---

# Author

Alejandro Castrillon

```
GitHub: https://github.com/
```
