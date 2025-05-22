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
If $\omega_g$ is unique, then the \textbf{phase margin} is
 
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

```{figure} images/Rec7/gain_phase_margin_fixed.png
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

















































