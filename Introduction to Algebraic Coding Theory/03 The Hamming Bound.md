# The Hamming Bound

We will see our first bound on the trade off between rate and distance, known as the Hamming bound.

## Hamming Bound: Basic Idea

**Question.** What is the best trade off between rate and distance?

Idea of Hamming Bound:
- We have $|C|$ disjoint Hamming balls of radius $\left\lfloor \frac{d-1}{2} \right\rfloor$
- There can't be too many of them or they wouldn't all fit in $\Sigma^n$

## The Volume of Hamming Balls

**Definition.** The Hamming Ball in $\Sigma^n$ of radius $e$ about $x \in \Sigma^n$ is
$$
B_{\Sigma^n}(x,e) = \{ y \in \Sigma^n : \Delta(x,y) \leq e \}
$$
The volume of $B_{\Sigma^n}(x,e)$ is
$$
Vol_{\Sigma}(e,n) = |B_{\Sigma^n}(x,e)|
$$

The definition of volume of Hamming ball is unusual, because there is $x$ on the right-hand side and there is no $x$ on the left-hand side. This is okay, because the size of Hamming ball does not depend on $x$. We can also revise the definition above to the following:

**Definition**. The volume of $B_{\Sigma^n}(x,e)$ is
$$
Vol_{\Sigma}(e,n) = |B_{\Sigma^n}(0,e)|
$$

The volume of a Hamming ball is given by
$$
Vol_q(e,n) = 1 + \begin{pmatrix} n \\ 1 \end{pmatrix} (q - 1) + \begin{pmatrix} n \\ 2 \end{pmatrix} (q - 1)^2 + \dots + \begin{pmatrix} n \\ e \end{pmatrix} (q - 1)^e
$$
The first term counts the zero vector. The second term counts all of the elements of weight 1. The third term counts all of the elements of weight 2.

**Definition.** For a vector $x \in \Sigma^n$, where $0 \in \Sigma$, $wt(x)$ is the number of nonzero entries of x. In the future, $\Sigma$ is a finite field.

## Returning to our Previous Idea

Let $C \subseteq \Sigma^n$ be a code with distance $d$ and message length $k$. Let $q = |\Sigma|$. Then,
$$
|C| \, Vol_q(\left\lfloor \frac{d-1}{2}, n \right\rfloor) \leq q^n
$$
The left-hand side represents the total volume of disjoint Hamming bound, whereas the right-hand side represents the volume of the whole space. Taking log based $q$ of both equations, we obtain:
$$
\log_q |C| + \log_q \left( Vol_q \left( \left\lfloor \frac{d-1}{2}, n \right\rfloor \right) \right) \leq n
$$
Rearranging this,
$$
Rate = \frac{\log_q |C|}{n} \leq 1 - \frac{\log_q \left( Vol_q \left( \left\lfloor \frac{d-1}{2}, n \right\rfloor \right) \right)}{n}
$$
Such equation gives bound on the rate in terms of distance. The distance $d$ shows up on the right-hand side, whereas the rate is in the left-hand side. This is called the Hamming bound.

## Back to Example 3

In Example 3, message length $k = 4$, block length $n = 7$, distance $d = 3$, and the alphabet size $q = 2$.

Start by computing the volume
$$
Vol_q \left( \left\lfloor \frac{d-1}{2}, n \right\rfloor \right) = Vol_2(1,7) = 1 + \begin{pmatrix} 7 \\ 1 \end{pmatrix} = 8
$$
Now, we write the Hamming bound
$$
\frac{k}{n} \leq 1 - \frac{3}{7} = \frac{4}{7}
$$
In Example 3, $\frac{k}{n} = \frac{4}{7}$, so the Hamming bound is tight in this case. Namely, this code achieves the best possible trade off between rate and distance.

**Question to Ponder**. Can you come up with other codes where the Hamming bound is tight? Such codes would be provably optimal, at least in the trade off between rate and distance. In particular, can you generalize Example 3? Can you come up with completely different code?