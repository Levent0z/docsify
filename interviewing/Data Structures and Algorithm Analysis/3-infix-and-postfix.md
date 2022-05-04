# Infix & Postfix

## Evalaute a postfix (reverse Polish notation) expression

| Postfix                     |
| --------------------------- |
| `a b c * + d e * f + g * +` |

### Algorithm

1. Push operand
2. At operator, pop two, calculate, push result

<details>
<summary>Step-by-Step</summary>

Note: xy = x * y

| Step | Cursor | Algorithm Step | Stack          |
| ---- | ------ | -------------- | -------------- |
| 1    | a      | 1              | a              |
| 2    | b      | 1              | a b            |
| 3    | c      | 1              | a b c          |
| 4    | *      | 2              | a bc           |
| 5    | +      | 2              | a+bc           |
| 6    | d      | 1              | a+bc d         |
| 7    | e      | 1              | a+bc d e       |
| 8    | *      | 2              | a+bc de        |
| 9    | f      | 1              | a+bc de f      |
| 10   | +      | 2              | a+bc de+f      |
| 11   | g      | 1              | a+bc de+f g    |
| 12   | *      | 2              | a+bc (de+f)g   |
| 13   | +      | 2              | (a+bc)+(de+f)g |
</details>
<br>

Also see Expression Trees.

## Convert Infix to Postfix

| Infix                         |
| ----------------------------- |
| `a + b * c + (d * e + f) * g` |

### Algorithm:

1. Process left-to-right.
2. **Operands** are output immediately.
3. Use the stack for **operators** and **open parentheses**. Popped items will be output, except for parantheses.
4. If at a **right-parenthesis**, **pop** the stack until an **open parenthesis**.
5. If at an **operator**:
    1. If current has a **lower or equal precedence** than the top of the stack, pop the stack until at an operator of a **lower precedence** or an **open parenthesis** or the stack is empty.
    2. Push the current operator onto the stack
6. At the end, pop the stack until empty.

<details>
<summary>Step-by-Step</summary>

| Step | Cursor | Algorithm Step | Output                    | Stack |
| ---- | ------ | -------------- | ------------------------- | ----- |
| 1    | a      | 2              | a                         |       |
| 2    | +      | 3              | a                         | +     |
| 3    | b      | 2              | a b                       | +     |
| 4    | *      | 5              | a b                       | + *   |
| 5    | c      | 2              | a b c                     | + *   |
| 6    | +      | 5-1, 5-2       | a b c * +                 | +     |
| 7    | (      | 3              | a b c * +                 | + (   |
| 8    | d      | 2              | a b c * + d               | + (   |
| 9    | *      | 5-2            | a b c * + d               | + ( * |
| 10   | e      | 2              | a b c * + d e             | + ( * |
| 11   | +      | 5-1, 5-2       | a b c * + d e *           | + ( + |
| 12   | f      | 2              | a b c * + d e * f         | + ( + |
| 13   | )      | 4              | a b c * + d e * f +       | +     |
| 14   | *      | 5              | a b c * + d e * f +       | + *   |
| 15   | g      | 2              | a b c * + d e * f + g     | + *   |
| 16   | _      | 6              | a b c * + d e * f + g * + |       |
</details>