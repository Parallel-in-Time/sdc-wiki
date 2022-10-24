_:postal_horn: This project intends to accumulate theoretical content and literature references on SDC and related time integration methods, using Markdown-based wiki pages. Its goal is to be an evolving source of knowledge, that could be used by people starting to learn about SDC, or eventually specialists in this field. **Any contribution to improve it is very welcome !**_

Spectral Deferred Correction (SDC) methods are a class of time-stepping algorithm allowing to approximate the solution of initial value problem of the form :

$$
\frac{du}{dt} = f(u,t),\quad t \in [0, T],\quad u(0) = u_0
$$

Those can Ordinary Differential Equations (ODEs) or systems of ODEs resulting from the partial discretization of Partial Differential Equations (PDEs).
SDC was originally introduced in 2000 [[1]](#ref1), based on the previously known Deferred Correction method, and allows to easily build time integration schemes with _piloted order of accuracy (from low to high)_.
It has received a particular attention since then, _e.g_ for the development of Implicit-Explicit (IMEX) time integration scheme [[2]](#ref2) or parallel-in-time methods [[3]](#ref3).
Many variants have been developed since, and this Wiki intends to provide a extended state-of-the art overview of SDC methods and their implementations.

## Table of content

:hammer_and_wrench: In construction ...

### To get started

1. Picard Formulation and Collocation methods 
2. Deferred Correction method and Gauss quadrature
3. [SDC sweep and preconditionners](./preconditioners.md)
4. Time-stepping and prolongation

### Advanced concepts

1. Error analysis and accuracy order
1. Algebraic representation
2. Node-to-node and zero-to-node formulation
3. High order SDC sweep
4. Numerical linear stability

### SDC variants

1. IMEX-SDC
2. Second Order Boris SDC
3. Adaptive and Fault-tolerant SDC
4. SDC for first order system of ODE's with mass matrix

### Parallel-in-time integration

1. Combining Parareal and SDC 
2. Multilevel-SDC
3. Parallel Full Approximation Scheme in Space and Time (PFASST)
4. Revisionist Integral Deferred Correction (RIDC)
5. Block Gauss-Seidel SDC

<a id="ref1">[1]</a> _Dutt, A., Greengard, L., & Rokhlin, V. (2000). [Spectral deferred correction methods for ordinary differential equations](https://link.springer.com/content/pdf/10.1023/A:1022338906936.pdf). BIT Numerical Mathematics, 40(2), 241-266._

<a id="ref2">[2]</a> _Minion, M. L. (2003). [Semi-implicit spectral deferred correction methods for ordinary differential equations](https://projecteuclid.org/journals/communications-in-mathematical-sciences/volume-1/issue-3/Semi-implicit-spectral-deferred-correction-methods-for-ordinary-differential-equations/cms/1250880097.pdf). Communications in Mathematical Sciences, 1(3), 471-500._

<a id="ref3">[3]</a> _Emmett, M., & Minion, M. (2012). [Toward an efficient parallel in time method for partial differential equations](https://projecteuclid.org/journals/communications-in-applied-mathematics-and-computational-science/volume-7/issue-1/Toward-an-efficient-parallel-in-time-method-for-partial-differential/10.2140/camcos.2012.7.105.pdf). Communications in Applied Mathematics and Computational Science, 7(1), 105-132._