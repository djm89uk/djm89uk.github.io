# [Project Euler](./euler.md) Challenges 1-50 (25/50)

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
9. [Special Pythagorean triplet](#special-pythagorean-triplet) 🗸
10. [Summation of primes](#summation-of-primes) 🗸
11. [Largest product in a grid](#largest-product-in-a-grid) 🗸
12. [Highly divisible triangular number](#highly-divisible-triangular-number) 🗸
13. [Large sum](#large-sum) 🗸
14. [Longest Collatz sequence](#longest-collatz-sequence) 🗸
15. [Lattice paths](#lattice-paths) 🗸
16. [Power digit sum](#power-digit-sum) 🗸
17. [Number letter counts](#number-letter-counts) 🗸
18. [Maximum path sum I](#maximum-path-sum-i) 🗸
19. [Counting Sundays](#counting-sundays) 🗸
20. [Factorial digit sum](#factorial-digit-sum) 🗸
21. [Amicable numbers](#amicable-numbers) 🗸
22. [Names scores](#names-scores) 🗸
23. [Non-abundant sums](#non-abundant-sums) 🗸
24. [Lexicographic permutations](#lexicographic-permutations) 🗸
25. [1000-digit Fibonacci number](#1000-digit-fibonacci-number) 🗸
26. [Reciprocal cycles](#reciprocal-cycles) 🗸
27. [Quadratic primes](#quadratic-primes) 🗸
28. [Number spiral diagonals](#number-spiral-diagonals) 🗸
29. [Distinct powers](#distinct-powers) 🗸
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

We can write a simple Python code to solve.  An efficient code is included to filter the integer string by splitting all continuous strings without "0" and removing strings less than 13 characters in length.
	
~~~py
import time

a = "7316717653133062491922511967442657474235534919493496983520312774506326239578318016984801869478851843858615607891129494954595017379583319528532088055111254069874715852386305071569329096329522744304355766896648950445244523161731856403098711121722383113622298934233803081353362766142828064444866452387493035890729629049156044077239071381051585930796086670172427121883998797908792274921901699720888093776657273330010533678812202354218097512545405947522435258490771167055601360483958644670632441572215539753697817977846174064955149290862569321978468622482839722413756570560574902614079729686524145351004748216637048440319989000889524345065854122758866688116427171479924442928230863465674813919123162824586178664583591245665294765456828489128831426076900422421902267105562632111110937054421750694165896040807198403850962455444362981230987879927244284909188845801561660979191338754992005240636899125607176060588611646710940507754100225698315520005593572972571636269561882670428252483600823257530420752963450"

def product(x):
    prod = 1
    for i in range(len(x)):
        prod *= int(x[i])
    return prod

def maxProduct(x,y):
    maxP = 1
    for i in range(len(x)-y+1):
        a = x[i:i+y]
        prod = product(a)
        if prod > maxP:
            maxP = prod
    return maxP

t0 = time.time()
maxP = maxProduct(a,13)
print(maxP)
t1 = time.time()
maxP = 1
c = [i for i in a.split("0") if len(i) >= 13]

maxP = 1
for d in c:
    maxP = max(maxP,maxProduct(d,13))
t2 = time.time()

print("Solver 1 solution in {} s".format(t1-t0))
print("Solver 2 solution in {} s".format(t2-t1))
print("Solution = {}".format(maxP))
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

## Special Pythagorean triplet

- Problem 9

### Description

A Pythagorean triplet is a set of three natural numbers, a < b < c, for which,

~~~
a**2 + b**2 = c**2
~~~

For example:

~~~
3**2 + 4**2 = 9 + 16 = 25 = 5**2.
~~~

There exists exactly one Pythagorean triplet for which a + b + c = 1000.
Find the product abc.

### Solutions

<details>

<summary markdown="span">Python</summary>

We can use Euclid's formula to solve:
	
~~~
a = m**2 - n**2
b = 2mn
c = m**2 + n**2
~~~

In python, our Euclidian Pythagorean Triplet solver:

~~~py
import time

t0 = time.time()
m = 2
end = False

for m in range(2,30):
    for n in range(1,m):
        if m%2!=0 and n%2!=0:
            continue
        else:
            a = m**2-n**2
            b = 2*m*n
            c = m**2+n**2
            if (a%1!=0) or (b%1!=0) or (c%1!=0):
                continue
            elif a+b+c==1000:
                print("a = {}\nb = {}\nc = {}".format(a,b,c))
                end = True
                break
    if end == True:
        break
t1 = time.time()
print("abc = {}".format(a*b*c))
print("Solution time = {} s".format(t1-t0))
~~~ 

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
31875000
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Summation of Primes

- Problem 10

### Description

The sum of the primes below 10 is 2 + 3 + 5 + 7 = 17.

Find the sum of all the primes below two million.

### Solutions

<details>

<summary markdown="span">Python</summary>

We can use a prime sieve to find all primes below 2 million and summate them:
	
~~~py
import time
import numpy as np

t0 = time.time()
integers = list(np.arange(0,int(2E6)))
isprime = np.ones(len(integers))
isprime[0] = 0
isprime[1] = 0
psum = 0

for i in range(len(integers)):
    if isprime[i]:
        prime = integers[i]
        psum += prime
        factor = 2*prime
        while factor < 2E6:
            isprime[factor] = 0
            factor += prime

t1 = time.time()
print("prime sum = {}".format(psum))
print("Solution time = {} s".format(t1-t0))
~~~ 

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
142913828922
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Largest product in a grid

- Problem 11

### Description

In the 20×20 grid below:

~~~
08 02 22 97 38 15 00 40 00 75 04 05 07 78 52 12 50 77 91 08
49 49 99 40 17 81 18 57 60 87 17 40 98 43 69 48 04 56 62 00
81 49 31 73 55 79 14 29 93 71 40 67 53 88 30 03 49 13 36 65
52 70 95 23 04 60 11 42 69 24 68 56 01 32 56 71 37 02 36 91
22 31 16 71 51 67 63 89 41 92 36 54 22 40 40 28 66 33 13 80
24 47 32 60 99 03 45 02 44 75 33 53 78 36 84 20 35 17 12 50
32 98 81 28 64 23 67 10 26 38 40 67 59 54 70 66 18 38 64 70
67 26 20 68 02 62 12 20 95 63 94 39 63 08 40 91 66 49 94 21
24 55 58 05 66 73 99 26 97 17 78 78 96 83 14 88 34 89 63 72
21 36 23 09 75 00 76 44 20 45 35 14 00 61 33 97 34 31 33 95
78 17 53 28 22 75 31 67 15 94 03 80 04 62 16 14 09 53 56 92
16 39 05 42 96 35 31 47 55 58 88 24 00 17 54 24 36 29 85 57
86 56 00 48 35 71 89 07 05 44 44 37 44 60 21 58 51 54 17 58
19 80 81 68 05 94 47 69 28 73 92 13 86 52 17 77 04 89 55 40
04 52 08 83 97 35 99 16 07 97 57 32 16 26 26 79 33 27 98 66
88 36 68 87 57 62 20 72 03 46 33 67 46 55 12 32 63 93 53 69
04 42 16 73 38 25 39 11 24 94 72 18 08 46 29 32 40 62 76 36
20 69 36 41 72 30 23 88 34 62 99 69 82 67 59 85 74 04 36 16
20 73 35 29 78 31 90 01 74 31 49 71 48 86 81 16 23 57 05 54
01 70 54 71 83 51 54 69 16 92 33 48 61 43 52 01 89 19 67 48
~~~

The product 4 of these adjacent numbers is 26 × 63 × 78 × 14 = 1788696.

What is the greatest product of four adjacent numbers in the same direction (up, down, left, right, or diagonally) in the 20×20 grid?

### Solutions

<details>

<summary markdown="span">Python</summary>

We can simply implement this in Python:
	
~~~py
import time
import numpy as np

t0 = time.time()

array = [ 8,  2, 22, 97, 38, 15,  0, 40,  0, 75,  4,  5,  7, 78, 52, 12, 50, 77, 91,  8,
         49, 49, 99, 40, 17, 81, 18, 57, 60, 87, 17, 40, 98, 43, 69, 48,  4, 56, 62,  0,
         81, 49, 31, 73, 55, 79, 14, 29, 93, 71, 40, 67, 53, 88, 30,  3, 49, 13, 36, 65,
         52, 70, 95, 23,  4, 60, 11, 42, 69, 24, 68, 56,  1, 32, 56, 71, 37,  2, 36, 91,
         22, 31, 16, 71, 51, 67, 63, 89, 41, 92, 36, 54, 22, 40, 40, 28, 66, 33, 13, 80,
         24, 47, 32, 60, 99,  3, 45,  2, 44, 75, 33, 53, 78, 36, 84, 20, 35, 17, 12, 50,
         32, 98, 81, 28, 64, 23, 67, 10, 26, 38, 40, 67, 59, 54, 70, 66, 18, 38, 64, 70,
         67, 26, 20, 68,  2, 62, 12, 20, 95, 63, 94, 39, 63,  8, 40, 91, 66, 49, 94, 21,
         24, 55, 58,  5, 66, 73, 99, 26, 97, 17, 78, 78, 96, 83, 14, 88, 34, 89, 63, 72,
         21, 36, 23,  9, 75,  0, 76, 44, 20, 45, 35, 14,  0, 61, 33, 97, 34, 31, 33, 95,
         78, 17, 53, 28, 22, 75, 31, 67, 15, 94,  3, 80,  4, 62, 16, 14,  9, 53, 56, 92,
         16, 39,  5, 42, 96, 35, 31, 47, 55, 58, 88, 24,  0, 17, 54, 24, 36, 29, 85, 57,
         86, 56,  0, 48, 35, 71, 89,  7,  5, 44, 44, 37, 44, 60, 21, 58, 51, 54, 17, 58,
         19, 80, 81, 68,  5, 94, 47, 69, 28, 73, 92, 13, 86, 52, 17, 77,  4, 89, 55, 40,
          4, 52,  8, 83, 97, 35, 99, 16,  7, 97, 57, 32, 16, 26, 26, 79, 33, 27, 98, 66,
         88, 36, 68, 87, 57, 62, 20, 72,  3, 46, 33, 67, 46, 55, 12, 32, 63, 93, 53, 69,
          4, 42, 16, 73, 38, 25, 39, 11, 24, 94, 72, 18,  8, 46, 29, 32, 40, 62, 76, 36,
         20, 69, 36, 41, 72, 30, 23, 88, 34, 62, 99, 69, 82, 67, 59, 85, 74,  4, 36, 16,
         20, 73, 35, 29, 78, 31, 90,  1, 74, 31, 49, 71, 48, 86, 81, 16, 23, 57,  5, 54,
          1, 70, 54, 71, 83, 51, 54, 69, 16, 92, 33, 48, 61, 43, 52,  1, 89, 19, 67, 48]

maxP = 0

for i in range(len(array)):
    idx = i%20
    idy = i//20
    if idx <= 16:  
        maxP = max(maxP,np.prod(array[i:i+4]))
    if idy <= 16:
        maxP = max(maxP,array[i]*array[i+20]*array[i+40]*array[i+60])
    if idx <= 16 and idy <= 16:
        maxP = max(maxP,array[i]*array[i+21]*array[i+42]*array[i+63])
    if idx >=4 and idy <= 16:
        maxP = max(maxP,array[i]*array[i+19]*array[i+38]*array[i+57])
t1 = time.time()
print("max product = {}".format(maxP))
print("Solution time = {} s".format(t1-t0))
~~~ 

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
70600674
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Highly divisible triangular number

- Problem 12

### Description

The sequence of triangle numbers is generated by adding the natural numbers. So the 7th triangle number would be 1 + 2 + 3 + 4 + 5 + 6 + 7 = 28. The first ten terms would be:

~~~
1, 3, 6, 10, 15, 21, 28, 36, 45, 55, ...
~~~

Let us list the factors of the first seven triangle numbers:

~~~
     1: 1
     3: 1,3
     6: 1,2,3,6
    10: 1,2,5,10
    15: 1,3,5,15
    21: 1,3,7,21
    28: 1,2,4,7,14,28
~~~

We can see that 28 is the first triangle number to have over five divisors.

What is the value of the first triangle number to have over five hundred divisors?

### Solutions

<details>

<summary markdown="span">Python</summary>

Triangle numbers can be found using the formula:

~~~
T = (n**2 + n)/2
~~~

This can be factored into the product of two coprime integers:

~~~
When n is even:
	N1 = n+1
	N2 = n/2

When n is odd:
	N1 = (n+1)/2
	N2 = n

T = N1*N2
~~~

The number of factors can be found by testing all integers from 1 to n/2 for each coprime and multiplying the result.  In Python a simple program can be written:
	
~~~py
import time

def divisor_count(n):
    count = 1
    for i in range(1,int(n/2)+1):
        if n%i == 0:
            count += 1
    return count

def tri_num(n):
    if n%2==0:
        N1 = int(n+1)
        N2 = int(n/2)
    else:
        N1 = int(n+1)/2
        N2 = int(n)
    factors = divisor_count(N1)*divisor_count(N2)
    return factors, int(N1*N2)

t0 = time.time()
n = 1
while True:
    F,T = tri_num(n)
    if F > 500:
        t1 = time.time()
        print("n = {}, T = {}, divisors = {}".format(n,T,F))
        print("Execution time = {} s".format(t1-t0))
        break
    else:
        n += 1
~~~

This executes in less than 2 seconds and returns the answer.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
76576500
~~~

</details>
	
---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---
	
## Large Sum
	
- Problem 13

### Description

Work out the first ten digits of the sum of the following one-hundred 50-digit numbers.

~~~
37107287533902102798797998220837590246510135740250
46376937677490009712648124896970078050417018260538
74324986199524741059474233309513058123726617309629
91942213363574161572522430563301811072406154908250
23067588207539346171171980310421047513778063246676
89261670696623633820136378418383684178734361726757
28112879812849979408065481931592621691275889832738
44274228917432520321923589422876796487670272189318
47451445736001306439091167216856844588711603153276
70386486105843025439939619828917593665686757934951
62176457141856560629502157223196586755079324193331
64906352462741904929101432445813822663347944758178
92575867718337217661963751590579239728245598838407
58203565325359399008402633568948830189458628227828
80181199384826282014278194139940567587151170094390
35398664372827112653829987240784473053190104293586
86515506006295864861532075273371959191420517255829
71693888707715466499115593487603532921714970056938
54370070576826684624621495650076471787294438377604
53282654108756828443191190634694037855217779295145
36123272525000296071075082563815656710885258350721
45876576172410976447339110607218265236877223636045
17423706905851860660448207621209813287860733969412
81142660418086830619328460811191061556940512689692
51934325451728388641918047049293215058642563049483
62467221648435076201727918039944693004732956340691
15732444386908125794514089057706229429197107928209
55037687525678773091862540744969844508330393682126
18336384825330154686196124348767681297534375946515
80386287592878490201521685554828717201219257766954
78182833757993103614740356856449095527097864797581
16726320100436897842553539920931837441497806860984
48403098129077791799088218795327364475675590848030
87086987551392711854517078544161852424320693150332
59959406895756536782107074926966537676326235447210
69793950679652694742597709739166693763042633987085
41052684708299085211399427365734116182760315001271
65378607361501080857009149939512557028198746004375
35829035317434717326932123578154982629742552737307
94953759765105305946966067683156574377167401875275
88902802571733229619176668713819931811048770190271
25267680276078003013678680992525463401061632866526
36270218540497705585629946580636237993140746255962
24074486908231174977792365466257246923322810917141
91430288197103288597806669760892938638285025333403
34413065578016127815921815005561868836468420090470
23053081172816430487623791969842487255036638784583
11487696932154902810424020138335124462181441773470
63783299490636259666498587618221225225512486764533
67720186971698544312419572409913959008952310058822
95548255300263520781532296796249481641953868218774
76085327132285723110424803456124867697064507995236
37774242535411291684276865538926205024910326572967
23701913275725675285653248258265463092207058596522
29798860272258331913126375147341994889534765745501
18495701454879288984856827726077713721403798879715
38298203783031473527721580348144513491373226651381
34829543829199918180278916522431027392251122869539
40957953066405232632538044100059654939159879593635
29746152185502371307642255121183693803580388584903
41698116222072977186158236678424689157993532961922
62467957194401269043877107275048102390895523597457
23189706772547915061505504953922979530901129967519
86188088225875314529584099251203829009407770775672
11306739708304724483816533873502340845647058077308
82959174767140363198008187129011875491310547126581
97623331044818386269515456334926366572897563400500
42846280183517070527831839425882145521227251250327
55121603546981200581762165212827652751691296897789
32238195734329339946437501907836945765883352399886
75506164965184775180738168837861091527357929701337
62177842752192623401942399639168044983993173312731
32924185707147349566916674687634660915035914677504
99518671430235219628894890102423325116913619626622
73267460800591547471830798392868535206946944540724
76841822524674417161514036427982273348055556214818
97142617910342598647204516893989422179826088076852
87783646182799346313767754307809363333018982642090
10848802521674670883215120185883543223812876952786
71329612474782464538636993009049310363619763878039
62184073572399794223406235393808339651327408011116
66627891981488087797941876876144230030984490851411
60661826293682836764744779239180335110989069790714
85786944089552990653640447425576083659976645795096
66024396409905389607120198219976047599490197230297
64913982680032973156037120041377903785566085089252
16730939319872750275468906903707539413042652315011
94809377245048795150954100921645863754710598436791
78639167021187492431995700641917969777599028300699
15368713711936614952811305876380278410754449733078
40789923115535562561142322423255033685442488917353
44889911501440648020369068063960672322193204149535
41503128880339536053299340368006977710650566631954
81234880673210146739058568557934581403627822703280
82616570773948327592232845941706525094512325230608
22918802058777319719839450180888072429661980811197
77158542502016545090413245809786882778948721859617
72107838435069186155435662884062257473692284509516
20849603980134001723930671666823555245252804609722
53503534226472524250874054075591789781264330331690
~~~

### Solutions

<details>

<summary markdown="span">Python</summary>

We can simply implement this in Python, optimising by using the first 11 digits of each big number:
	
~~~py
import numpy as np
import time

t0 = time.time()

a = [37107287533902102798797998220837590246510135740250,
    46376937677490009712648124896970078050417018260538,
    74324986199524741059474233309513058123726617309629,
    91942213363574161572522430563301811072406154908250,
    23067588207539346171171980310421047513778063246676,
    89261670696623633820136378418383684178734361726757,
    28112879812849979408065481931592621691275889832738,
    44274228917432520321923589422876796487670272189318,
    47451445736001306439091167216856844588711603153276,
    70386486105843025439939619828917593665686757934951,
    62176457141856560629502157223196586755079324193331,
    64906352462741904929101432445813822663347944758178,
    92575867718337217661963751590579239728245598838407,
    58203565325359399008402633568948830189458628227828,
    80181199384826282014278194139940567587151170094390,
    35398664372827112653829987240784473053190104293586,
    86515506006295864861532075273371959191420517255829,
    71693888707715466499115593487603532921714970056938,
    54370070576826684624621495650076471787294438377604,
    53282654108756828443191190634694037855217779295145,
    36123272525000296071075082563815656710885258350721,
    45876576172410976447339110607218265236877223636045,
    17423706905851860660448207621209813287860733969412,
    81142660418086830619328460811191061556940512689692,
    51934325451728388641918047049293215058642563049483,
    62467221648435076201727918039944693004732956340691,
    15732444386908125794514089057706229429197107928209,
    55037687525678773091862540744969844508330393682126,
    18336384825330154686196124348767681297534375946515,
    80386287592878490201521685554828717201219257766954,
    78182833757993103614740356856449095527097864797581,
    16726320100436897842553539920931837441497806860984,
    48403098129077791799088218795327364475675590848030,
    87086987551392711854517078544161852424320693150332,
    59959406895756536782107074926966537676326235447210,
    69793950679652694742597709739166693763042633987085,
    41052684708299085211399427365734116182760315001271,
    65378607361501080857009149939512557028198746004375,
    35829035317434717326932123578154982629742552737307,
    94953759765105305946966067683156574377167401875275,
    88902802571733229619176668713819931811048770190271,
    25267680276078003013678680992525463401061632866526,
    36270218540497705585629946580636237993140746255962,
    24074486908231174977792365466257246923322810917141,
    91430288197103288597806669760892938638285025333403,
    34413065578016127815921815005561868836468420090470,
    23053081172816430487623791969842487255036638784583,
    11487696932154902810424020138335124462181441773470,
    63783299490636259666498587618221225225512486764533,
    67720186971698544312419572409913959008952310058822,
    95548255300263520781532296796249481641953868218774,
    76085327132285723110424803456124867697064507995236,
    37774242535411291684276865538926205024910326572967,
    23701913275725675285653248258265463092207058596522,
    29798860272258331913126375147341994889534765745501,
    18495701454879288984856827726077713721403798879715,
    38298203783031473527721580348144513491373226651381,
    34829543829199918180278916522431027392251122869539,
    40957953066405232632538044100059654939159879593635,
    29746152185502371307642255121183693803580388584903,
    41698116222072977186158236678424689157993532961922,
    62467957194401269043877107275048102390895523597457,
    23189706772547915061505504953922979530901129967519,
    86188088225875314529584099251203829009407770775672,
    11306739708304724483816533873502340845647058077308,
    82959174767140363198008187129011875491310547126581,
    97623331044818386269515456334926366572897563400500,
    42846280183517070527831839425882145521227251250327,
    55121603546981200581762165212827652751691296897789,
    32238195734329339946437501907836945765883352399886,
    75506164965184775180738168837861091527357929701337,
    62177842752192623401942399639168044983993173312731,
    32924185707147349566916674687634660915035914677504,
    99518671430235219628894890102423325116913619626622,
    73267460800591547471830798392868535206946944540724,
    76841822524674417161514036427982273348055556214818,
    97142617910342598647204516893989422179826088076852,
    87783646182799346313767754307809363333018982642090,
    10848802521674670883215120185883543223812876952786,
    71329612474782464538636993009049310363619763878039,
    62184073572399794223406235393808339651327408011116,
    66627891981488087797941876876144230030984490851411,
    60661826293682836764744779239180335110989069790714,
    85786944089552990653640447425576083659976645795096,
    66024396409905389607120198219976047599490197230297,
    64913982680032973156037120041377903785566085089252,
    16730939319872750275468906903707539413042652315011,
    94809377245048795150954100921645863754710598436791,
    78639167021187492431995700641917969777599028300699,
    15368713711936614952811305876380278410754449733078,
    40789923115535562561142322423255033685442488917353,
    44889911501440648020369068063960672322193204149535,
    41503128880339536053299340368006977710650566631954,
    81234880673210146739058568557934581403627822703280,
    82616570773948327592232845941706525094512325230608,
    22918802058777319719839450180888072429661980811197,
    77158542502016545090413245809786882778948721859617,
    72107838435069186155435662884062257473692284509516,
    20849603980134001723930671666823555245252804609722,
    53503534226472524250874054075591789781264330331690]

b = [int(str(el)[:11]) for el in a]

answer = str(sum(b))[:10]
t1 = time.time()
print("First 10 digits = {}".format(answer[:10]))
print("Execution time = {}s".format(t1-t0))
~~~ 

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
5537376230
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Longest Collatz Sequence
	
- Problem 14

### Description

The following iterative sequence is defined for the set of positive integers:

~~~
n → n/2 (n is even)
n → 3n + 1 (n is odd)
~~~

Using the rule above and starting with 13, we generate the following sequence:

~~~
13 → 40 → 20 → 10 → 5 → 16 → 8 → 4 → 2 → 1
~~~

It can be seen that this sequence (starting at 13 and finishing at 1) contains 10 terms. Although it has not been proved yet (Collatz Problem), it is thought that all starting numbers finish at 1.

Which starting number, under one million, produces the longest chain?

NOTE: Once the chain starts the terms are allowed to go above one million.

### Solutions

<details>

<summary markdown="span">Python</summary>

We can write an efficient algorithm in Python using memoization:
	
~~~py
import numpy as np
import time

t0 = time.time()
memo = {}                               # initialize the memo dictionary
def collatz_seq(n):
    if not n in memo:                   # check if already computed
        if n == 1:                      # if not compute it
            memo[n] = 1                 # cache it
        elif n % 2 == 0:
            memo[n] = collatz_seq(n // 2) + 1
        else:
            memo[n] = collatz_seq(3*n + 1) + 1
    return memo[n]  

for i in range(1,int(1E6)):
    collatz_seq(i)
    
max_value = max(memo, key=memo.get)
t1 = time.time()

    
print("Longest Collatz Sequence starting below 1 million starts at {} with length {}.".format(max_value,memo.get(max_value)))
print("Execution time = {}s.".format(t1-t0))
~~~ 

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
837799
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Lattice paths

- Problem 15

### Description

Starting in the top left corner of a 2×2 grid, and only being able to move to the right and down, there are exactly 6 routes to the bottom right corner.

How many such routes are there through a 20×20 grid?

### Solutions

<details>

<summary markdown="span">Python</summary>

This is a simple combinatorics questions where the number of paths can be found from the binomial coefficient of the lattice dimensions:
	
~~~py
import time
import math

def lattice_paths(n,m):
    p = math.comb(n+m,n)
    return p

if __name__ == "__main__":
    t0 = time.time()
    ans = lattice_paths(20,20)
    t1 = time.time()
    print("Number of paths for {}x{} grid = {}".format(20,20,ans))
    print("Solution took {} s".format(t1-t0))
~~~

This provides the answer in 2e-6 seconds.

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
137846528820
~~~

</details>

	
---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Power digit sum

- Problem 16

### Description

~~~
2^15 = 32768
~~~

The sum of its digits is 3 + 2 + 7 + 6 + 8 = 26.

What is the sum of the digits of the number 

~~~
2^1000?
~~~

### Solutions

<details>

<summary markdown="span">Python</summary>

This can be implemented simply in Python:
	
~~~py
import time

t0 = time.time()

x = 2**1000
y = str(x)
ans = 0
for c in y:
    ans += int(c)
t1 = time.time()

print("2^1000 = {}".format(x))
print("Sum of all digits = {}".format(ans))
print("execution time = {} s".format(t1-t0))
~~~

This provides the answer in 4e-5

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
1366
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Number letter counts

- Problem 17

### Description

If the numbers 1 to 5 are written out in words: one, two, three, four, five, then there are 3 + 3 + 5 + 4 + 4 = 19 letters used in total.

If all the numbers from 1 to 1000 (one thousand) inclusive were written out in words, how many letters would be used?

NOTE: Do not count spaces or hyphens. For example, 342 (three hundred and forty-two) contains 23 letters and 115 (one hundred and fifteen) contains 20 letters. The use of "and" when writing out numbers is in compliance with British usage.

### Solutions

<details>

<summary markdown="span">Python</summary>

This can be implemented in python with the library num2words:
	
~~~py
import time
from num2words import num2words as n2w

t0 = time.time()
L = 0
for i in range(1,1001):
    word = "".join("".join(n2w(i,lang='en_GB').split(" ")).split("-"))
    L += len(word)

t1 = time.time()
print("Total character count = {}".format(L))
print("execution time = {} s".format(t1-t0))
~~~

This provides the answer in 0.02 seconds

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
21124
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Maximum path sum I

- Problem 17

### Description



By starting at the top of the triangle below and moving to adjacent numbers on the row below, the maximum total from top to bottom is 23.

~~~
3
7 4
2 4 6
8 5 9 3
~~~

That is, 3 + 7 + 4 + 9 = 23.

Find the maximum total from top to bottom of the triangle below:

~~~
75
95 64
17 47 82
18 35 87 10
20 04 82 47 65
19 01 23 75 03 34
88 02 77 73 07 63 67
99 65 04 28 06 16 70 92
41 41 26 56 83 40 80 70 33
41 48 72 33 47 32 37 16 94 29
53 71 44 65 25 43 91 52 97 51 14
70 11 33 28 77 73 17 78 39 68 17 57
91 71 52 38 17 14 91 43 58 50 27 29 48
63 66 04 68 89 53 67 30 73 16 69 87 40 31
04 62 98 27 23 09 70 98 73 93 38 53 60 04 23
~~~

NOTE: As there are only 16384 routes, it is possible to solve this problem by trying every route. However, Problem 67, is the same challenge with a triangle containing one-hundred rows; it cannot be solved by brute force, and requires a clever method! ;o)

### Solutions

<details>

<summary markdown="span">Python</summary>

This can be implemented in python by iterating through the rows of the triangle:
	
~~~py
import time

T = [[75],[95, 64],[17, 47, 82],[18, 35, 87, 10],[20, 4, 82, 47, 65],[19, 1, 23, 75, 3, 34],[88, 2, 77, 73, 7, 63, 67],[99, 65, 4, 28, 6, 16, 70, 92],[41, 41, 26, 56, 83, 40, 80, 70, 33],[41, 48, 72, 33, 47, 32, 37, 16, 94, 29],[53, 71, 44, 65, 25, 43, 91, 52, 97, 51, 14],[70, 11, 33, 28, 77, 73, 17, 78, 39, 68, 17, 57],[91, 71, 52, 38, 17, 14, 91, 43, 58, 50, 27, 29, 48],[63, 66, 4, 68, 89, 53, 67, 30, 73, 16, 69, 87, 40, 31],[4, 62, 98, 27, 23, 9, 70, 98, 73, 93, 38, 53, 60, 4, 23]]
t0 = time.time()
for i in range(1,len(T)):
    T[i][0] += T[i-1][0]
    T[i][-1] += T[i-1][-1]
    if len(T[i])>2:
        for j in range(1,len(T[i])-1):
            T[i][j] += max(T[i-1][j-1],T[i-1][j])
            
M = max(T[-1])

t1 = time.time()
print("Maximum sum = {}".format(M))
print("execution time = {} s".format(t1-t0))
~~~

This provides the answer in 30E-6 seconds.

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
1074
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---
	

## Counting Sundays

- Problem 19

### Description

You are given the following information, but you may prefer to do some research for yourself.

- 1 Jan 1900 was a Monday.
- Thirty days has September,
- April, June and November.
- All the rest have thirty-one,
- Saving February alone,
- Which has twenty-eight, rain or shine.
- And on leap years, twenty-nine.
- A leap year occurs on any year evenly divisible by 4, but not on a century unless it is divisible by 400.

How many Sundays fell on the first of the month during the twentieth century (1 Jan 1901 to 31 Dec 2000)?

### Solutions

<details>

<summary markdown="span">Python</summary>

This could be solved using simple algebra, however Python has a library, datetime that can solve this simply:
	
~~~py
import time
from datetime import datetime as dt

t0 = time.time()
count= 0
for i in range(1901,2001):
    for j in range(1,13):
        x = dt(i,j,1,12,00,00,00)
        if x.weekday() == 6:
            count += 1
            
t1 = time.time()

print("Total number of Sundays = {}".format(count))
print("execution time = {} seconds.".format(t1-t0))
~~~

This provides the answer in 0.3 milliseconds.

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
171
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Factorial digit sum

- Problem 20

### Description

n! means n × (n − 1) × ... × 3 × 2 × 1

For example, 10! = 10 × 9 × ... × 3 × 2 × 1 = 3628800,
and the sum of the digits in the number 10! is 3 + 6 + 2 + 8 + 8 + 0 + 0 = 27.

Find the sum of the digits in the number 100!

### Solutions

<details>

<summary markdown="span">Python</summary>

Two solutions in Python are provided, using math library and a simplified for loop:
	
~~~py
import time
import math
t0 = time.time()
total1 = 0
x = str(math.factorial(100))
for char in x:
    total1 += int(char)
t1 = time.time()
prod = 1
for i in range(0,100):
    if i%10 != 0:
        prod *= i
total2 = 0
x = str(math.factorial(100))
for char in x:
    total2 += int(char)
t2 = time.time()

print("Method 1 using math library:")
print("Total = {}".format(total1))
print("execution time = {} seconds.".format(t1-t0))

print("Method 2 using for loop:")
print("Total = {}".format(total2))
print("execution time = {} seconds.".format(t2-t1))
~~~

This provides the answer in 24E-6 seconds.

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
648
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Amicable Numbers

- Problem 21

### Description

Let d(n) be defined as the sum of proper divisors of n (numbers less than n which divide evenly into n).
If d(a) = b and d(b) = a, where a ≠ b, then a and b are an amicable pair and each of a and b are called amicable numbers.

For example, the proper divisors of 220 are 1, 2, 4, 5, 10, 11, 20, 22, 44, 55 and 110; therefore d(220) = 284. The proper divisors of 284 are 1, 2, 4, 71 and 142; so d(284) = 220.

Evaluate the sum of all the amicable numbers under 10000.

### Solutions

<details>

<summary markdown="span">Python</summary>

A simple solution can be written in Python:
	
~~~py
import time
import numpy as np

def d_n(n):
    divisors = [1]
    for i in range(2,n//2,2):
        if i in divisors:
            continue
        elif n%i == 0:
            divisors.append(i)
            divisors.append(n//i)
    divs = list(set(divisors))
    total = np.sum(divs)
    return total
    
def amicable(n):
    d = d_n(n)
    if d_n(d)==n:
        return d
    else:
        return 0
    
t0 = time.time()
a_list = []
for i in range(2,10000,2):
    d = amicable(i)
    if d in a_list:
        continue
    elif d!=0 and d!=i:
        a_list.append(i)
        a_list.append(d)
a_list = list(set(a_list))
total = np.sum(a_list)
t1 = time.time()

print("Total = {}".format(total))
print("execution time = {} seconds.".format(t1-t0))
~~~

This provides the answer in 7 seconds.

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
31626
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Names scores

- Problem 22

### Description

Using names.txt (right click and 'Save Link/Target As...'), a 46K text file containing over five-thousand first names, begin by sorting it into alphabetical order. Then working out the alphabetical value for each name, multiply this value by its alphabetical position in the list to obtain a name score.

For example, when the list is sorted into alphabetical order, COLIN, which is worth 3 + 15 + 12 + 9 + 14 = 53, is the 938th name in the list. So, COLIN would obtain a score of 938 × 53 = 49714.

What is the total of all the name scores in the file?


### Solutions

<details>

<summary markdown="span">Python</summary>

A simple solution can be written in Python:
	
~~~py
import time

t0 = time.time()

file = "names.txt"
names_file = open(file,"r")
names_raw = names_file.read().split("\"")
names_ascii = "".join(names_raw).split(",")
names_ascii.sort()
names_value = []
i = 1
totalval = 0
for name in names_ascii:
    val = 0
    for char in name:
        val += ord(char)-64
    names_value.append(val)
    totalval += val*i
    i += 1

t1 = time.time()

print("Total = {}".format(totalval))
print("execution time = {} seconds.".format(t1-t0))
~~~

This provides the answer in 4 milliseconds.

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
871198282
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Non abundant sums

- Problem 23

### Description

A perfect number is a number for which the sum of its proper divisors is exactly equal to the number. For example, the sum of the proper divisors of 28 would be 1 + 2 + 4 + 7 + 14 = 28, which means that 28 is a perfect number.

A number n is called deficient if the sum of its proper divisors is less than n and it is called abundant if this sum exceeds n.

As 12 is the smallest abundant number, 1 + 2 + 3 + 4 + 6 = 16, the smallest number that can be written as the sum of two abundant numbers is 24. By mathematical analysis, it can be shown that all integers greater than 28123 can be written as the sum of two abundant numbers. However, this upper limit cannot be reduced any further by analysis even though it is known that the greatest number that cannot be expressed as the sum of two abundant numbers is less than this limit.

Find the sum of all the positive integers which cannot be written as the sum of two abundant numbers.

### Solutions

<details>

<summary markdown="span">Python</summary>

A simple solution can be written in Python:
	
~~~py
import time
import numpy as np

def is_abundant(n):
    total = 1
    for i in range(2,int(np.sqrt(n))+1):
        if n/i==i:
            total += i
        elif n%i == 0:
            total += i + n//i
    if total > n:
        return 1
    else:
        return 0

t0 = time.time()

a_numbers = [12]
integers = list(range(1,28123+1))
integers.pop(integers.index(24))

for i in range(13,28123-12+1):
    if is_abundant(i):
        a_numbers.append(i)
        for num in a_numbers:
            newsum = num+i
            if newsum in integers:
                integers.pop(integers.index(newsum))
total = np.sum(integers)
t1 = time.time()

print("Total = {}".format(total))
print("execution time = {} seconds.".format(t1-t0))
~~~

This provides the answer in 10 minutes.

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
4179871
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Lexicographic Permutations

- Problem 24

### Description


A permutation is an ordered arrangement of objects. For example, 3124 is one possible permutation of the digits 1, 2, 3 and 4. If all of the permutations are listed numerically or alphabetically, we call it lexicographic order. The lexicographic permutations of 0, 1 and 2 are:

012   021   102   120   201   210

What is the millionth lexicographic permutation of the digits 0, 1, 2, 3, 4, 5, 6, 7, 8 and 9?

### Solutions

<details>

<summary markdown="span">Python</summary>

Each integer changes with the factorial of the index (e.g. the 10th index will change every 9! iterations).  We can write a simple python code to solve:
	
~~~py
import math
import time

t0 = time.time()
integers = list(range(0,10))
r = 999999
string = ""
for i in range(9,-1,-1):
    a = int(r//math.factorial(i))
    r -= a*math.factorial(i)
    x = integers.pop(a)
    string += str(x)
t1 = time.time()

print("1 millionth lexicographic number = {}".format(string))
print("execution time = {} s.".format(t1-t0))
~~~

This provides the answer in 10 nanoseconds.

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
2783915460
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## 1000 digit Fibonacci number

- Problem 25

### Description

The Fibonacci sequence is defined by the recurrence relation:

    Fn = Fn−1 + Fn−2, where F1 = 1 and F2 = 1.

Hence the first 12 terms will be:

    F1 = 1
    F2 = 1
    F3 = 2
    F4 = 3
    F5 = 5
    F6 = 8
    F7 = 13
    F8 = 21
    F9 = 34
    F10 = 55
    F11 = 89
    F12 = 144

The 12th term, F12, is the first term to contain three digits.

What is the index of the first term in the Fibonacci sequence to contain 1000 digits?

### Solutions

<details>

<summary markdown="span">Python</summary>

A simple python code to solve:
	
~~~py
import time

t0 = time.time()
a = 1
b = 1
l = 1
i = 2
while l != 1000:
    c = a + b
    l = len(str(c))
    a = b
    b = c
    i += 1
t1= time.time()
print("i = {}".format(i))
print("execution time = {} seconds.".format(t1-t0))
~~~

This provides the answer in 22 milliseconds.

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
4782
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---
	
## Reciprocal Cycles

- Problem 26

### Description

A unit fraction contains 1 in the numerator. The decimal representation of the unit fractions with denominators 2 to 10 are given:

1/2	= 	0.5
1/3	= 	0.(3)
1/4	= 	0.25
1/5	= 	0.2
1/6	= 	0.1(6)
1/7	= 	0.(142857)
1/8	= 	0.125
1/9	= 	0.(1)
1/10	= 	0.1

Where 0.1(6) means 0.166666..., and has a 1-digit recurring cycle. It can be seen that 1/7 has a 6-digit recurring cycle.

Find the value of d < 1000 for which 1/d contains the longest recurring cycle in its decimal fraction part.

### Solutions

<details>

<summary markdown="span">Python</summary>

A simple python code to solve:
	
~~~py
import time

t0 = time.time()
rlen_max = 0
ans = 0

for i in range(1,1000):
    if i%2==0:
        continue
    elif i%5==0:
        continue
    else:
        r = 10
        x = {}
        j = 0
        while r != 0:
            if r in x:
                rlen = j-x[r]
                if rlen > rlen_max:
                    rlen_max = rlen
                    ans = i
                break
            x[r] = j
            r = 10*(r%i)
            j+=1
t1 = time.time()
print("Reciprocal Cycles, Project Euler Problem 26")
print("Answer = {}".format(ans))
print("Recurring length = {}".format(rlen_max))
print("1/{} = {}...".format(ans,1.0/ans))
print("execution time = {} seconds.".format(t1-t0))
~~~

This provides the answer in 11 milliseconds:
	
~~~
Reciprocal Cycles, Project Euler Problem 26
Answer = 983
Recurring length = 982
1/983 = 0.001017293997965412...
execution time = 0.011209487915039062 seconds.
~~~

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
983
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## Quadratic primes

- Problem 27

### Description

Euler discovered the remarkable quadratic formula:
	
	n^2+n+41

It turns out that the formula will produce 40 primes for the consecutive integer values 0<=n<=39. However, when n =40, 40^2+40+41 = 40(40+1) + 41 is divisible by 41, and certainly when n=41, 41^2+41+41 is clearly divisible by 41.

The incredible formula n^2-79n+1601 was discovered, which produces 80 primes for the consecutive values 0<=n<=79. The product of the coefficients, −79 and 1601, is −126479.

Considering quadratics of the form:

	n^2 + an + b, where |a| < 1000 and |b| <= 1000
	where |n| is the modulus/absolute value of n
	e.g. |11| = 11 and |-4| = 4

Find the product of the coefficients, a and b, for the quadratic expression that produces the maximum number of primes for consecutive values of n, starting with n=0.

### Solutions

<details>

<summary markdown="span">Python</summary>

The solution includes the case where n=0; therefore, b must be prime. Further, the case of n=1: 1 + a + b = prime, a must be an odd number.  We can simplify the problem:
	
b is prime
1 < b < 1000
a is odd.
-1000 < a < 1000

We can implement a solution in Python:

~~~py
import time
import sympy

t0 = time.time()
# generate a list of primes for b:
b_primes = list(sympy.primerange(0,1000))[::-1]
ans_len = 0
ans_a = 0
ans_b = 0

for b in b_primes:
    if b-1 < ans_len:
        break
    for a in range(-999,1000,2):
        n = 0
        p_len = 0
        while(sympy.isprime(n**2+a*n+b)):
            p_len += 1
            n += 1
        if p_len > ans_len:
            ans_len = p_len
            ans_a = a
            ans_b = b
    
ans = ans_a*ans_b
t1 = time.time()

print("Quadratic primes, Project Euler Problem 27")
print("Answer = {}".format(ans))
print("a = {}, b = {}, consecutive primes = {}".format(ans_a,ans_b,ans_len))
print("execution time = {} seconds.".format(t1-t0))
~~~

This provides the answer in 259 milliseconds:
	
~~~
Quadratic primes, Project Euler Problem 27
Answer = -59231
a = -61, b = 971, consecutive primes = 71
execution time = 0.2599170207977295 seconds.
~~~

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
-59231
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---
	
## Number spiral diagonals

- Problem 28

### Description

Starting with the number 1 and moving to the right in a clockwise direction a 5 by 5 spiral is formed as follows:

21 22 23 24 25
20  7  8  9 10
19  6  1  2 11
18  5  4  3 12
17 16 15 14 13

It can be verified that the sum of the numbers on the diagonals is 101.

What is the sum of the numbers on the diagonals in a 1001 by 1001 spiral formed in the same way?

### Solutions

<details>

<summary markdown="span">Python</summary>

A simple python code to solve:
	
~~~py
import time

t0 = time.time()
T = 1

for i in range(3,1002,2):
    T += 4*i**2 - 6*i + 6
t1 = time.time()
ans = T

print("Number spiral diagonals, Project Euler Problem 27")
print("Answer = {}".format(ans))
print("execution time = {} seconds.".format(t1-t0))
~~~

This provides the answer in 0.1 milliseconds:
	
~~~
Number spiral diagonals, Project Euler Problem 28
Answer = 669171001
execution time = 0.0001323223114013672 seconds.
~~~

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
669171001
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---
	
## Distinct powers

- Problem 29

### Description

Consider all integer combinations of ab for 2 ≤ a ≤ 5 and 2 ≤ b ≤ 5:

    2^2=4,  2^3=8,   2^4=16,  2^5=32
    3^2=9,  3^3=27,  3^4=81,  3^5=243
    4^2=16, 4^3=64,  4^4=256, 4^5=1024
    5^2=25, 5^3=125, 5^4=625, 5^5=3125

If they are then placed in numerical order, with any repeats removed, we get the following sequence of 15 distinct terms:

4, 8, 9, 16, 25, 27, 32, 64, 81, 125, 243, 256, 625, 1024, 3125

How many distinct terms are in the sequence generated by ab for 2 ≤ a ≤ 100 and 2 ≤ b ≤ 100?

### Solutions

<details>

<summary markdown="span">Python</summary>

A simple python code to solve:
	
~~~py
import time

t0 = time.time()

solns = []

for a in range(2,101):
    for b in range(2,101):
        solns.append(a**b)

unique_solns = list(set(solns))
ans = len(unique_solns)

t1 = time.time()

print("Distinct powers, Project Euler Problem 29")
print("Answer = {}".format(ans))
print("execution time = {} seconds.".format(t1-t0))
~~~

This provides the answer in 0.1 milliseconds:
	
~~~
Distinct powers, Project Euler Problem 29
Answer = 9183
execution time = 0.0037431716918945312 seconds.
~~~

</details>


### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
9183
~~~

</details>

---

### [Project Euler 1-50](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---
	
This page was last updated Nov 22.
	
## [djm89uk.github.io](https://djm89uk.github.io)
