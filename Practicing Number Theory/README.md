<!--
Student: Abdur Rawf Akand
Student ID: IT23050
Project: Number Theory and Cryptography Workshop
-->

<h1 align="center">Number Theory and Cryptography Workshop</h1>

<div align="center">

# 👤 **Abdur Rawf Akand**

## 🎓 **Student ID: IT23050**

</div>

<p align="center">
<i>A mathematical and computational study of number theory, modular arithmetic, and public-key cryptography using Python.</i>
</p>

---

## 📚 Table of Contents

1. [Introduction](#1-introduction)
2. [Learning Objectives](#2-learning-objectives)
3. [Environment and Tools](#3-environment-and-tools)
4. [Foundations of Number Theory](#4-foundations-of-number-theory)
5. [Divisibility, Primes, and Factorization](#5-divisibility-primes-and-factorization)
6. [GCD and the Euclidean Algorithm](#6-gcd-and-the-euclidean-algorithm)
7. [Modular Arithmetic](#7-modular-arithmetic)
8. [Modular Inverses](#8-modular-inverses)
9. [Fermat's and Euler's Theorems](#9-fermats-and-eulers-theorems)
10. [Chinese Remainder Theorem](#10-chinese-remainder-theorem)
11. [Cryptography](#11-cryptography)
12. [RSA Cryptosystem](#12-rsa-cryptosystem)
13. [Python Practice](#13-python-practice)
14. [Worked Examples](#14-worked-examples)
15. [Security Notes](#15-security-notes)
16. [Learning Outcomes](#16-learning-outcomes)
17. [References](#17-references)

---

# 1. Introduction

Number Theory is the branch of mathematics concerned with integers and their properties. Important topics include divisibility, prime numbers, greatest common divisors, modular arithmetic, congruences, and integer equations.

Cryptography uses mathematics and algorithms to protect information. Modern cryptography relies heavily on Number Theory, especially prime numbers and modular arithmetic.

This document contains mathematical explanations, equations, Python implementations, worked examples, and practice material inspired by the topics covered in the public workshop repository:

**[Number Theory and Cryptography Workshop — mnp-club](https://github.com/mnp-club/Number_Theory_and_Cryptography_Workshop)**

> **Note:** This README is a consolidated educational study document. The original workshop repository, its slides, recordings, notebooks, and assignments remain the primary source for the exact workshop material.

---

# 2. Learning Objectives

After completing this study, I should be able to:

- Understand divisibility and prime factorization.
- Find GCD using the Euclidean Algorithm.
- Use the Extended Euclidean Algorithm.
- Understand modular arithmetic and congruence.
- Calculate modular inverses.
- Apply Fermat's Little Theorem and Euler's Theorem.
- Solve basic Chinese Remainder Theorem problems.
- Understand the mathematical structure of RSA.
- Implement important algorithms using Python.

---

# 3. Environment and Tools

The code can be practiced using:

- Google Colab
- Jupyter Notebook
- JupyterLab
- Python 3

Example installation:

```bash
pip install jupyter matplotlib
jupyter notebook
```

The algorithms below mainly use Python's standard library.

---

# 4. Foundations of Number Theory

## 4.1 Integers

The set of integers is

\[
\mathbb{Z}=\{\ldots,-3,-2,-1,0,1,2,3,\ldots\}.
\]

Number Theory studies the properties and relationships of these numbers.

## 4.2 Divisibility

For integers \(a\) and \(b\), we say that \(a\) divides \(b\) if there exists an integer \(k\) such that

\[
b=ak.
\]

This is written as

\[
a\mid b.
\]

For example:

\[
4\mid20
\]

because

\[
20=4\times5.
\]

### Python Example

```python
a = 20
b = 4

print(a % b == 0)
```

Output:

```text
True
```

## 4.3 Division Algorithm

For any integer \(a\) and positive integer \(b\), there exist unique integers \(q\) and \(r\) such that

\[
a=bq+r
\]

where

\[
0\leq r<b.
\]

Example:

\[
29=7\times4+1.
\]

```python
a = 29
b = 7

q = a // b
r = a % b

print("Quotient:", q)
print("Remainder:", r)
```

---

# 5. Divisibility, Primes, and Factorization

## 5.1 Prime Numbers

A prime number is an integer greater than 1 that has exactly two positive divisors:

\[
1 \quad \text{and} \quad p.
\]

Examples:

\[
2,3,5,7,11,13,17,\ldots
\]

The number 2 is the only even prime.

## 5.2 Composite Numbers

A composite number has more than two positive divisors.

For example:

\[
12=2\times2\times3.
\]

## 5.3 Prime Testing

```python
def is_prime(n):
    if n < 2:
        return False

    if n == 2:
        return True

    if n % 2 == 0:
        return False

    d = 3

    while d * d <= n:
        if n % d == 0:
            return False
        d += 2

    return True


for n in [1, 2, 7, 15, 17, 21, 29]:
    print(n, is_prime(n))
```

Expected result:

```text
1 False
2 True
7 True
15 False
17 True
21 False
29 True
```

## 5.4 Prime Factorization

The Fundamental Theorem of Arithmetic states that every integer greater than 1 has a unique prime factorization, apart from the order of its factors.

Example:

\[
360=2^3\times3^2\times5.
\]

```python
def prime_factorization(n):
    factors = {}
    d = 2

    while d * d <= n:
        while n % d == 0:
            factors[d] = factors.get(d, 0) + 1
            n //= d
        d += 1

    if n > 1:
        factors[n] = factors.get(n, 0) + 1

    return factors


print(prime_factorization(360))
```

Output:

```text
{2: 3, 3: 2, 5: 1}
```

---

# 6. GCD and the Euclidean Algorithm

## 6.1 Greatest Common Divisor

The Greatest Common Divisor of two integers is the largest positive integer that divides both.

It is written as

\[
\gcd(a,b).
\]

For example:

\[
\gcd(18,30)=6.
\]

## 6.2 Euclidean Algorithm

The Euclidean Algorithm uses:

\[
\gcd(a,b)=\gcd(b,a\bmod b).
\]

Example:

\[
\begin{aligned}
30&=18\times1+12\\
18&=12\times1+6\\
12&=6\times2+0
\end{aligned}
\]

Therefore:

\[
\boxed{\gcd(30,18)=6}
\]

### Python Implementation

```python
def gcd_euclid(a, b):
    a = abs(a)
    b = abs(b)

    while b != 0:
        a, b = b, a % b

    return a


print(gcd_euclid(30, 18))
print(gcd_euclid(252, 105))
```

Output:

```text
6
21
```

## 6.3 Extended Euclidean Algorithm

The Extended Euclidean Algorithm finds integers \(x\) and \(y\) such that

\[
ax+by=\gcd(a,b).
\]

```python
def extended_gcd(a, b):
    if b == 0:
        return a, 1, 0

    g, x1, y1 = extended_gcd(b, a % b)

    x = y1
    y = x1 - (a // b) * y1

    return g, x, y


g, x, y = extended_gcd(30, 18)

print("GCD:", g)
print("x:", x)
print("y:", y)
print("Verification:", 30*x + 18*y)
```

---

# 7. Modular Arithmetic

## 7.1 Congruence

Two integers \(a\) and \(b\) are congruent modulo \(n\) if

\[
a\equiv b\pmod n.
\]

This means:

\[
n\mid(a-b).
\]

Example:

\[
17\equiv5\pmod{12}.
\]

Because:

\[
17-5=12.
\]

## 7.2 Modular Operations

Addition:

\[
(a+b)\bmod n
\]

Subtraction:

\[
(a-b)\bmod n
\]

Multiplication:

\[
(ab)\bmod n.
\]

### Python Example

```python
a = 17
b = 23
n = 7

print("Addition:", (a + b) % n)
print("Subtraction:", (a - b) % n)
print("Multiplication:", (a * b) % n)
```

---

## 7.3 Fast Modular Exponentiation

We often need to calculate:

\[
a^b\bmod n.
\]

Repeated squaring makes this calculation efficient.

```python
def modular_power(base, exponent, modulus):
    result = 1
    base %= modulus

    while exponent > 0:
        if exponent % 2 == 1:
            result = (result * base) % modulus

        base = (base * base) % modulus
        exponent //= 2

    return result


print(modular_power(7, 128, 13))
print(pow(7, 128, 13))
```

Both methods produce:

```text
3
```

---

# 8. Modular Inverses

The modular inverse of \(a\) modulo \(n\) is a number \(x\) such that

\[
ax\equiv1\pmod n.
\]

An inverse exists if and only if:

\[
\gcd(a,n)=1.
\]

Example:

\[
3^{-1}\equiv5\pmod7
\]

because

\[
3\times5=15\equiv1\pmod7.
\]

### Python Implementation

```python
def modular_inverse(a, n):
    g, x, y = extended_gcd(a, n)

    if g != 1:
        return None

    return x % n


inverse = modular_inverse(3, 7)

print(inverse)
print((3 * inverse) % 7)
```

Output:

```text
5
1
```

---

# 9. Fermat's and Euler's Theorems

## 9.1 Fermat's Little Theorem

If \(p\) is prime and \(p\nmid a\), then

\[
\boxed{a^{p-1}\equiv1\pmod p}.
\]

Example:

\[
3^6\equiv1\pmod7.
\]

```python
print(pow(3, 6, 7))
```

Output:

```text
1
```

## 9.2 Euler's Totient Function

Euler's Totient Function \(\phi(n)\) counts the positive integers less than or equal to \(n\) that are coprime with \(n\).

For a prime \(p\):

\[
\phi(p)=p-1.
\]

For distinct primes \(p\) and \(q\):

\[
\phi(pq)=(p-1)(q-1).
\]

## 9.3 Euler's Theorem

If

\[
\gcd(a,n)=1,
\]

then

\[
\boxed{a^{\phi(n)}\equiv1\pmod n}.
\]

---

# 10. Chinese Remainder Theorem

Suppose we have:

\[
x\equiv a_1\pmod{n_1}
\]

and

\[
x\equiv a_2\pmod{n_2}.
\]

If \(n_1\) and \(n_2\) are coprime, the Chinese Remainder Theorem guarantees a unique solution modulo

\[
n_1n_2.
\]

Example:

\[
x\equiv2\pmod3
\]

\[
x\equiv3\pmod5.
\]

The smallest solution is:

\[
\boxed{x=8}.
\]

Because:

\[
8\bmod3=2
\]

and

\[
8\bmod5=3.
\]

### Python Implementation

```python
def chinese_remainder(remainders, moduli):
    total = 1

    for m in moduli:
        total *= m

    result = 0

    for remainder, modulus in zip(remainders, moduli):
        partial = total // modulus
        inverse = modular_inverse(partial, modulus)

        result += remainder * partial * inverse

    return result % total


print(chinese_remainder([2, 3], [3, 5]))
```

Output:

```text
8
```

---

# 11. Cryptography

Cryptography is the science of protecting information.

Important concepts include:

| Term | Meaning |
|---|---|
| Plaintext | Original readable message |
| Ciphertext | Encrypted message |
| Encryption | Converting plaintext into ciphertext |
| Decryption | Recovering plaintext |
| Key | Secret or public value used by an algorithm |

## 11.1 Main Security Goals

### Confidentiality

Only authorized people should read the information.

### Integrity

Unauthorized modification should be detectable.

### Authentication

A system should be able to verify identity.

### Non-repudiation

A valid digital-signature process can provide evidence that a party performed a signing action.

## 11.2 Symmetric vs Asymmetric Cryptography

| Symmetric | Asymmetric |
|---|---|
| Uses a shared secret key | Uses public/private key pair |
| Usually faster | Usually computationally heavier |
| Key distribution is challenging | Public key can be openly shared |
| Example: AES | Example: RSA |

---

# 12. RSA Cryptosystem

RSA is a public-key cryptosystem based on Number Theory.

## 12.1 Key Generation

### Step 1: Choose two prime numbers

\[
p,\quad q
\]

### Step 2: Calculate

\[
n=pq.
\]

### Step 3: Calculate Euler's Totient

\[
\phi(n)=(p-1)(q-1).
\]

### Step 4: Choose \(e\)

Choose \(e\) such that

\[
1<e<\phi(n)
\]

and

\[
\gcd(e,\phi(n))=1.
\]

### Step 5: Find \(d\)

Find \(d\) such that

\[
ed\equiv1\pmod{\phi(n)}.
\]

The public key is:

\[
(n,e)
\]

and the private exponent is:

\[
d.
\]

---

## 12.2 Encryption

For a message integer \(m\):

\[
\boxed{c=m^e\bmod n}.
\]

## 12.3 Decryption

The receiver calculates:

\[
\boxed{m=c^d\bmod n}.
\]

---

## 12.4 Complete RSA Example

Choose:

\[
p=61,\qquad q=53.
\]

Then:

\[
n=61\times53=3233.
\]

And:

\[
\phi(n)=60\times52=3120.
\]

Choose:

\[
e=17.
\]

The modular inverse gives:

\[
d=2753.
\]

Because:

\[
17\times2753\equiv1\pmod{3120}.
\]

Therefore:

- Public Key: \((3233,17)\)
- Private Exponent: \(2753\)

Let:

\[
m=65.
\]

Encryption:

\[
65^{17}\bmod3233=2790.
\]

So:

\[
c=2790.
\]

Decryption:

\[
2790^{2753}\bmod3233=65.
\]

The original message is successfully recovered.

---

## 12.5 RSA Python Implementation

```python
def rsa_key_generation(p, q, e):
    n = p * q
    phi = (p - 1) * (q - 1)

    if gcd_euclid(e, phi) != 1:
        raise ValueError("e must be coprime with phi(n)")

    d = modular_inverse(e, phi)

    return (n, e), (n, d)


def rsa_encrypt(message, public_key):
    n, e = public_key

    if not 0 <= message < n:
        raise ValueError("Message must satisfy 0 <= message < n")

    return pow(message, e, n)


def rsa_decrypt(ciphertext, private_key):
    n, d = private_key
    return pow(ciphertext, d, n)


public_key, private_key = rsa_key_generation(61, 53, 17)

message = 65

ciphertext = rsa_encrypt(message, public_key)
decrypted = rsa_decrypt(ciphertext, private_key)

print("Public Key:", public_key)
print("Private Key:", private_key)
print("Message:", message)
print("Ciphertext:", ciphertext)
print("Decrypted:", decrypted)
print("Success:", decrypted == message)
```

Expected output:

```text
Public Key: (3233, 17)
Private Key: (3233, 2753)
Message: 65
Ciphertext: 2790
Decrypted: 65
Success: True
```

---

# 13. Python Practice

## Experiment 1: Verify GCD

```python
import math

pairs = [
    (30, 18),
    (252, 105),
    (100, 75),
    (17, 19)
]

for a, b in pairs:
    print(a, b)
    print("My GCD:", gcd_euclid(a, b))
    print("Python GCD:", math.gcd(a, b))
    print()
```

## Experiment 2: Verify Modular Inverses

```python
examples = [
    (3, 7),
    (7, 26),
    (10, 17),
    (6, 9)
]

for a, n in examples:
    inverse = modular_inverse(a, n)

    if inverse is None:
        print(f"{a} has no inverse modulo {n}")
    else:
        print(
            f"Inverse of {a} modulo {n} = {inverse}"
        )
        print("Check:", (a * inverse) % n)
```

## Experiment 3: Verify RSA

```python
pub, priv = rsa_key_generation(61, 53, 17)

for message in [2, 10, 42, 65, 100]:
    cipher = rsa_encrypt(message, pub)
    recovered = rsa_decrypt(cipher, priv)

    print(
        f"Message={message}, "
        f"Cipher={cipher}, "
        f"Recovered={recovered}"
    )
```

---

# 14. Worked Examples

## Example 1: GCD

Find:

\[
\gcd(252,105).
\]

\[
252=2(105)+42
\]

\[
105=2(42)+21
\]

\[
42=2(21)+0.
\]

Therefore:

\[
\boxed{\gcd(252,105)=21}.
\]

---

## Example 2: Modular Inverse

Find the inverse of 7 modulo 26.

We need:

\[
7x\equiv1\pmod{26}.
\]

Since:

\[
7\times15=105
\]

and

\[
105=4\times26+1,
\]

we get:

\[
\boxed{7^{-1}\equiv15\pmod{26}}.
\]

---

## Example 3: Modular Power

Calculate:

\[
2^{10}\bmod13.
\]

\[
2^{10}=1024.
\]

Since:

\[
1024=78\times13+10,
\]

therefore:

\[
\boxed{2^{10}\equiv10\pmod{13}}.
\]

---

# 15. Security Notes

⚠️ **Important:** The RSA example in this README is only for educational purposes.

The values \(p=61\) and \(q=53\) are extremely small and insecure.

Real-world RSA requires:

- Very large primes.
- Secure random number generation.
- Standardized padding.
- Trusted cryptographic libraries.
- Secure private-key storage.

Do not use this implementation to protect real information.

---

# 16. Learning Outcomes

Through this project, I learned:

- The mathematical meaning of divisibility.
- How prime numbers are tested and factorized.
- How to calculate GCD efficiently.
- How the Extended Euclidean Algorithm helps find modular inverses.
- How modular arithmetic works.
- How Fermat's and Euler's theorems connect powers and modular arithmetic.
- How the Chinese Remainder Theorem combines congruences.
- How Number Theory provides the mathematical foundation of RSA.
- How Python can be used to implement and verify mathematical algorithms.

---

# 17. References

1. **Primary Workshop Repository:**  
   [Number Theory and Cryptography Workshop — mnp-club](https://github.com/mnp-club/Number_Theory_and_Cryptography_Workshop)

2. **Python Documentation:**  
   [Python Documentation](https://docs.python.org/3/)

3. **Jupyter Project:**  
   [Jupyter](https://jupyter.org/)

4. **Google Colab:**  
   [Google Colab](https://colab.research.google.com/)

5. Rivest, R. L., Shamir, A., & Adleman, L. (1978).  
   *A Method for Obtaining Digital Signatures and Public-Key Cryptosystems.*

---

<div align="center">

# 👤 **Abdur Rawf Akand**

## 🎓 **Student ID: IT23050**

### Number Theory and Cryptography Workshop

</div>
