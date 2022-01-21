# [Project Euler](./euler.md) Challenges 1-50 (8/50)

[Project Euler](https://projecteuler.net/) was started by Colin Hughes (a.k.a. euler) in October 2001 as a sub-section on mathschallenge.net. Who could have known how popular these types of problems would turn out to be? Since then the membership has continued to grow and Project Euler moved to its own domain in 2006.

These are the first 50 challenges from the site.

## Contents

1. [Multiples of 3 or 5](#multiples-of-3-or-5) 🗸
2. [Even Fibonacci numbers](#even-fibonacci-numbers) 🗸
3. [Largest prime factor](#largest-prime-factor) 🗸
4. [Largest palindrome product](#largest-palindrome-product) 🗸
5. [Smallest multiple](#smallest-multiple) 🗸
6. [Sum square difference](#sum-square-difference) 🗸
7. [10001st prime](#10001st-prime) 🗸
8. [Largest product in a series](#largest-product-in-a-series) 🗸
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
while np.greater(N,1) and np.less(f,maxFactor):
    if N % f == 0:
        N = N/f
        bigFactor = f
        while N % f ==0:
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

## Smallest Multiple

- Problem 5

### Description

2520 is the smallest number that can be divided by each of the numbers from 1 to 10 without any remainder.

What is the smallest positive number that is evenly divisible by all of the numbers from 1 to 20?

### Solutions

<details>

<summary markdown="span">By Hand</summary>

We can simplify the integers as below:
	
| Int | Prime Factors | Is Prime |
|-----|---------------|----------|
|  2  | 2             | Y        |
|  3  | 3             | Y        |
|  4  | 2*2           | N        |
|  5  | 5             | Y        |
|  6  | 2*3           | N        |
|  7  | 7             | Y        |
|  8  | 2*2*2         | N        |
|  9  | 3*3           | N        |
| 10  | 2*5           | N        |
| 11  | 11            | Y        |
| 12  | 2*2*3         | N        |
| 13  | 13            | Y        |
| 14  | 2*7           | N        |
| 15  | 3*5           | N        |
| 16  | 2*2*2*2       | N        |
| 17  | 17            | Y        |
| 18  | 2*3*3         | N        |
| 19  | 19            | Y        |
| 20  | 2*2*5         | N        |

The solution will be a product of primes with minimum power of the maximum in the table above:
	
~~~
2*2*2*2 * 3*3 * 5 * 7 * 11 * 13 * 17 * 19 = 232792560
~~~

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
232792560
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Sum Square Difference

- Problem 6

### Description

The sum of the squares of the first ten natural numbers is:

~~~
1**2 + 2**2 + 3**2 + ... + 10**2 = 385
~~~

The square of the sum of the first ten natural numbers is,

~~~
(1+2+3+...+10)**2 = 3025
~~~

Hence the difference between the sum of the squares of the first ten natural numbers and the square of the sum is

~~~
3025 - 385 = 2640
~~~

Find the difference between the sum of the squares of the first one hundred natural numbers and the square of the sum.

### Solutions

<details>

<summary markdown="span">By Hand</summary>

We can rewite the problem as:
	
~~~
(sum(i))**2 - sum(i**2)  where i is in range 1 - 100
~~~

The first part of the equation can be simplified where:
	
~~~
sum(i) = n(n+1)/2
sum(i)**2 = n**2(n+1)**2/2
	  = n**2(n**2+2n+2)/2
	  = n**4/2 + n**3 + n**2
~~~

The second part can be written as a cubic equation:

~~~
sum(i**2) = a * n**3 + b * n**2 + c * n + d = f(n)
~~~

We can solve for the first few numbers:
	
~~~
f(0) = 0  -> d = 0
f(1) = 1  ->   a +   b +  c = 1
f(2) = 5  ->  8a +  4b + 2c = 5
f(3) = 14 -> 27a +  9b + 3c = 14
f(4) = 30 -> 64a + 16b + 4c = 30
~~~
	
We can solve this:

~~~
2a + 2b + 2c = 2
6a + 2b = 3

3a + 3b + 3c + 3d = 3
24a + 6b = 11

18a + 6b = 9
6a = 2

a = 1/3
b = 1/2
c = 1/6
d = 0
~~~

We can use this formula to calculate the second part of the equation:

~~~
sum(i**2) = n**3/3 + n**2/2 + n/6
~~~
	
We can now solve for n=100:

~~~
sum(1-100)**2 = (100(100+1)/2)**2 = (10100/2)**2 = 5050**2  = 25502500
sum(1**2 ... 100**2 = 100**3/3 + 100**2/2 + 100/6 = 333,333+1/3 + 5000 + 16 + 2/3  = 338350

sum(1-100)**2 - sum(1**2-100**2) = 25502500 - 338350 = 25164150
~~~

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
25164150
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## 10001st prime

- Problem 7

### Description

By listing the first six prime numbers: 2, 3, 5, 7, 11, and 13, we can see that the 6th prime is 13.

What is the 10 001st prime number?

### Solutions

<details>

<summary markdown="span">By Hand</summary>

We can write a simple Python prime sieve and solver:
	
~~~py
import numpy as np
def isprime(n):
    if n<2:
        return False
    elif n==2:
        return True
    else:
        lim = int(np.ceil(np.sqrt(n)))
        for i in range(2,lim+1):
            if n%i==0:
                return False
        return True

def findNprime(N):
   cand = 3
   pcount = 1
   while pcount < N:
       if isprime(cand):
           pcount += 1
           prime = cand
       cand += 2
   return prime

if __name__ == "__main__":
    N = findNprime(10001)
    print(N)
~~~

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
104743
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---


## Largest product in a series

- Problem 8

### Description

The four adjacent digits in the 1000-digit number that have the greatest product are 9 × 9 × 8 × 9 = 5832.

~~~
73167176531330624919225119674426574742355349194934
96983520312774506326239578318016984801869478851843
85861560789112949495459501737958331952853208805511
12540698747158523863050715693290963295227443043557
66896648950445244523161731856403098711121722383113
62229893423380308135336276614282806444486645238749
30358907296290491560440772390713810515859307960866
70172427121883998797908792274921901699720888093776
65727333001053367881220235421809751254540594752243
52584907711670556013604839586446706324415722155397
53697817977846174064955149290862569321978468622482
83972241375657056057490261407972968652414535100474
82166370484403199890008895243450658541227588666881
16427171479924442928230863465674813919123162824586
17866458359124566529476545682848912883142607690042
24219022671055626321111109370544217506941658960408
07198403850962455444362981230987879927244284909188
84580156166097919133875499200524063689912560717606
05886116467109405077541002256983155200055935729725
71636269561882670428252483600823257530420752963450
~~~

Find the thirteen adjacent digits in the 1000-digit number that have the greatest product. What is the value of this product?

### Solutions

<details>

<summary markdown="span">Python</summary>

We can write a simple Python code to solve:
	
~~~py
a = "7316717653133062491922511967442657474235534919493496983520312774506326239578318016984801869478851843858615607891129494954595017379583319528532088055111254069874715852386305071569329096329522744304355766896648950445244523161731856403098711121722383113622298934233803081353362766142828064444866452387493035890729629049156044077239071381051585930796086670172427121883998797908792274921901699720888093776657273330010533678812202354218097512545405947522435258490771167055601360483958644670632441572215539753697817977846174064955149290862569321978468622482839722413756570560574902614079729686524145351004748216637048440319989000889524345065854122758866688116427171479924442928230863465674813919123162824586178664583591245665294765456828489128831426076900422421902267105562632111110937054421750694165896040807198403850962455444362981230987879927244284909188845801561660979191338754992005240636899125607176060588611646710940507754100225698315520005593572972571636269561882670428252483600823257530420752963450"

maxP = 1

for i in range(len(a)-13):
    b = a[i:i+13]
    prod = 1
    for j in range(len(b)):
        prod *= int(b[j])
    if prod > maxP:
        maxP = prod
        
print(maxP)
~~~

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
23514624000
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

This page was last updated Jan 22.
	
## [djm89uk.github.io](https://djm89uk.github.io)
