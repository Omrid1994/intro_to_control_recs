---
title: Introduction to Control -- Recitation 7
---

# Introduction to Control -- Recitation 7

## Gain and Phase Margins

Recall that the denominator of the closed-loop transfer function is:

$$
    1 + G(j\omega).
$$

The system will be unstable if there exists a value of $\omega$ such that $1+G(j\omega) = 0$. Therefore, the system is unstable for values $\omega$ where:

$$
G(j\omega) = -1.
$$

Since we are dealing with complex numbers, this means that both the magnitude and phase of $G(j\omega)$ must satisfy:

$$
|G(j\omega)| = 1, \quad \angle G(j\omega) = -180^\circ.
$$

If there exists a frequency $\omega$ where the system has this gain and phase, the system will be unstable at that frequency. How does this manifest in the Bode diagram?

```{pr:remark}
The magnitude plot of the Bode diagram is in $dB$. We know that

$$
    \text{gain} \;[dB]=20\log_{10}\big(\text{gain}\;[linear]\big).
$$

So $|G(j\omega)|=1$ in dB is:

$$
    20\log_{10}(1)=0.
$$

When we cross the value $0$ in the magnitude plot of the Bode diagram, the gain is $1$. 
```

## Definitions

````{prf:definition}
The **gain crossover frequency** is a number $\omega_g>0$ such that

```{math}
:label: eq:gain_crossover
        |G(j\omega_g)|=1.
```

Or equivocally, a number $\omega_g>0$ such that

$$
    |G(j\omega_g)|=0\;dB.
$$
````

````{prf:definition}
If $\omega_g$ is unique, then the **phase margin** is
 
```{math}
:label: eq:phase_margin
    \varphi_m=\arg\big(G(j\omega_g)\big)-(-180^\circ).
```
````

```{prf:remark}
The phase margin is the distance in the phase plot of the Bode diagram, between the phase at $\omega_g$ and the phase $-180^\circ$.
```

````{prf:definition}
The **phase crossover frequency** is a number $\omega_c>0$ such that

```{math}
:label: eq:phase_crossover
        \angle G(j\omega_c)=-180^\circ.
```
````

````{prf:definition}
If $\omega_c$ is unique, then the **gain margin** (in dB) is 

```{math}
:label: eq:gain_margin
    \text{GM}_{dB}=-20\log_{10}\big(|G(j\omega_c)|\big).
```
````

```{prf:remark}
The gain margin is the distance in the magnitude plot of the Bode diagram, between the gain $0$ and the gain at $\omega_c$.
```

Essentially, the gain margin tells us how much gain variation is allowed before instability occurs at the phase crossover frequency, and the phase margin tells us how much phase variation is allowed before instability occurs at the gain crossover frequency.

```{figure} images/Rec7/gain_phase_margin.svg
---
width: 80%
name: fig:r6_ex3
---

```

**Solution Steps**

1. Compute the magnitude function and phase function of $G(j\omega)$, $|G(j\omega)|$, $\angle G(j\omega)$.
2. Find the gain crossover frequency using {eq}`eq:gain_crossover`.
3. Find phase margin using {eq}`eq:phase_margin`.
4. Find phase crossover frequency using {eq}`eq:phase_crossover`.
5. Find gain margin using {eq}`eq:gain_margin`.



### Exercise

Given the controller:

$$
C(s) = 40,
$$

and the plant

$$
    P(s)=\frac{1}{s(s+3)(s+1)}.
$$

Find the gain and phase margins of the closed-loop system.

### Solution

we need to determine the phase and gain margins of the system.

1. **Finding the Magnitude and Argument**:

In our case

$$
    G(j\omega)=C(j\omega)P(j\omega)=\frac{40}{j\omega(j\omega+3)(j\omega+1)}.
$$

We start by deriving the expressions for the magnitude and phase:

$$
	|G(j\omega)| = \frac{40}{\omega\sqrt{(\omega^2+9)(\omega^2+1)}}.
$$

$$
    \angle G(j\omega)=-90^\circ-\tan^{-1}\big(\frac{\omega}{3}\big)-\tan^{-1}(\omega).
$$

2. **Finding the Gain Crossover Frequency**:

The gain crossover frequency $\omega_{g}$ is the frequency for which:

$$
|G(j\omega_{g})| = 1\rightarrow \frac{40}{\omega\sqrt{(\omega^2+9)(\omega^2+1)}}=1.
$$

We find the values of $\omega$ for which:

$$
    40=\omega\sqrt{(\omega^2+9)(\omega^2+1)}.
$$

Squaring both sides:

$$
40^2=\omega^2(\omega^2+9)(\omega^2+1).
$$

Defining a new variable $t=\omega^2$ we have:

$$
40^2=t(t+9)(t+1)\rightarrow t^3+10t^2+9t-40^2=0.
$$

Solving we have

$$
t_1=8.95,\quad t_{2,3}=-9.47\pm j9.4.
$$

There is no such thing as a complex frequency so only $t_1=8.95$ is relevant.

Thus:

$$
\omega_{g} = \sqrt{8.95}\approx3.
$$

3. **Computing the Phase Margin**:

Substituting $\omega_{g}$ into the phase expression:

$$
\angle G(j\omega_g)=-90^\circ-\tan^{-1}(1)-\tan^{-1}(3)=-206.5^\circ.
$$

The phase margin is then (using {eq}`eq:phase_margin`):

$$
\varphi_m = 180^\circ -|-206.5^\circ|=-27^\circ.
$$

3. **Finding the Phase Crossover Frequency**:

We extract the real and imaginary parts of $G(j\omega)$:

$$
    G(j\omega)&=\frac{40}{j\omega(j\omega+3)(j\omega+1)}\\
              &=\frac{40}{-4\omega^2-j\omega^3+3j\omega}\\
              &=\frac{40}{-4\omega^2-j\omega^3+3j\omega}\cdot\frac{-j\omega(3-\omega^2)-4\omega^2}{-j\omega(3-\omega^2)-4\omega^2}\\
              &=\frac{-160\omega^2-j40(3-\omega^2)}{\omega\big(j(3-\omega^2-4\omega^2)\big(-j(3-\omega^24\omega^2)\big)\big)}.
$$

We can stop here since we only care about the numerator. The phase crossover frequency is the frequency that will nullify the imaginary part of $G(j\omega)$ since it corresponds to the real axis. We have

$$
    40(3-\omega^2)=0\rightarrow \omega_c=\sqrt{3}.
$$


We verify that indeed $\angle G(j\sqrt{3})=-180^\circ$:

$$
\angle G(j\sqrt{3})=-90^\circ-\tan^{-1}\big(\frac{\sqrt{3}}{3}\big)-\tan^{-1}\big(\sqrt{3}\big)=-180^\circ.
$$

4. **Computing the Gain Margin**:

Using {eq}`eq:gain_margin` we have

$$
    GM_{dB}&=-20\log_{10}\big(|G(j\omega_c)|\big)\\
    &=-20\log_{10}\Big(\Big|\frac{40}{\sqrt{3}j\cdot(\sqrt{3}j+3)(\sqrt{3}j+1)}\Big|\Big)\\
    &=-20\log_{10}\Big(\frac{40}{\sqrt{3}\sqrt{(\sqrt{3}^2+9)(\sqrt{3}^2+1)}}\Big)
    \approx-10.5\;\text{dB}.
$$

```{figure} images/Rec7/r7_ex1_bodeplot.png
---
width: 85%
name: fig:r6_ex3
---

```


## Phase Lead Controller

The phase lead controller is a controller of the form

```{math}
:label: eq:lead_compensator
    C(s)=\frac{1+\tau s}{1+\alpha\tau s},\quad 0<\alpha<1,\;\tau>0.
```

```{figure} images/Rec7/lead_compensator.png
---
width: 85%
name: fig:r6_ex3
---
Bode plot of {eq}`eq:lead_compensator`.
```

There is no additional gain for low frequencies. The controller contributes phase which will increase the phase margin.

The maximum phase in $C$ is obtained for 

```{math}
:label: eq:omega_m
    \boxed{\omega_m=\frac{1}{\sqrt{\alpha}\tau}}
```

The maximal phase value, $\phi_m$ is given by

```{math}
:label: eq:phi_m
    \boxed{\sin(\phi_m)=\frac{1-\alpha}{1+\alpha}}
```

The magnitude at $\omega_m$ is

$$
    |C(j\omega_m)|_{dB}=20\log_{10}(\frac{1}{\sqrt{\alpha}})\iff |C(j\omega_m)|=\frac{1}{\sqrt{\alpha}}.
$$

Designing a lead controller:


1. Draw the Bode plot of $P(j\omega)$.
2. Find the gain and phase margins.
3. $\phi_m=PM_{requirement}-PM_{of\;P}$.
4. $\phi_m$ gives the value for $\alpha$ using {eq}`eq:phi_m`.
5. Find $\omega_m$ using:

```{math}
:label: eq:find_omega_m
        |P(j\omega_m)|_{dB}=20\log_{10}(\sqrt{\alpha})\iff|P(j\omega_m)|=\sqrt{\alpha}.
```	

6. Obtain $\tau$ from {eq}`eq:omega_m`.


### Exercise


Consider the plant

```{math}
:label: eq:P
    P(s)=\frac{0.09}{s^2+0.15s+0.09}.
```

1. Find the phase and gain margins of $P$.
2. Design a lead controller such that the phase margin is $60^\circ$.


### Solution

The Bode plot of $P$ is:

```{figure} images/Rec7/Bode_exercise_2.png
---
width: 85%
name: fig:r6_ex3
---

```

1. We find the magnitude function of $P$:

$$
    P(j\omega)=\frac{0.09}{0.09-\omega^2+j0.15\omega}.
$$

The magnitude is

$$
    |P(j\omega)|=\frac{0.09}{\sqrt{(0.09-\omega^2)^2+(0.15\omega)^2}}.
$$

We find the gain crossover frequency, $\omega_g$:

$$
    |P(j\omega_g)|=\frac{0.09}{\sqrt{(0.09-\omega_g^2)^2+(0.15\omega_g)^2}}=1.
$$

We have

$$
    8\cdot10^{-1}=(0.09-\omega_g^2)^2+(0.15\omega_g)^2.
$$

From which we obtain

$$
    \omega_g\approx0.396.
$$

We cannot find an explicit expression for the phase of $P$, so we write:

$$
    P(j\omega)&=\frac{0.09}{0.09-\omega^2+j0.15\omega}\cdot\frac{0.09-\omega^2-j0.15\omega}{0.09-\omega^2-j0.15\omega}\\
    &=\frac{0.09(0.09-\omega^2)}{(0.09-\omega^2)^2+(0.15\omega)^2}-j\frac{0.0135\omega}{(0.09-\omega^2)^2+(0.15\omega)^2}.
$$

```{prf:remark}
Note that for any $\omega>0$, $P(j\omega)\in\mathbb{C}$, that is, $P(j\omega)=a_\omega+jb_\omega$ for some $a_\omega,\;b_\omega\in\mathbb{R}$. The phase is $\angle P(j\omega)=tan^{-1}\big(\frac{b_\omega}{a_\omega}\big)$ adding $\pm180$ if needed. The magnitude is $|P(j\omega)|=\sqrt{a_\omega^2+b_\omega^2}$.
```

We have

$$
    P(j\omega_g=0.396)&=\frac{0.09(0.09-0.396^2)}{(0.09-0.396^2)^2+(0.15\cdot0.396)^2}-j\frac{0.0135\cdot0.396}{(0.09-0.396^2)^2+(0.15\cdot0.396)^2}&\\&=-0.75-j0.66.
$$

Since $-0.75-j0.66$ is in the third quadrant, we deduct $-180^\circ$ from the phase:

$$
    \angle P(j\omega_g=0.396)=-180^\circ+\tan^{-1}\big(\frac{0.66}{0.75}\big)=-180^\circ+41.34^\circ=-138.65^\circ.
$$

To reach $-138.65^\circ$ from $-180^\circ$ we need an **increase** in phase of $41.34^\circ$, thus

$$
    PM_{\text{of }P}=41.34^\circ.
$$

It is clear from the Bode plot of $P$ that we never reach $-180^\circ$, this implies that $\omega_c\rightarrow\infty$, and the gain margin is infinite,

$$
    GM_{dB}=\infty.
$$

2. We design a controller of the form:

$$
    C(s)=\frac{1+\tau s}{1+\alpha\tau s},\quad 0<\alpha<1,\;\tau>0.
$$

The additional phase we need is:

$$
    \phi_m&=PM_{requirement}-PM_{of\;P}\\
    &=60^\circ-41.34^\circ\\
    &=18.66^\circ.
$$

```{prf:remark}
Sometimes, we take margin of safety, adding $10-15\%$ to the required increase in phase. For example, we would sometimes take $\phi_m=18.66\cdot1.1^\circ$.
```

From {eq}`eq:phi_m` we have

$$
    \sin(\phi_m)&=\sin(18.66)\\
                &=0.868\\
                &=\frac{1-\alpha}{1+\alpha}.
$$

We have

$$
    0.868(1+\alpha)=1-\alpha\rightarrow \alpha=0.07.
$$

Note that in fact $0<\alpha<1$. Next, we find $\omega_m$ using {eq}`eq:find_omega_m`. We have

$$
    |P(j\omega_m)|=\frac{0.09}{\sqrt{(0.09-\omega_m^2)^2+(0.15\omega_m)^2}}=\sqrt{\alpha}\approx0.26.
$$

Solving for $\omega_m$ we have:

$$
    \omega_m\approx0.5.
$$

:::{admonition} Click here for the derivation
:class: seealso, dropdown

Raising to the power of two we have

$$
    \frac{(0.09)^2}{(0.09-\omega_m^2)^2+(0.15\omega_m)^2}=(0.26)^2\rightarrow(0.09)^2=(0.26)^2\big((0.09-\omega_m^2)^2+(0.15\omega_m)^2\big).
$$

Denote $t=\omega^2$. Then we have

$$
    (0.09)^2=(0.26)^2\big((0.09-t)^2+(0.15)^2t\big)\rightarrow t^2-0.1575t-0.1117=0.
$$

The roots are:

$$
    t_1=0.422151,\quad t_2=-0.4194.
$$

We only consider real positive $t$. Then

$$
    \omega_m^2=t=0.422151\rightarrow \omega_m=\sqrt{0.422151}\approx0.65.
$$
:::

Finally, from {eq}`eq:omega_m` we have

$$
    0.65=\frac{1}{0.26\cdot\tau}\rightarrow\tau\approx6.
$$

Note that in fact $\tau>1$. We obtained:

$$
    C(s)=\frac{1+6s}{1+0.42s}.
$$

The Bode plot of $C$ is:


```{figure} images/Rec7/lead_compensator_q2.png
---
width: 85%
name: fig:r6_ex3
---
Bode plot of {eq}`eq:lead_compensator`.
```

The Bode plot of $PC$ is:

```{figure} images/Rec7/P_with_PC.png
---
width: 85%
name: fig:r6_ex3
---

```

## Drawing Nyquist from a Bode Plot

For any $\omega>0$, $G(j\omega)\in\mathbb{C}$. That is, for any $\omega>0$, $G(j\omega)=a_\omega+jb_\omega$, where $a_\omega,\;b_\omega\in\mathbb{R}$. The Nyquist plot is a literal plot of $G(j\omega)$ for any $\omega\in[0,\infty)$  on the complex plane, and then reflecting to account for $\omega\in(-\infty,0]$. Any complex number $a_\omega+jb_\omega$ can be written in terms of magnitude (distance from origin) and phase (angle with respect to the positive real axis), $a_\omega+jb_\omega=r_\omega e^{j\theta_\omega}$. The Bode plot depicts these magnitudes and phases for any $\omega$ (on a logarithmic scale). 

This implies that the Nyquist plot and the Bode plot are two representations of the same thing - all complex numbers produces by $G(j\omega)$. 

First note that for any $\omega>0$

$$
    |G(j\omega)|_{dB}=20\log_{10}(|G(j\omega)|_{linear})\rightarrow |G(j\omega)|_{linear}=10^{\frac{|G(j\omega)|_{dB}}{20}}.
$$

From the Bode plot, we obtain gain and phase values for $\omega=0,\;\omega\rightarrow\infty$, the intersections with the real axis (values where the phase plot crosses $0^\circ$ and $-180^\circ$, intersections with the imaginary axis (values where the phase plot crosses $90^\circ$, $270^\circ$). The trend of the phase plot implies the trend of the Nyquist curve.

### Exercise

Consider

$$
    G(s)=\frac{(s+1)(s+5)}{(s^2-2)(s^2+s+1)}.
$$

The magnitude Bode plot of $G$ is:

```{figure} images/Rec7/Bode_For_Recitation_2.png
---
width: 85%
name: fig:r6_ex3
---

```

The phase Bode plot of $G$ is:

```{figure} images/Rec7/Bode_For_Recitation.png
---
width: 85%
name: fig:r6_ex3
---

```

By observing the phase plot, it is clear that we do not intersect the imaginary axis, since the phase plot does not intersect $-90^\circ,\;-270^\circ$. It is also clear that we intersect the negative real axis three times, once for $\omega=0$, once for $\omega\rightarrow\infty$, and one other time, at $\omega_c$.

It is clear from the Bode plot that

$$
    |G(j\cdot0)|_{dB}=7.5 [dB]\rightarrow |G(j\cdot0)|=10^{\frac{7.5}{20}}=2.371.
$$

At $\omega\rightarrow\infty$,

$$
    |G(j\omega\rightarrow\infty)|_{dB}\rightarrow-\infty.
$$

This corresponds to

$$
    |G(j\omega\rightarrow\infty)|=0,
$$

since $20\log_{10}(0)=-\infty$. We are also given

$$
    |G(j\omega_c)|_{dB}=9.31[dB]\rightarrow |G(j\omega_c)|=10^{\frac{9.31}{20}}=2.921.
$$

To summarize

$$
    |G(j0)|=2.371,&\quad\angle G(j0)=-180^\circ,\\
    |G(j\omega_c)|=2.921,&\quad \angle G(j\omega_c)=-180^\circ,\\
    |G(j\omega\rightarrow\infty)|=0,&\quad \angle G(j\omega\rightarrow\infty)=-180^\circ.
$$

We also know that we do not intersect the imaginary axis. It is clear from the phase plot that for small values of $\omega$, the phase increases as we increase $\omega$, this implies that the Nyquist plot initially trends "downwards" that is, counter-clockwise. This defines the trend of the entire Nyquist curve. 

We are ready to draw the Nyquist plot of $G$:

```{figure} images/Rec7/Nyquist_For_Rec.png
---
width: 85%
name: fig:r6_ex3
---

```


We zoom in on the origin:

```{figure} images/Rec7/Nyquist_For_Rec_2.png
---
width: 85%
name: fig:r6_ex3
---

```















































