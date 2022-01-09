# [Project Euler](./euler.md) Challenges 1-50 (4/50)

[Project Euler](https://projecteuler.net/) was started by Colin Hughes (a.k.a. euler) in October 2001 as a sub-section on mathschallenge.net. Who could have known how popular these types of problems would turn out to be? Since then the membership has continued to grow and Project Euler moved to its own domain in 2006.

These are the first 50 challenges from the site.

## Contents

1. [Multiples of 3 or 5](#multiples-of-3-or-5) 🗸
2. [Even Fibonacci numbers](#even-fibonacci-numbers) 🗸
3. [Largest prime factor](#largest-prime-factor) 🗸
4. [Largest palindrome product](#largest-palindrome-product) 🗸
5. [Smallest multiple](#smallest-multiple) 
6. [Sum square difference](#sum-square-difference) 
7. [10001st prime](#10001st-prime) 
8. [Largest product in a series](#largest-product-in-a-series) 
9. [Special Pythagorean triplet](#special-pythagorean-triplet) 
10. [Summation of primes](#summation-of-primes) 
11. [Largest product in a grid](#largest-product-in-a-grid) 
12. [Highly divisible triangular number](#highly-divisible-triangular-number) 
13. [Large sum](#large-sum) 
14. [Longest Collatz sequence](#longest-collatz-sequence) 
15. [Lattice paths](#lattice-paths) 
16. [Power digit sum](#power-digit-sum) 
17. [Number letter counts](#number-letter-counts) 
18. [Maximum path sum I](#maximum-path-sum-i) 
19. [Counting Sundays](#counting-sundays) 
20. [Factorial digit sum](#factorial-digit-sum) 
21. [Amicable numbers](#amicable-numbers) 
22. [Names scores](#names-scores) 
23. [Non-abundant sums](#non-abundant-sums) 
24. [Lexicographic permutations](#lexicographic-permutations) 
25. [1000-digit Fibonacci number](#1000-digit-fibonacci-number) 
26. [Reciprocal cycles](#reciprocal-cycles) 
27. [Quadratic primes](#quadratic-primes) 
28. [Number spiral diagonals](#number-spiral-diagonals) 
29. [Distinct powers](#distinct-powers) 
30. [Digit fifth powers](#digit-fifth-powers) 
31. [Coin sums](#coin-sums) 
32. [Pandigital products](#pandigital-products) 
33. [Digit cancelling fractions](#digit-cancelling-fractions) 
34. [Digit factorials](#digit-factorials) 
35. [Circular primes](#circular-primes) 
36. [Double-base palindromes](#double-base-palindromes) 
37. [Truncatable primes](#truncatable-primes) 
38. [Pandigital multiples](#pandigital-multiples) 
39. [Integer right triangles](#integer-right-triangles) 
40. [Champernowne's constant](#champernownes-constant) 
41. [Pandigital prime](#pandigital-prime) 
42. [Coded triangle numbers](#coded-triangle-numbers) 
43. [Sub-string divisibility](#sub-string-divisibility) 
44. [Pentagon numbers](#pentagon-numbers) 
45. [Triangular, pentagonal, and hexagonal](#triangular-pentagonal-and-hexagonal) 
46. [Goldbach's other conjecture](#goldbachs-other-conjecture) 
47. [Distinct primes factors](#distinct-primes-factors) 
48. [Self powers](#self-powers) 
49. [Prime permutations](#prime-permutations) 
50. [Consecutive prime sum](#consecutive-prime-sum) 

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Multiples of 3 or 5

- Problem 1

### Description

If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.

Find the sum of all the multiples of 3 or 5 below 1000.

### Solutions

<details>

<summary markdown="span">Brute Force</summary>

~~~py
print("Project Euler. Problem 1: Multiples of 3 or 5.")
total = 0
for i in range(1000):
    if i%3==0 or i%5==0:
        total += i

print("The sum of all the multiples of 3 or 5 below 1000 is: {}.".format(total))
~~~

~~~shell
$ python3 001_BF.py 
Project Euler. Problem 1: Multiples of 3 or 5.
The sum of all the multiples of 3 or 5 below 1000 is: 233168.
~~~

</details>

<details>

<summary markdown="span">Efficient Solution</summary>

We can calculate the sum of all multiple of a number by hand: the problem specifies we need to sum numbers below 1000 (up to 999) so we can find the number of multiples of an integer by dividing the maximum by an integer:

~~~
N_total = I_max / N:

N_3  = 999 / 3  = 333
N_5  = 999 / 5  = 199
N_15 = 999 / 15 = 66
~~~

The sum of all digits between A and B equal to the total count multiplied by the average.  The average of each number can be found:

~~~
Ave_N = (N(1) + N(max))/2

Ave_3  = (3+999)/2  = 501
Ave_5  = (5+995)/2  = 500
Ave_15 = (15+990)/2 = 502.5
~~~

Now the totals can be calculated:

~~~
T_3  = 333 x 501  = 166,833
T_5  = 199 x 500  =  99,500
T_15 = 66 x 502.5 =  33,165
~~~

Now we can summate the totals for the 3 and 5, however we will count multiples of both 3 and 5 twice, hence we should subtract the total of multiples of 15:

~~~
166,833 + 99,500 - 33,165 = 233,168
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
233,168
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Even Fibonacci numbers

- Problem 2

### Description

Each new term in the Fibonacci sequence is generated by adding the previous two terms. By starting with 1 and 2, the first 10 terms will be:

~~~
1, 2, 3, 5, 8, 13, 21, 34, 55, 89, ...
~~~

By considering the terms in the Fibonacci sequence whose values do not exceed four million, find the sum of the even-valued terms.

### Solutions

<details>

<summary markdown="span">Brute Force</summary>

~~~py
print("Project Euler. Problem 2: Even Fibonacci numbers.")
a = 1
b = 1
total = 0
while True:
    c = a+b
    if c > 4000000:
        break
    elif c%2 == 0:
        total += c
    a = b
    b = c
    
print("The sum of all the even fibonacci numbers below 4,000,000 is: {}.".format(total))
~~~

~~~shell
$ python3 002_BF.py 
Project Euler. Problem 2: Even Fibonacci numbers.
The sum of all the even fibonacci numbers below 4,000,000 is: 4613732.
~~~

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
4,613,732
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Largest Prime Factor

- Problem 3

### Description

The prime factors of 13195 are 5, 7, 13 and 29.

What is the largest prime factor of the number 600851475143 ?

### Solutions

<details>

<summary markdown="span">Brute Force</summary>

~~~py
import numpy as np
print("Project Euler. Problem 3: Largest Prime Factor.")
N = 600851475143
maxFactor = np.sqrt(N)
while N % 2 == 0:
    bigFactor = 2
    N = N/2
f = 3
while N > 1 and f < maxFactor:
    if N%f==0:
        N = N/f
        bigFactor = f
        while N%f ==0:
            N = N/f
        maxFactor = np.sqrt(N)
    f += 2
bigFactor = max(int(N),int(bigFactor))
print("maximum factor = {}".format(bigFactor))        
~~~

~~~shell
$ python3 003_BF.py 
Project Euler. Problem 3: Largest Prime Factor.
maximum factor = 6857
~~~

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
6857
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Largest palindrome product

- Problem 4

### Description

A palindromic number reads the same both ways. The largest palindrome made from the product of two 2-digit numbers is 9009 = 91 × 99.

Find the largest palindrome made from the product of two 3-digit numbers.

### Solutions

<details>

<summary markdown="span">Brute Force</summary>

~~~py
print("Project Euler. Problem 4: Largest Palindrome Product.")

done = 0
solution = 0

for i in range(10):
    for j in range(10):
        for k in range(10):
            a = str(9-i)
            b = str(9-j)
            c = str(9-k)
            dec_str = a+b+c+c+b+a
            NUM = int(dec_str)
            for l in range(999):
                x = 999-l
                if NUM%x==0:
                    y = int(NUM/x)
                    if y>99 and y < 1000:
                        solution = NUM
                        done = 1
                        break
                if NUM/x < 100:
                    break
                        
        if done == 1:
            break
    if done == 1:
        break

print("The largest palindromic number = {}.".format(solution))       
~~~

~~~shell
$ python3 004_BF.py 
Project Euler. Problem 4: Largest Palindrome Product.
The largest palindromic number = 906609.
~~~

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
906609
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---
This page was last updated Jan 22.
	
## [djm89uk.github.io](https://djm89uk.github.io)
