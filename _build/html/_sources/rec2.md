---
title: Introduction to Control -- Recitation 2
---

# Introduction to Control -- Recitation 2

## Block Diagrams

### Basic Block

Systems with transfer function $ G(s) $, input $ \hat{u}(s) $, and output $ \hat{y}(s) $ are described in the following manner:

```{figure} images/Rec2/1.png
---
width: 70%
name: Basic Block
---
A basic block.
```

Here

$$
\hat{y}(s) = G(s)\hat{u}(s),
$$

and 

$$
G(s) = \frac{\hat{y}(s)}{\hat{u}(s)}.
$$

### Series Connection

```{figure} images/Rec2/2.png
---
width: 70%
name: series_connection
---
Two blocks in series connection.
```


We want to relate the output $ \hat{y}_2(s) $ to the input $ \hat{u}_1(s) $. From the first block:


```{math}
\hat{y}_1(s) = G_1(s) \hat{u}_1(s).
```

From the second block

$$
 \hat{y}_2(s)&=G_2(s)\hat{y}_1(s)\\
 &=G_2(s)G_1(s)\hat{u}_1(s).
$$

So finally we have:

$$
\frac{\hat{y}_2(s)}{\hat{u}_1(s)} = G_2(s) G_1(s).
$$

### Parallel Connection

```{figure} images/Rec2/3.png
---
width: 70%
name: Parallel_connection
---
Two blocks in parallel connection.
```

In this case

$$
    \hat{y}(s)&=\hat{y}_1(s)+\hat{y}_2(s)\\
              &=G_1(s)\hat{u}(s)+G_2(s)\hat{u}(s)\\
              &=\big(G_1(s)+G_2(s)\big)\hat{u}(s).
$$

We have

$$
    \frac{\hat{y}(s)}{\hat{u}(s)}=G_1(s)+G_2(s).
$$

### Feedback Connection

Consider the negative feedback connection:

```{figure} images/Rec2/4.png
---
width: 70%
name: feedback_connection
---
Two blocks in negative feedback connection.
```

We have

$$
    \hat{y}(s)&=\hat{e}(s)G_1(s)\\
              &=G_1(s)\big(\hat{u}(s)-G_2(s)\hat{y}(s)\big),
$$

Thus,  

$$
    \hat{y}(s)\big(1+G_1(s)G_2(s)\big)=G_1(s)\hat{u}(s).
$$

Finally we have

$$
    \frac{\hat{y}(s)}{\hat{u}(s)}=T(s)=\frac{G_1(s)}{1+G_1(s)G_2(s)}.
$$



## Stability Analysis of a Closed Loop System using Routh’s Criterion

### Exercise

Consider the following closed-loop system:

```{figure} images/Rec2/Picture5.png
---
width: 70%
name: feedback_connection_ex1
---
Negative feedback connection with loop-gain $G(s)$.
```


Where

$$
G(s) = k\frac{(s+2)}{s(s+5)(s^2+2s+5)}.
$$

Find values of the gain $ k $ for which the closed-loop system is stable.

### Solution

We compute the transfer function of the closed-loop system:

$$
    T(s)&=\frac{G(s)}{1+G(s)}\\
        &=\frac{\frac{k(s+2)}{s(s+5)(s^2+2s+5)}}{1+\frac{k(s+2)}{s(s+5)(s^2+2s+5)}}\\
        &=\frac{k(s+2)}{s(s+5)(s^2+2s+5)+k(s+2)}.
$$

:::{tip}
If we let $G(s)=\frac{n(s)}{d(s)}$, then

$$
    T(s)=\frac{\frac{n(s)}{d(s)}}{1+\frac{n(s)}{d(s)}}=\frac{n(s)}{d(s)+n(s)}.
$$

:::

The transfer function of the closed loop system is

$$
T(s) = \frac{k(s+2)}{s^4+7s^3 + 15s^2 +(25+k)s + 2k}.
$$

The poles of the system are the roots of the polynomial:

$$
p(s)=s^4+7s^3 + 15s^2 +(25+k)s + 2k.
$$

We use the Routh stability test to determine the values of $k$ for which all the roots of $p(s)$ have a negative real value.

$$
\begin{array}{c|ccc}
s^4 & 1 & 15 &2k\\
s^3 & 7 & 25+k \\
s^2 & \frac{15\cdot 7-(25+k)}{7} & 2k \\
s^1 & \frac{-k^2-43k+2000}{15\cdot 7-(25+k)}  \\
s^0 & 2k &  
\end{array}
$$

:::{admonition} Click here for the derivation of the table elements
:class: seealso, dropdown

The general table is

$$
\begin{array}{c|ccc}
s^4 & 1 & 15 &2k\\
s^3 & 7 & 25+k \\
s^2 & b_1 & b_2 \\
s^1 & c_1  \\
s^0 & d_2 &  
\end{array}
$$

In this case:

```{math}
b_1 = \frac{7\cdot 15-1\cdot(25+k)}{7}, \quad
b_2 = \frac{7\cdot 2k-1\cdot0}{7}=2k.
```

Moreover,

$$
c_1&=\frac{\frac{15\cdot 7-(25+k)}{7}\cdot(25+k)-14k}{\frac{15\cdot 7-(25+k)}{7}}\\
   &=\frac{\big(15\cdot 7-(25+k)\big)\cdot(25+k)-7\cdot 14k}{15\cdot 7-(25+k)}\\
   &=\frac{-k^2-43k+2000}{15\cdot 7-(25+k)}.
$$

Finally, we have:

```{math}
d_1 = \frac{\frac{-k^2-43k+2000}{15\cdot 7-(25+k)}\cdot 2k-0}{\frac{-k^2-43k+2000}{15\cdot 7-(25+k)}}=2k.
```

:::

Since the first two elements of the first column are positive, all other elements must also be positive. We obtain the following conditions:

$$
    15\cdot 7-25-k>0\rightarrow 80-k>0\rightarrow k<80.
$$

So far we have

$$
    \boxed{k<80}
$$

Next, assuming $k<80$, the denominator of $\frac{-k^2-43k+2000}{15\cdot 7-(25+k)}$ is positive, so we can only focus on the numerator:

```{math}
:label: eq:inequality
    -k^2-43k+2000>0.
```

```{figure} images/Rec2/output_(13).png
---
width: 70%
name: ex1
---

```


The value of $k$ for which {eq}`eq:inequality` holds are the values for which the function $f(k)=-k^2-43k+2000$ is positive. That is, the values of $k$ which are between the roots of

$$
    -k^2-43k+2000=0.
$$

In this case,

$$
    -71.1\leq k\leq 28.1.
$$

Moreover, from the last row of the table we have

$$
    2k>0\rightarrow k>0.
$$

To summarize

$$
    \boxed{k>0\quad \& \quad k<80\quad \&\quad -71.1\leq k\leq 28.1}
$$

We take into account all inequality conditions

```{figure} images/Rec2/inequalities1.png
---
width: 70%
name: ex1.1
---

```



So the stability condition is $0<k<28.1$.


### Exercise

Consider the following feedback system:

```{figure} images/Rec2/Picture6.png
---
width: 70%
name: ex1.1
---
Negative Feedback System with loop-gain $G(s)$.
```


For which value of $k$ is the closed loop system stable?

### Solution

The closed-loop system transfer function is

$$
 T(s)&=\frac{G(s)}{1+G(s)}\\
 &= \frac{k}{s(s^2+s+1)(s+2) + k}.
$$





The denominator of the closed-loop system transfer function is:

$$
p(s)=s^4+3s^3+3s^2+2s+k.
$$

We use the Ruth stability test:

$$
\begin{array}{c|ccc}
s^4&1&3&k\\
s^3 & 3 & 2 \\
s^2 & \frac{7}{3} & k \\
s^1 & \frac{14-9k}{7}  \\
s^0 & k   
\end{array}
$$

:::{admonition} Click here for the derivation of the table elements
:class: seealso, dropdown

The general table is

$$
\begin{array}{c|ccc}
s^4 & 1 & 3 &k\\
s^3 & 3 & 2 \\
s^2 & b_1 & b_2 \\
s^1 & c_1  \\
s^0 & d_2 &  
\end{array}
$$

In this case:

```{math}
b_1 = \frac{3\cdot 3-1\cdot 2}{3}=\frac{9-2}{3}=\frac{7}{3}, \quad
b_2 = \frac{3\cdot k-1\cdot0}{3}=k.
```

Moreover,

$$
c_1&=\frac{2\cdot\frac{7}{3}-3\cdot k}{\frac{7}{3}}\\
   &=\frac{2\cdot 7-9\cdot k}{7}\\
   &=\frac{14-9k}{7}.
$$

Finally, we have:

```{math}
d_1 = \frac{\frac{14-9k}{7}\cdot k-0}{\frac{14-9k}{7}}=k.
```

:::

Since the first three elements of the first column are positive, we need all the elements of the first column to be positive, thus:

$$
2-\frac{8}{7}k > 0 \quad \rightarrow \quad k < \frac{14}{9}.
$$

From the last row:

$$
k > 0.
$$

Combining the inequalities we obtain that the system is stable for:

$$
0<k<\frac{14}{9}.
$$


## Exercise -- Block Diagrams

Find the transfer function from input $u$ to output $y$ of the following diagram:

```{figure} images/Rec2/Picture7.png
---
width: 70%
name: ex3.1
---

```



## Solution

We recognize known structures in this diagram: We have two negative feedback loops, and a parallel connection.

```{figure} images/Rec2/Picture8.png
---
width: 70%
name: ex3.2
---

```


We replace each block with its transfer function, starting with the inner feedback loop:

```{figure} images/Rec2/Picture9.png
---
width: 70%
name: ex3.3
---

```



Continuing with the parallel connection:

```{figure} images/Rec2/Picture10.png
---
width: 70%
name: ex3.4
---

```



The upper feedback loop and parallel connection are now in series, so we have:

```{figure} images/Rec2/Picture11.png
---
width: 70%
name: ex3.5
---

```


We are only left with a closed-loop feedback system, so:

$$
    G(s)=\frac{G_1\big(G_2+G_3\big)}{1+G_1H_1}.
$$

Finally we have

$$
    T(s)&=\frac{G(s)}{1+G(s)H_2(s)}\\
        &=\frac{\frac{G_1\big(G_2+G_3\big)}{1+G_1H_1}}{1+\frac{H_2H_1\big(G_2+G_3\big)}{1+G_1H_1}}\\
        &=\frac{G_1\big(G_2+G_3\big)}{1+G_1\Big(H_1+H_2\big(G_1+G_2\big)\Big)}.
$$
