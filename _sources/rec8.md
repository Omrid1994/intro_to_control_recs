---
title: Introduction to Control -- Recitation 8
---

# Introduction to Control -- Recitation 8

## LTI Systems

Consider the system


```{math}
:label: eq:state_space
  \dot x(t)&=Ax(t)+B u(t),\\
y(t)&=C x(t)+D u(t).
```

Here, $x:[0,\infty)\to \mathbb{R}^n$
is the state vector that describes the internal state of the system, $u:[0,\infty)\to\mathbb{R}^m$
is the input, and $y:[0,\infty)\to \mathbb{R}^p$ is the output. The dimensions of the matrices are then 

$$
A\in\mathbb{R}^{n\times n},\; 
B\in \mathbb{R}^{n\times m},\; 
C\in \mathbb{R}^{p\times n},\; 
D\in \mathbb{R}^{p\times m}.
$$

The solution of {eqref}`eq:state_space` is

$$
    x(t)&= e^{At}x(0)+\int_0^t e^{A(t-s)}Bu(s)ds,\\
    y(t)&= C \left  (e^{At}x(0)+\int_0^t e^{A(t-s)}Bu(s)ds \right )+Du(t),\nonumber
$$

where $e^A$ is the matrix exponential of $A$. The Laplace representation of {eq}`eq:state_space` is

$$
\boxed{\frac{\hat y(s)}{\hat u(s)}  = C (sI_n-A)^{-1} B+D}
$$

### Exercise

Consider the LTI system

$$
    \dot{x}_1(t)=a_{11}x_1(t)+b_11(t),\\
    \dot{x}_2(t)=a_{22}x_2(t)+b_21(t),
$$

with initial conditions $x_1(0)=x_1,\;x_2(0)=x_2$.


1. Write the equations in matrix form. What is $A,B$?
2. Find the solution $x(t)$.

### Solution


1.

$$
        \begin{bmatrix}
            \dot{x}_1(t)\\
            \dot{x}_2(t)
        \end{bmatrix}=\begin{bmatrix}
            a_{11}&0\\0&a_{22}
        \end{bmatrix}\begin{bmatrix}
            x_1(t)\\x_2(t)
        \end{bmatrix}+\begin{bmatrix}
            b_1\\b_2
        \end{bmatrix}1(t).
$$
    
In this case,

$$
        A=\begin{bmatrix}
            a_{11}&0\\0&a_{22}
        \end{bmatrix},\quad B=\begin{bmatrix}
            b_1\\b_2
        \end{bmatrix},\quad u(t)=1(t).
$$

The initial condition is $\vec{x}(0)=\begin{bmatrix}
        x_1\\x_2
    \end{bmatrix}$.
	
2. First we compute the matrix exponential $e^{At}$. Since $A$ is diagonal,

$$
        e^{At}=\begin{bmatrix}
            e^{a_{11}t}&0\\0&e^{a_{22}t}
        \end{bmatrix}
$$

Next, we have

$$
        e^{A(t-s)}Bu(s)&=\begin{bmatrix}
            e^{a_{11}(t-s)}&0\\0&e^{a_{22}(t-s)}
        \end{bmatrix}\begin{bmatrix}
            b_1\\b_2
        \end{bmatrix}1(t)\\
        &=\begin{bmatrix}
            b_1e^{a_{11}(t-s)}\\
            b_2e^{a_{22}(t-s)}
        \end{bmatrix}1(t).
$$
	
Since we integrate over $s\in[0,t]$, $1(s)=1$. We have:

$$
        \int_0^t e^{A(t-s)}Bu(s)ds&=\int_0^t\begin{bmatrix}
            b_1e^{a_{11}(t-s)}\\
            b_2e^{a_{22}(t-s)}
        \end{bmatrix}ds\\
        &=\begin{bmatrix}
            -\frac{b_1}{a_{11}}e^{a_{11}(t-s)}\\
            -\frac{b_2}{a_{22}}e^{a_{22}(t-s)}
        \end{bmatrix}\Bigg|_{s=0}^{s=t}\\
        &=\begin{bmatrix}
            \frac{b_1}{a_{11}}\big(e^{a_{11}t}-1\big)\\
            \frac{b_2}{a_{22}}\big(e^{a_{22}t}-1\big)
        \end{bmatrix}.
$$

Putting everything together, we have

$$
        x(t)&= e^{At}x(0)+\int_0^t e^{A(t-s)}Bu(s)ds\\
        &=\begin{bmatrix}
            e^{a_{11}t}&0\\0&e^{a_{22}t}
        \end{bmatrix}\begin{bmatrix}
            x_1\\x_2
        \end{bmatrix}+\begin{bmatrix}
            \frac{b_1}{a_{11}}\big(e^{a_{11}t}-1\big)\\
            \frac{b_2}{a_{22}}\big(e^{a_{22}t}-1\big)
        \end{bmatrix}\\
        &=\begin{bmatrix}
            x_1e^{a_{11}t}+\frac{b_1}{a_{11}}\big(e^{a_{11}t}-1\big)\\
            x_2e^{a_{22}t}+\frac{b_2}{a_{22}}\big(e^{a_{22}t}-1\big)
        \end{bmatrix}.
$$

<center>
<a href="https://mybinder.org/v2/gh/Omrid1994/intro_to_control_recs/main?urlpath=voila/render/interactive_system.ipynb" target="_blank">
    <button style="font-size:18px; padding:10px 20px; background-color:#0078D4; color:white; border:none; border-radius:5px; cursor:pointer;">
        ▶️ Click to Open Interactive System Plot
    </button>
</a>
</center>


```{prf:remark}
Note that $\vec{x}(t)\xrightarrow{t\rightarrow\infty}0$ if and only if $a_{11}<0$ and $a_{22}<0$. This implies that an LTI system is asymptotically stable if and only if $\text{Re}(\lambda)<0$ for all $\lambda\in\sigma(A)$.
```

## Observability

Consider the system {eq}`eq:state_space` is called observable on the time interval $[0,T]$ if it is possible to uniquely determine $x(0)$ from observing $u(t),y(t)$ for $t\in[0,T]$. Since we assume that the input is known, it is enough to consider the system:


```{math}
:label: eq:system_obsvr
        \dot{x}(t)&=Ax(t),\\
        y(t)&=Cx(t).
```

Note that this implies that 


```{math}
:label: eq:yt_obser
  y(t)=Ce^{At}x(0) \text{ for all } t\geq0.   
```
 
```{prf:definition}
The system {eq}`eq:system_obsvr` is called observable on the time interval $[0,T]$ if it is possible to uniquely determine $x(0)$ from   observing $ y(t)$ for $t\in[0,T]$.
```

Since the system is defined by the pair of matrices $(A,C)$,  we will sometimes use the terminology $(A,C)$ is observable rather than {eq}`eq:system_obsvr` is observable. 

Define the $L_2$ norm of the vector $y(t)\in\mathbb{R}^p$ by

$$
| y(t)  |_2 : =(|y_1(t)|^2+|y_2(t)|^2+\cdots+|y_p(t)|^2)^{1/2}.
$$

```{prf:proposition}
:label: prop:obser_y2
The system {eq}`eq:system_obsvr` is  observable on $[0,T]$ if and only if for every $x(0)\in\mathbb{R}^n$, $x(0)\neq0$, the output $y$ that corresponds to the initial state $x(0)$ satisfies
$$
        \int_0^T | y(t) |_2^2 dt>0.
$$
```

In other words, $y(t)$ is not zero on   the entire time   interval $t\in[0,T]$. 


### Kalman Rank Condition for Observability

We define the observability matrix of {eq}`eq:system_obsvr` as

$$
\mathcal O(A,C):= \begin{bmatrix} 
C\\CA\\CA^2\\ \vdots\\CA^{n-1}
\end{bmatrix}.
$$

Note that $\mathcal{O}(A,C)$ has dimensions $(np) \times n$. 

```{prf:theorem}
The system {eq}`eq:system_obsvr` is observable if and only if 

$$
   \text{rank}( \mathcal{O} (A,C))=n. 
$$
	
```

### Popov-Belevitch-Hautus Test for Observability

Another important way to verify  observability is the Popov-Belevitch-Hautus (PBH)test for observability.

````{prf:theorem}
(PBH Test for Observability) Consider the system {eq}`eq:system_obsvr`.
Let $\sigma(A)$ denote the set of eigenvalues of $A$.
Then $(A,C)$ is observable if and only if

```{math}
:label: eq:pbh_test
        rank\begin{bmatrix}
            \lambda I_n-A\\
            C
        \end{bmatrix}=n,\text{ for any }\lambda\in\sigma(A).
```
````

```{prf:remark}
Notice that the above tests depend only on the matrices $ A $ and $ C $. Therefore, controllability is a property of the pair $ (A, C) $. Since $ A $ and $ C $ are constant matrices in time-invariant systems, the controllability property does not change over time. If a system is controllable at a certain time, it is controllable at all times.
```


### Exercise

Consider the following system:

```{figure} images/Rec8/ex1fig.png
---
width: 85%
name: fig:r8_ex1_fig
---
Water Level Control System.
```

Here {numref}`fig:r8_ex1_fig` describes a water level control system for two water tanks using inlet flow rates. The water levels are $h_1$ and $h_2$. The inlet flow rates are $q_1$ and $q_2$. We know that: 
Cross-sectional areas of the tanks:

$$
  A_1=1,\quad A_2=0.5.
$$
  
Valve resistance coefficients:

$$
  R_1=R_2=1.
$$
  
Moreover, we know that:

$$
q_{12}=\frac{h_1}{R_1}, \quad q_{out} = \frac{h_2}{R_2}.
$$

We treat the variables as deviation variables around some operating point, meaning that it is possible that $h<0$ and $q<0$.
 
1. Write a physical realization of the system with state vectors $\vec{x}=\begin{bmatrix}h_1\\h_2\end{bmatrix}$  and inputs  $\vec{u}=\begin{bmatrix}q_1\\q_2\end{bmatrix}$.


We want to determine whether the water levels in the tanks can be reconstructed (that is, if the system is observable) using:

2. A single measured outflow rate, $ q_{1,2} $.
3. A single measured outflow rate, $q_{out}$.
4. Both measured outflow rates $ q_{1,2} $ and $ q_{out} $.


### Solution

1. The difference between the inflow rate and the outflow rate equals the rate of change of the water volume in the tank. Therefore, the system equations are:

$$
q_1-q_{12}=\dot{V}_1=A_1\dot{h}_1.
$$

$$
q_{12}+q_2-q_{out}=\dot{V}_2=A_2\dot{h}_2.
$$

We know that:

$$
q_{12}=\frac{h_1}{R_1}, \quad q_{out} = \frac{h_2}{R_2}.
$$

Substituting the expressions for the outflow rates into the system equations and inserting numerical values, we obtain:

$$
\dot{h}_1=-\frac{1}{R_1A_1}h_1+\frac{1}{A_1}q_1=-h_1+q_1.
$$

$$
\dot{h}_2=\frac{1}{R_1A_2}h_1=\frac{1}{R_2A_2}h_2+\frac{1}{A_2}q_2=2h_1-2h_2+2q_2.
$$

The state vector consists of the water levels:

$$
\vec{x} = \begin{bmatrix} h_1 \\ h_2 \end{bmatrix}.
$$

The input vector consists of the flow rates:

$$
\vec{u} = \begin{bmatrix} q_{1} \\ q_{2} \end{bmatrix}.
$$

Thus, the physical realization of the system is:

$$
    \dot{\vec{x}}=A\vec{x}+B\vec{u}=\begin{bmatrix}
        -1&0\\2&-2
    \end{bmatrix}\vec{x}+\begin{bmatrix}
        1&0\\0&2
    \end{bmatrix}\vec{u}.
$$

In this case

$$
    A=\begin{bmatrix}
        -1&0\\2&-2
    \end{bmatrix},\quad B=\begin{bmatrix}
        1&0\\0&2
    \end{bmatrix}.
$$

**Eigenvalues and Characteristic Polynomial**:

The characteristic polynomial of the system is given by:

$$
p_A(\lambda)=\det(\lambda I - A) .
$$

The eigenvalues of the system are the eigenvalues of $A$, which are the roots of $p_A(s)$.

We have

$$
    \lambda I-A=\begin{bmatrix}
        \lambda+1&0\\-2&\lambda+2
    \end{bmatrix}.
$$

Then

$$
    p_A(\lambda)=(\lambda+1)(\lambda+2).
$$

The roots are $\lambda_1=-1$ and $\lambda_2=-2$, thus

$$
    \sigma(A)=\{-1,\;-2\}.
$$

2. We check observability with respect to the first outflow measurement, $q_{1,2}$.
In this case


$$
y(t) = q_{1,2}=h_1=\begin{bmatrix}
    1&0
\end{bmatrix}\vec{x}(t).
$$

Thus, the output matrix is:

$$
C=\begin{bmatrix}
    1&0
\end{bmatrix}.
$$

Note that

$$
    CA=\begin{bmatrix}
        1&0
    \end{bmatrix}\begin{bmatrix}
        -1&0\\2&-2
    \end{bmatrix}=\begin{bmatrix}
        -1&0
    \end{bmatrix}.
$$

The observability matrix:

$$
\mathcal{O} = \begin{bmatrix} C \\ C A \end{bmatrix}=\begin{bmatrix}
    1&0\\-1&0
\end{bmatrix}.
$$

Clearly the rank is $1$.

Since this rank is less than the state dimension, the system is not observable. This result aligns with intuition: measuring only the second outflow provides no information about the upper tank, meaning we cannot reconstruct the full state.

Checking the PBH test:

$$
\begin{bmatrix}
    \lambda_1 I-A\\C
\end{bmatrix}=\begin{bmatrix}
    0&0\\-2&1\\1&0
\end{bmatrix}.
$$

The rank is $2$.

$$
    \begin{bmatrix}
        \lambda_2 I-A\\C
    \end{bmatrix}=\begin{bmatrix}
        -1&0\\-2&0\\1&0
    \end{bmatrix}.
$$

The rank is $1$ so the PBH test fails (the rank should be $2$ for all eigenvalues of $A$). The system is not observable.

3. We check observability with respect to a single outflow measurement $q_{out}$.

In this case:

$$
y(t) = q_{out}(t)=h_2(t)=\begin{bmatrix}
    0&1
\end{bmatrix}\begin{bmatrix}
    h_1(t)\\h_2(t)
\end{bmatrix}.
$$

Thus, the output equation is:

$$
y(t) = \underbrace{\begin{bmatrix}
    0&1
\end{bmatrix}}_{C} \vec{x}(t).
$$

To check observability using Kalman’s test, we compute the observability matrix:

$$
\mathcal{O} = \begin{bmatrix} C \\ C A \end{bmatrix}.
$$

That is
$$
    CA=\begin{bmatrix}
        0&1
    \end{bmatrix}\begin{bmatrix}
        -1&0\\2&-2
    \end{bmatrix}=\begin{bmatrix}
        2&-2
    \end{bmatrix}.
$$
So

$$
    \mathcal{O}=\begin{bmatrix}
        0&1\\2&-2
    \end{bmatrix}.
$$

Evaluating the determinant:

$$
\det(\mathcal{O}) \neq 0.
$$

Since the rank of $ O $ is equal to the state dimension, the system is observable. This result makes sense, as the outermost outflow includes information about both tank levels. Thus, given knowledge of the inflow, we can fully reconstruct the tank states.



Using the PBH Test for Observability:


$$
    \lambda_1 I-A=\begin{bmatrix}
        0&0\\-2&1
    \end{bmatrix},\;\lambda_2I-A=\begin{bmatrix}
        -1&0\\-2&0
    \end{bmatrix}.
$$

Then we have

$$
    \begin{bmatrix}
        \lambda_1 I-A\\C
    \end{bmatrix}=\begin{bmatrix}
        0&0\\-2&1\\0&1
    \end{bmatrix}.
$$

Clearly the rank is $2$ which is the order of the system. Moreover, we have

$$
    \begin{bmatrix}
        \lambda_2 I-A\\C
    \end{bmatrix}=\begin{bmatrix}
        -1&0\\-2&0\\0&1
    \end{bmatrix}.
$$

In this case as well, the rank is $2$ which is the order of the system. Then according to the PBH test, the system is observable.


4. We check observability with respect to both outflow measurements, $q_{1,2}$ and $q_{out}$. In this case

$$
y(t) = \begin{bmatrix} q_{1,2} \\ q_{out} \end{bmatrix}=\begin{bmatrix}
    h_1(t)\\h_2(t)
\end{bmatrix}=\begin{bmatrix}
    1&0\\0&1
\end{bmatrix}\begin{bmatrix}
    h_1(t)\\h_2(t)
\end{bmatrix}.
$$

The output matrix is:

$$
C = I_2.
$$

The observability matrix becomes:

$$
\mathcal{O} = \begin{bmatrix} C\\CA\end{bmatrix}=\begin{bmatrix}
    1&0\\0&1\\-1&0\\2&-2
\end{bmatrix}.
$$

Clearly the rank is $2$.  Since the rank matches the state dimension, the system is observable (according to the Kalman test) when measuring both outflows.

## Exercise

Consider the system

$$
    \dot{\vec{x}}(t)=A\vec{x}(t),\quad y(t)=C\vec{x}(t).
$$

With

$$
    A=\begin{bmatrix}
        -1&0\\0&-2
    \end{bmatrix},\quad C=\begin{bmatrix}
        c_1&c_2
    \end{bmatrix},
$$

where $c_1,\;c_2\in\mathbb{R}$. The an initial condition is:

$$
\vec{x}(0) = \begin{bmatrix}
    x_1^0\\x_2^0
\end{bmatrix},
$$

where $x_1^0\neq x_2^0$. We seek to determine for which values of $ c_1,c_2 $ the system is observable using the definition of observability.



### Solution

To check observability, we compute $ y(t) $ explicitly. First, we find $ e^{At} $. Since $A$ is diagonal, 

$$
e^{At} = \begin{bmatrix}
    e^{-t}&0\\0&e^{-2t}
\end{bmatrix},
$$

where $-1,\;-2$ are the eigenvalues of $A$. The homogeneous solution is:

$$
\vec{x}(t) &= e^{At} \vec{x}(0)\\
           &= \begin{bmatrix}
    e^{-t}&0\\0&e^{-2t}
\end{bmatrix}\begin{bmatrix}
    x_1^0\\x_2^0
\end{bmatrix}\\
&=\begin{bmatrix}
    x_1^0e^{-t}\\ x_2^0e^{-2t}
\end{bmatrix}.
$$

The output equation gives:

$$
y(t) &= C e^{At} \vec{x}(0)\\
     &=\begin{bmatrix}
         c_1&c_2
     \end{bmatrix}\begin{bmatrix}
    x_1^0e^{-t}\\ x_2^0e^{-2t}
\end{bmatrix}=c_1x_1^0e^{-t}+c_2x_2^0e^{-2t}.
$$

To check observability, we compute:

```{math}
:label: eq:ex2_observability
\int_{t_0}^{t_f} y^T(t) y(t) dt.
```

The system is observable if this expression is poisitive.
By direct computation

$$
    y^T(t)y(t)=c_1^2(x_1^0)^2e^{-2t}+2c_1c_2x_1^0x_2^0e^{-3t}+c_2^2(x_2^0)^2e^{-4t}.
$$

Since the integrand is positive, {eq}`eq:ex2_observability` is zero only if the integrand is equal to zero for all $t\in[t_0,t_f]$. 

We analyze when this condition holds. For $c_1=0$,

$$
    y^T(t)y(t)=c_2^2(x_2^0)^2e^{-4t}.
$$

We emphasize that {eq}`eq:ex2_observability` must be positive for any non-zero initial condition. Take $\vec{x}(0)=\begin{bmatrix}
    1\\0
\end{bmatrix},$

then $\vec{x}(0)\neq\vec{0}$, but $y^T(t)y(t)=0$ for all $t\in[t_0,t_f]$.
If $c_2=0$, then 

$$
    y^T(t)y(t)=c_1^2(x_1^0)^2e^{-2t}.
$$

Again, {eq}`eq:ex2_observability` must be positive for any non-zero initial condition. Take $\vec{x}(0)=\begin{bmatrix}
    0\\1
\end{bmatrix},$

then $\vec{x}(0)\neq\vec{0}$, but $y^T(t)y(t)=0$ for all $t\in[t_0,t_f]$. So if $c_1=0$ or $c_2=0$ the system is not observable. Exponents of different powers are linearly independent, so it is enough that

$$
    c_1\neq0,\quad c_2\neq0,
$$

for observability. We confirm this result with the Kalman test for observability.

Here

$$
    CA=\begin{bmatrix}
        -2c_1&c_2
    \end{bmatrix}.
$$

The observability matrix is

$$
    \mathcal{O}=\begin{bmatrix}
        C\\CA
    \end{bmatrix}=\begin{bmatrix}
        c_1&c_2\\-2c_1&c_2.
    \end{bmatrix}
$$

We know that $\text{rank}(\mathcal{O})=2$ if and only if $\det(\mathcal{O})\neq0$.

$$
    \det(\mathcal{O})=c_1c_2+2c_1c_2=3c_1c_2.
$$

Clearly if $c_1=0$ or $c_2=0$, then $\det(\mathcal{O})=0$ and the system is not observable.

```{prf:remark}
If $A$ is an invertible diagonal matrix, $C$ is a vector (the system is SISO/MIMO), we can know of the system is observable by observing $C$. If $C$ has a zero element, then the system is not observable.
```
