# C960 WGU C960 Discrete Math II
# 2.Number Theory & Cryptography
## Successive Squaring
**Example: Compute $`3^{50} \mod 23`$**

1. **Convert the Exponent to Binary:**
   - The exponent $`50`$ in binary is $`110010_2`$. This means:

```math
50 = 2^5 + 2^4 + 2^1
```

   - This tells us that $`3^{50}`$ can be rewritten using the binary representation:

```math
3^{50} = 3^{2^5} \cdot 3^{2^4} \cdot 3^{2^1}
```

2. **Compute Powers of 3 Using Successive Squaring:**
   - We compute $`3^{2^n} \mod 23`$ for $`n = 0, 1, 2, 3, 4, 5`$. Create a table for these computations:

```math
\begin{array}{c|c}
n & 3^{2^n} \mod 23 \\ \hline
0 & 3^1 \mod 23 = 3 \\
1 & 3^2 \mod 23 = 9 \\
2 & (3^2)^2 = 3^4 \mod 23 = 81 \mod 23 = 12 \\
3 & (3^4)^2 = 3^8 \mod 23 = 144 \mod 23 = 6 \\
4 & (3^8)^2 = 3^{16} \mod 23 = 36 \mod 23 = 13 \\
5 & (3^{16})^2 = 3^{32} \mod 23 = 169 \mod 23 = 8 \\
\end{array}
```

3. **Combine the Required Powers:**
   - Using the binary expansion of $`50`$, we need:

```math
3^{50} \mod 23 = 3^{32} \cdot 3^{16} \cdot 3^2 \mod 23
```

   - Substitute from the table:

```math
3^{50} \mod 23 = 8 \cdot 13 \cdot 9 \mod 23
```

4. **Calculate the Result:**
   - Multiply step-by-step modulo $`23`$:

```math
8 \cdot 13 = 104 \quad \text{and} \quad 104 \mod 23 = 12
```

```math
12 \cdot 9 = 108 \quad \text{and} \quad 108 \mod 23 = 16
```

   Thus, $`3^{50} \mod 23 = 16`$.
   
### Unit digits
To find the last $x$ binary digits of an exponential expression $a^b$, you need to compute $a^b \mod 2^x$. This result will give you the last $x$ binary digits of $a^b$. Here's how you can do it step-by-step:

**Example**

Suppose you want to find the last 5 binary digits of $3^{13}$.

1. **Calculate $2^5$**: 
```math
2^5 = 32
```

2. **Compute $3^{13} \mod 32$**:
   - Instead of calculating $3^{13}$ directly, use modular exponentiation.

Here's a breakdown using the method of exponentiation by squaring:

```math
3^{13} \mod 32
```

- Write 13 in binary: $13 = 1101_2$. This means $13 = 2^3 + 2^2 + 2^0$.

- Compute the following:
```math
3^1 \mod 32 = 3
```
```math
3^2 \mod 32 = 9
```
```math
3^4 \mod 32 = (3^2)^2 \mod 32 = 9^2 \mod 32 = 81 \mod 32 = 17
```
```math
3^8 \mod 32 = (3^4)^2 \mod 32 = 17^2 \mod 32 = 289 \mod 32 = 1
```

Now, combine the relevant powers (those corresponding to 1s in the binary representation of 13):

```math
3^{13} \mod 32 = (3^8 \times 3^4 \times 3^1) \mod 32
```
```math
= (1 \times 17 \times 3) \mod 32
```
```math
= 51 \mod 32
```
```math
= 19
```

The last 5 binary digits of $3^{13}$ are the binary representation of 19, which is $10011_2$.

To calculate the last $x$ digits of an exponential expression, $a^b$, you can use modular arithmetic. Specifically, you're looking for $a^b \mod 10^x$.

## RSA Encryption

**Step 1: Key Generation**
1. **Choose two distinct prime numbers**:  
   - Let $p = 61$ and $q = 53$. These are two large prime numbers.
   - **Example**: We select $p = 61$ and $q = 53$.

2. **Compute their product**:  
   - $n = p \cdot q$
   - **Example**: $n = 61 \cdot 53 = 3233$

3. **Calculate the totient (Euler's totient function)**:  
   - $\phi(n) = (p - 1)(q - 1)$
   - **Example**: $\phi(n) = (61 - 1)(53 - 1) = 60 \cdot 52 = 3120$

4. **Choose an encryption exponent**:  
   - Select an integer $e$ such that $1 < e < \phi(n)$ and $\gcd(e, \phi(n)) = 1$.
   - **Example**: Choose $e = 17$ (17 is a common choice as it is relatively prime to $3120$).

5. **Determine the decryption exponent**:  
   - Compute $d$ as the modular multiplicative inverse of $e$ modulo $\phi(n)$.
   - $d \cdot e \equiv 1 \pmod{\phi(n)}$
   - **Example**: Calculate $d$ such that $d \cdot 17 \equiv 1 \pmod{3120}$. The result is $d = 2753$.

6. **Public and Private Keys**:  
   - The **public key** is $(e, n)$.
   - The **private key** is $(d, n)$.
   - **Example**: Public key is $(17, 3233)$, and private key is $(2753, 3233)$.

**Step 2: Encryption**

1. **Convert the plaintext message into an integer**:  
   - Let the plaintext be represented as an integer $m$ such that $0 \leq m < n$.
   - **Example**: Suppose we want to encrypt the message $m = 65$.

2. **Compute the ciphertext**:  
   - The ciphertext $c$ is computed using the public key $(e, n)$:
   - $c \equiv m^e \pmod{n}$
   - **Example**: Compute $c \equiv 65^{17} \pmod{3233}$.  
     To simplify:  
     $65^{17} \pmod{3233} = 2790$  
   - So, the ciphertext $c = 2790$.

**Step 3: Decryption**

1. **Compute the plaintext from the ciphertext**:  
   - Using the private key $(d, n)$, the plaintext $m$ is recovered from the ciphertext $c$:
   - $m \equiv c^d \pmod{n}$
   - **Example**: Compute $m \equiv 2790^{2753} \pmod{3233}$.  
     To simplify:  
     $2790^{2753} \pmod{3233} = 65$  
   - The original message $m = 65$ is recovered.

### Shortcut for finding the private key
An individual has chosen the public key of $N = 187 = 11 \times 17$ and $e = 3$. What is the private key using RSA encryption?  
a) 2   b) 107   c) 15   d) 160

Given:  
$e = 3$  

Calculate $\phi$:  
$\phi = (11 - 1) \times (17 - 1) = 160$

On a calculator, compute:

$\text{mod}(e \times a, \phi)$

$\text{mod}(e \times b, \phi)$

$\text{mod}(e \times c, \phi)$

$\text{mod}(e \times d, \phi)$

We want the answer to be $1$:  

$\text{mod}(3 \times 107, 160) = 1$

Thus, the answer is b) 107.  
