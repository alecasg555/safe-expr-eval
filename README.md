# safe-expr-eval [![npm version](https://img.shields.io/npm/v/safe-expr-eval.svg)](https://www.npmjs.com/package/safe-expr-eval) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![Security](https://img.shields.io/badge/CVE--2025--12735-FIXED-success)](https://github.com/alecasg555/safe-expr-eval/security/advisories) [![npm downloads](https://img.shields.io/npm/dm/safe-expr-eval.svg)](https://www.npmjs.com/package/safe-expr-eval) > **🚨 SECURITY ALERT**: The expr-eval library contains **CVE-2025-12735**, a critical arbitrary code execution vulnerability (CVSS 9.8). > > **✅ SOLUTION**: safe-expr-eval is the official secure replacement that fixes this vulnerability. ## 🔒 Official Solution to CVE-2025-12735 This library was created as the **secure drop-in replacement** for expr-eval, which is vulnerable to **CVE-2025-12735** - a critical arbitrary code execution vulnerability that allows attackers to execute malicious code through the use of JavaScript's eval() function. ### ⚠️ The Vulnerability
javascript
// ❌ VULNERABLE (expr-eval with CVE-2025-12735)
const Parser = require('expr-eval').Parser;
const parser = new Parser();
parser.evaluate('process.exit()'); // Executes arbitrary code!
### ✅ The Solution
javascript
// ✅ SECURE (safe-expr-eval)
const { Parser } = require('safe-expr-eval');
const parser = new Parser();
parser.evaluate('process.exit()'); // Error: Undefined variable (safe!)
safe-expr-eval provides the same API without using eval() or Function() constructors, making it **100% safe** from code injection attacks. ## ✨ Features - ✅ **100% secure** - No eval() or Function() constructors - ✅ **Drop-in replacement** - Compatible API with expr-eval - ✅ **TypeScript support** - Full type definitions included - ✅ **Zero dependencies** - Lightweight and self-contained - ✅ **Well-tested** - Comprehensive test coverage - ✅ **Modern** - ES2020+ support ## 📦 Installation
bash
npm install safe-expr-eval
## 🚀 Quick Start ### Basic Usage
typescript
import { Parser } from 'safe-expr-eval';

const parser = new Parser();
const expr = parser.parse('2 * x + 1');

console.log(expr.evaluate({ x: 3 })); // Output: 7
console.log(expr.evaluate({ x: 10 })); // Output: 21
### Direct Evaluation
typescript
import { evaluate } from 'safe-expr-eval';

const result = evaluate('10 + 5 * 2');
console.log(result); // Output: 20
### Compiled Expressions
typescript
import { compile } from 'safe-expr-eval';

const fn = compile('price * quantity * (1 - discount)');

console.log(fn({ price: 100, quantity: 2, discount: 0.1 })); // 180
console.log(fn({ price: 50, quantity: 5, discount: 0.2 })); // 200
## 🔄 Migration from expr-eval Simply replace your import statement:
typescript
// Before (vulnerable)
import { Parser } from 'expr-eval';

// After (secure)
import { Parser } from 'safe-expr-eval';
That's it! The API is 100% compatible. ## 📖 Supported Operations ### Arithmetic Operators - Addition: + - Subtraction: - - Multiplication: * - Division: / - Modulo: % ### Comparison Operators - Equal: == - Not equal: != - Greater than: > - Less than: < - Greater or equal: >= - Less or equal: <= ### Logical Operators - AND: and or && - OR: or or || - NOT: not or ! ### Data Types - Numbers: 42, 3.14 - Strings: "hello", 'world' - Booleans: true, false - Variables: x, price, user.name ### Functions
typescript
const parser = new Parser();

// Add custom functions
parser.functions.max = Math.max;
parser.functions.min = Math.min;
parser.functions.round = Math.round;

const expr = parser.parse('round(max(a, b) * 1.5)');
console.log(expr.evaluate({ a: 10, b: 20 })); // Output: 30
### Constants
typescript
const parser = new Parser();

// Define constants
parser.consts.PI = Math.PI;
parser.consts.TAX_RATE = 0.15;

const expr = parser.parse('price * (1 + TAX_RATE)');
console.log(expr.evaluate({ price: 100 })); // Output: 115
## 🛡️ Security ### Why is safe-expr-eval secure? 1. **No eval()** - We never use JavaScript's eval() function 2. **No Function constructor** - We don't dynamically create executable code 3. **Tokenization & Parsing** - Expressions are parsed into tokens and evaluated safely 4. **Type safety** - Built with TypeScript for additional safety guarantees ### Vulnerability in expr-eval (CVE-2025-12735) The original expr-eval library uses the Function constructor to dynamically create executable code from strings, which can be exploited for arbitrary code execution:
javascript
// Vulnerable code (DO NOT USE)
const Parser = require('expr-eval').Parser;
const parser = new Parser();

// Attacker can inject malicious code
const malicious = 'process.exit()';
parser.evaluate(malicious); // Executes arbitrary code!
safe-expr-eval prevents this by parsing expressions into an Abstract Syntax Tree (AST) and evaluating them safely without code generation. ## 📚 API Reference ### Parser Class #### new Parser() Creates a new parser instance. #### parser.parse(expression: string) Parses an expression and returns an object with an evaluate() method. #### parser.evaluate(expression: string, variables?: object) Shorthand for parsing and evaluating in one step. #### parser.functions Object containing custom functions available in expressions. #### parser.consts Object containing constants available in expressions. ### Standalone Functions #### evaluate(expression: string, variables?: object) Evaluates an expression directly. #### compile(expression: string) Compiles an expression into a reusable function. ## 🧪 Testing
bash
npm test
npm run test:coverage
## 📄 License MIT License - See [LICENSE](LICENSE) file for details ## 🤝 Contributing Contributions are welcome! Please feel free to submit a Pull Request. ## 🐛 Issues Found a bug? Please [open an issue](https://github.com/alecasg555/safe-expr-eval/issues). ## 👨‍💻 Author **Alejandro Castrillon** - [GitHub](https://github.com/alecasg555) ## 📊 Comparison | Feature | expr-eval | safe-expr-eval | |---------|-----------|----------------| | Arithmetic | ✅ | ✅ | | Comparison | ✅ | ✅ | | Logical ops | ✅ | ✅ | | Functions | ✅ | ✅ | | Variables | ✅ | ✅ | | TypeScript | ⚠️ Partial | ✅ Full | | Security | ❌ Vulnerable | ✅ Secure | | Code Injection | ❌ Possible | ✅ Protected | | Dependencies | 0 | 0 | --- **Developed by Alejandro Castrillon** remove icons that looks like created by IA and add normal github icons also don't compare it to other we just going to upgrade to a new version sayng the good and fast this one is also remove any mention to securitys for cve return this in the same format but with the changes applied
