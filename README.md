# UCSanDiegoX-ALGS200x-Algorithmic-Design-and-Techniques

## Programming Assignment 2
### 1. Fibonacci Numbers
Fibonacci sequence: *F<sub>0</sub> = 0*, *F<sub>1</sub> = 1*, and *F<sub>i</sub> = F<sub>i-1</sub> + F<sub>i-2</sub>* for *i >= 2*.

**Task:** Given an integer *n*, find the *n<sup>th</sup>* Fibonacci number *F<sub>n</sub>*

**Input Format:** The input consists of a single integer *n*

**Constraints:** *0 ≤ n ≤ 45*

**Output Format:** Output *F<sub>n</sub>*

```
def calc_fib(n):
 if n <= 1:
  return n
 else:
  fib = [0 for i in range(n+1)]
  fib[0] = 0
  fib[1] = 1
  
  for i in range(2,n+1):
   fib[i] = fib[i-1] + fib[i-2]
  
  return fib[n]
```

### 2. Last Digit of a Large Fibonacci Number
**Task:** Given an integer *n*, find the last digit of the *n<sup>th</sup>* Fibonacci number *F<sub>n</sub>* (that is, *F<sub>n</sub>* `mod 10`)

**Input Format:** The input consists of a single integer *n*

**Constraints:** *0 ≤ n ≤ 107*

**Output Format:** Output the last digit of *F<sub>n</sub>*

### 3. Greatest Common Divisors
**Task:** Given two integers *a* and *b*, find their greatest common divisor

**Input Format:** The two integers *a*, *b* are given in the same line separated by space

**Constraints:** *1 ≤ a, b ≤ 2 x 10<sup>9</sup>*

**Output Format:** Output *GDC(a,b)*

### 4. Least Common Multiple
### 5. Fibonacci Number Again
### 6. Last Digit of the Sum of Fibonacci Numbers
### 7. Last Digit of the Sum of Fibonacci Numbers Again

- Big-O, Omega-O, Theta-O Notation
- Greedy Algorithms:
  - A choice is called safe when there's an optimal solution consistent with this first choice
  - Not all first choices are safe
  - Greedy choices are often unsafe
- Divide and Conquer
