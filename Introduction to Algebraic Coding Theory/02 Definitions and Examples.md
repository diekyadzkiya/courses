# Formal Definitions

**Definition.** A code $C$ of block length $n$ over an alphabet $\Sigma$ is $C \subseteq \Sigma^n$. The elements $c \in C$ are codewords.

**Example 1.** $C = \\{HELLOWORLD, BRUNCHTIME, ALLTHETIME\\}$ is a code of block length 10 over $\Sigma = \{A,B,\dots,Z\}$. Sometimes, "block length" is replaced by "length".

**Example 2.** $C = \{(0,0,0,0), (0,0,1,1), (0,1,0,1), (0,1,1,0), (1,0,0,1), (1,0,1,0), (1,1,0,0), (1,1,1,1)\}$ is a code of block length 4 over $\Sigma = \{0, 1\}$. When $\Sigma = \{0, 1\}$ the code is called binary code.

## Relationship to Alice and Bob

We have a message $x \in \Sigma^k$. Then we encode it to $c \in \Sigma^n$. Something bad happens to it, then we get some corrupted codeword $\tilde c$. Our job is to figure out $x$ given $\tilde c$.

Let us return to Example 2. Consider the encoding map $ENC: \{0,1\}^3 \to \{0,1\}^4$ given by $ENC(x_1,x_2,x_3) = (x_1,x_2,x_3,x_1 + x_2 + x_3 mod 2)$, e.g. $ENC(0,1,1) = (0,1,1,0)$. Notice that $C$ is the image of this encoding map $C = Im(ENC)$. That is, $C$ is the set of all vectors of the form $(x_1,x_2,x_3,x_1+x_2+x_3)$.

This example can correct one erasure, e.g. $\tilde c = (0,\dots,0,1)$. What was the original codeword? The missing bit must be a "1" because $0 + x_2 + 0 mod 2 = 1$. We can correctly deduce the original message. Erasure means some bit got erased and we do not know the actual value.

This example can detect one error, e.g. $\tilde c = (0,0,0,1)$. Either everything is fine or one of the bit got flipped? One bit is wrong but we do not know which one. It can not correct the error.

**Example 3.** Consider $ENC: \{0,1\}^4 \to \{0,1\}^7$ given by $ENC(x_1,x_2,x_3,x_4) = (x_1,x_2,x_3,x_4,x_2+x_3+x_4,x_1+x_3+x_4,x_1+x_2+x_4)$, where all operations are mod 2. This is called the Hamming code. Let $C = Im(ENC)$. Notice that $C$ is a binary code of length 7. There is a nice way to visualize it using circles.

This code can correct one error. We see $\tilde c = (0,1,1,1,0,1,0)$. What is $c$? $c = (0,1,0,1,0,1,0)$. The error is in the third bit, which can be obtained using circle visualization. This seems ad hoc. Does there always a method based on circle drawing solution to this problem?

## A Few More Definitions

**Definition.** The Hamming distance between $x,y \in \Sigma^n$ is
$$
\Delta(x,y) := \sum_{i=1}^n \mathbb{1}\{x_i \neq y_i\}
$$
The number of positions in which the vector $x$ and $y$ differ. The Hamming distance is a metric (prove it).

**Definition.** The relative Hamming distance between $x,y \in \Sigma^n$ is
$$
\delta(x,y) := \frac{\Delta(x,y)}{n} = \frac{1}{n} \sum_{i=1}^n \mathbb{1}\{x_i \neq y_i\}
$$
The fraction of positions in which they differ.

**Definition.** The minimum distance of a code $C \subseteq \Sigma^n$ is
$$
\min_{c \neq c' \in C} \Delta(c,c')
$$
The smallest distance between two different codewords. Sometimes called the distance of $C$. We will see that a code with large minimum distance can be used to correct errors.

## Minimum Distance is a Proxy for Robustness

**Theorem.** A code with minimum distance $d$ can:
- correct $\leq d-1$ erasures
- detect $\leq d-1$ errors
- correct $\leq \left\lfloor \frac{d-1}{2} \right\rfloor$ errors

For "correct $\leq d-1$ erasures" and "correct $\leq \left\lfloor \frac{d-1}{2} \right\rfloor$ errors", consider the following algorithm: return $c \in C$ such that $\Delta(c,\tilde c)$ is minimized.

For "detect $\leq d-1$ errors", consider the following algorithm: if $\tilde c \in C$, then say "no error", else say "error".

## Returning to Our Examples

**Example 2.** This code has distance 2. It can correct up to one erasure and it can detect up to one error.

**Example 3.** This code has distance 3. Look at the circles again and check that these codes do indeed have these distances. When the distance is 3, it explains why the code can correct one error.

## Things We Care About

1. Handling something bad, a.k.a, $\left\lfloor \frac{d-1}{2} \right\rfloor$ errors or $d-1$ erasures
1. Recovering info about $x$, a.k.a. all of $x$

Requirement 1 and 2 can be combined: we want minimum distance $d$ (correct $d-1$ worst-case erasures or $\left\lfloor \frac{d-1}{2} \right\rfloor$ worst-case errors)

3. Minimizing overhead, i.e. $k/n$ should be large
4. Doing all of this efficiently

## Yet More Definitions

**Definition.** The message length of a code $C$ over an alphabet $\Sigma$ is defined to be $k = \log_{|\Sigma|} |C|$. Sometimes caled "dimension".

This definition makes sense. A message $x$ of length $k$ is encoded into a codeword $c \in C$. There are $\Sigma^k$ possible messages and there are $|C|$ possible codewords. Because the number of messages is the same with the number of codewords, thus $|\Sigma|^k = |C|$. Taking logaritms of based $|\Sigma|$ on both sides, yields $k = \log_{|\Sigma|} |C|$, which is the same with the definition.

## The Definitions Keeps on Coming

**Definition.** The rate of a code $C \subseteq \Sigma^n$ is
$$
R = \frac{\log_{|\Sigma|} |C|}{n} = \frac{\text{message length } k}{\text{block length } n}
$$
So, $R \in [0,1]$. If $R$ is close to one, good, not much overhead. If $R$ is close to 0, bad, lots of overhead.

**Definition.** A code with distance $d$, message length $k$ and block length $n$ over an alphabet $\Sigma$ is called an $(n,k,d)_{|\Sigma|}$ - code.

## Things We Care About

1+2. We want minimum distance $d$ (correct $d-1$ worst-case erasures or $\left\lfloor \frac{d-1}{2} \right\rfloor$ worst-case errors)

3. Minimizing overhead, i.e. $k/n$ should be large. Namely, we want rate as close to one as possible.
4. Doing all of this efficiently

We focus on item 1+2 and 3. Item 3 will be discussed later. Item 1+2 and 3 raise an interesting question: what is the best trade off between rate and distance? This question is still open, at least for binary codes.

## Reference

[Lecture 1 Video 2: Definitions and Examples](https://youtu.be/nL2ikRhDO4k)
