# [ProjectEuler](./euler.md) Project Euler 001-100

Binary exploitation is the process of subverting a compiled application such that it violates some trust boundary in a way that is advantageous to you, the attacker.

## Contents

- [001. Multiples of 3 and 5](#1-multiples-of-3-and-5)
- [002. Even Fibonacci Numbers](#2-even-fibonacci-numbers)
- [003. Largest Prime Factor](#3-largest-prime-factor)
- [seed-sPRiNG](#seed-spring)
- [sice_cream](#sice-cream)
- [zero_to_hero](#zero-to-hero)

---

### [PE 0-100](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## 1. Multiples of 3 and 5

### Description

If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.

Find the sum of all the multiples of 3 or 5 below 1000.

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This can be solved using a simple for loop in Python:

~~~py
total = 0
for i in range(0,1000,1):
    if i%3==0 or i%5==0:
        total += i

print(total)
~~~

This returns 233168.

</details>

<details>

<summary markdown="span">Solution 2</summary>

We can solve this by hand:

$$\mathrm{floor}\left(\frac{999}{3}\right) = 333$$

There are 333 multiples of 3 between 1 and 999.  The total can be found from:

$$\left(3+999\right)\times\left(\frac{333}{2}\right) = 1002\times166.5 = 166833$$

We can do the same for 5:

$$\mathrm{floor}\left(\frac{999}{5}\right) = 199$$

$$\left(5+995\right)\times\left(\frac{199}{2}\right) = 1000\times 99.5 = 99500$$

We need to remove integers that have been counted twice (multiples of both 3 and 5):

$$\mathrm{floor}\left(\frac{999}{15}\right) = 66$$

$$\left(15+990\right)\times\left(\frac{66}{2}\right) = 1005\times 33 = 33165$$

The total can be found from the above:

$$166833 + 99500 - 33165 = 233168$$

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
233168
~~~

</details>

---

### [PE 0-100](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## 2. Even Fibonacci Numbers

### Description

Each new term in the Fibonacci sequence is generated by adding the previous two terms. By starting with 1 and 2, the first 10 terms will be:

1, 2, 3, 5, 8, 13, 21, 34, 55, 89, ...

By considering the terms in the Fibonacci sequence whose values do not exceed four million, find the sum of the even-valued terms.


### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This can be solved using a simple while-loop in Python:

~~~py
a = 1
b = 2
total = 2

while a<=4E6 and b<=4E6:
    c = a+b
    a = b
    b = c
    if c%2==0:
        total+= c

print(total)
~~~

This returns 4613732.

</details>

<details>

<summary markdown="span">Solution 2</summary>

A simpler algorithm can be implemented:

~~~py
a = 2
b = 8
total = a+b

while a<=4E6 and b<=4E6:
    c = 4*b+a
    a = b
    b = c
    if c<=4E6:
        total += c

print(total)
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
4613732
~~~

</details>

---

### [PE 0-100](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## 3. Largest Prime Factor

### Description

The prime factors of 13195 are 5, 7, 13 and 29.

What is the largest prime factor of the number 600851475143?

### Solutions

<details>

<summary markdown="span">Solution</summary>

~~~py
num = 600851475143
i = 2

while i<=num**0.5:
    while num%i == 0:
        num = num/i
    i += 1
    
print(num)
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

### [PE 0-100](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## 4. Largest Palindrome Product

### Description

A palindromic number reads the same both ways. The largest palindrome made from the product of two 2-digit numbers is 9009 = 91 ?? 99.

Find the largest palindrome made from the product of two 3-digit numbers.

### Solutions

<details>

<summary markdown="span">Solution</summary>

~~~py
maxpal = 0

for i in range(999,99,-1):
    for j in range(999,99,-1):
        prod = str(i*j)
        l = len(prod)
        if (i*j>maxpal) and (prod==prod[::-1]):
            maxpal = i*j
        elif (i*j<maxpal):
            break
    if(999*i<maxpal):
       break
   
print(maxpal)
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

### [PE 0-100](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## 5. Smallest Multiple

### Description

2520 is the smallest number that can be divided by each of the numbers from 1 to 10 without any remainder.

What is the smallest positive number that is evenly divisible by all of the numbers from 1 to 20?

### Solutions

<details>

<summary markdown="span">Solution</summary>

~~~py
end=0
d = 1*2*3*5*7*11*13*17*19
x = 0
while end==0:
    x+=d
    for i in range(11,21,1):
        if x%i!=0:
            break
        elif i==20:
            end=1
    
print(x)
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

### [PE 0-100](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## 6. Sum Square Difference

### Description

The sum of the squares of the first ten natural numbers is,

$$1^2 + 2^2 + ... + 10^2 = 385$$

The square of the sum of the first ten natural numbers is,

$$(1+2+...+10)^2=55^2=3025$$

Hence the difference between the sum of the squares of the first ten natural numbers and the square of the sum is

$$3025-385=2640$$

Find the difference between the sum of the squares of the first one hundred natural numbers and the square of the sum.

### Solutions

<details>

<summary markdown="span">Solution</summary>

~~~py
sum_of_sq = 0
sq_of_sum = 0

for i in range(101):
    sum_of_sq += i**2
    sq_of_sum+=i

sq_of_sum = sq_of_sum**2

diff = sq_of_sum-sum_of_sq

print(diff)
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

### [PE 0-100](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## X.

### Description



### Solutions

<details>

<summary markdown="span">Solution</summary>

~~~py
pass
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
1
~~~

</details>

---

### [PE 0-100](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## X.

### Description



### Solutions

<details>

<summary markdown="span">Solution</summary>

~~~py
pass
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
1
~~~

</details>

---

### [PE 0-100](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## X.

### Description



### Solutions

<details>

<summary markdown="span">Solution</summary>

~~~py
pass
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
1
~~~

</details>

---

### [PE 0-100](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## X.

### Description



### Solutions

<details>

<summary markdown="span">Solution</summary>

~~~py
pass
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
1
~~~

</details>

---

### [PE 0-100](#contents) | [Project Euler](./euler.md) | [Home](./index.md)

---

## X.

### Description



### Solutions

<details>

<summary markdown="span">Solution</summary>

~~~py
pass
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
1
~~~

</details>

## [djm89uk.github.io](https://djm89uk.github.io)
