---
title: How the backpropagation algorithm works
categories: [Math, ML]
math: true
---

This study note is a summary of [Neural Networks and Deep Learning](https://neuralnetworksanddeeplearning.com/)  , [3blue1brown neural networks](https://www.youtube.com/watch?v=aircAruvnKk&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi)


# Notation
$w_{jk}^{l}$ is the weight from the $k^{th}$ neuron in the $(l-1)^{th}$ layer to the $j^{th}$ neuron in the $l^{th}$ layer

# Things should know
The Hadamard product or Schur product
Component of $s\odot t$ are just $(s\odot t)_j = s_jt_j$

Example
$$\begin{equation}
\left[\begin{array}{l}
1 \\
2
\end{array}\right] \odot\left[\begin{array}{l}
3 \\
4
\end{array}\right]=\left[\begin{array}{l}
1 * 3 \\
2 * 4
\end{array}\right]=\left[\begin{array}{l}
3 \\
8
\end{array}\right] \tag{28}
\end{equation}$$

# warm up
$$\begin{equation}
a_j^l=\sigma\left(\sum_k w_{j k}^l a_k^{l-1}+b_j^l\right) \tag{23}
\end{equation}$$
rewrite in the compact vectorized form
$$\begin{equation}
a^l=\sigma\left(w^l a^{l-1}+b^l\right) \tag{25}
\end{equation}$$


# computing relevant derivatives

$$\begin{aligned}
C_0 & =\left(a^{(L)}-y\right)^2 \\
z^{(L)} & =w^{(L)} a^{(L-1)}+b^{(L)} \\
a^{(L)} & =\sigma\left(z^{(L)}\right)
\end{aligned}$$

## sensitive to weights
$$\begin{aligned}
& \frac{\partial C_0}{\partial w^{(L)}}=\frac{\partial z^{(L)}}{\partial w^{(L)}} \frac{\partial a^{(L)}}{\partial z^{(L)}} \frac{\partial C 0}{\partial a^{(L)}} \\
& \frac{\partial C 0}{\partial a^{(L)}}=2\left(a^{(L)}-y\right) \\
& \frac{\partial a^{(L)}}{\partial z^{(L)}}=\sigma^{\prime}\left(z^{(L)}\right) \\
& \frac{\partial z^{(L)}}{\partial w^{(L)}}=a^{(L-1)}
\end{aligned}$$

## what the derivatives mean
$$\nabla C=\left[\begin{array}{c}
\frac{\partial C}{\partial w^{(1)}} \\
\frac{\partial C}{\partial b^{(1)}} \\
\vdots \\
\frac{\partial C}{\partial w^{(L)}} \\
\frac{\partial C}{\partial b^{(L)}}
\end{array}\right]$$

## Sensitive to biases
$$\frac{\partial C_0}{\partial b^{(L)}}=\frac{\partial z^{(L)}}{\partial b^{(L)}} \frac{\partial a^{(L)}}{\partial z^{(L)}} \frac{\partial C 0}{\partial a^{(L)}}=\quad 1 \sigma^{\prime}\left(z^{(L)}\right) 2\left(a^{(L)}-y\right)$$

## backpropagation
$$\frac{\partial C_0}{\partial a^{(L-1)}}=\frac{\partial z^{(L)}}{\partial a^{(L-1)}} \frac{\partial a^{(L)}}{\partial z^{(L)}} \frac{\partial C 0}{\partial a^{(L)}}=w^{(L)} \sigma^{\prime}\left(z^{(L)}\right) 2\left(a^{(L)}-y\right)$$

## Layers with additional neurons
### basic equations
$$\begin{aligned}
& a_j^{(L)}=\sigma\left(z_j^{(L)}\right) \\
& C_0=\sum_{j=0}^{n_L-1}\left(a_j^{(L)}-y_j\right)^2
\end{aligned}$$

$$z_j^{(L)}=w_{j 0}^{(L)} a_0^{(L-1)}+w_{j 1}^{(L)} a_1^{(L-1)}+w_{j 2}^{(L)} a_2^{(L-1)}+b_j^{(L)}$$

### influence multiple path
neuron influences the cost function through multiple different paths.

$$\frac{\partial C_0}{\partial a_k^{(L-1)}}=\underbrace{\sum_{j=0}^{n_L-1} \frac{\partial z_j^{(L)}}{\partial a_k^{(L-1)}} \frac{\partial a_j^{(L)}}{\partial z_j^{(L)}} \frac{\partial C_0}{\partial a_j^{(L)}}}_{\text {Sum over layer L }}$$




$$\frac{\partial C}{\partial w_{j k}^{(l)}}=a_k^{(l-1)} \sigma^{\prime}\left(z_j^{(l)}\right) \frac{\partial C}{\partial a_j^{(l)}}$$

$$\begin{gathered}
\text{where } \;\;\;\;\; \frac{\partial C}{\partial a_j^{(l)}} = \sum_{j=0}^{n_{l+1-1}-1} w_{j k}^{(l+1)} \sigma^{\prime}\left(z_j^{(l+1)}\right) \frac{\partial C}{\partial a_j^{(l+1)}} \\
\text { or } \\
2\left(a_j^{(L)}-y_j\right)
\end{gathered}$$


