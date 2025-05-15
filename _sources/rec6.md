---
title: Introduction to Control -- Recitation 6
---

# Introduction to Control -- Recitation 6

## Nyquist Plot

The denominator of a closed-loop system is of the form:

$$
1 + G(s).
$$

The idea behind the Nyquist plot is to study this expression as a function of frequency $\omega$ to determine at whether the system is unstable.

## Reminder – Cauchy’s Principle

If we map a contour $\Gamma_s$ in the $s$-plane to the $\omega$-plane, we obtain a contour $\Gamma_\omega$ that encircles the origin $N$ times in the counter-clockwise direction, then:

$$
N = P-Z.
$$

Where $P$ is the number of poles of $G(s)$ enclosed by $\Gamma_s$ in the original plane, and $Z$ is the number of zeros of $G(s)$ enclosed by $\Gamma_s$. Essentially, there are $N$ more zeros than poles.

### Example

For a given transfer function:

$$
G(s) = \frac{(s-1)(s-2)}{s-3}.
$$

There are two zeros in the right half-plane, $s=1,2$ and one pole in the right half-plane, $s=3$, so:

```{figure} images/Rec6/rec61.png
---
width: 70%
name: fig:ex4
---
Contour $\Gamma_s$ in the $s$-plane and $\Gamma_\omega$ in the $\omega$-plane.
```

$$
N = 2 - 1 = 1.
$$

This means there is one encirclement of the origin. The number of encirclements around the origin indicates how many more zeros exist than poles. However, we prefer to have no zeros at all (since a zero in $1+G(s)$ corresponds to a pole in the closed-loop system). Hence, we want to know the number of poles in advance.

To determine if there are zeros in the right half-plane of $1 + G(s) $, we choose a contour $\Gamma_s$ that encloses the entire right half-plane. This means it extends from $-j\infty$ to $+j\infty$, encloses the right half-plane, and returns to the origin.

The Nyquist plot is the contour in the $\omega$-plane, $\Gamma_\omega$ corresponding to the contour $\Gamma_s$ in the $s$-plane that encloses the right half-plane.

Instead of plotting $1+G(s)$, we directly plot the Nyquist plot of $G(s)$ and analyze encirclements around $-1$. By symmetry, we can calculate only the upper half-plane and mirror it downwards.

## Magnitude Function of a Transfer Function

Consider the transfer function:

$$
    H(j\omega)=\frac{j\omega(j\omega+a)(j\omega-d)}{(j\omega+b)(j\omega-c)j\omega},\quad a,b,c,d>0.
$$

Then the magnitude function of $H(j\omega)$ is:

$$
    \big|H(j\omega)\big|=\frac{\omega\sqrt{\omega^2+a^2}\sqrt{\omega^2+d^2}}{\omega\sqrt{\omega^2+b^2}\sqrt{\omega^2+c^2}}.
$$

```{prf:remark}
If we write

$$
     H(j\omega)=\frac{a+jb}{c+jd},\quad a,b,c,d\in\mathbb{R},
$$
	
then
	
$$
    \big|H(j\omega)\big|=\frac{\sqrt{a^2+b^2}}{\sqrt{c^2+d^2}}.
$$
	
```
## Phase Function of a Transform Function

Consider the transfer function:

$$
    H(j\omega)=\frac{j\omega(j\omega+a)(j\omega-d)}{(j\omega+b)(j\omega-c)j\omega},\quad a,b,c,d>0.
$$

Elements in the numerator will contribute $\tan^{-1}(\cdot)$, elements in the denominator will contribute $-\tan^{-1}(\cdot)$, a zero [pole] will contribute $90^\circ$ [$-90^\circ$].

```{prf:remark}
Since $-90^\circ\leq\tan^{-1}(x)\leq90^\circ$, if a complex number is in the left-hand plane, we will add $180^\circ$. In our case, since $\omega>0$ if we have a right-handed pole/zero we will add $180^\circ$.
```

We obtain

$$
    \angle H(j\omega)=90^\circ+\tan^{-1}\big(\frac{\omega}{a}\big)+\tan^{-1}\big(\frac{\omega}{-d}\big)+180^\circ-\tan^{-1}\big(\frac{\omega}{b}\big)-\tan^{-1}\big(\frac{\omega}{-c}\big)-180^\circ-90^\circ.
$$

We also remind that

$$
    \lim_{\theta\rightarrow\infty}\tan^{-1}(\theta)=90^\circ,\;\lim_{\theta\rightarrow-\theta}\tan^{-1}(\theta)=-90^\circ,\;\lim_{\theta\rightarrow0}\tan^{-1}(\theta)=0.
$$

We also note that for $|\theta|\ll1$, then $\tan^{-1}(\theta)\approx\theta$. Finally we give the following formula which we will use later on:

```{math}
:label: eq:arctan_formula
    \tan^{-1}(\alpha)\pm\tan^{-1}(\beta)=\tan^{-1}\Big(\frac{\alpha\pm\beta}{1\mp \alpha\beta}\Big).
```


## Nyquist Plot Drawing Rules


1. Substitute $s=j\omega$ in $G(s)$.
2. Compute $\big|G(j\omega)\big|$ and $\angle G(j\omega)$.
3. Evaluate $\big|G(j\omega)\big|$ and $\angle G(j\omega)$ at $\omega\rightarrow0$ and $\omega\rightarrow\infty$.
4. Evaluate the trend of the curve.
5. Find intersections with the real and imaginary axis. 
6. Draw the curve for $\omega\in[0,\infty)$. 
7. Reflect with respect to the real axis.


```{prf:remark}
Note that the Nyquist plot is the plot of the complex function $G(j\omega):\mathbb{R}\rightarrow\mathbb{C}$ for all values of $\omega\in\mathbb{R}$.
```

```{prf:remark}
The intersection with the real axis can be obtained by finding the values of $\omega\geq0$ such that

$$
    \text{Img}\big(G(j\omega)\big)=0.
$$

After finding the relevant values of $\omega$, we substitute into $\big|G(j\omega)\big|$ and $\angle G(j\omega)$ to find the exact location of the intersection on the real axis. Alternatively, we can find the values of $\omega$ using

$$
    \angle G(j\omega)=\pm180^\circ,0,360^\circ.
$$

```

```{prf:remark}
The intersection with the imaginary axis can be obtained by finding the values of $\omega\geq0$ such that

$$
    \text{Re}\big(G(j\omega)\big)=0.
$$

After finding the relevant values of $\omega$, we substitute into $\big|G(j\omega)\big|$ and $\angle G(j\omega)$ to find the exact location of the intersection on the imaginary axis. Alternatively, we can find the values of $\omega$ using

$$
    \angle G(j\omega)=\pm90^\circ,\pm270^\circ.
$$

```

```{prf:remark}
We can find the trend of the curve in many ways. First note that the Nyquist plot is one uniform continuous curve, so if we find the trend of the curve in one place, we know the trend of the plot throughout. One way is to examine the phase for $\omega\ll1$. If the phase increases, the curve goes counter-clockwise, if the phase decreases, the curve goes clockwise. If we have the Bode plot of $G(j\omega)$ we can examine it and see if the phase increases or decreases around $\omega=0$.
```

## Stability Condition


- $P$ is the number of right-handed poles of $G(s)$.
- $N$ is the number of \underline{counter-clockwise} encirclements around $-1$.
- $Z$ is the number of unstable poles of the closed-loop transfer function.


We want to have $Z=0$, when the following always holds:

$$
    N=P-Z.
$$

```{prf:remark}
Note that a clockwise encirclement around $-1$ counts as a negative value for $N$. That is, if we have two clockwise encirclements around $-1$, then $N=-2$.
```

### Exercise 1

Consider the unit feedback system with

$$
C(s)=1,\quad P(s)=\frac{150}{(s+2)(s+5)(s+10)}.
$$

Determine, using the Nyquist stability criterion, whether the closed-loop system is stable.

### Solution

In this case

$$
    G(s)=C(s)P(s)=\frac{150}{(s+2)(s+5)(s+10)}.
$$


1. **Substitute $s=j\omega$**:
   
Substituting $s=j\omega$ we have

$$
    G(j\omega)=\frac{150}{(j\omega+2)(j\omega+5)(j\omega+10)}.
$$

2. **Compute the Argument and Magnitude of $G(j\omega)$**:

In this case we have

$$
    \big|G(j\omega)\big|=\frac{150}{\sqrt{\omega^2+4}\sqrt{\omega^2+25}\sqrt{\omega^2+100}}.
$$

Moreover,

$$
    \angle G(j\omega)=-\tan^{-1}\big(\frac{\omega}{2}\big)-\tan^{-1}\big(\frac{\omega}{5}\big)-\tan^{-1}\big(\frac{\omega}{10}\big).
$$

3. **Limits of Phase and Magnitude**:

By substitution:

$$
    \big|G(j\cdot0)\big|=\frac{150}{\sqrt{4}\sqrt{25}\sqrt{100}}=\frac{150}{2\cdot5\cdot10}=1.5.
$$

$$
    \angle G(j\cdot0)=-\tan^{-1}(0)-\tan^{-1}(0)-\tan^{-1}(0)=0^\circ.
$$

This implies that for $\omega=0$ we have the real number $1.5$. Continuing:

$$
    \big|G(j\omega\rightarrow\infty)\big|=\frac{150}{"\infty"}=0.
$$

$$
    \angle G(j\omega\rightarrow\infty)=-90^\circ-90^\circ-90^\circ=-270^\circ.
$$

This implies that for $\omega\rightarrow\infty$ we converge to the origin, from above. 

4. **Trend of the Nyquist Curve**:

It is evident that the  phase decrease as $\omega$ increases. Thus, we start at $|G(j0)|$ with zero phase and end at $|G(j\infty)|$ with phase $-180^\circ$. Since the phase decreases, the trend will be clockwise.

5. **Intersection with the Real Axis**:

We compare the argument of $G(j\omega)$ to $-180^\circ$ to find the values of $\omega$ for which we cross the real axis:

```{math}
:label: eq:phase_real
    -\Big(\tan^{-1}\big(\frac{\omega}{2}\big)+\tan^{-1}\big(\frac{\omega}{5}\big)+\tan^{-1}\big(\frac{\omega}{10}\big)\Big)=-180^\circ.
```

We use {eq}`eq:arctan_formula` twice to unify the left hand term into one single $tan^{-1}$:

:::{admonition} Click here for the derivation of the table elements
:class: seealso, dropdown
$$
    \tan^{-1}\big(\frac{\omega}{2}\big)+\tan^{-1}\big(\frac{\omega}{5}\big)=tan^{-1}\Big(\frac{7\omega}{10-\omega^2}\Big).
$$

Derivation:

$$
    \tan^{-1}\big(\frac{\omega}{2}\big)+\tan^{-1}\big(\frac{\omega}{5}\big)=\tan^{-1}\Big(\frac{\frac{\omega}{2}+\frac{\omega}{5}}{1-\frac{\omega}{2}\frac{\omega}{5}}\Big).
$$

Simplifying the expression in the brackets we have:

$$
    \frac{\frac{\omega}{2}+\frac{\omega}{5}}{1-\frac{\omega}{2}\frac{\omega}{5}}=\frac{\frac{5\omega+2\omega}{10}}{\frac{10-\omega^2}{10}}=\frac{7\omega}{10-\omega^2}.
$$

Finally we have

$$
    tan^{-1}\Big(\frac{7\omega}{10-\omega^2}\Big)+\tan^{-1}\big(\frac{\omega}{10}\big)=\tan^{-1}\Big(\frac{\omega(80-\omega^2)}{100-17\omega^2}\Big).
$$

Derivation:

$$
    tan^{-1}\Big(\frac{7\omega}{10-\omega^2}\Big)+\tan^{-1}\big(\frac{\omega}{10}\big)=\tan^{-1}\Big(\frac{\omega(80-\omega^2)}{100-17\omega^2}\Big)=\tan^{-1}\Bigg(\frac{\frac{7\omega}{10-\omega^2}+\frac{\omega}{10}}{1-\frac{7\omega}{10-\omega^2}\frac{\omega}{10}}\Bigg).
$$

Simplifying the expression in the brackets we have:

$$
    \frac{\frac{7\omega}{10-\omega^2}+\frac{\omega}{10}}{1-\frac{7\omega}{10-\omega^2}\frac{\omega}{10}}=\frac{\frac{70\omega+\omega(10-\omega^2)}{10(10-\omega^2)}}{\frac{10(10-\omega^2)-4\omega^2}{10(10-\omega^2)}}=\frac{\omega(80-\omega^2)}{100-17\omega^2}.
$$

Substituting back in {eq}`eq:phase_real` we have:
:::

$$
    \tan^{-1}\Big(\frac{\omega(80-\omega^2)}{100-17\omega^2}\Big)=180^\circ.
$$

Taking $tan(\cdot)$ on both sides we have:

$$
    \frac{\omega(80-\omega^2)}{100-17\omega^2}=0.
$$

Clearly one solution is $\omega\rightarrow\infty$ which we already know is an intersection of the real axis. The solutions for the numerator are

$$
    \omega=0,\sqrt{80}.
$$

We know that $\omega=0$ is an intersection. We need to substitute $\omega=\sqrt{80}$ to see where the plot intersects for this value of $\omega$:

$$
    \big|G(j\sqrt{80})\big|\approx0.12,\quad \angle G(j\sqrt{80})=-180^\circ.
$$

To the intersection is of the negative real axis. Here we skip the intersection of the imaginary axis. Try finding it as a homework exercise. 

We can now plot the Nyquist curve:

```{figure} images/Rec6/r6_ex1_nyquist.png
---
width: 70%
name: fig:R6_EX1
---
Nyquist Plot of $G(s)=\frac{150}{(s+2)(s+5)(s+10)}$.
```

We move on to stability. $G(s)$ has no right-handed poles, so $P=0$. We have no encirclements of $-1$ in {numref}`fig:R6_EX1`, so $N=0$. We thus have

$$
    N=P-Z\rightarrow 0=0-Z\rightarrow Z=0.
$$

We obtained that the closed-loop transfer function is stable. 

## Affect of Gain on the Nyquist Plot

One of the factors determining stability is the intersection of the Nyquist curve with the negative real axis. The location of this intersection can be found by substituting the relevant frequency into the magnitude expression. Multiplying a transfer function by a constant gain simply scales the magnitude of the transfer function by that gain, thereby shifting the Nyquist curve accordingly. 

More precisely, for a given transfer function $G(s)$ and a real constant $k$, we have:

$$
\big|kG(s)\big|=|k|\cdot\big|G(s)\big|.
$$


1. If $k > 1$, the Nyquist curve expands.
2. If $0 < k < 1$, the Nyquist curve contracts.
3. If $k < 0$, the Nyquist curve rotates by $180^\circ$ and undergoes expansion or contraction as per rules 1. and 2. **The trend of the curves remains unchanged!**


### Example

The following is the the Nyquist plot of the transfer function:

$$
G(s) = \frac{k}{s+2},\quad k=-1,0.5,1,2.
$$

```{figure} images/Rec6/r6_nyquist_different_k.png
---
width: 70%
name: fig:r6_different_k
---
Nyquist Plot of $G(s)=\frac{k}{s+2}$ for $k=-1,0.5,1,2$.
```

```{prf:remark}
Note that if $a_1,...,a_n$ are the intersection points of the Nyquist plot of $G(s)$ with the real axis, then $ka_1,...,ka_n$ are the intersection points of the Nyquist plot of $kG(s)$ with the real axis. 
```

```{prf:remark}
Note that for negative $k$, the trend of the Nyquist plot remains the same.
```


### Exercise 2

Draw the Nyquist plot of 

$$
    G(s)=\frac{k}{(s+1)(s-1)},\quad k>0.
$$

## Solution

1. **Substitute $s=j\omega$**:

In this case

$$
    G(j\omega)=\frac{k}{(j\omega+1)(j\omega-1)}=-\frac{k}{\omega^2+1}.
$$
	
Note that for every $\omega\geq0$, $k>0$, $G(j\omega)\in\mathbb{R}_-$. We will always get a negative real number so there is no need to calculate the expression for the magnitude and phase. The phase is always $-180^\circ$. The magnitude is the value for any given $\omega$. 

2. **Value at $\omega\rightarrow0$ and $\omega\rightarrow\infty$**:

Calculating explicitly we have:

$$
\lim_{\omega \to 0} G(j\omega) = -k, \quad \lim_{\omega \to \infty} G(j\omega) = 0.
$$

Observing that the magnitude decreases as $\omega$ increases, the Nyquist plot starts at $-k$, moves along the real axis to zero, and completes a clockwise encirclement:

```{figure} images/Rec6/download(2).png
---
width: 70%
name: fig:R6_EX2
---
Nyquist Plot of $G(s)=\frac{2}{(s+1)(s-1)}$.
```

$G(s)$ has one right-hand pole, meaning:

$$
P = 1.
$$

By applying the Nyquist criterion:

$$
N=P-Z\rightarrow N=1-Z\rightarrow Z=1-N.
$$

For stability, we need to have one counter-clockwise encirclement around $-1$. It is important to emphasize that here we only pass through $-1$, and we never encircle it. So in this case, the system is no stable for any value of $k$.

```{prf:remark}
It is important to emphasize that if the Nyquist plot of $G(s)$ passes through $-1$, we will not have stability. This case corresponds to being on the verge if stability, that is, the closed-loop transfer function will have purely imaginary poles.
```

## Nyquist Plot of a Transfer Function with Imaginary Poles

$\Gamma_s$ encircles all right-handed poles and zeros. If we have a pole on the imaginary axis, they will not be encircled by $\Gamma_s$. In order to make up for this, we encircle the pole itself and take the radius go to zero. 

```{figure} images/Rec6/r6_pole_at_Zero.png
---
width: 70%
name: fig:r6_different_k
---
Nyquist Plot of $G(s)=\frac{k}{s+2}$ for $k=-1,0.5,1,2$.
```

We draw the Nyquist plot per usual, and for the pole at the origin, we take

$$
    s=\varepsilon e^{j\theta},\; \varepsilon\rightarrow0,\;\theta\in[-90^\circ,90^\circ].
$$

We obtain that $\angle G(s=\varepsilon e^{j\theta},\;\varepsilon\rightarrow0)$ is in some range of angles. The trend of the angles will imply clock-wise or counter-clockwise rotation around the right or left handed plane. 


### Exercise 3

Draw the Nyquist plot of

$$
    G(s)=\frac{s+1}{s(s+3)(s+10)}.
$$

For what values of $k\in\mathbb{R}$ is the closed-loop system stable?

### Solution


1. **Substituting $s = j\omega$**:

$$
G(j\omega) = \frac{j\omega+1}{j\omega (j\omega + 3)(j\omega+10)}.
$$

2.  **Magnitude and Phase Expressions**: 

The magnitude is given by:

$$
|G(j\omega)| = \sqrt{\frac{\omega^2+1}{\omega^2(\omega^2+9)(\omega^2+100)}}.
$$

The expression for the phase is:

$$
    \angle G(j\omega)=-90^\circ+\tan^{-1}(\omega)-\tan^{-1}\big(\frac{\omega}{3}\big)-\tan^{-1}\big(\frac{\omega}{10}\big).
$$

Note that $-90^\circ$ is due to the pole at the origin.

3. **Boundary Analysis**:

Checking the limits:

$$
    \big|G(j\cdot0)\big|=\sqrt{\frac{1}{0\cdot9\cdot100}}\rightarrow\infty.
$$

$$
    \angle G(j\cdot0)=-90^\circ.
$$

The Nyquist plot begins at infinity along the negative imaginary axis. 

$$
    \big|G(j\omega\rightarrow\infty)\big|\rightarrow\infty,
$$

since the denominator is dominant.

$$
    \angle G(j\omega\rightarrow\infty)=-90^\circ+90^\circ-90^\circ-90^\circ=-180^\circ.
$$

We converge to the origin along the negative real axis.

As $\omega$ increases, the magnitude decreases, meaning the curve follows the imaginary axis from negative infinity up to the origin, where it approaches from the left. Since the curve starts from an infinite value, we examine the asymptotic behavior along the real axis.

We explicitly write the real and imaginary parts of the transfer function:

$$
    G(j\omega) &= \frac{j\omega+1}{j\omega (j\omega + 3)(j\omega+10)}\\
     &=\frac{j\omega+1}{-13\omega^2+j\omega(30-\omega^2)}\\
     &=\frac{j\omega+1}{-13\omega^2+j\omega(30-\omega^2)}\cdot\frac{-13\omega^2-j\omega(30-\omega^2)}{-13\omega^2-j\omega(30-\omega^2)}.
$$

After simplifying the expression and separating real and imaginary parts we obtain

```{math}
:label: eq:G_real_img
    G(j\omega)=\frac{17-\omega^2}{(30-\omega^2)^2+169\omega^2}-j\frac{12\omega^2+30}{\omega\big((30-\omega^2)^2+169\omega^2\big)}.
```

We are interested in the real part when $\omega \to 0$:

$$
    \frac{17-0^2}{(30-0^2)^2}=\frac{17}{30^2}\approx0.02.
$$

The curve begins at negative infinity along the imaginary axis, and raises upwards along the vertical asymptote "x=0.02".

4. **Intersection with the Imaginary Axes**:

To find intersections with the imaginary axis, we set the real part to zero:

$$
\text{Re}\big(G(j\omega)\big)=\frac{17-\omega^2}{(30-\omega^2)^2+169\omega^2}=0.
$$

This holds for $\omega\rightarrow0$, which we already know corresponds to an intersection with the origin (the imaginary axis). Nullifying the numerator we have:

$$
    17-\omega^2=0\rightarrow \omega=\sqrt{17}.
$$

Substituting this value in the imaginary part, we determine the intersection point:

$$
\text{Im}(G(j\cdot\sqrt{17})) = -\frac{12\cdot17+30}{\sqrt{17}\big((30-17)^2+169\cdot17\big)}\approx-0.02.
$$

It is evident that there are no intersections with the real axis since setting the imaginary part to zero yields a complex frequency. So far, we obtain:

```{figure} images/Rec6/r6_ex3_half.png
---
width: 70%
name: fig:r6_different_k
---
Nyquist Plot of $G(s)=\frac{k}{s+2}$ for $k=-1,0.5,1,2$.
```

5. **Handling the Pole at the Origin**:

We substitute $s=\varepsilon e^{j\theta}$ in $G(s)$:

$$
G(s=\varepsilon e^{j\theta}) = \frac{\varepsilon e^{j\theta}+1}{\varepsilon e^{j\theta}(\varepsilon e^{j\theta}+3)(\varepsilon e^{j\theta}+10)}.
$$

We evaluate each expression in brackets separately for $\varepsilon\rightarrow0$:

$$
    \varepsilon e^{j\theta}+1\approx1,\\
    \varepsilon e^{j\theta}+3\approx3,\\
    \varepsilon e^{j\theta}+10\approx10.
$$

We thus have

$$
    G(s=\varepsilon e^{j\theta})\underbrace{\approx}_{\varepsilon\rightarrow0}\frac{1}{30\varepsilon}e^{-j\theta}.
$$

Clearly, as $\varepsilon\rightarrow0$, 

$$
    \Big|\frac{1}{30\varepsilon}e^{-j\theta}\Big|\rightarrow\infty.
$$

Clearly,

$$
    \angle \frac{1}{30\varepsilon}e^{-j\theta}=-\theta.
$$

Since $\theta\in[-90^\circ,90^\circ]$, $-\theta\in[90^\circ,-90^\circ]$, so we encircle starting from $\infty$ along the positive imaginary axis, all the way to $-\infty$ along the negative imaginary axis.

Altogether, the Nyquist plot is:

```{figure} images/Rec6/r6_ex3.png
---
width: 70%
name: fig:r6_ex3
---
Nyquist Plot of $G(s)=\frac{s+1}{s(s+3)(s+10)}$.
```

Note that here the encirclement is around the entire right-half plane, not as depicted in the figure. 

Regarding stability, $G(s)$ has no right-handed poles, so $P=0$. We have

$$
    N=P-Z\rightarrow Z=P-N\rightarrow Z=-N.
$$

We want there to be no encirclements around $-1$. This holds as long as $k>0$ since the only intersection of the real axis is at $\infty$. For $k=-1$, we have:

```{figure} images/Rec6/r6_ex3_negative.png
---
width: 70%
name: fig:r6_ex3
---
Nyquist Plot of $G(s)=-\frac{s+1}{s(s+3)(s+10)}$.
```

This will be the Nyquist for any value of $k<0$. In this case there is one clockwise encirclement around $-1$, so $-N=1$, in this case

$$
    Z=-N=1.
$$

The closed-loop system is not stable. To summarize, the closed-loop system is stable for any $k>0$ and unstable for any $k<0$.

### Exercise - 4

Draw the Nyquist plot of

$$
    G(s)=\frac{8(s-25)}{s^2+4s+70}.
$$

For which values of $k\in\mathbb{R}$ is the closed-loop system stable?

### Solution


1. **Substitute $s=j\omega$**:

We have

$$
    G(j\omega)=\frac{8(j\omega-25)}{(j\omega)^2+4j\omega+70}=\frac{8(j\omega-25)}{70-\omega^2+4j\omega}.
$$

2. **Magnitude and Phase Analysis**:

We compute the magnitude function for $G(j\omega)$:

$$
    \big|G(j\omega)\big|=\frac{\sqrt{64\omega^2+(200)^2}}{\sqrt{\big(70-\omega^2\big)^2+16\omega^2}}.
$$

Computing for $\omega\rightarrow0$ and $\omega\rightarrow\infty$ we have

$$
    \big|G(j\cdot0)\big|=\frac{\sqrt{200^2}}{\sqrt{70^2}}=2.85,\quad \big|G(j\cdot\omega\rightarrow\infty)\big|\rightarrow\infty.
$$

The last result holds since the denominator is dominant.

Note that the roots of the denominator are complex, we cannot write the denominator in the form:

$$
(s + a)(s + b)
$$

which is a problem when expressing the phase of the transfer function, since a denominator of this form contributes specific phase shifts. 

Instead of computing a closed-form expression for the phase, we compute $G(j\omega)$ as $s\rightarrow0$ and $s\rightarrow\infty$ and figure the phase. 

$$
    G(0)=-\frac{8\cdot25}{70}.
$$

This is a negative real number. The phase which corresponds to such a number is $-180^\circ$. for $s\rightarrow\infty$ we do an asymptotic analysis, we only keep the dominant terms in the denominator and numerator:

$$
    G(s)\underbrace{\approx}_{s\rightarrow\infty}\frac{8s}{s^2}=\frac{8}{s}.
$$

Clearly,

$$
    \angle \frac{8}{s}=-90^\circ,
$$

so,

$$
    \angle G(j\omega\rightarrow\infty)=-90^\circ.
$$

To summarize,

$$
    \big|G(j\cdot0)\big|=2.85,\quad \angle G(j\cdot0)=-180^\circ,\\
    \big|G(j\omega\rightarrow\infty)\big|=0,\quad \angle G(j\omega\rightarrow\infty)=-90^\circ.
$$

3. **Curve Trend**:

We know that complex poles in the denominator contribute to a decrease in phase. The numerator will contribute an increase, but for $\omega\ll1$, the phase will decrease, so the phase decreases and the trend is clockwise.

4. **Intersections with the Real Axis**:

Since computing $G(j\omega)$ explicitly is complex, we decompose it into real and imaginary parts. The intersection with the real axis occurs where the imaginary part is zero:

$$
    G(j\omega)&=\frac{8(j\omega-25)}{70-\omega^2+4j\omega}\cdot\frac{70-\omega^2-4j\omega}{70-\omega^2-4j\omega}\\
    &=\frac{32\omega^2-200(70-\omega^2)}{(70-\omega^2)^2+16\omega^2}+j\frac{8\omega(70-\omega^2)+800\omega}{(70-\omega^2)^2+16\omega^2}.
$$

Setting the imaginary part to zero:

$$
8\omega(70-\omega^2)+800\omega=0.
$$

Solving for $\omega$:

$$
\omega=0,\quad\omega=\pm\sqrt{170}.
$$

For $\omega = 0$, we already found the intersection where the Nyquist curve begins. The valid solution corresponds to the positive root (no such thing as a negative frequency), yielding an intersection on the positive real axis:

$$
G(j\sqrt{170})=\frac{32\cdot(\sqrt{170})^2-200\big(70-(\sqrt{170})^2\big)}{\big(70-(\sqrt{170})^2\big)^2+16\cdot(\sqrt{170})^2}=2.
$$

That is, $\big|G(j\sqrt{170})\big|=2$, $\angle G(j\sqrt{170})=0^\circ$.

We can now draw the Nyquist plot:

```{figure} images/Rec6/r6_ex4_nyquist1.png
---
width: 70%
name: fig:r6_ex3
---
Nyquist Plot of $G(s)=\frac{8(s-25)}{s^2+4s+70}$.
```

We now move on to stability. The poles of $G(s)$ are 

$$
    s^2+4s+70=0\rightarrow s=-2\pm j\sqrt{66}.
$$

There are no poles in the right half plane, so $P=0$. We have

$$
    N=P-Z\rightarrow Z=P-N=-N.
$$

We have one clockwise rotation around $-1$, so $-N=1$, and we have

$$
    Z=1,
$$

and the system is not stable. Now, assume we add gain $k>0$. The Nyquist plot will be:

```{figure} images/Rec6/r6_ex4_nyquistk.png
---
width: 70%
name: fig:r6_ex3
---
Nyquist Plot of $kG(s)=k\frac{8(s-25)}{s^2+4s+70}$.
```

If $k>1$, the gain $k$ will increase the distance of the intersection points from the origin. If $0<k<1$, the gain will decrease the intersection points to the origin. We want no rotation around $-1$. For $k=\frac{1}{2.85}$, we obtain:

```{figure} images/Rec6/r6_ex4_nyquist_verge.png
---
width: 70%
name: fig:r6_ex3
---
Nyquist Plot of $\frac{1}{2.85}\cdot G(s)=\frac{1}{2.85}\cdot\frac{8(s-25)}{s^2+4s+70}$.
```

Note that in this case, the Nyquist plot crosses the point $-1$. This implies the closed-loop system is on the verge of stability (but is not stable). As we decrease $k$, the intersection point will go towards the origin, and there will be no rotation around $-1$. This implies that if $k>0$, the closed-loop system is stable for 

$$
    0<k<\frac{1}{2.85}.
$$

If we take  $-k$, we obtain:

```{figure} images/Rec6/r6_ex4_nyquist_negative_k.png
---
width: 70%
name: fig:r6_ex3
---
Nyquist Plot of $-kG(s)=-k\frac{8(s-25)}{s^2+4s+70}$.
```

Note that the Nyquist is rotated with respect to the imaginary axis, but the phase tendency is the same. If we take $k=\frac{1}{2}$, we exactly cross the point $-1$:

```{figure} images/Rec6/r6_ex4_nyquist_negative_k_half.png
---
width: 70%
name: fig:r6_ex3
---
Nyquist Plot of $-\frac{1}{2}\cdot G(s)=-\frac{1}{2}\cdot\frac{8(s-25)}{s^2+4s+70}$.
```

<center>
<a href="https://mybinder.org/v2/gh/Omrid1994/intro_to_control_recs/main?urlpath=voila/render/nyquist_slider.ipynb" target="_blank">
    <button style="font-size:18px; padding:10px 20px; background-color:#0078D4; color:white; border:none; border-radius:5px; cursor:pointer;">
        🚀 Click to Open Interactive Nyquist Plot
    </button>
</a>
</center>

Again, since the Nyquist crosses $-1$ the closed-loop system will be on the verge of stability (but not stable). As we decrease $k$ the intersection moves closer to the origin, so there will be no rotations around $-1$ and the closed-loop system will be stable. So we have

$$
    -\frac{1}{2}<k<0.
$$

Combining both cases, we have that the closed-loop system is stable for

$$
    -\frac{1}{2}<k<\frac{1}{2.85}.
$$