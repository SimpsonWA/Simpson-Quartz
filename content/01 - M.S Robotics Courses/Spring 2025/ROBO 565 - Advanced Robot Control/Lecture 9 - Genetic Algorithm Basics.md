# Genetic Algorithms Basics

- Algorithms for optimized problems
  - also called Evolutionary Computation or Evolutionary Optimization

- Genetic Algorithms (GAs): 5 Basic Components
  1. A genetic representation of potential solutions
  2. A way to create a population
  3. An evaluation function rating solutions in terms of their fitness
  4. Genetic operations that alter the genetic composition of offspring
  5. Parametric values that genetic algorithm uses
     - population size, probability of genetic operators

## 1.2 General Structure of GAs

- **Genetic representation and initialization:**
	- The genetic algorithm maintains a population $P(t)$ of chromosomes or individuals $V_k(t)$, $k=1,2,...$ population size for generation $t$.
	- Each chromosome represents a potential solution to the problem at hand.
- **Evaluation**:
	- Each chromosome is evaluated to give some measure of its fitness eval(Ch).
- **Genetic Operators**
	- Some chromosomes undergo stochastic transformations by means of genetic operators to form new chromosomes (offspring).
	- There are 2 kinds of operators:
		- **Crossover**: which creates a new chromosome by combining parts from 2 chromosomes.
		- **Mutation**: which creates new chromosomes by making changes in a single chromosome.
	- New chromosomes (called offspring Ch) are then evaluated.
- **Selection**
	- A new population is formed by selecting the more fit chromosomes from the parent population and the offspring population.
- **Best Solution**
	- After several generations, the algorithm converges to the best chromosome, which hopefully represents an optimal or suboptimal solution to the problem.

``` pseudo

\begin{algorithm}
\caption{Simple Genetic Algorithm (GA)}
\begin{algorithmic}
\Procedure{SimpleGA}{GA parameters}
    \State $t \gets 0$ \Comment{Generation number}
    \State Initialize $P(t)$ by encoding routine \Comment{Population of chromosomes}
    \State Evaluate fitness of $P(t)$ using decoding routine
    \While {not termination condition}
        \State Perform crossover on $P(t)$ to yield $C(t)$ \Comment{Generate offspring}
        \State Perform mutation on $C(t)$
        \State Evaluate fitness of $C(t)$ using decoding routine
        \State Select $P(t+1)$ from $P(t)$ and $C(t)$
        \State $t \gets t + 1$
    \EndWhile
    \State \textbf{output} best solution
\EndProcedure
\end{algorithmic}
\end{algorithm}


```

# How GA Works

## Binary String Representation -- Encoding

- The domain of $x_j$ is $[a_j, b_j]$ and required precision is 5 places after the decimal point.
- The precision requirement implies the range or domain of each variable should be divided into at least $(b_j - a_j) \times 10^5$ size ranges.
- The required bits (denoted $m_j$) for a variable is calculated by:
  $$2^{m_j} - 1 \ge (b_j - a_j) \times 10^5 \le 2^{m_j} - 1$$

- The mapping from a binary string to a real number for variable $x_j$ is completed as follows:
  $$x_j = a_j + \text{decimal}(\text{substring}_j) \times \frac{(b_j - a_j)}{2^{m_j} - 1}$$

## Example

Unconstrained optimization problem:
$$\text{max } f(x_1, x_2) = 21.5 + x_1 \sin(4\pi x_1) + x_2 \sin(20\pi x_2)$$
subject to
$$-3.0 \le x_1 \le 12.1$$
$$4.1 \le x_2 \le 5.8$$
# Representation

## Binary String Representation -- Encoding

1. For $x_1$:
   - $(12.1 - (-3.0)) \times 10^5 = 151,000$
   - $2^{17} \leq 151,000 < 2^{18}$, so $M_1 = 18$ bits

2. For $x_2$:
   - $(5.8 - 4.1) \times 10^5 = 17,000$
   - $2^{14} \leq 17,000 < 2^{15}$, so $M_2 = 15$ bits

- Total precision requirement: $M = M_1 + M_2 = 37$ bits

## Example

- Chromosome (binary string): $V_j$: `0000010101001001` | `0(111)011111110`
  - $x_1$: 18 bits
  - $x_2$: 15 bits

### Binary String Decoding

| Binary \# |         | Decimal  |
| --------- | ------- | -------- |
| $x_1$     | 0000010101001001 | 5417 |
| $x_2$     | 101111011111110 | 24318 |

### Conversion to Real Numbers

- $x_j = a_j + \text{decimal (substring)} \times \frac{b_j - a_j}{2^{M_j} - 1}$

- For $x_1$: 
  $$x_1 = -3.0 + 5417 \times \frac{12.1 - (-3.0)}{2^{18} - 1} = -2.687064$$

- For $x_2$:
  $$x_2 = 4.1 + 24318 \times \frac{5.8 - 4.1}{2^{15} - 1} = 5.361653$$

## Initial Population

- The initial population is randomly sampled.

$$V1 = [x1, x2] = [33 bit string] \\

...\\
\\
V10
$$
## 2.3 Evaluation

- **Input**: chromosome Vk, k=1,2,...,popsize
- **Output**: fitness eval(Vk)

1. Convert chromosome's genotype to its phenotype (convert binary string to real values)
   - $X_n = (X_{n1}, X_{n2})$
2. Evaluate the objective function $f(X_n)$
3. Convert the value of the objective function into fitness

Example:
   - $f(X_{n1}, X_{n2}) = 21.5 \cdot X_{n1} \cdot \sin(4\pi X_{n1}) + X_{n2} \cdot \sin(20\pi X_{n2})$
   - $(X_{n1} = -2.637, X_{n2} = 5.361) = V1$
   - $\text{eval}(V1) = f(-2.637, 5.361) = 19.805$

## 2.4 Genetic Operators

- **Selection**:
  - Most common approach is the roulette wheel approach
  - Roulette wheel is constructed by:
     - **Input**: population $P(t-1)$, $C(t-1)$
     - **Output**: population $P(t)$,

1. **Calculate the total fitness for the population**:
   $$F = \sum_{k=1}^{popsize} eval(U_k)$$

2. **Calculate the selection probability \(p_k\) for each chromosome \(U_k\)**:
   $$p_k = \frac{eval(U_k)}{F}, \quad k = 1, 2, \ldots, popsize$$

3. **Calculate the cumulative probability \(q_k\) for each chromosome \(U_k\)**:
   $$q_k = \sum_{j=1}^{k} p_j, \quad k = 1, 2, \ldots, popsize$$

4. **Generate a random number \(V\) from $\([0,1]\)$**.

5. **Selection of Chromosomes**:
   - If \(V \leq q_1\), then select the 1st chromosome \(U_1\).
   - Otherwise, select the \(k\)-th chromosome \(U_k\) (where \(2 \leq k \leq popsize\)) such that:
     $$q_{k-1} \leq V \leq q_k$$
### Example:

Copy the pseudo code


