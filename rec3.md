---
title: Introduction to Control -- Recitation 3
---

# Introduction to Control -- Recitation 3


## Closed-Loop System Stability

Consider the following system:

```{figure} images/Rec3/closed_loop1.png
---
width: 70%
name: fig:closed_loop_1
---
The feedback connection of two SISO linear systems with transfer functions "Plant" and "Controller".
```

We list each element in {numref}`fig:closed_loop_1`:


- $P$ is the transfer function of the plant.
- $C$ is the transfer function of the controller.
- $d$ is the *disturbance* acting on the plant.
- $u$ is the *input* signal of the plant.
- $y$ is the *output* signal of the plant.
- $r$ is the *reference* signal.
- $e=r-y$ is the *tracking error*.


:::{admonition} Remark

Note that the following block diagram

```{figure} images/Rec3/alt_closed_loop.png
---
width: 70%
name: fig:alt_closed_loop
---
The feedback connection of two SISO linear systems with transfer functions "Plant" and "Controller".
```


Is equivalent to the block diagram in {numref}`fig:closed_loop_1`, in the sense that the relations between all signals are the same, and all subsequent transfer functions are also the same.
:::

We assume zero initial conditions, and denote the transfer function of the Plant by $P$, and the transfer function of the Controller by $C$. Then

$$
\begin{bmatrix}
    \hat{d}(s)\\\hat{r}(s)
	\end{bmatrix}=\begin{bmatrix}
        1&-C(s)\\
        P(s)&1
    \end{bmatrix}\begin{bmatrix}
        \hat{u}(s)\\\hat{e}(s)
    \end{bmatrix}.
$$

This implies that

$$
    \begin{bmatrix}
        \hat{u}\\\hat{e}
    \end{bmatrix}&=\begin{bmatrix}
        1&-C\\
        P&1
    \end{bmatrix}^{-1}\begin{bmatrix}
        \hat{d}\\\hat{r}
    \end{bmatrix}\nonumber\\
    &=\begin{bmatrix}
        (1+PC)^{-1}&C(1+PC)^{-1}\\
        -P(1+PC)^{-1}&(1+PC)^{-1}
    \end{bmatrix}\begin{bmatrix}
        \hat{d}\\\hat{r}
    \end{bmatrix}.
$$

We call $PC$ the **loop gain**. We define  $S:=(1+PC)^{-1}$,  and refer to this as the **sensitivity function**. Note that $S$ is the  transfer function from $r$ to $e$ (or from $d$ to $u$). We then have

```{math}
:label: eq:closed_loop_trasnferfunctions
	\begin{bmatrix}
        \hat{u}\\\hat{e}
    \end{bmatrix}&=\begin{bmatrix}
        S&CS\\
        -PS&S
    \end{bmatrix}\begin{bmatrix}
        \hat{d}\\\hat{r}
	\end{bmatrix}.
```

:::{admonition} Remark
If

$$
    P(s)C(s)=\frac{n(s)}{d(s)},
$$

where $n(s)$ and $d(s)$ are polynomials, then

$$
    S(s)=\Big(1+\frac{n(s)}{d(s)}\Big)^{-1}=\frac{d(s)}{d(s)+n(s)}.
$$

Thus, we see that  the poles of $PC$ become zeros of $S$. 
:::



```{prf:definition}
The feedback connection of $P$ and $C$ is called **stable** if the transfer function from $(d,r)$ to $(u,e)$ is stable, i.e., if all four 
entries of the matrix in {eq}`eq:closed_loop_trasnferfunctions` are stable.     
```

```{prf:proposition}
:label: prop:stable_closed_loop

The feedback connection of $P$ and $C$ is stable if and only if the following two conditions hold:

1. $S=(1+PC)^{-1}$ is stable.
2. There is no unstable pole-zero cancellation in the product $PC$.
```

```{prf:definition}
The closed-loop is called **w-stable** if

$$
     \big| P(\infty)C(\infty)\big|<1.
$$
```

```{admonition} Remark
If the loop-gain is strictly-proper, then the closed-loop system is $w$-stable.
```



### Exercise 1

Consider the closed-loop system with:

$$
    P(s)=\frac{s+b}{s+a},\; C(s)=\frac{1}{s}.
$$

For which values of $a,b\in\mathbb{R}$ is the closed-loop system stable?

### Solution

We need to check that

1. $S(s)$ is stable.
2. There are no unstable pole-zero cancellations in $P(s)C(s)$.

We compute $S(s)$:

$$
    S(s)&=\frac{1}{1+P(s)C(s)}\\
        &=\frac{1}{1+\frac{s+b}{s(s+a)}}\\
        &=\frac{1}{\frac{s^2+as+(s+b)}{s(s+a)}}\\
        &=\frac{s(a+b)}{s^2+s(a+1)+b}.
$$

We have a polynomial of degree $2$ in the denominator. We know that this polynomial has stable roots if all the coefficients are positive, that is, if

$$
    a+1>0\quad\&\quad b>0.
$$

To summarize, $S(s)$ is stable if

$$
    \boxed{b>0\quad a>-1}
$$

Next, we check for unstable cancellation in the loop-gain:

$$
    P(s)C(s)=\frac{s+b}{s(s+a)}.
$$

If $b=0$, there is an unstable pole-zero cancellation at $s=0$. If $b=a$, there is a cancellation, but it is not necessarily unstable. It will be unstable if $a=b<0$. So, there are no unstable zero-pole cancellations in the loop gain if

$$
    \boxed{b\neq0\quad \text{or if }a=b\text{ then }a>0}
$$

Combining both requirements, we have

$$
    \boxed{b>0\quad a>-1}
$$

Note that for  $-1<a\leq0$, $P(s)$ is unstable, but the closed-loop system is stable.



## Steady State Error due to Reference Signal

In this section we assume $\hat{d}(s)=0$. For the system depicted in Figure {numref}`fig:closed_loop_1`,

$$
    \frac{\hat{e}(s)}{\hat{r}(s)}=S(s)=\frac{1}{1+P(s)C(s)}.
$$

<mark>If the system is stable</mark>, the steady-state error can be computed using the <em>Final Value Theorem</em>:

$$
\boxed{e_{ss}=\lim_{t\rightarrow\infty}e(t)=\lim_{s \to 0} s \hat{e}(s) = \lim_{s\rightarrow0}s\cdot\frac{\hat{r}(s)}{1+P(s)C(s)}}
$$

```{admonition} Remark
This theorem is valid for any function $f(t)$ where $F(s)$ has left-half plane poles and at most a single pole at the origin.
```

### System Type

The system type is determined by the number of loop-gain poles at the origin:

$$
    P(s)C(s)=\frac{(b_0s+1)(b_1s+1)\cdots(b_ms+1)}{s^{\textcolor{red}{N}}(a_0s+1)(a_1s+1)\cdots(a_ns+1)}.
$$

Thus, the system type is <font color="red">N</font>.

We consider three types of inputs:

$$
\renewcommand{\arraystretch}{1.5}
\begin{array}{|c|c|c|}
    \hline
    \text{Input} & \text{Time Domain} & \text{Laplace Domain} \\
    \hline
    \text{Step} & r(t)=1(t) & \frac{1}{s} \\
    \hline
    \text{Ramp} & r(t)=t & \frac{1}{s^2} \\
    \hline
    \text{Acceleration} & r(t)=t^2 & \frac{2}{s^3} \\
    \hline
\end{array}
$$

Steady-state error for each system type and input type:

```{table} Steady-State Error Constants for Different System Types
:name: tbl-error-constants

| Type/Input   | Step               | Ramp          | Acceleration    |
|--------------|--------------------|---------------|-----------------|
| Type 0       | $\frac{1}{1 + K_p}$ | $\infty$      | $\infty$        |
| Type 1       | $0$                | $\frac{1}{K_v}$ | $\infty$       |
| Type 2       | $0$                | $0$           | $\frac{1}{K_a}$ |
```


where 

```{math}
:label: eq:gains
    K_p&=\lim_{s\rightarrow0}P(s)C(s),\nonumber\\
    K_v&=\lim_{s\rightarrow0}sP(s)C(s),\\
    K_a&=\lim_{s\rightarrow0}s^2P(s)C(s).\nonumber
```

If a system diverges for a given input, an integrator controller can be added to increase system type.

<u>Solution Steps</u>

We always use a controller of the form $C(s)=\frac{k}{s^\ell}$, choosing integer $\ell$ as small as possible such that conditions are met.

1. Determine system type from $P(s)$.
2. Given the input, use {numref}`tbl-error-constants` to determine the required system type for finite steady-state error, selecting $\ell$ accordingly.
3. Compare the relevant value from the table to the system condition on $e_{ss}$ to obtain value range for $K_p,\;K_v,\;K_a$.
4. Compute $K_p,\;K_v,\;K_a$ explicitly using {eq}`eq:gains` and compare with step 3. to find range of values of $k$.
5. Compute the sensitivity transfer function $S(s)$ and determine the range of values of $k$ for stability.
6. The valid $k$ values are the intersection of step 4. and step 5. results.
7. If unsuccessful, increase $\ell$ by $1$ and repeat steps 3.- 6. .


For a general input , compute the Laplace transform and apply the Final Value Theorem.

### Exercise

Given the plant:

$$
P(s)=\frac{1}{s+1}.
$$

We design a controller of the form $C(s)=\frac{k}{s^\ell}$ as simple as possible such that:

1. For a step input: $|e_{ss}| < 0.1$.
2. For a velocity input: $|e_{ss}| < 0.1$.
3. For an acceleration input: $K_a>20$. 


### Solution
We can write:

$$
P(s)C(s)=\frac{k}{s^\ell(s+1)}.
$$

Thus, the system is type $\ell$.

#### 1.

From {numref}`tbl-error-constants`, we see that for system of type $0$ and step input,

$$
    e_{ss}=\frac{1}{1+K_p},
$$

the steady-state error is finite, thus, we do not need to increase the system type. We take $\ell=0$. 

Finding the possible range for $K_p$:

```{math}
:label: eq:inequ
 |e_{ss}|=\Big|\frac{1}{1+K_p}\Big|<0.1.
```

If $K_p>0$, then {eq}`eq:inequ` holds if

$$
    1+K_p=10\rightarrow K_p>9.
$$

If $K_p<0$, then {eq}`eq:inequ` holds if

$$
    1-K_p=10\rightarrow K_p<-11.
$$

To summarize, {eq}`eq:inequ` holds if

$$
    K_p>9\quad\text{or}\quad K_p<-11.
$$

Next, we relate $K_p$ and $k$:

$$
    K_p=\lim_{s\rightarrow0}P(s)C(s)=\lim_{s\rightarrow0}\Big(k\cdot\frac{1}{s+1}\Big)=k.
$$

So the condition on the steady-state error holds if:

```{math}
:label: eq:ineq_k
    \boxed{k>9\quad\text{or}\quad k<-11}
```

Next, we verify closed-loop stability: There is no cancellation of unstable pole/zero in the loop-gain. We check the sensitivity transfer function:

$$
    S(s)=\frac{1}{1+\frac{k}{s+1}}=\frac{s+1}{s+(1+k)}.
$$

The denominator is a first order polynomial, $S(s)$ is thus stable if all the coefficients of the denominator are positive, that is

```{math}
:label: ineq_k2
    1+k>0\rightarrow k>-1.
```

Unifying the inequalities in {eq}`eq:ineq_k` and {eq}`ineq_k2` we have:

```{figure} images/Rec3/ineq.png
---
width: 70%
name: fig:closed_system
---

```



So the controller is

$$
    C(s)=k,\quad k>9. 
$$

#### 2.

Now the input is a velocity $r(t)=t$. From {numref}`tbl-error-constants`, we see that for finite steady-state error, the loop-gain must be type 1. Thus, we choose $\ell=1$.

Now the loop-gain transfer function is:

$$
    C(s)P(s)=\frac{k}{s(s+1)}.
$$

which is indeed type 1. From {numref}`tbl-error-constants`, we obtain:

```{math}
:label: eq:ineqb
    e_{ss}=\frac{1}{K_v}\rightarrow\Big|\frac{1}{K_v}\Big|<0.1.
```

Clearly

$$
    K_v>10\quad\text{or}\quad K_v<-10.
$$

We write $K_v$ in terms of $k$:

$$
    K_v&=\lim_{s\rightarrow0}\big(sP(s)C(s)\big)\\
    &=\lim_{s\rightarrow0}\Big(s\cdot\frac{k}{s(s+1)}\Big)\\
    &=\lim_{s\rightarrow0}\frac{k}{s+1}\\
    &=k.
$$

Thus, we get:

```{math}
:label: ineq_partb_e
   \boxed{ k>10\quad\text{or}\quad k<-10}
```

Computing the sensitivity transfer function we have

$$
    S(s)=\frac{1}{1+\frac{k}{s(s+1)}}=\frac{s(s+1)}{s^2+s+k}.
$$

Since the denominator is second-order, all coefficients must be positive:

```{math}
:label: eq:ineq_partb_sen
	k>0.
```

Combining {eq}`ineq_partb_e` and {eq}`eq:ineq_partb_sen` we have

$$
    C(s)=\frac{k}{s},\quad k>10.
$$

#### 3.

Now the input is an acceleration input $r(t)=t^2$, requiring the loop-gain to be type 2. Thus, we choose:

$$
 \ell=2.
$$

Now, the loop-gain transfer function is:

$$
C(s)P(s)=\frac{k}{s^2(s+1)},
$$

which is indeed type 2. From {numref}`tbl-error-constants`:

$$
    e_{ss}=\frac{1}{K_a}.
$$

As we increase $K_a$, $e_{ss}$ decreases. In this case $K_a>20$, so the maximal value for $e_{ss}$ is for $K_a=20$. The value will be

$$
    |e_{ss}|<\frac{1}{20}=0.05.
$$

Computing $K_a$ explicitly:

$$
K_a&=\lim_{s\rightarrow0}\big(s^2 C(s)P(s)\big)\\
&=\lim_{s\rightarrow0}\Big(\frac{s^2k}{s^2(s+1)}\Big)\\
&=\lim_{s\rightarrow0}\frac{k}{s+1}\\
&=k.
$$

We compute the sensitivity transfer function:

$$
    S(s)=\frac{1}{1+\frac{k}{s^2(s+1)}}=\frac{s^2(s+1)}{s^3+s^2+k}.
$$

A necessary (but not sufficient) condition for stability, is that all coefficient should be positive. Here, the coefficient of $s$ is zero, making the system unstable for all $k$. Thus, the given controller cannot achieve stability, and a more complex controller is needed.

### Exercise

Consider the system:

```{figure} images/Rec3/closed_loop_system_for_Exercise.png
---
width: 70%
name: fig:closed_system
---

```


Here

$$
    C(s)=k\frac{(s+\alpha)^2}{s^2+\omega_0^2},\quad P(s)=\frac{1}{s(s+1)}.
$$

1. Assuming the system is stable, show that it can track a reference signal of the form:

$$
r(t)=\sin(\omega_0 t),
$$

with zero steady-state error.

2. We no longer assume the system is stable. Find the range of gain values $k>0$ for which the closed-loop system is stable, given that $\omega_0=1,\;\alpha=0.25$.


### Solution

#### 1.
We begin by finding the relation between $\hat{e}(s)$ and the input $\hat{r}(s)$. We know that, $\frac{\hat{e}(s)}{\hat{r}(s)}=S(s)$.

$$
    S(s)=\frac{1}{1+k\frac{(s+\alpha)^2}{s^2+\omega_0^2}\frac{1}{s(s+1)}}=\frac{s(s+1)(s^2+\omega_0^2)}{s(s+1)(s^2+\omega_0^2)+k(s+\alpha)^2}.
$$

Note that

$$
    \hat{r}(s)=\frac{\omega_0}{s^2+\omega_0^2}.
$$

So

$$
    \hat{e}(s)=S(s)\hat{r}(s)=\frac{\omega_0s(s+1)}{s(s+1)(s^2+\omega_0^2)+k(s+\alpha)^2}.
$$

Since the closed-loop system is stable, this expression is also stable. We use the final value theorem:

$$
    e_{ss}&=\lim_{s\rightarrow0}s\hat{e}(s)\\
          &=\lim_{s\rightarrow0}\Big(s\cdot \frac{\omega_0s(s+1)}{s(s+1)(s^2+\omega_0^2)+k(s+\alpha)^2}\Big)\\
          &=0
$$

#### 2.

We find values of $k>0$ such that $S(s)$ is stable. 

$$
    S(s)=\frac{s(s+1)(s^2+\omega_0^2)}{s(s+1)(s^2+\omega_0^2)+k(s+\alpha)^2}.
$$

We focus on the denominator

$$
    p(s)&=s(s+1)(s^2+\omega_0^2)+k(s+\alpha)^2\\
    &=s^4+s^3+(\omega_0^2+k)s^2+(\omega_o^2+2k\alpha)s+k\alpha^2.
$$

Substituting the values for $\alpha,\;\omega_0$ we have

$$
    p(s)=s^4+s^3+(1+k)s^2+(1+0.5k)s+0.0625k.
$$

A necessary condition for stability is that all coefficients of $p(s)$ are positive:

$$
    1+k>0,\;1+0.5k>0,\;0.0625k>0.
$$

Clearly, all three hold if $k>0$. We find sufficient values for $k>0$ using the Routh table:

$$
    \begin{array}{c|cccc}
    s^4&1&1+k&0.0625k\\
    s^3&1&1+0.5k\\
    s^2&0.5k&0.0625k\\
    s^1&0.875+0.5k\\
    s^0&0.0625k
\end{array}
$$

:::{admonition} Click here for the derivation of the table elements
:class: seealso, dropdown

The general table is

$$
\begin{array}{c|ccc}
s^4 & 1 & 1+k &0.0625k\\
s^3 & 1 & 1+0.5k \\
s^2 & b_1 & b_2 \\
s^1 & c_1  \\
s^0 & d_1 &  
\end{array}
$$

In this case:

```{math}
b_1 = \frac{(1+k)-(1+0.5k)}{1}=0.5k, \quad
b_2 = \frac{1*0.0625k-1*0}{1}.
```

Moreover,

$$
c_1&=\frac{b_1(1+0.5k)-b_2}{b_1}\\
   &=\frac{0.5k(1+0.5k)-0.0625k}{0.5k}\\
   &=\frac{0.5+0.25k-0.0625}{0.5}\\
   &=0.875+0.5k.
$$

Finally, we have:

```{math}
d_1 = \frac{c_1b_2-b_1*0}{c_1}=b_2.
```

:::

We need to make sure that all the elements of the first column are positive.

$$
    0.5k,\;0.0625k>0\rightarrow k>0.
$$

Moreover,

$$
    0.875+0.5k>0\rightarrow k>-1.75.
$$

Negative elements are non-relevant. We conclude that the closed-loop system is stable for 

$$
    k>0.
$$

```{figure} images/Rec3/error_different_k.png
---
width: 70%
name: fig:closed_system
---

```

Note that as we increase $k$ the error converges faster to zero.