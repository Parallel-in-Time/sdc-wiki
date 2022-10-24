# Preconditioners for Spectral Deferred Corrections
Preconditioners are vital for ensuring fast convergence and stable iterations in SDC.
However, it does not appear that there is a universally best choice.
In fact, developing preconditioners is still an active area of research.
Here, we want to shed some light on various aspects of preconditioners, which can appear obscure.

## Interpretation of preconditioners in SDC
In SDC, the interpretation of the preconditioner can become quite obscure when looking only at the simplified derivation of SDC as shown for instance in the [pySDC paper](https://doi.org/10.1145/3310410).
Here, SDC is derived in four steps to solve the initial value problem $\partial_t u=F(t, u)$, $u(0)=u_0$:
 - Integrate both sides of the initial value problem with respect to time
 - Discretize with a quadrature rule
 - Form Picard iteration
 - Precondition the system

Finally, one arrives at this formula for performing a sweep:

$$
(I - \Delta t Q_\Delta)(u^{k+1}) = u_0 + \Delta t(Q-Q_\Delta)F(u^k),
$$

where $k$ is the iteration index, $Q$ realizes the quadrature rule and $Q_\Delta$ is the preconditioner.

It becomes perfectly obvious that a lower triangular $Q_\Delta$ is useful, such that we can solve the system with forward substitution and it is clear how to implement this from this equation, but since the preconditioner appears on both sides, it is difficult to interpret.
Why would implicit Euler be a good preconditioner for this system?
What are we actually integrating with implicit Euler here?

To understand this, it makes sense to go through the [original derivation](https://doi.org/10.1023/A:1022338906936) of SDC from Dutt et al.
We do not need to understand all the nuances, but the crucial point is that the update between sweeps is

$$
u^{k+1} = u^{k} + \delta^{k+1},
$$

where $\delta^{k+1}$ is the error of iteration $k$.
This is the "deferred correction" part in spectral deferred corrections.
Instead of solving the original equation, we are solving an equation for the error and adding correction terms to the approximate solution to make it more accurate.

In section 2.1, of the Dutt et al. paper, are the crucial steps outlining how to arrive at the equation for the error.
We only present the result here:

$$
\delta^{k+1}(t) - \int_0^t\left(F(\tau, u^k(\tau) + \delta^{k+1}(\tau)) - F(\tau, u^{k}(\tau))\right) d\tau = r^k(t),\\
r^k(t) = u_0 + \int_0^t F(\tau, u^k(\tau))d\tau - u^k(t)
$$

where $r^k$ is the residual after $k$ iterations.

The next step is to descretize the integrals with quadrature rules.
Since the residual only depends on the iteration that we already know, we do not need to solve any system but just evaluate the right hand side at the quadrature nodes.
While this is also not computationally free, evaluating this with very high accuracy is crucial to solving the equation for the error accurately, so we do this with the full (and dense) quadrature rule $Q$.

Now for solving the error equation at $t=\Delta t$, we get a system of equations that requires solving and this is precisely where we put in the preconditioner $Q_\Delta$ as a simplified quadrature rule that is easier to apply.
The resulting system is:

$$
\delta^{k+1} = r^k + \Delta t Q_\Delta(F(u^k + \delta^{k+1}) - F(u^k)),\\
r^k = u_0 + \Delta t QF(u^k) - u^k.
$$

Now let's plug this into the update formula where we add the corrections:

$$
u^{k+1} = u^{k} + \delta^{k+1} = u^{k} + u_0 + \Delta t QF(u^k) - u^k + \Delta t Q_\Delta(F(u^k + \delta^{k+1}) - F(u^k)).
$$

We see that the $u^k$ on the right hand side cancel, and we plug in the update formula on the right to replace the argument of $F(\Delta t, u^k + \delta^{k+1})$ with $F(\Delta t, u^{k+1}).$
We end up with

$$
u^{k+1} = u_0 + \Delta t QF(u^k) + \Delta t Q_\Delta(F(u^{k+1}) - F(u^k)),
$$

which becomes exactly the formula from the simple derivation if we move both $u^{k+1}$ terms to the left hand side.

Following these extra steps makes clear that we are still solving an equation for the defect with the preconditioner and then correcting the solution with the computed defect, even though it becomes obscure in the final equation.
Another fact becomes apparent: The accuracy of computing the corrections is limited by how well we can compute the residual, which, in turn, depends on the accuracy of the full quadrature rule.

## Popular choices for preconditioners
:hammer_and_wrench: In construction ...

## Assembling a time marching scheme into a quadrature matrix
:hammer_and_wrench: In construction ...

## Parallel SDC across the method: Diagonal preconditioners
:hammer_and_wrench: In construction ...