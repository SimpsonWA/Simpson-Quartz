A **graph** is defined as:
$$G=(V,E)$$

where:

- $V = {v_1, v_2, \dots}$ is a set of **vertices** (or **nodes**)
- $E = {e_1, e_2, \dots}$ is a set of **edges**, where each edge $e_k \in E$ is associated with a pair of vertices $(v_i, v_j)$

---

#### 🔹 End Vertices

The pair $(v_i, v_j)$ associated with an edge $e_k$ are called its **end vertices**.

---

#### 🔹 Loop (or Self-Loop)

An edge of the form $(v_i, v_i)$, where both end vertices are the same, is called a **loop** or **self-loop**.

---

#### 🔹 Parallel Edges

Two or more edges that connect the **same pair of vertices** are called **parallel edges** (or **multiple edges**).  
For example:

$$e1=(v1,v2),\quad e2=(v1,v2))$$

---
#### 🔹 Simple Graph

If  a graph doesn't have any loops or parallel edges it is known as a **Simple Graph**

---

## 1.4 Incidence and Degree

### 🔹 Incidence

If a vertex $v_i$ is one of the **end vertices** of an edge $e_k$, then $v_i$ and $e_k$ are said to be **incident** with each other.

---

### 🔹 Adjacent Edges

Two **non-parallel edges** are said to be **adjacent** if they are both incident on the same vertex.

---

### 🔹 Adjacent Vertices

Two vertices $v_i$ and $v_j$ are **adjacent** if they are connected by an edge — that is, if there exists an edge $e_k = (v_i, v_j)$ in the graph.

---

### 🔹 Degree

The **degree** of a vertex $v_i$, denoted by $d(v_i)$, is the **number of edges incident** on $v_i$.

> Note: A **self-loop** is counted **twice**, as it contributes two incidences to the same vertex.

---

### 🔸 Handshaking Lemma

Let a graph $G$ have $n$ vertices and $e$ edges. Since each edge connects two vertices (and therefore contributes two to the total degree count), the sum of the degrees of all vertices is:

$$\sum_{i=1}^{n} d(v_i) = 2e$$

This is known as the **Handshaking Lemma**.

## 1.5 Isolated vertex, Pendant Vertex, Null Graph

### 🔹 Isolated Vertex

An **isolated vertex** is a vertex with **no incident edges**, meaning its **degree is 0**.

---

### 🔹 Pendant Vertex

A **pendant vertex** is a vertex with **degree 1**—that is, it is connected to the graph by **exactly one edge**.

---

### 🔹 Null Graph

A **null graph** is a graph in which the **edge set $E$ is empty**, while the **vertex set $V$ is non-empty**.

$$G = (V, \emptyset), \quad \text{where } V \neq \emptyset$$