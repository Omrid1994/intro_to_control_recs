---
title: Summary -- Transfer Functions
---
# Suammary -- Transfer Functions

In this course, we will deal with a system of the following form:

```{figure} images/Summary/s1.png
---
width: 70%
name: fig:system_b_2
---
Negative Feedback Closed-Loop Block Diagram.
```

where $ r(t) $ is the input signal, $ y(t) $ is the output signal, $ u(t) $ is the control signal, and $ e(t) $ is the error signal or the tracking signal:

$$
e(t) = r(t) - y(t).
$$

The transfer function $ P(s)=\frac{\hat{y{(s)}}}{\hat{u}(s)} $ is the transfer function of the controlled system, also known as the <b>plant</b>. We can think of it as the transfer function representing the physical system that we want to control.

The transfer function $ C(s)=\frac{\hat{u}(s)}{\hat{e}(s)} $ is the transfer function of the controller. $ H(s) $ is the feedback transfer function.

The <b>loop-gain transfer function</b> is the transfer function of the system without feedback. That is, only the transfer functions between the summation point and the output signal:

$$
\frac{\hat{y}(s)}{\hat{e}(s)} = G(s) = C(s)P(s).
$$

The <b>closed-loop transfer function</b> is the transfer function of the system with feedback between the output $ y(t) $ and the input $ r(t) $:

$$
\hat{y}(s) &= \hat{e}(s) G(s) \\
          &= \big(\hat{r}(s) - \hat{y}(s) H(s)\big) G(s) \\
\Rightarrow \hat{y}(s) + \hat{y}(s) H(s) G(s) &= \hat{r}(s) G(s).
$$

Thus, we get:

$$
\hat{y}(s)(1 + H(s)G(s)) = \hat{r}(s)G(s),
$$

and we obtain:

$$
\frac{\hat{y}(s)}{\hat{r}(s)} = \frac{G(s)}{1 + H(s)G(s)}.
$$

In the course so far, we have dealt with cases where $ H(s) = 1 $. Therefore, we refer to the closed-loop transfer function as:

$$
\frac{\hat{y}(s)}{\hat{r}(s)} = \frac{G(s)}{1 + G(s)}.
$$

Now we will find the transfer function between the error signal $ e(t) $ and the input $ r(t) $:

$$
\hat{e}(s) = \hat{r}(s) - \hat{y}(s) H(s).
$$

Note that $ \hat{y}(s) = \hat{e}(s) C(s) P(s) = \hat{e}(s) G(s) $. Substituting this, we get:

$$
\hat{e}(s) = \hat{r}(s) - \hat{e}(s) G(s) H(s).
$$

Rearranging the terms:

$$
\hat{e}(s)(1 + G(s)H(s)) = \hat{r}(s),
$$

thus, we obtain:

\[
\frac{\hat{e}(s)}{\hat{r}(s)} = S(s) = \frac{1}{1 + G(s)H(s)}.
\]

This is also called the <b>sensitivity transfer function</b>. In our course so far, $ H(s) = 1 $, so we get:

$$
\frac{\hat{e}(s)}{\hat{r}(s)} = S(s) = \frac{1}{1 + G(s)}.
$$

Notice that the denominator of the sensitivity transfer function and the closed-loop transfer function is identical.

## Note Regarding Alternative Block Diagram

```{figure} images/Summary/s2.png
---
width: 70%
name: fig:system_b_2
---
Negative Feedback Closed-Loop Block Diagram.
```

This system is equivalent to the system shown at the beginning of the document with the addition of a disturbance signal. Simply place the controller $ C(s) $ below, but it is still connected in the same line with $ P(s) $. Note that the input $ r(t) $ enters the lower right part and the feedback enters the system in the same way as at the beginning of the document. Essentially, we can move the controller $ C(s) $ to the left of $ P(s) $ to obtain the system at the beginning of the document. Additionally, since $ d = 0 $, the signals $ v $ and $ u $ merge into a single signal.

\section*{Disturbance Signal}

A system with a disturbance signal will be of the following form:

```{figure} images/Summary/s3.png
---
width: 70%
name: fig:system_b_2
---
Negative Feedback Closed-Loop Block Diagram with disturbance signal.
```

When we work with a disturbance signal $ d(t) $, we will use superposition between the disturbance signal and the reference/input signal $ r(t) $. To calculate the transfer function between the disturbance signal and the output signal, we set the reference signal to zero.

Notice that in this case, we can think of $ H(s)C(s) $ as the feedback transfer function because if we analyze the exit point from $ C(s) $, we see that the input signal there is:

$$
-\hat{y}(s) H(s) C(s).
$$

Therefore, the transfer function between the output and the disturbance signal is simply the closed-loop transfer function with feedback transfer function $ H(s)C(s) $ and open-loop transfer function composed only of $ P(s) $:

$$
\frac{\hat{y}(s)}{\hat{d}(s)} = \frac{P(s)}{1 + H(s)C(s)P(s)}.
$$

In our case, $ H(s) = 1 $, so we get:

$$
\frac{\hat{y}(s)}{\hat{d}(s)} = \frac{P(s)}{1 + C(s)P(s)}.
$$

