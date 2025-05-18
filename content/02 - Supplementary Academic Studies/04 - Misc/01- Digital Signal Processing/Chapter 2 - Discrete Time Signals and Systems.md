## 2.1 Discrete Time Signals

### 2.1.1 Elementary DTS

- **Unit sample sequence (unit impulse):**
  $$
  \delta(n) = 
  \begin{cases} 
  1, & n = 0 \\ 
  0, & n \neq 0 
  \end{cases}
  $$

- **Unit step sequence:**
  $$
  u(n) = 
  \begin{cases} 
  1, & n \geq 0 \\ 
  0, & n < 0 
  \end{cases}
  $$

- **Unit ramp signal:**
  $$
  u_r(n) = 
  \begin{cases} 
  n, & n \geq 0 \\ 
  0, & n < 0 
  \end{cases}
  $$

- **Exponential signal:**
  $$
  x(n) = a^n \text{ for all } n
  $$

- **When complex:**
  - $a = re^{j\theta}$
  - $x(n) = re^{j\theta n} = r^n (\cos \theta n + j \sin \theta n)$
  - $x_R(n) = r^n \cos \theta n$
  - $x_I(n) = r^n \sin \theta n$

We can also represent this by an amplitude and phase functions:

- **Amplitude**: $|x(n)| = A(n) = r^n$
- **Phase**: $\angle x(n) = \theta(n) = \theta_n$

### 2.1.2 Classification of Discrete-time signals

- **Energy (E)** of a signal $x(n)$ is defined as:
$$
E = \sum_{n=-\infty}^{\infty} |x(n)|^2
$$

- The energy of a signal can be infinite or finite.

- If $E$ is finite $(0 < E < \infty)$ then the signal $x(n)$ is called an energy signal and can be denoted by $E_x$.

- The average power of a discrete-time signal $x(n)$ is:
$$
P = \lim_{N \to \infty} \frac{1}{2N+1} \sum_{n=-N}^{N} |x(n)|^2
$$
* A signal $x(n)$ is periodic with period $N$ (non-zero) if and only if:
$$x(n+N) = x(n) \text{ for all } n$$

* The smallest value where $N$ holds is called the **fundamental period**.

* If there is no $N$ that satisfies the above, then the signal is **nonperiodic** or **aperiodic**.

### 2.1.3 Simple Manipulations of Discrete Time Signals

* Time shifting:
$$y(n) = x(n-k)$$
  * Advancing: $k < 0$
  * Delay: $k > 0$

* Time reversal (folding):
$$y(n) = x(-n)$$

* Time-scaling (downsampling):
$$y(n) = x(Mn)$$

## 2.2 Discrete-Time Systems

* A system is a type of function (operator) that takes in an input signal $x(n)$ and outputs some signal $y(n)$  
  - Input $\Rightarrow$ excitation  
  - Output $\Rightarrow$ response  

* Formally this is expressed as:  
$$ y(n) = T[x(n)] $$

### 2.2.1 Input-output Description of Systems

* Commonly blocks of $T(.)$ can be thought of as a black box but some common systems are:  
  - Identity system: $y(n) = x(n)$  
  - Unit delay system: $y(n) = x(n-1)$  
  - Unit advance system: $y(n) = x(n+1)$  
  - Moving average filter: $y(n) = \frac{1}{3}[x(n) + x(n+1) + x(n-1)]$  
  - Median filter: $y(n) = \text{median} \{x(n+1), x(n), x(n-1)\}$  
  - Accumulator:  
    $$ y(n) = \sum_{k=0}^{n} x(k) = x(n) + x(n-1) + \dots $$
### 2.2.2 Block diagram representation of D.T.S

### Basic building blocks of Discrete Time Systems

#### Adder: 
Takes the sum of 2 signals and outputs the summed result. This operation is memory-less.

$$ y(n) = x_1(n) + x_2(n) $$

#### Constant multiplier:
Applies a scale factor on the input signal (also memory-less).

$$ y(n) = ax(n) $$

#### Signal multiplier:
Multiplies 2 signals and outputs results.

$$ y(n) = x_1(n) \cdot x_2(n) $$

#### Unit delay element:
A system that delays the signal passing through it by one sample.

$$ y(n) = x(n-1) $$
- unit advance: moves the input signal ahead by one sample in time: (memory)

$$y(n) = x(n+1)$$

$$x(n) \rightarrow \boxed{z} \rightarrow y(n) = x(n+1)$$

- copy figure 2.2.7 (pg 79)

## 2.2.3 Classification of Discrete-Time Systems

A discrete-time system is:

- **Static (memoryless)**: If its output at any instance $n$ depends at most on the input sample at the same time, but not on past or future samples of the input.

- **Dynamic**: If the output is dependent on the input sample at any past or future samples.

- We can further divide the general class of systems into two broad categories: time-invariant systems and time-variant systems.

- **Time-invariant**: If the I/O characteristics do not change with time.

Which is to say if and only if:

$$ x(n) \rightarrow y(n) $$

Implies that

$$ x(n-k) \rightarrow y(n-k) $$

The general classes of systems can also be subdivided into linear and nonlinear systems.

A system is linear if:

$$ \mathcal{T}[a_1x_1(n) + a_2x_2(n)] = a_1\mathcal{T}[x_1(n)] + a_2\mathcal{T}[x_2(n)] $$

If this is not satisfied then we say the system is nonlinear.

An arbitrary relaxed system is said to be bounded input-bounded output (BIBO) stable if and only if every bounded input produces a bounded output.

$ |x(n)| \leq M_x < \infty, |y(n)| \leq M_y < \infty $

for all $ n $

## 2.3 Analysis of Discrete-Time Linear Time Invariant Systems

### 2.3.1 Techniques for the analysis of linear systems

One useful way of representing signals as a linear combination of other signals:

$$
X(n) = \sum_{k} c_k x_k(n)
$$

$c_k$: Set of amplitudes (weighting coefficients)

### 2.3.2 Resolution of Discrete Time Signal into Impulses

Suppose we have a signal $X(n)$ that we want to resolve into a sum with sample sequences. Then $x_k(n) = \delta(n-k)$.

This really gives us the signal $X(n)$ at some specific time delay $k$, so it gives us a single value $X(k)$ of the signal $X(n)$.

To reconstruct $X(n)$:

$$
X(n) = \sum_{k=-\infty}^{\infty} X(k) \delta(n-k)
$$

### 2.3.3 Response of LTI Systems to Arbitrary Inputs: The Convolution Sum

Having resolved $X(n)$ into a weighted sum of impulses, we can determine the response of any relaxed linear system to any input system.

Response of system $y(n,k)$ to input sample sequence at $k=n$ by special symbol $h(n,k)$, $-\infty < k < \infty$:
$$
y(n,k) = h(n,k) = \mathcal{T}[\delta(n-k)]
$$

Note that $h(n)$ is the impulse response of the system with an impulse applied as an input: $h(n) = \mathcal{T}[\delta(n)]$

The response of the system to $x(n)$ is:
$$
y(n) = \mathcal{T}[x(n)] = \mathcal{T}\left[\sum_{k=-\infty}^{\infty} x(k) \delta(n-k)\right]
$$
$$
= \sum_{k=-\infty}^{\infty} x(k) h(n,k)
$$
$$
= \sum_{k=-\infty}^{\infty} h(k) x(n-k) = \sum_{k=-\infty}^{\infty} x(k) h(n-k)
$$

So we can see for a LTI system the response $y(n)$ to any input $x(n)$ is characterized by:
- How $x(n)$ can be broken into a stream of impulses
- How the system responds to any one of these impulses

#### Convolution Steps

The convolution between $x(k)$ and $h(k)$ is broken into 4 steps:
1. **Folding**: Fold $h(k)$ about $k=0$ to obtain $h(-k)$
2. **Shifting**: Shift $h(-k)$ by $n$ to the right (left) at $n$ as positive (negative) to obtain $h(n-k)$
3. **Multiplication**: Multiply $x(k)$ by $h(n-k)$ to obtain the product sequence $h(n-k) = x(k) h(n-k)$
4. **Summation**: Sum over all $k$ values to get the result.

#### LTI system properties

- **Causality**: Output depends only on present and past inputs
  - $T[\cdot]$ is causal if and only if $h(n)=0$ for all $n<0$
  - This causes the convolution formula to become:
    $$
    y(n) = \sum_{k=0}^{\infty} h(k)x(n-k)
    $$
- **BIBO stability**: Bounded inputs produce bounded outputs
  - $T[\cdot]$ is stable iff $h(n)$ is absolutely summable:
    $$
    \sum_{k=-\infty}^{\infty} |h(k)| < \infty
    $$
## 2.4 Discrete-time systems described by difference equations

### 2.4.1 Recursive and non-recursive discrete-time systems

Suppose we want to compute the cumulative average of a signal $x(n)$ in the interval $0 \leq k \leq n$ defined as:

$$
y(n) = \frac{1}{n+1} \sum_{k=0}^{n} x(k), \quad n=0,1,\ldots
$$
The computation of $y(n)$ would require storage of all input samples $x(k)$, $0 \leq k \leq n$.

We notice that we can simply use the previous output value and rearrange the equation to:

$$
y(n) = \frac{n}{n+1} y(n-1) + \frac{1}{n+1} x(n)
$$

Now $y(n)$ can be solved recursively.

We can turn this into a recursive system as shown below:

*Copy figure 2.4.1 Pg 111*

A non-recursive system, the output $y(n)$ is only dependent on current or past inputs (not output).

### 2.4.2 LTI Systems Characterized by Constant Coefficient Difference Equations

Suppose we have an input-output recursive system described by:

$$
y(n) = a y(n-1) + x(n)
$$

where $a$ is constant.

$$y(0) = ay(-1) + x(0)$$

$$y(1) = ay(0) + x(1) = a^2y(-1) + ax(0) + x(1)$$

$$y(2) = ay(1) + x(2) = a^3y(-1) + a^2x(0) + ax(1) + x(2)$$

$$y(n) = a^{n+1}y(-1) + \sum_{k=0}^{n} a^{k}x(n-k), \quad n \geq 0$$

So if the state is initially relaxed at $n = 0$ then $y(-1) = 0$. For this we say the system is zero state and its output is called zero state response denoted as $y_{zs}(n)$.

$$y_{zs}(n) = \sum_{k=0}^{n} a^{k}x(n-k), \quad n \geq 0$$

Now suppose the initial state is not relaxed $y(-1) \neq 0$. Then the output of the system with zero input is called the zero-input response or the natural response denoted by $y_{zi}(n)$.

$$y_{zi}(n) = a^{n+1}y(-1), \quad n \geq 0$$

In general the total response of the system can be written as:

$$y(n) = y_{zi}(n) + y_{zs}(n)$$

Another general form is: $\forall \text{cases not just } \text{1st order}$

$$ y(n) = - \sum_{k=1}^{N} a_k y(n-k) + \sum_{\mu=0}^{M} b_\mu x(n-\mu) $$

$N$ is called the order of the difference equation.

A system is linear if:

1. The total response is equal to the sum of the zero input and zero state responses $(y(n) = y_{zi}(n) + y_{zs}(n))$
2. The principle of superposition applies to the zero state response (zero-state linear)
3. The principle of superposition applies to the zero-input response (zero-input linear)


## 2.5 Implementation of Discrete Time Systems

Skipped error in textbook only have half of the section

## 2.6 Correlation of Discrete Time Signals

### 2.6.1 Crosscorrelation and Autocorrelation Sequences

- The **crosscorrelation** of $x(n)$ and $y(n)$:

$$
r_{xy}(l) = \sum_{n=-\infty}^{\infty} x(n) y(n-l), \quad l = 0, \pm 1, \pm 2, \ldots
$$

or

$$
r_{xy}(l) = \sum_{n=-\infty}^{\infty} x(n+l) y(n), \quad l = 0, \pm 1, \pm 2, \ldots
$$

- $l$: time shift/lag

- $xy$: indicates the signals being crosscorrelated

- If roles were reversed, then:

$$
r_{yx}(l) = \sum_{n=-\infty}^{\infty} y(n) x(n-l), \quad l = 0, \pm 1, \pm 2, \ldots
$$

- So we can see that:

$$
r_{xy}(l) = r_{yx}(-l)
$$

- So $r_{yx}(l)$ is a folded (at $l=0$) $r_{xy}(l)$

- the convolution of $x(n)$ with $y(-n)$ yields the crosscorrelation $r_{xy}(l)$

$$
r_{xy}(l) =  x(n) * y(-n)
$$
**Autocorrelation:**
For autocorrelation, $x(n) = y(n)$, so we have:

$$
r_{xx}(l) = \sum_{n=-\infty}^{\infty} x(n) x(n-l)
$$

$$
r_{xx}(l) = \sum_{n=-\infty}^{\infty} x(n+l) x(n)
$$

where $l = 0, \pm 1, \pm 2, \ldots$
