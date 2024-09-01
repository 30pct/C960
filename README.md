# C960 WGU C960 Discrete Math II
# 2.Number Theory & Cryptography
## Successive Squaring / Fast Exponentiation
### Step-by-Step Guide to Successive Squaring
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

### General Steps for Successive Squaring

1. **Convert the exponent to binary form** to determine which powers of the base are needed.
2. **Compute powers of the base up to the largest power needed** using repeated squaring.
3. **Multiply the required powers together modulo $`m`$** to get the final result.

By following this method, large powers modulo $`m`$ can be computed efficiently without directly calculating very large numbers.
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

Done in 5 seconds.
