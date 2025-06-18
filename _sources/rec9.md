---
title: Introduction to Control -- Recitation 9
---

# Introduction to Control -- Recitation 9

## Controllability


Consider the system


```{math}
:label: eq:state_space
\dot x(t)&=Ax(t)+B u(t),\\
y(t)&=C x(t)+D u(t).\nonumber
```

```{prf:definition}
The system {eq}`eq:state_space` is called controllable if for any $a,b\in\mathbb{R}^n$ there exists a time $T\geq 0$ and a control $u(t)$, $t\in[0,T]$, such that for $x(0)=a$ the solution $x(t)$ of the system satisfies $x(T)=b$. 
```

In other words, we can steer  the state from any initial condition $a$ to any desired final condition $b$ in finite time. 


````{prf:theorem}
:label: thm:controll
(Kalman Controllability Test) The system {eq}`eq:state_space` is controllable if and only if

```{math}
:label: eq:necc_sugg_cont
 \text{rank}\begin{bmatrix}
     B&AB&\dots&A^{n-1}B
 \end{bmatrix}=n. 
```
````




````{prf:proposition}
(PBH test for controllability) The pair $(A,B)$ is controllable if and only if 

$$
     \text{rank}\begin{bmatrix}
         \lambda I_n-A & B
     \end{bmatrix}=n \text{ for any }\lambda\in\sigma(A). 
$$

````

```{prf:remark}
Notice that the above tests depend only on the matrices $ A $ and $ B $. Therefore, controllability is a property of the pair $ (A, B) $. Since $ A $ and $ B $ are constant matrices in time-invariant systems, the controllability property does not change over time. If a system is controllable at a certain time, it is controllable at all times.
```



## Dual Systems

````{prf:definition}
The dual system of  the system {eq}`eq:state_space` is the control system
```{math}
:label: eq:dual
    \dot{\tilde x} &=A^\top \tilde x+C^\top \tilde u ,\nonumber \\
    \tilde y&= B^\top \tilde x+D^\top \tilde u.
```
````

Note that the matrix dimensions imply that $\tilde x(t) \in\mathbb{R}^n$, $\tilde u(t)\in\mathbb{R}^p$, and $\tilde y(t)\in\mathbb{R}^m$.


```{prf:theorem}
:label: thm:dula
The system {eq}`eq:state_space` is controllable if and only if the dual system {eq}`eq:dual` is observable. 
```

## Stabilizability

Suppose that we have access to the entire state-space vector and we design a controller by

$$
u(t)=Fx(t)
$$

with a matrix $F\in\mathbb{R}^{ m\times n}$. The closed-loop system is

$$
    \dot x&= A x+B F x\\
    &=(A+BF)x.
$$

```{prf:definition}
:label: def:stabiliz

The system {eq}`eq:state_space` is called stabilizable if
there exists a matrix $F\in\mathbb{R}^{ m\times n}$ such that $A+BF$ is stable
(that is, every eigenvalue of $A+BF$ has a negative real part).
```

```{prf:proposition}
The system {eq}`eq:state_space` is stabilizable if and only if for any $x(0)\in\mathbb{R}^n$ there exists a control $u:[0,\infty)\to\mathbb{R}^m$, with $\lim_{t\to\infty}u(t)=0$, such that
	
$$
    \lim_{t\to\infty}x(t)=0. 
$$
```


```{prf:proposition}
(PBH test for stabilizability) The pair $(A,B)$ is stabilizable if and only if 

$$
     \text{rank}\begin{bmatrix}
         \lambda I_n-A & B
     \end{bmatrix}=n \text{ for any }\lambda\in\sigma(A)\text{ with Re$(\lambda)\geq0$}. 
$$
```

```{prf:lemma}
If {eq}`eq:state_space` is controllable then it is stabilizable. 
```

## Detectability

````{prf:definition}
The system {eq}`eq:state_space` is called detectable if $y(t)=0$ for all $ t\geq 0$ implies that
 
```{math}
:label: eq:contoze
 \lim_{t\to\infty}x(t)= 0 .
```
````

  
````{prf:theorem}
(PBH Test for Detectability) Consider the system {eq}`eq:system_obsvr`.
Let $\sigma(A)$ denote the set of eigenvalues of $A$.
Then $(A,C)$ is detectable 
if and only if
```{math}
:label: eq:pbh_test_detect

        rank\begin{bmatrix}
            \lambda I_n-A\\
            C
        \end{bmatrix}=n,\text{ for any }\lambda\in\sigma(A) \text{ with }
        \text{Re}(\lambda)\geq  0.
```
````

```{prf:lemma}
If {eq}`eq:state_space` is observable then it is detectable. 
```

### Exercise 1

Let $ x_1(t)$ represent the population density of the prey (e.g., rabbits) per square kilometer.

Let $ x_2(t) $ represent the population density of the predator (e.g., foxes) per square kilometer.

Then, $ \dot{x}_1(t) $ and $ \dot{x}_2 (t)$ denote the rate of change over time of the prey and predator populations, respectively.

Let $ \alpha $ be the natural growth rate of the prey population, and $ \beta $ be the effect of the predator on the prey population.

Let $ \gamma $ be the death rate of the predator population, and $ \delta $ be the effect of the prey on the predator population.

The system is given by:

$$
\dot{x}_1(t) = \alpha x_1(t) - \beta x_2(t),
$$

$$
\dot{x}_2(t) = -\gamma x_2(t) + \delta x_1(t).
$$

Here $\alpha,\beta,\gamma,\delta\geq0$. Denote $\vec{x}(t)=\begin{bmatrix}x_1(t)\\x_2(t)\end{bmatrix}$, then

$$
    \begin{bmatrix}\dot{x}_1(t)\\\dot{x}_2(t)\end{bmatrix}=\begin{bmatrix}
        \alpha&-\beta\\\delta&-\gamma
    \end{bmatrix}\begin{bmatrix}x_1(t)\\x_2(t)\end{bmatrix}.
$$


Assume $ \alpha = \delta=0 $ and $ \beta = \gamma=2 $, meaning that the populations of predators and prey affect each other directly without natural birth or death. Assume also that the system has control inputs:

$$
B = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}.
$$

We obtain

$$
    \begin{bmatrix}\dot{x}_1(t)\\\dot{x}_2(t)\end{bmatrix}=\begin{bmatrix}
        0&-2\\2&0
    \end{bmatrix}\begin{bmatrix}x_1(t)\\x_2(t)\end{bmatrix}+\begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}\vec{u}(t).
$$


1. Is the system controllable with respect to input $u_1(t)$?
2. Is the system controllable with respect to input $u_2(t)$?
3. Is the system controllable with respect to input $\vec{u}(t)$?
4. Repeat items $1.-2.$ using the duality theorem.


### Solution

    
1. In this case, $ B = \begin{bmatrix} 1 \\ 0 \end{bmatrix} $, we compute the Kalman controllability matrix:

$$
\mathcal{C} = \begin{bmatrix} B & AB \end{bmatrix}.
$$

$$
    AB=\begin{bmatrix}
        0&-2\\2&0
    \end{bmatrix}\begin{bmatrix}
        1\\0
    \end{bmatrix}=\begin{bmatrix}
        0\\2
    \end{bmatrix}.
$$

Then

$$
    \mathcal{C}=\begin{bmatrix}
        1&0\\0&2
    \end{bmatrix}.
$$

We have $ \text{rank}(\mathcal{C}) = 2 $, so the system is controllable.

2. In this case

$ B = \begin{bmatrix} 0 \\ 1 \end{bmatrix} $, we compute:

$$
    AB=\begin{bmatrix}
        0&-2\\2&0
    \end{bmatrix}\begin{bmatrix}
        0\\1
    \end{bmatrix}=\begin{bmatrix}
        -2\\0
    \end{bmatrix}.
$$

The controllability matrix is

$$
    \mathcal{C}=\begin{bmatrix}
        B&AB
    \end{bmatrix}=\begin{bmatrix}
        0&-2\\1&0
    \end{bmatrix}.
$$

Clearly, $\text{rank}(\mathcal{C})=2$, so the system is controllable.

3. In this case

For $ B = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} $, the controllability matrix is:

$$
\mathcal{C} = \begin{bmatrix} B & AB \end{bmatrix}=\begin{bmatrix}
    0&-2&0&-2\\2&0&2&0
\end{bmatrix}.
$$

Clearly, $\text{rank}(\mathcal{C})=2$, so the system is controllable.


We confirm controllability using the PBH Test

Finding the eigenvalues of $ A $:

$$
\det(A - \lambda I) = \lambda^2+\delta\beta=0\rightarrow\lambda_{1,2}=\pm j\sqrt{\delta\beta}.
$$

In this case $\beta=\delta=2$, so

$$
    \lambda_{1,2}=\pm j2.
$$

Checking the **Hautus criterion**:

$$
\text{rank} \begin{bmatrix} \lambda I - A & B \end{bmatrix}.
$$

For $B=\begin{bmatrix}
    1\\0
\end{bmatrix}$:

$$
    \begin{bmatrix}
        \lambda_{1,2}I-A&B
    \end{bmatrix}=\begin{bmatrix}
        \pm j2&2&1\\-2&\pm j2&0
    \end{bmatrix}\rightarrow\text{rank}\begin{bmatrix}
        \lambda_{1,2}I-A&B
    \end{bmatrix}=2.
$$

So the system is controllable with respect to $u_1(t)$. 

For $B=\begin{bmatrix}
    0\\1
\end{bmatrix}$:

$$
    \begin{bmatrix}
        \lambda_{1,2}I-A&B
    \end{bmatrix}=\begin{bmatrix}
        \pm j2&2&0\\-2&\pm j2&1
    \end{bmatrix}\rightarrow\text{rank}\begin{bmatrix}
        \lambda_{1,2}I-A&B
    \end{bmatrix}=2.
$$

So the system is controllable with respect to $u_2(t)$. 
As an exercise, confirm that the system is controllable with respect to both inputs. 


4. 

The **dual system** is:

$$
\dot{\tilde{x}}(t) = A^\top \tilde{x}(t) ,\quad y(t)=B^\top \tilde{x}(t).
$$

If we consider the first output only, we have $B^\top=\begin{bmatrix}
    1&0
\end{bmatrix}$. In this case

$$
    B^\top A=\begin{bmatrix}
    1&0
\end{bmatrix}\begin{bmatrix}
    0&2\\-2&0
\end{bmatrix}=\begin{bmatrix}
    0&2
\end{bmatrix}.
$$

The observability matrix is

$$
    \mathcal{O}=\begin{bmatrix}
        B^\top\\B^\top A
    \end{bmatrix}=\begin{bmatrix}
        1&0\\0&2
    \end{bmatrix}.
$$

Clearly, the rank is $2$, so the dual system is observable. Which implies that the original system is controllable. 

For the second output, $B^\top=\begin{bmatrix}
    0&1
\end{bmatrix}$. In this case

$$
    B^\top A=\begin{bmatrix}
    0&1
\end{bmatrix}\begin{bmatrix}
    0&2\\-2&0
\end{bmatrix}=\begin{bmatrix}
    -2&0
\end{bmatrix}.
$$

The observability matrix is

$$
    \mathcal{O}=\begin{bmatrix}
        B^\top\\ B^\top A
    \end{bmatrix}=\begin{bmatrix}
        0&1\\-2&0
    \end{bmatrix}.
$$

Clearly, the rank is $2$, so the dual system is observable, and this implies that the original system is controllable. 

### Exercise 2



Consider the system

$$
    \dot{\vec{x}}(t)=\begin{bmatrix}
        2&0\\3&-1
    \end{bmatrix}\vec{x}(t)+\begin{bmatrix}
        1&2\\1&0
    \end{bmatrix}\vec{u}(t),\quad y(t)=\begin{bmatrix}
        0&2
    \end{bmatrix}\vec{x}(t).
$$


1. Is the system observable? Is it detectable?
2. Is the system controllable with respect to the first input? Is it stabilizable?
3. Is the system controllable with respect to the second input? is it stabilizable?



### Solution


1. We check if the system is observable.

To check observability, we compute the observability matrix:

$$
CA=\begin{bmatrix}
    0&2
\end{bmatrix}\begin{bmatrix}
    2&0\\3&-1
\end{bmatrix}=\begin{bmatrix}
    6&-2
\end{bmatrix}\rightarrow \mathcal{O} = \begin{bmatrix} C \\ CA  \end{bmatrix}=\begin{bmatrix}
    0&2\\6&-2
\end{bmatrix}.
$$

Since $ \text{rank}(\mathcal{O}) = 2 $, the system is observable.



2. We find the eingevalues of $A$:

$$
    \lambda I-A=\begin{bmatrix}
        \lambda-2&0\\-3&\lambda+1
    \end{bmatrix}\rightarrow \det(\lambda I-A)=(\lambda-2)(\lambda+1).
$$

The eigenvalues of $A$ are $\lambda_1=-1,\;\lambda_2=2$.
To check controllability with respect to  the first input, we use the PBH test:

In this case 

$$
    B=\begin{bmatrix}
        1\\1
    \end{bmatrix}.
$$

Then, for $\lambda_1$:

$$
\text{rank} \begin{bmatrix} \lambda_1 I - A & B \end{bmatrix}=\text{rank}\begin{bmatrix}
    -3&0&1\\-3&0&1
\end{bmatrix}=1.
$$


Since the rank condition fails, we conclude: The system is NOT controllable with respect to the first input.

The system will be stabilizable (with respect to the first input) only if the rank condition holds for $\lambda_2$ since $\lambda_2>0$.

$$
\text{rank} \begin{bmatrix} \lambda_2 I - A & B \end{bmatrix}=\text{rank}\begin{bmatrix}
    0&0&1\\-3&3&1
\end{bmatrix}=2.
$$

So the system is stabilizable.

3. We check Controllability with respect to the second input. In this case

$$
    B=\begin{bmatrix}
        2\\0
    \end{bmatrix}.
$$

Using the PBH test:

$$
    \text{rank}\begin{bmatrix}
        \lambda_1-A&B
    \end{bmatrix}=\text{rank}\begin{bmatrix}
        -3&0&2\\-3&0&0
    \end{bmatrix}=2,
$$


and

$$
    \text{rank}\begin{bmatrix}
        \lambda_2-A&B
    \end{bmatrix}=\text{rank}\begin{bmatrix}
        0&0&2\\-3&3&0
    \end{bmatrix}=2.
$$

The rank is $2$ in both cases, so the system is controllable with respect to the second input.
Since the system is controllable, it is also stabilizable.


### Exercise 3

Consider the system

$$
    \dot{\vec{x}}(t)=\begin{bmatrix}
        -1&0\\0&-2
    \end{bmatrix}\vec{x}(t)+\begin{bmatrix}
        b_1\\b_2
    \end{bmatrix}\vec{u}(t),\quad \vec{x}(0)=\vec{x}_0=\begin{bmatrix}
        x_1^0\\x_2^0
    \end{bmatrix}.
$$

For which values of $b_1,b_2\in\mathbb{R}$ is the system controllable? Prove this using the definition of controllability. 

### Solution

We find the explicit solution $\vec{x}(t)=\begin{bmatrix}
    x_1(t)\\x_2(t)
\end{bmatrix}$, and find the values of $b_1,b_2$ such that for any non-zero initial condition $\vec{x}_0$ and each vector $\vec{x}_f=\begin{bmatrix}
    x_1^f\\x_2^f
\end{bmatrix}$ we can find some input $\vec{u}(t)=\begin{bmatrix}
    u_1(t)\\u_2(t)
\end{bmatrix}$ such that $\vec{x}(T)=\vec{x}_f$. We know that

$$
    \vec{x}(t)=e^{At}\vec{x}_0+\int_0^t e^{A(t-\tau)}Bu(\tau)d\tau.
$$

Since $A$ is diagonal,

$$
    e^{At}\vec{x}(t)=\begin{bmatrix}
        e^{-t}&0\\0&e^{-2t}
    \end{bmatrix}\begin{bmatrix}
        x_1^0\\x_2^0
    \end{bmatrix}=\begin{bmatrix}
        x_1^0e^{-t}\\x_2^0e^{-2t}
    \end{bmatrix}.
$$

Moreover, 

$$
    e^{A(t-\tau)}B=\begin{bmatrix}
        e^{-(t-\tau)}&0\\0&e^{-2(t-\tau)}
    \end{bmatrix}\begin{bmatrix}
        b_1\\b_2
    \end{bmatrix}=\begin{bmatrix}
        b_1e^{-(t-\tau)}\\b_2 e^{-2(t-\tau)}
    \end{bmatrix}.
$$

We have

$$
    \vec{x}(t)=\begin{bmatrix}
        x_1^0e^{-t}\\x_2^0e^{-2t}
    \end{bmatrix}+\int_0^t\begin{bmatrix}
        b_1e^{-(t-\tau)}\\b_2 e^{-2(t-\tau)}
    \end{bmatrix}\vec{u}(\tau)d\tau.
$$

Decomposing element wise, we have

$$
    x_1(t)=x_1^0e^{-t}+\int_0^tb_1e^{-(t-\tau)}u_1(\tau)d\tau,\\
    x_2(t)=x_2^0e^{-2t}+\int_0^tb_2e^{-2(t-\tau)}u_2(\tau)d\tau.
$$

Rearranging is

$$
    x_1(t)=x_1^0e^{-t}+b_1e^{-t}\int_0^te^{\tau}u_1(\tau)d\tau,\\
    x_2(t)=x_2^0e^{-2t}+b_2e^{-2t}\int_0^tbe^{2\tau}u_2(\tau)d\tau.
$$

The solution at time $t=T$ is

$$
    x_1(T)=x_1^0e^{-T}+b_1e^{-T}\int_0^Te^{\tau}u_1(\tau)d\tau,\\
    x_2(T)=x_2^0e^{-2T}+b_2e^{-2T}\int_0^Tbe^{2\tau}u_2(\tau)d\tau.
$$

We want $\vec{x}(T)=\vec{x}_f$, that is:

$$
    x_1^f=x_1^0e^{-T}+b_1e^{-T}\int_0^Te^{\tau}u_1(\tau)d\tau,\\
    x_2^f=x_2^0e^{-2T}+b_2e^{-2T}\int_0^Tbe^{2\tau}u_2(\tau)d\tau.
$$

Clearly, if $b_1=0$ or $b_2=0$ or both, the system won't be controllable, since then we cannot control either $x_1(t)$ or $x_2(t)$ (or both) using $\vec{u}(t)$. For example, if $b_1=0$, $x_1(T)=x_1^0e^{T}$, that is, for any $\vec{u}(t)$. So clearly, unless $x_1^f=x_1^0e^{-T}$, we cannot control the system such that $x_1(t)=x_1^f$. 

```{prf:remark}
If $A$ is diagonal and invertible, and $B$ is a vector (the system is SISO/SIMO), then we can know if the system is controllable simply by observing the vector $B$. If $B$ has a zero element, then the system is not controllable. 
```
