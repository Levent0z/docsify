
## Math Review

### Exponents

$x^a x^b = x^{a+b}$

$\dfrac{x^a}{x^b} = x^{a-b}$

$(x^a)^b = x^{ab}$

$2^n + 2^n = 2^{n+1}$

<br>

### Logarithms

$x^a = b \;\leftrightarrow\; \log_xb$

$\log_ab = \dfrac{\log_cb}{\log_ca}$

$\log \dfrac {a}{b} = \log a - \log b$

$\log a^b = b \log a$

$\forall x > 0,\quad \log x < x$

<br>

### Polynomials

$f(x) = \sum_{i=0}^n a_ix^i$

<br>

#### Horner's Rule

$f(x) = a_0 + a_1x + a_2x^2 + \cdots + a_nx^n$

$f(x) = a_0 + x(a_1 + a_2x^1 + \cdots + a_nx^{n-1})$

$f(x) = a_0 + x(a_1 + x(a_2x + \cdots + a_nx^{n-2})$

```javascript
// Using recursion
function hornerRecurse(a, x, i) {  
  if (!i) {
    i = 0;
  }
  if (i === a.length - 1) {
    return a[a.length - 1];
  }
  return a[i] + x * hornerRecurse(a, x, i+1)
}

// Not using recursion
function hornerSimple(a, x) {
  let sum = 0;
  for (let i = a.length - 1; i >= 0; i -= 1) {
    sum = sum * x + a[i];
  }
  return sum;
}
```

[See it on replit.com](https://replit.com/@leventoz/hornersrule#index.js)

<br>

### Geometric Series

$2^0 + 2^1 + 2^2 + \cdots + 2^n = 2^{n+1} - 1 = \sum_{i=0}^{n} 2^i$

<br>

### Arithmetic Series

Sum of first $n$ positive integers:

$1 + 2 + 3 + \cdots + n = \sum_{i=1}^{n} i = \dfrac{n(n+1)}{2}$

Note:

$\sum_{n=1}^{\infty} \dfrac{n(n+1)}{2} = 1 + 3 + 6 + 10 + \cdots$

<br>

$\sum_{n=1}^{\infty} 2^n - 1 = 1 + 3 + 7 + 15 + \cdots$

<br>

### Harmonic Sum

$H_n = 1 + \dfrac{1}{2} + \dfrac{1}{3} + \dfrac{1}{4} + \cdots = \sum_{i=1}^{n}\dfrac{1}{i} \approx \log_en$

<br>

### Modular Arithmetic

Given
- $a \equiv b\; (mod\;n)$
  
Then:
- $a + c \equiv b + c\; (mod\;n)$
- $ad \equiv bd\; (mod\;n)$

\
Given:
- $m > 0, e > 0$
- $a,b,c,d$ are integers
- $a \equiv b\;(mod\;m)$
- $c \equiv d\;(mod\;m)$

then:
- $a + c \equiv b + d\;(mod\;m)$
- $a - c \equiv b - d\;(mod\;m)$
- $ac \equiv bd\;(mod\;m)$
- $a^e \equiv b^e\;(mod\;m)$

\
Also:
- $ab\;(mod\;m) \equiv a\;(mod\;m) \times b\;(mod\;m)$

<br>

## Power Set 
Note: this is not in the book

For a given set $S$ with $n$ elements, number of elements in $P(S) = 2^n$. As each element has two possibilities (present or absent). The powerset in includes the set itself and the empty set

[See it on replit.com](https://replit.com/@leventoz/PowerSet#index.js)

<br>

## Factorial

$n! = n\times(n-1)\times\cdots\times1$

$n! = n\times(n-1)!$

$0! = 1$

<br>

### Permutations / Arrangements

Number of ways $n$ items can be arranged in $k$ places (order of items matters):

$P(n,k) = \dfrac{n!}{(n-k)!}$

Note that $P(n,n) = n!$

<br>

### Combinations

Number of ways $k$ items can be selected from $n$ items (order does not matter):

$\dbinom{n}{k} = \dfrac{n!}{k!(n-k)!}\quad$ when $k \le n$

<br>

## Proofs
### 1. Proof by Induction

1. Establish truth of the base case, e.g. $k=1$
2. Assuming that the hypothesis is true for a range ($1 \leq k \leq n$), show that hypothesis is true for $k=n+1$.

### 2. Prove false by counter-example

- Find an example that shows the hypothesis is false

### 3. Prove true by contradiction

1. Assume that the hypothesis is false.
2. The assumption leads to the conclusion that something known to be true is false. Therefore the assumption must be wrong.

<details>
<summary>Example: "There are an infinite number of primes."</summary>

If there were not an infinite number of primes, there must be a prime number that's greater than all the other primes, namely $p_{max}$.

If we multiply all the prime numbers up to and including $p_{max}$ and add 1, it will be a prime number by definition. It will also be greater than $p_{max}$:

$p_{test} = p_1p_2...p_{max} + 1 > p_{max}$

</details>




