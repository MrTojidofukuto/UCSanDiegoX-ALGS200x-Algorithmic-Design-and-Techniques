# UCSanDiegoX-ALGS200x-Algorithmic-Design-and-Techniques

## Course Summary
- Big-O, Omega-O, Theta-O Notation
- Greedy Algorithms:
  - A choice is called safe when there's an optimal solution consistent with this first choice
  - Not all first choices are safe
  - Greedy choices are often unsafe
- Divide and Conquer

## Programming Assignment 2: Algorithmic Warmup
### 2.1. Fibonacci Numbers
Fibonacci sequence: *F<sub>0</sub> = 0*, *F<sub>1</sub> = 1*, and *F<sub>i</sub> = F<sub>i-1</sub> + F<sub>i-2</sub>* for *i ≥ 2*.\
**Task:** Given an integer *n*, find the *n<sup>th</sup>* Fibonacci number *F<sub>n</sub>*.\
**Input Format:** The input consists of a single integer *n*.\
**Constraints:** *0 ≤ n ≤ 45*.\
**Output Format:** Output *F<sub>n</sub>.*

```python
def fib(n):
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

### 2.2. Last Digit of a Large Fibonacci Number
**Task:** Given an integer *n*, find the last digit of the *n<sup>th</sup>* Fibonacci number *F<sub>n</sub>* (that is, *F<sub>n</sub>* `mod` 10).\
**Input Format:** The input consists of a single integer *n*.\
**Constraints:** *0 ≤ n ≤ 107*.\
**Output Format:** Output the last digit of *F<sub>n</sub>.*

```python
def get_fibonacci_last_digit(n):
    if n <= 1:
        return n

    last_digit = [0 for i in range(n+1)]
    last_digit[0] = 0
    last_digit[1] = 1

    for i in range(2,(n+1)):
        last_digit[i] = (last_digit[i-1] + last_digit[i-2]) % 10

    return last_digit[n]
```

### 2.3. Greatest Common Divisors
**Task:** Given two integers *a* and *b*, find their greatest common divisor.\
**Input Format:** The two integers *a*, *b* are given in the same line separated by space.\
**Constraints:** *1 ≤ a, b ≤ 2 x 10<sup>9</sup>*.\
**Output Format:** Output the greatest common divisor of *a* and *b*.

```python
def gcd(a, b):
    while min(a,b) != 0:
        if a > b:
            a %= b
        else:
            b %= a
     
    return max(a,b)
```

### 2.4. Least Common Multiple
**Task:** Given two integers *a* and *b*, find their least common multiple.\
**Input Format:** The two integers *a*, *b* are given in the same line separated by space.\
**Constraints:** *1 ≤ a, b ≤ 2 x 10<sup>9</sup>*.\
**Output Format:** Output the least common multiple of *a* and *b*.

```python
def lcm(a, b):
    return int(a * b // gcd(a,b))
```

### 2.5. Fibonacci Number Again
**Task:** Given two integers *n* and *m*, output *F<sub>n</sub>* `mod` *m* (that is, the remainder of *F<sub>n</sub>* `mod` *m*).\
**Input Format:** The two integers *n*, *m* are given in the same line separated by space.\
**Constraints:** *1 ≤ n ≤ 10<sup>18</sup>, 2 ≤ m ≤ 10<sup>5</sup>*.\
**Output Format:** Output *F<sub>n</sub>* `mod` *m*.

```python
def pisano_period_len(m):
    if m < 2:
        return None
    else:
        fib_last_index = 3
        fib_2nd_last = 1 #F(2) = 1
        fib_last = 2 #F(3) = 2

        while True:
            if (fib_2nd_last % m == 0) and (fib_last % m == 1):
                return (fib_last_index-1)
            else:
                temp = fib_2nd_last
                fib_2nd_last = fib_last
                fib_last += temp
                fib_last_index += 1
                
def get_fibonacci_huge(n, m):
    if n <= 1:
        return n
    n %= pisano_period_len(m)
    return (fib(n) % m)
```

### 2.6. Last Digit of the Sum of Fibonacci Numbers
**Task:** Given an integer *n*, find the last digit of the sum *F<sub>0</sub> + F<sub>1</sub> + ... + F<sub>n</sub>*.\
**Input Format:** The input consists of a single integer *n*.\
**Constraints:** *0 ≤ n ≤ 10<sup>14</sup>*.\
**Output Format:** Output the last digit of the sum *F<sub>0</sub> + F<sub>1</sub> + ... + F<sub>n</sub>.*

```python
def last_digit_of_sum(pisano_len):
	if pisano_len <= 1:
		return n

	last_digit = [0 for i in range(pisano_len)]
	last_digit[0] = 0
	last_digit[1] = 1
	
	for i in range(2,pisano_len):
		last_digit[i] = (last_digit[i-1] + last_digit[i-2] + 1) % 10

	return last_digit[pisano_len-1]

def fibonacci_sum(n):
	if n <= 1:
		return n

	# n = pisano_len * divisor + remainder
	pisano_len = pisano_period_len(10)
	divisor = n // pisano_len
	remainder = n % pisano_len

	last_digit = ((divisor % 10) * last_digit_of_sum(pisano_len)) % 10

	for i in range(n-remainder,n+1):
		last_digit += get_fibonacci_huge(i, 10)
		last_digit %= 10
	
	return last_digit
```

### 2.7. Last Digit of the Sum of Fibonacci Numbers Again
**Task:** Given two non-negative integers *m* and *n*, where *m ≤ n*, find the last digit of the sum *F<sub>m</sub> + F<sub>m+1</sub> + ... + F<sub>n</sub>*.\
**Input Format:** The two non-negative integers *m*, *n* are given in the same line separated by space.\
**Constraints:** *0 ≤ m ≤ n ≤ 10<sup>18</sup>*.\
**Output Format:** Output the last digit of the sum *F<sub>m</sub> + F<sub>m+1</sub> + ... + F<sub>n</sub>*.

```python
def fibonacci_partial_sum(m, n):
	last_digit_sum_fn = fibonacci_sum(n)
	if m <= 1:
		return last_digit_sum_fn
	
	last_digit_sum_fm_1 = fibonacci_sum(m-1)
	
	if last_digit_sum_fn < last_digit_sum_fm_1:
		last_digit_sum_fn += 10
	
	return (last_digit_sum_fn - last_digit_sum_fm_1)
```

## Programming Assignment 3: Greedy Algorithms
### 3.1. Changing Money
**Task:** The goal in this problem is to find the minimum number of coins needed to change the input value (an integer) into coins with denominations 1, 5, and 10 cents.\
**Input Format:** The input consists of a single integer *m*.\
**Constraints:** *0 ≤ m ≤ 10<sup>3</sup>*.\
**Output Format:** Output the minimum number of coins with denominations 1, 5, 10 that changes *m*.

```python
```

### 3.2. Maximizing the Value of a Loot
**Task:** The goal of this code problem is to implement an algorithm for the fractional knapsack problem.\
**Input Format:** The first line of the input contains the number of *n* items and the capacity *W* of a knapsack. The next *n* lines define the values and weights of the items. The *i<sup>th</sup>* line contains integers *v<sub>i</sub>* and *w<sub>i</sub>* - the value and the weight of the *i<sup>th</sup>* item respectively.\
**Constraints:** *0 ≤ n ≤ 10<sup>3</sup>, 0 ≤ W ≤ 2 x 10<sup>6</sup>, 0 ≤ v<sub>i</sub> ≤ 2 x 10<sup>6</sup>, 0 ≤ w<sub>i</sub> ≤ 2 x 10<sup>6</sup>* for all *0 ≤ i ≤ n.* All the numbers are integers.\
**Output Format:** Output the maximal value of fractions of items that fit into the knapsack. The absolute value of the difference between the answer of your program and the optimal value should be at most *10<sup>-3</sup>*. To ensure this, out put your answer with at least four digits after the decimal points. Otherwise, your answer, while being computed correctly, can turn out to be wrong because of rounding issues.

```python
```

### 3.3. Maximizing Revenue in Online Ad Placement
**Task:** Given two sequences *a<sub>1</sub>, a<sub>2</sub>,..., a<sub>n</sub>* (*a<sub>i</sub>* is the profit per click of the *i<sup>th</sup>* ad) and *b<sub>1</sub>, b<sub>2</sub>,..., b<sub>n</sub>* (*b<sub>i</sub>* is the average number of clicks per day of the *i<sup>th</sup>* slot), we need to partition them into *n* pairs (*a<sub>i</sub>, b<sub>j</sub>*) such that the sum of their products is maximized.\
**Input Format:** The first line contains an integer *n*. The second one contains a sequence of integers *a<sub>1</sub>, a<sub>2</sub>, ... a<sub>n</sub>*. The third one contains a sequence of integers *b<sub>1</sub>, b<sub>2</sub>, ... b<sub>n</sub>*.\
**Constraints:** *0 ≤ n ≤ 10<sup>3</sup>, -10<sup>5</sup> ≤ a<sub>i</sub>, b<sub>i</sub> ≤ 10<sup>5</sup>* for all *1 ≤ i ≤ n*.\
**Output Format:** Output the maximum value of *Σ︀ a<sub>i</sub>c<sub>i</sub>*, where *c<sub>1</sub>, c<sub>2</sub>, ... c<sub>n</sub>* is a permutation of *b<sub>1</sub>, b<sub>2</sub>, ... b<sub>n</sub>*.

```python
```
