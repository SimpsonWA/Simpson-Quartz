**Idea**: Basically the bayes' filter is an algorithm to compute the [[Belief]] from observations and control data. 

---

**Pseudo Code:**
```pseudo 
\begin{algorithm}
\caption{Bayes\_Filter}
\begin{algorithmic}
\REQUIRE $bel(x_{t-1})$, $u_t$, $z_t$
\FORALL{$x_t$}
    \STATE $bel(x_t) = \eta \, p(z_t | x_t) \int p(x_t | u_t, x_{t-1}) \, bel(x_{t-1}) \, dx$
\ENDFOR
\RETURN $bel(x_t)$
\end{algorithmic}
\end{algorithm}
```
