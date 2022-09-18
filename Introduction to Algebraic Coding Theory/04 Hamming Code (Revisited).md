# The Hamming Code (Revisited)

## Recall The Example

This is a code with message length $k = 4$, block length $n = 7$ over the alphabet $\\{0,1\\}$ with the following encoding map $ENC(x_1,x_2,x_3,x_4) = (x_1,x_2,x_3,x_4,x_2+x_3+x_4,x_1+x_3+x_4,x_1+x_2+x_4)$. The message appears in the first four bits of the codewords and the last three bits of the codeword is the linear combination (modulo two) of the various message bits. The code $C$ is defined as the image of the encoding map $C = Im(ENC)$. This code can be visualized using circles. This is the Hamming Code of length 7.

We will describe two new ways to look at the Hamming code. We can view the encoding map as a multiplication by a matrix (modulo two):
$$ENC(\bar x) = G \bar x \\, \text{mod } 2 = {\left\lbrack \matrix{1 & 0 & 0 & 0 \cr 0 & 1 & 0 & 0 \cr 0 & 0 & 1 & 0 \cr 0 & 0 & 0 & 1 \cr 0 & 1 & 1 & 1 \cr 1 & 0 & 1 & 1 \cr 1 & 1 & 0 & 1} \right\rbrack} {\left\lbrack \matrix{x_1 \cr x_2 \cr x_3 \cr x_4} \right\rbrack} \\, \text{mod } 2$$
$G$ is called a generator matrix. Informally, a generator matrix is a matrix so that you can think of the encoding map as a multiplication with that matrix.

## Linear Algebraic Observations

Assume linear algebra "works" mod 2.
- $C$ is closed under addition: for any $c,c' \in C$, $c+c' \in C$. To see this, we write
$$c + c' = Gx + Gx' = G(x + x') \in C$$
- $C$ is a linear subspace of $\\{0,1\\}^7$ of dimension 4.
$$C = column-span(G)$$
- The distance of $C$ is the same as the minimum weight of any nonzero $c \in C$.
$$\Delta(c,c') = \Delta(G x, G x') = \Delta(G x - G x', 0) = \Delta(G (x - x'), 0) = wt(G(x - x'))$$

There is another way to write a Hamming code, as follows.
$${\left\lbrack \matrix{0 & 1 & 1 & 1 & 1 & 0 & 0 \cr 1 & 0 & 1 & 1 & 0 & 1 & 0 \cr 1 & 1 & 0 & 1 & 0 & 0 & 1} \right\rbrack} {\left\lbrack \matrix{x_1 \cr x_2 \cr x_3 \cr x_4 \cr c_5 \cr c_6 \cr c_7} \right\rbrack} = {\left\lbrack \matrix{0 \cr 0 \cr 0} \right\rbrack} \\, \text{mod } 2$$
Any codeword $c \in C$ satisfies the equation $Hc=0$. Equivalently, $C \subseteq Ker(H)$. We claim that $C = Ker(H)$ by counting dimensions. First, $dim(Ker(H)) = 7 \\, (\text{number of columns of } H) - 3 \\, (\text{rank of } H) = 4$. The dimension of $C$ is also equal to 4, i.e. $dim(C) = 4$. Since the dimension of $C$ and $Ker(H)$ are equal, then $C = Ker(H)$. $H$ is a parity check matrix for $C$. Informally, a parity check matrix is just a matrix so that the code is equal to the kernel of that matrix. Parity check matrix can be really useful.

## C has distance 3

- We saw that it suffices to show that the minimum weight of $C$ is 3
- Use contradiction: say that there is a $c \in C$ that has weight 1 or 2. That means there is a linear combination of one or two columns of $H$ that equals to 0 mod 2. Since any pair of columns of $H$ are linearly independent (no column is zero and anly linear combination of two columns is not zero, in mod 2 this means all elements must be the same), this can't happen. Therefore, for any code $c \in C$, the weight $wt(c) \geq 3$, hence the distance of $C$ is also greater than or equal to three.
- To show that the distance is at most 3, observe that codeword $(0,1,0,1,0,1,0)$ has weight 3, which means the distance of $C$ is less than or equal to 3.
- Combining the following two observations, we conclude that the distance of $C$ is 3.

## An Efficient Decoding Algorithm for C

Previously, $\tilde c = (0,1,1,1,0,1,0)$, find $c$ such that $\Delta(c,\tilde c) \leq 1$. We can use parity check matrix. On one hand, we can compute $H \tilde c$ as follows
$$H \tilde c = {\left\lbrack \matrix{0 & 1 & 1 & 1 & 1 & 0 & 0 \cr 1 & 0 & 1 & 1 & 0 & 1 & 0 \cr 1 & 1 & 0 & 1 & 0 & 0 & 1} \right\rbrack} {\left\lbrack \matrix{0 \cr 1 \cr 1 \cr 1 \cr 0 \cr 1 \cr 0} \right\rbrack} = {\left\lbrack \matrix{1 \cr 1 \cr 0} \right\rbrack}$$

On the other hand, $\tilde c = c + z \\, (\text{mod } 2)$, where $c$ is the original codeword and $z$ is the error. $z$ is a weight one error vector. This means $H \tilde c = H(c+z) = Hc + Hz = Hz \\, (\text{mod } 2)$.

This means $Hz = H\tilde c = {\left\lbrack \matrix{1 \cr 1 \cr 0} \right\rbrack} \\, (\text{mod } 2)$. Since $z$ has weight one, this means we pick one of the columns of $H$. It turns out that the right-hand side is equal to the third column of $H$. This means
$$z = {\left\lbrack \matrix{0 \cr 0 \cr 1 \cr 0 \cr 0 \cr 0 \cr 0} \right\rbrack} = {\left\lbrack \matrix{1 \cr 1 \cr 0} \right\rbrack}$$
Finally, we can compute $c$ as follows:
$$c = \tilde c + z = {\left\lbrack \matrix{0 \cr 1 \cr 0 \cr 1 \cr 0 \cr 1 \cr 0} \right\rbrack}$$

## Moral of the Story

Assuming that "linear algebra works" mod 2.

- The Hamming code $C$ of length 7 is a linear subspace of $\\{0,1\\}^7$
- $C = \\{ G x : x \in \\{0,1\\}^4 \\} = col-span(G)$, where $G$ is a generator matrix
- $C = \\{ c \in \\{0,1\\}^7 : Hc = 0 \\} = Ker(H)$, where $H$ is a parity check matrix
- This linear algebraic view is useful!
  - easy to compute the distance of $C$
  - easy to decode $\tilde c$ from 1 error
