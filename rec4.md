---
title: Introduction to Control -- Recitation 4
---

# Introduction to Control -- Recitation 4

## Second Order Systems

Consider the loop-gain

$$
G(s) = \frac{\omega_n^2}{s(s+2\xi\omega_n)}.
$$

where $\omega_n$ and $\xi$ are positive real numbers. We assume that $0 < \xi < 1$.

If we close a loop with a unit feedback around $P(s)$, then the closed-loop transfer function from the reference signal to the output of the plant is:


$$
T(s) = \frac{G(s)}{1 + G(s)} = \frac{\omega_n^2}{s^2 + 2\xi \omega_n s + \omega_n^2}.
$$


The closed-loop poles are the roots of the denominator above, that is,

$$
s^2 + 2\xi \omega_n s + \omega_n^2 = 0.
$$

Solving for $s$, we obtain:

$$
s_{1,2} &= \frac{-2\xi \omega_n \pm \sqrt{4\xi^2 \omega_n^2 - 4\omega_n^2}}{2}\\
&= -\xi \omega_n \pm j \omega_n \sqrt{1 - \xi^2}.
$$

Since $\xi,\;\omega_n>0$, we have two complex poles with a negative real part.


```{figure} images/Rec4/poles_of_second_order_system.png
---
width: 70%
name: fig:closed_system
---
Poles location of a second order system.
```

The amplitude of these complex poles is:

$$
|s_{1,2}| = \sqrt{(-\xi \omega_n)^2 + (\omega_n \sqrt{1 - \xi^2})^2} = \omega_n.
$$

The phase is:

$$
    \cos(\alpha)=\frac{\xi\omega_n}{\omega_n}=\xi.
$$

So, $\omega_n$, called the "natural frequency," is the distance from the origin to the pole, and the phase, also called the "damping ratio," is $\xi$.

## Step Response Characteristics of a Second Order System

The step response of the closed-loop system is:

$$
y(t) = 1 - \frac{e^{-\xi \omega_n t}}{\sqrt{1-\xi^2}}  \sin\big(\omega_dt+\alpha\big),
$$

where $\omega_d = \omega_n \sqrt{1 - \xi^2}$.

This is one minus a sinusoidal signal that is modulated by a decaying exponential. Note that the step response converges to one, meaning that the plant output converges to the value of the reference signal.


```{figure} images/Rec4/step_response.png
---
width: 70%
name: fig:closed_system_1
---
Step response of second order system.
```

### Rise Time

The rise time, $ t_r $, is the time it takes for the response to rise from $ 0.1 $ of the step signal to $ 0.9 $ of the step signal.

$$
t_r \approx \frac{1.8}{\omega_d}.
$$

### Peak Time

The peak time, $ t_p $, is the time it takes for the response to reach its maximal value.

$$
t_p = \frac{\pi}{\omega_d}.
$$

### Overshoot

The overshoot is the maximal value of the response signal relative to the input.

```{math}
:label: eq:overshoot
\sigma = e^{-\frac{\pi \xi}{\sqrt{1 - \xi^2}}}\rightarrow\xi=\sqrt{\frac{\ln^2(\sigma)}{\pi^2+\ln^2(\sigma)}}.
```

### Settling Time

The settling time, $ t_s $, is the time it takes for the response signal to decay to $ 5\% $ of the input signal.

$$
t_s \approx \frac{3}{\xi \omega_n}.
$$


### Exercise

Consider the closed-loop system:


```{figure} images/Rec4/ex1.png
---
width: 70%
name: fig:closed_system_2
---

```

The required step-response of this closed-loop system is:

```{figure} images/Rec4/ex11.png
---
width: 70%
name: fig:closed_system_2
---
Step response of second order system.
```

Find the values of $K,T$.

### Solution 

The closed-loop system transfer function is:

$$
T(s) = \frac{G(s)}{1 + G(s)} = \frac{K}{Ts^2+s+k}=\frac{K/T}{s^2+s/T+K/T}.
$$

From the graph, we are given the overshoot $ \sigma=0.254 $, which is related to $ \xi $ via {eq}`eq:overshoot`:

$$
    \xi=\sqrt{\frac{\ln^2(0.254)}{\pi^2+\ln^2(0.254)}}=0.4.
$$

We are also given the peak time, $ t_p=3\;\text{sec} $, which is related to both $ \xi $ and $ \omega_n $:

$$
t_p = \frac{\pi}{\omega_d} = \frac{\pi}{\omega_n \sqrt{1 - \xi^2}}=3\rightarrow\omega_n=\frac{\pi}{3\sqrt{1-(0.4)^2}}=1.14\frac{\text{rad}}{\text{sec}}.
$$

We compare the transfer function we obtained to the canonical form of a second-order system:

$$
\frac{\omega_n^2}{s^2 + 2\xi \omega_n s + \omega_n^2}=\frac{K/T}{s^2+s/T+K/T}.
$$

From this, we identify:

$$
    \omega_n^2=\frac{K}{T},\quad2\xi\omega_n=\frac{1}{T}.
$$

Substituting $\xi=0.4,\;\omega_n=1.14$, we have

$$
    (1.14)^2=\frac{K}{T},\quad 2\cdot0.4\cdot1.14=\frac{1}{T}.
$$

Solving for $K,\;T$ we have 

$$
    T=1.09\text{ sec},\quad K=1.42.
$$

### Exercise 

For the system given in {numref}`fig:system_a` below, the damping ratio is $ \xi=0.158 $ and the natural frequency is $ \omega_n=3.16\text{ rad/sec} $ for $ K = 1 $. To improve the stability of the system, two feedback loops were added, as seen in {numref}`fig:system_b`.

1. What value of $K$ of system (a) will yield $\xi=0.5$?
2. For which value of $K_h$ the damping ration of system (b) is $\xi=0.5$?
3. Plot the step-response of: The system (a) with $K=1$, system (a) with $K$ from 2., system (b) with $K_h$.

```{figure} images/Rec4/ex2a.png
---
width: 70%
name: fig:system_a
---
System (a).
```


```{figure} images/Rec4/ex2b.png
---
width: 70%
name: fig:system_b
---
System (b).
```

### Solution

#### 1.
The closed-loop transfer function of system (a) is:

$$
T_a(s) = \frac{G(s)}{1+G(s)}=\frac{10K}{s(s+1)+10K}=\frac{10K}{s^2+s+10K}.
$$

Comparing with the canonical form of a second-order system, we have:

$$
\omega_n^2 = 10K\rightarrow\omega_n=\sqrt{10K},
$$

moreover,

$$
2\xi \omega_n = 1=2\xi\sqrt{10K}.
$$

We want $ \xi = 0.5 $, so:

$$
1=2\cdot0.5\sqrt{10K}\rightarrow K=0.1.
$$

Note that with a constant gain $ K $, we controlled the value of both $ \xi $ and $ \omega_n $.  

#### 2.

Computing the closed-loop transfer function of system (b), we have:

$$
T_b(s) =\frac{10}{s^2+(1+10K_h)s+10}.
$$

Comparing with the canonical form of a second-order system, we have:

$$
\omega_n^2 = 10\rightarrow \omega_n=\sqrt{10}.
$$

Moreover,

$$
2\xi \omega_n = 1+10K_h.
$$

Again, we want $ \xi = 0.5 $, so we obtain:

$$
2\cdot0.5\cdot\underbrace{\sqrt{10}}_{\omega_n} = 1+10K_h \Rightarrow K_h = \frac{2.16}{10}=0.216.
$$

Note that $K_h$ affects only $\xi$!

```{figure} images/Rec4/step_responseex2.png
---
width: 70%
name: fig:system_b_1
---

```

Note that the for system (b) the system converges much quicker.

#### Exercise

Consider the angular control system of a robotic arm, as described in the block diagram below.

```{figure} images/Rec4/ex3.png
---
width: 70%
name: fig:system_b_2
---

```

The controller $D_c(s)$ is a PD controller

$$
D_c(s) = K_p + K_d s.
$$


1. What is the type of the system, and is it capable of tracking a step input without error?

2. Can the system with the given controller reject disturbances of impulse and step types?

3. Set $ J = 1\;kg\cdot m^2 $. Design the controller so that the overshoot does not exceed $ 0.1 $, and the steady-state error due to a step disturbance does not exceed $ 0.02 $. Compute the settling time.

4. Plot the system response to a step reference input, once with an impulse disturbance and once with a step disturbance. Does the system meet the requirements?


### Solution
#### 1.
To find the open-loop transfer function, substitute $ \hat{d}=0 $. We obtain:

$$
G(s) =\frac{D_c(s)}{Js^2}= \frac{K_p s + K_p}{Js^2}.
$$

The system is of type 2, meaning the steady-state error for a step input is zero.

#### 2.
The transfer function from the disturbance input to the output is:

```{math}
:label: eq:H_d
H_{\hat{d}}=\frac{\hat{y}(s)}{\hat{d}(s)} = \frac{P(s)}{1+D_c(s)P(s)}=\frac{1}{Js^2 + K_d s + K_p}.
```

The output due to a disturbance is:

$$
\hat{y}_{\hat{d}}(s) = \frac{\hat{d}(s)}{Js^2+K_ds+K_p}.
$$

For an impulse disturbance $ \hat{d}(s) = 1 $. Using the final value theorem we have

$$
    \big(y_{ss}\big)_{\hat{d}}&=\lim_{s\rightarrow0}s\hat{y}(s)\\
    &=\lim_{s\rightarrow0}s\cdot\frac{1}{Js^2+K_ds+K_p}\\
    &=0.
$$

The final value theorem shows that an impulse disturbance does not affect the steady-state value.

For a step disturbance $ \hat{d}(s) = \frac{1}{s} $:


```{math}
:label: eq:disturbance_step
    \big(y_{ss}\big)_{\hat{d}}&=\lim_{s\rightarrow0}s\cdot\frac{1}{Js^2+K_ds+K_p}\cdot\frac{1}{s}\nonumber\\
    &=\lim_{s\rightarrow0}\frac{1}{Js^2+K_ds+K_p}\nonumber\\
    &=\frac{1}{K_p}.
```

Thus, an impulse disturbance does not influence the final value, whereas a step disturbance causes a steady-state offset.

As we increase $K_p$ we decrease the affect of the disturbance on the output. 

#### 3.
The closed-loop system obtained is a second-order system, focusing on the characteristic polynomial:

$$
p(s)=s^2 + K_d s + K_p.
$$

Comparing to the canonical form of a second order system we have

```{math}
:label: eq:req
    \omega_n^2=K_p,\quad K_d=2\xi\omega_n.
```

The requirements are:

$$
\sigma=0.1,\;\Big|\big(y_{ss}\big)_{\hat{d}(s)}\Big|<0.02.
$$

The requirement on $\sigma$ gives a required value for $\xi$:

$$
    \xi=\sqrt{\frac{\ln^2(0.1)}{\pi^2+\ln^2(0.1)}}\approx0.6
$$

We showed that for step disturbance ({eq}`eq:disturbance_step`):

$$
    \big(y_{ss}\big)_{\hat{d}}=\frac{1}{K_p}.
$$

So

$$
    \Big|\frac{1}{K_p}\Big|<0.02\rightarrow |K_p|>50.
$$

We work with $K_p=50$. Substituting in {eq}`eq:req` we have

$$
    \omega_n=\sqrt{K_p}=\sqrt{50},
$$

and

$$
    K_d=2\cdot0.6\cdot\sqrt{50}=8.5.
$$

To summarize

$$
    K_p=50,\quad K_d=8.5,\\
    \omega_n=\sqrt{50},\quad\xi=0.6.
$$

The settling time is:

$$
t_s = \frac{3}{\zeta \omega_n}=\frac{3}{0.6\cdot\sqrt{50}}=0.707\text{ sec}.
$$

The peak time is:

$$
t_p = \frac{\pi}{\omega_d}=\frac{\pi}{\omega_n\sqrt{1-\xi^2}}=0.55\text{ sec}.
$$

#### 4.
The output can be expressed as a superposition of the reference input and the disturbance:

$$
\hat{y}(s) = H_{\hat{r}}\hat{r}+H_{\hat{d}}\hat{d}.
$$

where,

$$
H_{\hat{r}}&=\frac{\hat{y}(s)}{\hat{r}(s)}\\&=\frac{D_c(s)P(s)}{1+D_c(s)P(s)}\\
&=\frac{K_ds+K_p}{Js^2+K_ds+K_p}.
$$

$H_{\hat{d}}$ is given in {eq}`eq:H_d`. According to the principle of superposition:

$$
y(t) = y_{\text{ref}}(t) + y_{\text{dist}}(t).
$$

Thus, we can simulate the response for each input separately and then sum them to obtain the overall response.

```{figure} images/Rec4/response_ex3.png
---
width: 70%
name: fig:system_b_3
---

```

