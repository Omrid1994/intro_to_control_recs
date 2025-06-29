---
title: Introduction to Control -- Recitation 5
---

# Introduction to Control -- Recitation 5


## Root Locus Diagram

We usually deal with loop-gain of the form $P(s)C(s)=k\tilde{G}(s)$. In this case, the closed-loop system is:

$$
    T(s) = \frac{k\tilde{G}(s)}{1 + k\tilde{G}(s)}.
$$

If we write $C(s)P(s) = k\frac{n(s)}{d(s)}$, we obtain:

$$
    T(s) = \frac{k n(s)}{d(s) +  kn(s)}.
$$

Of course, every choice of $k$ yields different denominator roots. 

````{prf:example}
Let

$$
    C(s)=k,\quad P(s) = \frac{1}{s(s+2)},
$$

we get the closed-loop system:

$$
    P(s) = \frac{5k}{s^2+s + 5k}.
$$

For $k = 0$, we obtain the roots: $s = -1, 0$. For $k = 1$, we obtain the roots $s=-0.5\pm j\frac{\sqrt{19}}{2}$.
````

$$
\boxed{\text{The Root-Locus diagram provides all the possible poles that can be achieved from the system for all values of $k\in\mathbb{R}$}}
$$

We focus on the denominator of the closed-loop system:

$$
    1 + k\tilde{G}(s) = 0,
$$

which always satisfies:

$$
    k\tilde{G}(s) = -1.
$$

From this, we can define two conditions in the complex plane for the open-loop system:

**Magnitude Condition:**

$$
    |k\tilde{G}(s)| = 1.
$$

**Phase Condition:**

$$
    \angle k\tilde{G}(s) = (2\ell+1) \pi, \quad \ell \in \mathbb{Z}.
$$

```{prf:remark}
If $k<0$, the phase condition becomes

$$
        \angle k\tilde{G}(s)=2\pi\ell,\quad \ell\in\mathbb{Z}.
$$
```

Therefore, every point in the Root-Locus must satisfy these two conditions.

We describe the loop-gain system as a ratio of polynomials:

$$
    k\tilde{G}(s) = k\frac{n(s)}{d(s)}.
$$

where $n(s)$ is a polynomial of degree $w$, and $d(s)$ is a polynomial of degree $m$. Since we are dealing with **proper** systems, $w \leq m$.

### Drawing a Root Locus Diagram

Below are some general rules of thumb for the Root Locus diagram:

- There will be $\tilde{n}$ curves when $\tilde{n}=\max(m,w)$. If the system is proper, there will be $m$ curves.
- As $k$ increases from $0$ to infinity, the curves move from the poles of $G(s)$ to the zeros of $G(s)$.
- Complex roots always appear in conjugate pairs, making the diagram symmetric about the real axis.
- The branches do not intersect, meaning there are no loops. If two branches meet, they split apart at that point.

These rules will not be used to draw the Root Locus but can serve as a consistency check to ensure the diagram aligns with the fundamental rules.

Using these rules along with the magnitude and angle conditions, we can construct the Root Locus:


    
1. **Marking Poles and Zeros of the Loop-Gain on the Complex Plane**: Poles are marked with an 'X', and zeros are marked with a circle.
2. **Determining the Real Axis Branches**: We use the angle condition to determine segments of the Root Locus along the real axis. A real pole contributes an angle of $180^\circ$, and a real zero contributes an angle of $0^\circ$. The angles from complex pole-zero pairs cancel out. A segment belongs to the Root Locus if the sum of angles contributed by all poles and zeros to that segment is $180^\circ$.
**Alternative Real Axis Rule**: If the number of poles and zeros to the right of a segment is odd, that segment belongs to the Root Locus; otherwise, it does not.

```{prf:remark}
For $k<0$, a real point $s\in\mathbb{R}$ is included in the root locus plot if and only if the number of real poles and zeros of $\frac{n(s)}{d(s)}$ to the right of $s$ is even.
```

3. **Asymptotes**: The angles of the asymptotes are given by:

```{math}
:label: eq:asymptotoes
\theta = \frac{180^\circ}{m-w}\cdot\ell, 
```

where $\ell$ runs through the first $m-w$ **odd** numbers if $k>0$ and through the first $m-w$ **even** numbers if $k<0$.

The center of the asymptotes is given by:

$$
\gamma = \frac{\sum_{i=1}^m p_i - \sum_{i=1}^w z_i}{m-w},
$$

where $p_i$ are the real parts of the poles and $z_i$ are the real parts of the zeros.

4. **Break-away and Break-in Points**:
If two Root Locus branches meet on the real axis, they split apart at a breakaway or break-in point.

To find breakaway points, we express the characteristic equation as:

$$
d(s)+kn(s)=0\rightarrow k=-\frac{d(s)}{n(s)}.
$$

We differentiate and set it to zero:

```{math}
:label: eq:breakinpoint
\frac{dk}{ds}= \frac{d'(s)n(s)-d(s)n'(s)}{n^2(s)} = 0.
```

The roots of this equation give the breakaway points. **A root is valid only if it is real and belongs to the Root Locus*.

5.  **Exit and Entry Angles**:
The Root Locus leaves complex poles and enters complex zeros at specific angles. The angle of departure from a complex pole is:

$$
\theta_{exit} = 180^\circ - \sum (\text{angles from other poles}) + \sum (\text{angles from other zeros}).
$$

Similarly, the angle of entry to a complex zero is:

$$
\theta_{entry} = 180^\circ - \sum (\text{angles from other zeros}) + \sum (\text{angles from poles}).
$$

where the sums are taken over all other poles and zeros relative to the given pole or zero.

````{prf:remark}
The angles between two poles (or any two points on the complex plane) is as follows: First, we draw a straight line between the poles. Then, we draw a horizontal line to the right of the first pole. The angle between the first pole and the second pole is the angle between the horizontal line and the line connecting the poles. 

```{figure} images/Rec5/angle_between_roots.png
---
width: 70%
name: fig:closed_system_1
---
Angle between $p_1$ and $p_2$.
```

````

6. **Imaginary Axis Crossings**:
To find where the Root Locus crosses the imaginary axis, we set $s = j\omega$ in the characteristic equation and separate the real and imaginary parts. Solving for $\omega$ and $k$ gives the crossing point and the corresponding gain.


### Finding the Gain Corresponding to some Point $s_0$ on the Root Locus Diagram

Every point $s_0$ on the Root Locus satisfies the magnitude condition:

$$
|k\tilde{G}(s_0)|=k\Bigg|\frac{n(s_0)}{d(s_0)}\Bigg| = 1.
$$

To find the gain for a specific system requirement, locate the desired point on the Root Locus,$s_0$, and solve for $k$ using:

```{math}
:label: eq:k_for_s
k = \Bigg|\frac{n(s_0)}{d(s_0)}\Bigg|.
```




### Exercise 1

Consider a system with:

$$
C(s)P(s) = \frac{k}{s(s^2+4s+8)}.
$$

Sketch the Root Locus diagram for the system. For which values of $k$ is the closed-loop system stable?

### Solution

1. **Poles and Zeros of the Open-Loop System**:

The loop-gain has the following poles:

$$
    s=0,\;-2\pm j2.
$$

```{figure} images/Rec5/Ex1.1.png
---
width: 70%
name: fig:closed_system_1
---

```

2. **Root Locus Branches on the Real Axis**:

- If no poles or zeros exist to the right of a segment, the Root Locus does not pass through it.
- If the number of poles to the right is odd, then the segment belongs to the Root Locus.
In this case, if $s<0$ there are no poles and zeros to the right on the real axis. If $s>0$ there is an odd number of poles and zeros (one pole) on the real axis, this pole will contribute $-180^\circ$.

```{figure} images/Rec5/Ex1.2.png
---
width: 70%
name: fig:closed_system_1
---

```

3. **Determining Asymptotes**:

The degree of the denominator is $m=3$, the degree of the numerator is $w=0$. We have $m-w=3$.

To compute the angles of the asymptotes, we use {eqref}`eq:asymptotoes`:

$$
    \theta_1&=\frac{180^\circ}{3-0}\cdot 1=\frac{180^\circ}{3}\cdot1=60^\circ,\\
    \theta_2&=\frac{180^\circ}{3-0}\cdot 3=\frac{180^\circ}{3}\cdot 3=180^\circ,\\
    \theta_3&=\frac{180^\circ}{3-0}\cdot 5=\frac{180^\circ}{3}\cdot 5=300^\circ=-60^\circ.
$$

The center point of the asymptotes on the real axis is:

$$
    \gamma=\frac{0-2-2}{3-0}=-\frac{4}{3}.
$$

```{figure} images/Rec5/Ex1.3.png
---
width: 70%
name: fig:closed_system_1
---

```

4. **Finding Breakaway Points**:

We have:

$$
n(s)=1,\quad d(s)=s^3+4s^2+8s.
$$

differentiating we have:

$$
    n'(s)=0,\quad d'(s)=3s^2+8s+8.
$$

Substituting in {eqref}`eq:breakinpoint` we have:

$$
d'(s)n(s)-d(s)n'(s)&=3s^2+8s+8-0\\
                   &=3s^2+8s+8.
$$

Comparing to zero and solving this equation, we obtain:

$$
s_{1,2} =-1.333\pm j0.943. 
$$

Since these roots are not on the real axis, they do not form valid break-away and break-in points. Therefore, there are no break-in and break-out points.

5. **Exit Angles from Complex Poles**:

We compute the exit angle from the pole $-2+j2$. From symmetry, this also gives the exit angle from $-2-j2$.

The angle between $-2-j2$ and $-2+j2$ is $90^\circ$. The angle between $s=0$ and $-2+j2$ is $135^\circ$.

```{figure} images/Rec5/Ex1.4.png
---
width: 70%
name: fig:closed_system_1
---

```

The sum of these angles and the exit angles from $-2+j2$ should be $\pm180^\circ$:

$$
    -\theta_3-\theta_2-\theta_3=-90^\circ-\theta_2-135^\circ=180.
$$

We obtain $\theta_2=-405^\circ=-45^\circ$.

By symmetry, the exit angle from the other complex pole is $45$ degrees.

```{figure} images/Rec5/Ex1.5.png
---
width: 70%
name: fig:closed_system_1
---

```

6. **Imaginary Axis Crossing**:
The denominator of the closed-loop is:

$$
    p(s)=d(s)+kn(s)=s^3+4s^2+8s+k.
$$

Substituting $s=j\omega$ we have:

$$
    p(j\omega)&=(j\omega)^3+4(j\omega)^2+8j\omega+k\\
              &=k-4\omega^2+j\omega(8-\omega^2).
$$

Comparing with zero we have:

$$
    k-4\omega^2+j\omega(8-\omega^2)=0.
$$

We separately compare the real and imaginary parts with zero:

$$
    k-4\omega^2&=0,\\
    \omega(8-\omega^2)&=0.
$$

Solving, we obtain the following pairs:

$$
    (\omega,k)=(0,0),\quad (\omega,k)=(\pm\sqrt{8},32).
$$

Clearly we already found the origin. The intersection with the imaginary axis is at $\pm j\sqrt{8}$. The intersection is obtained for $k=32$.

We are ready to draw the root locus diagram.

```{figure} images/Rec5/EX1_final.png
---
width: 70%
name: fig:ex1rl
---
The Root Locus diagram of $G(s)=\frac{k}{s(s^2+4s+8)}$.
```

We know the closed-loop system is stable if **all** the poles of the closed-loop system have a negative real part. Figure {numref}`fig:ex1rl` gives us all possible poles of the closed-loop system for $k>0$. For $k=0$ the poles are exactly the poles of the loop-gain. As we increase $k$ the poles go along the root locus diagram. They will all have a negative real part until we intersect the imaginary axis. We know this happends for $k=32$. To conclude, the closed-loop system is stable for

$$
    0<k<32.
$$


### Exercise 2

Given a system with:

$$
C(s)=k,\quad P(s)= \frac{(s+2)(s+3)}{s(s+1)}.
$$

- Draw the Root Locus of the system.

- Determine the gain range for which the system is under-damped.

### Solution


1. **Marking the Poles and Zeros of the Open-Loop System**:

The system has the following open-loop poles and zeros:

$$
\text{Poles: } s = -1,
$$

$$
\text{Zeros: } s = -2,-3.
$$

```{figure} images/Rec5/r5_ex2.1.png
---
width: 70%
name: fig:closed_system_1
---

```


2. **Root Locus Branches on the Real Axis**:

Using the angle condition, we determine segments of the Root Locus along the real axis:

$$
    \angle k\frac{(s+2)(s+3)}{s(s+1)}=\angle(s+2)+\angle(s+3)-\angle s-\angle(s+1).
$$

We want this sum to be $\pm180^\circ$. For the interval $s\in(-\infty, -3)$:

$$
    \angle(s+2)+\angle(s+3)-\angle s-\angle(s+1)=0^\circ+0^\circ-0^\circ-0^\circ=0^\circ.
$$

Even number of poles and zeros to the right implies no root locus. For the interval $s\in(-3, -2)$:

$$
    \angle(s+2)+\angle(s+3)-\angle s-\angle(s+1)=0^\circ+0^\circ-180^\circ-0^\circ=-180^\circ.
$$

Odd number of poles and zeros to the right implies root locus exists. For the interval $s\in(-2, -1)$:

$$
    \angle(s+2)+\angle(s+3)-\angle s-\angle(s+1)=0^\circ+0^\circ-180^\circ-180^\circ=-360^\circ.
$$

Even number of poles and zeros to the right implies no root Locus. For the interval $s\in(-1, 0)$:

$$
    \angle(s+2)+\angle(s+3)-\angle s-\angle(s+1)=180^\circ+0^\circ-180^\circ-180^\circ=-180^\circ.
$$

Odd number of poles and zeros to the right implies root locus exists. For the interval $s\in(0, \infty)$: 

$$
    \angle(s+2)+\angle(s+3)-\angle s-\angle(s+1)=180^\circ+180^\circ-180^\circ-180^\circ=0^\circ.
$$

No poles or zeros to the right implies no root locus.

```{figure} images/Rec5/r5_ex2.2.png
---
width: 70%
name: fig:closed_system_1
---

```

3. **Determining Asymptotes**:

Since $n = m$, there are no asymptotes.

4. Finding Breakaway Points:

In this case

$$
    n(s)&=(s+2)(s+3)=s^2+5s+6.\\
    d(s)&=s(s+1)=s^2+s.
$$

Differentiating we have

$$
    n'(s)=2s+5,\quad d'(s)=2s+1.
$$

Substituting in {eqref}`eq:breakinpoint` we have

$$
    d'(s)n(s)-n'(s)d(s)&=(2s+1)(s^2+5s+6)-(2s+5)(s^2+s)\\
    &=4s^2+12s+16.
$$

Comparing with zero and solving for $s$:

$$
s = -\frac{3}{2}\pm\frac{\sqrt{3}}{2}.
$$

These roots are real, but this is not enough for them to be valid breakaway points. They must also be on the root locus. Note that

$$
    -\frac{3}{2}+\frac{\sqrt{3}}{2}\approx-0.63,
$$

which is on the root locus. Moreover,

$$
    -\frac{3}{2}-\frac{\sqrt{3}}{2}\approx-2.36,
$$

which is also on the root locus. Since the root locus goes from the poles of the loop-gain to the zeros of the loop-gain, $-\frac{3}{2}+\frac{\sqrt{3}}{2}$ is the breakout point and $-\frac{3}{2}-\frac{\sqrt{3}}{2}$ is the break-in point. The corresponding gain values at these points can be obtained using {eqref}`eq:k_for_s`:

$$
k_{s_{in}}=\Bigg|\frac{s(s+1)}{(s+2)(s+3)}\Bigg|_{s=-\frac{3}{2}-\frac{\sqrt{3}}{2}}=13.93,\quad k_{s_{out}}= \Bigg|\frac{s(s+1)}{(s+2)(s+3)}\Bigg|_{s=-\frac{3}{2}+\frac{\sqrt{3}}{2}}=0.0718.
$$

```{figure} images/Rec5/r5_ex2.3.png
---
width: 70%
name: fig:closed_system_1
---

```

5. **Exit Angles from Complex Poles**:

There are no complex poles and zeros so there are no exit angles.

We are ready to draw the root locus diagram.

```{figure} images/Rec5/RL_Rec5_Ex2.png
---
width: 70%
name: fig:ex2rl
---
The Root Locus diagram of $G(s)=k\frac{(s+2)(s+3)}{s(s+1)}$.
```

The system is under-damped if $0<\zeta<1$. That is, if the pole of the closed-loop system has an imaginary component. A system is damped if $\zeta=0$. As $k$ increases from 0 to $0.0718$ the poles are on the real axis, so the system is damped for these values. For $0.0718<k<13.93$ the poles are complex so the system is under-damped. For $13.93\leq k <\infty$ the poles are again real so the system is damped.

### Exercise 3

Consider the loop-gain with:

$$
    C(s)=\frac{k}{(s-1)},\quad P(s)=\frac{1}{s^2+4s+7}.
$$

- Draw the Root Locus diagram of the open-loop system.

- Determine the values of $k$ for which the closed-loop system is stable.

### Solution

 
1. **Loop-Gain Poles**

The open-loop poles are:

$$
s = 1,\;-2\pm j\sqrt{3}.
$$

```{figure} images/Rec5/r5_ex3.1.png
---
width: 70%
name: fig:ex2rl
---

```

2. **Root Locus Branches on the Real Axis**:

From $s\rightarrow\infty$ to $s = 1$, there are no poles or zeros to the right.
From $s = 1$ to $s\rightarrow-\infty$, there is one pole, which is an odd number, so there is a Root Locus branch along this segment.

```{figure} images/Rec5/r5_ex3.2.png
---
width: 70%
name: fig:ex2rl
---

```

3. **Asymptotes**:

In this case $m=3$ and $n=0$ so there are $m-n=3$ asymptotes. The angles 

To compute the angles of the asymptotes, we use {eqref}`eq:asymptotoes`:

$$
    \theta_1&=\frac{180^\circ}{3-0}\cdot 1=\frac{180^\circ}{3}\cdot1=60^\circ,\\
    \theta_2&=\frac{180^\circ}{3-0}\cdot 3=\frac{180^\circ}{3}\cdot 3=180^\circ,\\
    \theta_3&=\frac{180^\circ}{3-0}\cdot 5=\frac{180^\circ}{3}\cdot 5=300^\circ=-60^\circ.
$$

The center point of the asymptotes on the real axis is:

$$
    \gamma=\frac{1-2-2}{3-0}=-1.
$$

```{figure} images/Rec5/r5_ex3.3.png
---
width: 70%
name: fig:ex2rl
---

```

4. **Exit Angles from Complex Poles**:

We compute the angle between $s=1$ and $s=-2+j\sqrt{3}$:

```{figure} images/Rec5/r5_ex3.4.png
---
width: 70%
name: fig:ex2323
---

```

From this figure, it is clear that

$$
    \varphi=\arctan\Big(\frac{\sqrt{3}}{3}\Big)=30^\circ.
$$

Then the angle between $s=-1$ and $s=-2+j\sqrt{3}$ is
 
$$
    180^\circ-\varphi=180^\circ-30^\circ=150^\circ.
$$

The angle between pole $p_2$ and pole $p_3$ is 90 degrees. The total sum must be 180 degrees, so:

$$
-90^\circ-150^\circ-\theta=-180^\circ\rightarrow\theta=-60^\circ.
$$

By symmetry, the exit angle from pole $s=-2-j\sqrt{3}$ is also 60 degrees. 

```{figure} images/Rec5/r5_ex3.5.png
---
width: 70%
name: fig:ex2rl
---

```

5. **Breakaway Points**:

In this case

$$
    n(s)=1,\quad d(s)=(s-1)(s^2+4s+7).
$$

Differentiating we have

$$
    n'(s)=0,\quad d'(s)=3s^2+6s+3.
$$

Substituting in {eq}`eq:breakinpoint`, we have

```{math}
d'(s)n(s) - n'(s)d(s) = 3s^2 + 6s + 3
```

Finding the roots we have

$$
    s_{1,2}=-1.    
$$

Thus, the breakaway occurs at $s = -1$.

6. **Imaginary Axis Intersection**

The characteristic equation of the closed-loop system is:

$$
d(s)+kn(s)=s^3+3s^2+3s-7+k.
$$

Setting $s = j\omega$ and comparing to zero we have:

$$
(j\omega)^3+3(j\omega)^2+3j\omega-7+k = 0.
$$

We re-write and obtain

$$
    k-7-3\omega^2+j\omega(3-\omega^2)=0.
$$

Equating the real and imaginary parts:

$$
    k-7-3\omega^2&=0,\\
    \omega(3-\omega^2)&=0.
$$

The solutions are the pairs:

$$
    (\omega,k)=(0,7),\quad (\omega,k)=(\pm \sqrt{3},16).
$$

We can now draw the root locus diagram.

```{figure} images/Rec5/r5_ex3.6.png
---
width: 70%
name: fig:ex3
---
Root Locus of $G(s)=k\frac{1}{(s-1)(s^2+4s+7)}$.
```

**Stability Analysis**:


From $k = 0$ to $k = 7$, the system is unstable since the poles are in the right half-plane.
From $k = 7$ to $k = 16$, the system is stable as all poles are in the left half-plane.
For $k > 16$, the system becomes unstable again as poles move back to the right half-plane.

Thus, stability is achieved for:

$$
7 < k < 16.
$$

### Exercise 4

Consider the closed-loop system with PD controller

$$
    C(s)=K_p(1+T_ds),
$$

and plant

$$
    P(s)=\frac{1}{10000(s^2-1.1772)}.
$$

- Using the Root Locus method, design the PD controller constants $K_p$ and $T_d$ such that the closed-loop damping ratio is $\zeta=0.7$ and the natural frequency is $\omega_n=0.5 \text{ rad/sec}$.

- Plot the Root Locus diagram for the $T_d$ you found, determine the values of $K_p$ for which the system is stable, and for which the system is under-damped.

### Solution

Note that since the system is a second order system, we want to design the controller such that the closed-loop system has a pair of complex poles:

$$
s = -\zeta \omega_n \pm j \omega_n \sqrt{1 - \zeta^2}=-0.35\pm j0.357.
$$

The loop-gain transfer function is:

$$
G(s) = \frac{K_pT_d(s+\frac{1}{T_d})}{10000(s^2-1.1772)}.
$$

where we have control over the location of the loop-gain zero, and there is an overall gain $K_p$ as required by the RL method. The loop-gain poles are:

$$
s_{1,2}=\pm\sqrt{1.1772}=\pm1.085.
$$

We mark the gain-loop poles with an 'X' and the gain-loop poles with circles. The goal is to design the controller such that $s=-0.35\pm j0.357$ lie on the root locus.

```{figure} images/Rec5/r5_ex4.1.png
---
width: 70%
name: fig:ex3
---

```

To ensure that these points are on the root locus, they must satisfy the angle condition. We will design the zero $\frac{1}{T_d}$ such that these points meet the angle condition. We find the angle between each pole and zero with respect to the desired pole location.

```{figure} images/Rec5/r5_ex4.2.png
---
width: 70%
name: fig:ex3
---

```

It is clear from the figure that

$$
    \theta'=\arctan\Big(\frac{0.357}{1.435}\Big)=13.9^\circ,\quad\theta_2=\arctan\Big(\frac{0.357}{0.735}\Big)=25.9^\circ.
$$

This implies that

$$
    \theta_1=180^\circ-\theta'=166.03^\circ.
$$

The phase condition is

$$
    \theta_1+\theta_2-\phi_1=166.03^\circ+25.9^\circ-\phi_1=180^\circ.
$$

From this we obtain that

$$
    \phi_1=11.93^\circ.
$$

Clearly, this angle depends on $T_d$. We have

$$
    \tan(11.93)=\frac{0.357}{\frac{1}{T_d}-0.357}=0.211.
$$

From here we obtain that

$$
    \boxed{T_d=0.49}
$$

For this $T_d$, $s=-0.35\pm j0.357$ is part of the root locus. We need to find the value of $K_p$ for which these values are obtained as the closed-loop poles.

For any point $s_0$ on the root locus, the magnitude condition holds:

$$
|G(s_0)| = 1.
$$

In our case, after substituting $T_d=0.49$ and $s=-0.35+j0.357$ we have

```{math}
:label: eq:ex4_amp_cond
    \frac{0.49K_p}{10^4}\Bigg|\frac{-0.35+j0.357+2.039}{\big(-0.35+j0.357)^2-1.1772\big)}\Bigg|=1.
```

For the magnitude we have

$$
    \Bigg|\frac{-0.35+j0.357+2.039}{\big(-0.35+j0.357)^2-1.1772\big)}\Bigg|&=\sqrt{\frac{(1.689)^2+(0.357)^2}{(1.182)^2+(0.499)^2}}\\
    &=\sqrt{\frac{2.98}{1.646}}\\
    &=\sqrt{1.81}\\
    &=1.34.
$$

Substituting back in {eq}`eq:ex4_amp_cond` we have

$$
    \frac{0.49\cdot K_p\cdot1.34}{10^4}=1\rightarrow\boxed{K_p=14273}
$$

To conclude, if $T_d=0.49$ and $K_p=14273$, the poles of the closed-loop system are $s=-0.35\pm j0.357$.

**Plotting the Root Locus Diagram**:
 
We take $T_d=0.49$. We root the root locus of the gain-loop:


$$
G(s) = K_p\frac{0.49(s+2.04)}{10000(s^2-1.1772)}.
$$



1. **Drawing Poles and Zeros of the Loop-Gain**:


The poles of the system are:

$$
s_{1,2} = \pm 1.08.
$$

The zero of the system is:

$$
s = -2.04.
$$

```{figure} images/Rec5/r5_ex4.3.png
---
width: 70%
name: fig:ex3
---

```

2. **Determining the RL along the Real Axis**:

Using the root locus rule, if to the right of a given point there is an odd number of poles and zeros, the root locus exists at that segment.

For our system:

- From $-\infty$ to $-2.04$: Odd number ($3$) of poles/zeros to the right $\rightarrow$ root locus exists.
- From $-2.04$ to $-1.085$: Even number ($2$) of poles/zeros to the right $\rightarrow$ root locus does not exists.
- From $-1.085$ to $1.085$: Odd number ($1$) of poles/zeros to the right $\rightarrow$ root locus exists.
- From $1.085$ to $+\infty$: even number ($0$) of poles/zeros to the right $\rightarrow$ RL does not exists.

```{figure} images/Rec5/r5_ex4.4.png
---
width: 70%
name: fig:ex3
---

```

3. **Asymptotes Calculation**:

In this case $m=2$ and $n=1$, so we will have $m-n=1$ asymptotes. The single asymptote is at $-180^\circ$ as we already calculated. Since it is the only asymptote it is not critical to calculate its midpoint.


4. **Breakaway Points**:


In our case we have

$$
    n(s)=0.49s+0.99,\quad d(s)=10000s^2-11772.
$$

Differentiating we have

$$
    n'(s)=0.49,\quad d'(s)=20000s.
$$

Substituting in \eqref{eq:breakinpoint} we have

$$
    d'(s)n(s)-n'(s)d(s)&=20000s\cdot(0.49s+0.99)-0.49\cdot(10000s^2-11772)\\
    &=4900s^2+19800s+5768.28.
$$

Comparing with zero and solving for $s$:

$$
s_{1,2}\approx-3.42,\;-0.31.
$$

These roots are real and they are on the root locus so they are valid break-away and break-in points:

```{figure} images/Rec5/r5_ex4.5.png
---
width: 70%
name: fig:ex3
---

```


5. **Exit Angles from Complex Poles**:

Since there are no complex poles, there are no exit angles.

6. **Intersection with the Imaginary Axis**:

The denominator of the closed-loop transfer function is

$$
    p(s)=d(s)+kn(s).
$$

In this case

$$
    p(s)=10000s^2-11772+k(0.49s+0.99).
$$

Substituting $s=j\omega$ we have

$$
    p(j\omega)&=10000(j\omega)^2-11772+K_p(0.49j\omega+0.99)\\
     &=0.99K_p-11772-10000\omega^2+j0.49k\omega.
$$

We compare the real and imaginary part with zero and obtain

$$
    0.99K_p-11772-10000\omega^2=0,\\
    j0.49K_p\omega=0.
$$

For $\omega=0$ (which corresponds to the origin) we obtain

$$
    0.99K_p-11772=0\rightarrow K_p=11891.
$$

This is the only intersection with the imaginary axis. 

We are ready to draw the root locus.

```{figure} images/Rec5/r5_ex4.6.png
---
width: 70%
name: fig:ex4
---

```

**Stability Condition**:
The system is stable for any $K_p$ such that all the poles have a negative real part. For $K_p=0$ the system is not stable since we obtain all poles of the loop-gain. As we increase $K_p$, we go along the loci of the root locus, from the poles to the zero and the asymptote. We know that for $K_p=11891$ the root locus crosses from the positive real part to the negative real part (crosses the imaginary axis). It is clear from Figure {ref}`fig:ex4` that we stay in the left hand plane. So the system is stable for $K_p>11891$.

The system is damped if all the poles are real. The system is under-damped if some poles have an imaginary part. We need to find the values of $K_p$ for which we have breakaway points. We know that the poles which correspond to the breakaway points are $s\approx-3.42,\;-0.31$. Substituting in \eqref{eq:k_for_s} for $s=-3.42$ we have:

$$
    K_p=\Bigg|\frac{10000\big((-3.42)^2-1.1772\big)}{0.49(-3.42+2.04)}\Bigg|\approx155563.
$$

For $s=-0.31$ we have

$$
    K_p=\Bigg|\frac{10000\big((-0.31)^2-1.1772\big)}{0.49(-3.42+2.04)}\Bigg|\approx15988.
$$

The break-out point is at $s=-0.31$, it is obtained for $K_p=15988$. The break-in point is $s=-3.42$ and is obtained for $K_p=155563$. The system is under-damped for

$$
    15988<K_p<155563,
$$

since in this region the closed-loop transfer function will have complex poles.

