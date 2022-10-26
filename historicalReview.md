# Historical review of SDC

_This page is based on reviews done by [[Ong22](#ong22), [Skeel82](#skeel82)] with additional elements from other contributions._

## 1940 - 2000 : Genesis and development of Deferred Correction methods

### Introduction of the method and first steps

In the 1940's, using an inspiration from "relaxation methods" used for simultaneous algebraic equations, Fox introduced a "difference correction method" [[Fox47](#fox47)] intending to solve ordinary and partial differential equations.
Noting that derivatives are infinite series of differences, such that truncated version of those series are simply finite-difference approximations, Fox uses approximations of different orders to estimate a correction term allowing to improve the accuracy of a first approximate solution.
Its method is later called "Deferred Correction" (DC), and its correction term turns out to be an estimate of the locale discretization error [[Skeel82](#skeel82)].
The main advantage of this method is to _"allow an improvement of the accuracy of finite-difference solutions without increasing the complexity of the algebraic systems required for the solution"_ [[Ong22](#ong22)].
But its main default lays on the use of high-order finite differences to compute the correction term,
which requires solution values outside of the domain of integration and is prone to non-negligible round-off errors with equi-spaced grids.

While [[Fox47](#fox47)] uses DC for Boundary Value Problem (BVP) and eigenvalue problems linked to ODE, the approach was applied for Initial Value Problem (IVP) in [[Fox49](#fox49)].
Additionnaly, Pereyra generalized DC to functionnal equations in [[Pereyra66](#pereyra66)] and applied it to specific types of BVPs in [[Pereyra68](#pereyra68)].
A decade after, Skeel credited Pereyra for a renewed perspective on DC methods, as he was _"the first to put the deferred correction procedure into a general and mathematically
rigorous setting"_ and his _"theoretical and practical contributions did much to revive interest in the idea"_ [[Skeel82](#skeel82)].
Even if DC methods where usually referred to "Fox and Pereyra" method at that time, we can also mention a similar contribution of [[Hausman47](#hausman47)] who introduced a DC-like method with a different approach to estimate the correction term.
Finally, a proper definition of DC was given by Mayers in the book of Fox [[Fox62](#fox62)] :

> "_An alternative method, of deferred correction, uses approximate formulae to find a first approximation to the required solution in the complete range of integration._
> _The local truncation errors are assessed from this approximation and included in a correcting run, which again is repeated as often as necessary._"

### Early developments and applications

With the main theoretical basis brought by Pereyra,
many contributions were added to the field of DC methods.
Zadunaisky considered in [[Zadunaisky66](#zadunaisky66)]
an alternative DC method mentionned as "defect correction", where the correction term does not include the computation of local truncation error, but requires an interpolation of the numerical solution. Those interpolations are prone to numerical problem for large equi-spaced grids and solved using a decomposition into several interpolation intervals [[Zadunaisky76](#zadunaisky76)].
This idea was generalized by [[Stetter74](#stetter74)] who consider adding error approximation
to the numerical solution to form a new one.
Its algorithm was referred later as "Classical Deferred Correction" [[Ong22](#ong22)],
and motivated extended analysis from [[Lindberg76](#lindberg76), [Frank77a](#frank77a)] as long as new variation of DC methods, _e.g_ with [[Frank76](#frank76), [Frank77b](#frank77b)].
Skeel also brought its contributions, along with a thorough review of the different DC approaches at that time [[Skeel82](#skeel82)].
All those developments were mostly focused on proving the convergence of each DC flavours, as well as searching for more efficient technics to compute the error correction term, or _"defect"_.


DC methods have been since then applied to many types of problem, among them :

- Ordinary Differential Equations
  - Initial Value Problems : [[Fox49](#fox49), [Dutt00](#dutt00), [Hansen11](#hansen11), [Christlieb09](#christlieb09), [Christlieb10a](#christlieb10a), [Christlieb10b](#christlieb10b)]
  - Boundary Value Problems : [[Fox47](#fox47), [Pereyra66](#pereyra66), [Pereyra68](#pereyra68)]
- Partial Differential Equations : [[Fox47](#fox47), [Kress02](#kress02), [Rangan03](#rangan03)]
- Differential-Algebraic Equations : [[Huang06](#huang06), [Rangan03](#rangan03)]
- Eigenvalue problems : [[Fox49](#fox49), [Chu81](#chu81)]

They have also be used in conjunction with :

- linear multistep methods : [[Geng85](#geng85)]
- Krylov subspace methods : [[Huang06](#huang06), [Bu12](#bu12)]
- splitting methods : [[Hansen11](#hansen11)]

Usually, interpolation is done in DC methods using Lagrange polynomials, which appears to be the most classical approach. The use of rational functions for interpolant were also considered by [[Güttel13](#guettel13)], as well as continuous extensions and splines in [[Ong22](#ong22)].

## 2000 - 2012 : Introducing SDC and its first applications

:hammer_and_wrench: In construction ...

## 2012 - now : SDC as major component for parallel-in-time integration

:hammer_and_wrench: In construction ...

[<a id="ong22">Ong22</a>] _Ong, B. W., & Spiteri, R. J. (2020). [Deferred correction methods for ordinary differential equations](https://link.springer.com/content/pdf/10.1007/s10915-020-01235-8.pdf). Journal of Scientific Computing, 83(3), 1-29._

[<a id="fox47">Fox47</a>] _Fox, L. (1947). [Some improvements in the use of relaxation methods for the solution of ordinary and partial differential equations](https://royalsocietypublishing.org/doi/pdf/10.1098/rspa.1947.0060). Proceedings of the Royal Society of London. Series A. Mathematical and Physical Sciences, 190(1020), 31-59._

[<a id="skeel82">Skeel82</a>] _Skeel, R. D. (1982). [A theoretical framework for proving accuracy results for deferred corrections](https://doi.org/10.1137/0719009). SIAM Journal on Numerical Analysis, 19(1), 171-196_

[<a id="fox49">Fox49</a>] _Fox, L., & Goodwin, E. T. (1949, July). [Some new methods for the numerical integration of ordinary differential equations](https://www.cambridge.org/core/services/aop-cambridge-core/content/view/01540A9AB523A969D6F2019CC10F9FED/S0305004100025007a.pdf/div-class-title-some-new-methods-for-the-numerical-integration-of-ordinary-differential-equations-div.pdf). In Mathematical Proceedings of the Cambridge Philosophical Society (Vol. 45, No. 3, pp. 373-388). Cambridge University Press._

[<a id="fox62">Fox62</a>] _Fox, L. (1962). [Numerical solution of ordinary and partial differential equations: based on a summer school held in Oxford, August-September 1961](https://books.google.ch/books?hl=de&lr=&id=mHTiBQAAQBAJ&oi=fnd&pg=PP1&dq=Numerical+Solution+of+Ordinary+and+Partial+Differential+Equations+fox&ots=Dw-4YYLSM6&sig=MednN8EdIm3wEC0o6dnliDqb5I8). Pergamon Press,
Oxford._

[<a id="pereyra66">Pereyra66</a>] _Pereyra, V. (1966). [On improving an approximate solution of a functional equation by deferred corrections](https://link.springer.com/content/pdf/10.1007/BF02162981.pdf). Numerische Mathematik, 8(4), 376-391._

[<a id="pereyra68">Pereyra68</a>] _Pereyna, V. (1968). [Iterated deferred corrections for nonlinear boundary value problems](https://link.springer.com/content/pdf/10.1007/BF02165307.pdf). Numerische Mathematik, 11(2), 111-125._

[<a id="hausman47">Hausman47</a>] _Hausman, L. F., & Schwarzschild, M. (1947). [Automatic Integration of Linear Sixth‐Order Differential Equations by Means of Punched‐Card Machines](https://aip.scitation.org/doi/pdf/10.1063/1.1740873). Review of Scientific Instruments, 18(12), 877-883._

[<a id="zadunaisky66">Zadunaisky66</a>] _Zadunaisky, P. E. (1966). [A method for the estimation of errors propagated in the numerical solution of a system of ordinary differential equations](https://adsabs.harvard.edu/pdf/1966IAUS...25..281Z). In The Theory of Orbits in the Solar System and in Stellar Systems (Vol. 25, p. 281)._

[<a id="zadunaisky76">Zadunaisky76</a>] _Zadunaisky, P. E. (1976). [On the estimation of errors propagated in the numerical integration of ordinary differential equations](https://link.springer.com/content/pdf/10.1007/BF01399082.pdf). Numerische Mathematik, 27(1), 21-39._

[<a id="stetter74">Stetter74</a>] _Stetter, H. J. (1974). Economical global error estimation. In Stiff differential systems (pp. 245-258). Springer, Boston, MA._

[<a id="lindberg76">Lindberg76</a>] _Lindberg, B. (1976). Error Estimation and Iterative Improvement for the Numerical Solution of Operator Equations. ILLINOIS UNIV AT URBANA-CHAMPAIGN DEPT OF COMPUTER SCIENCE._

[<a id="frank76">Frank76</a>] _Frank, R., Hertling, J., & Ueberhuber, C. W. Iterated Defect Correction based on Estimates of the Local Discretization Error Report Nr. 18/76, Inst. f. Num. Math. Technical University of Vienna._

[<a id="frank77a">Frank77a</a>] _Frank, R., Hertling, J., & Ueberhuber, C. W. (1977). An extension of the applicability of iterated deffered corrections. Mathematics of Computation, 31(140), 907-915._

[<a id="frank77b">Frank77b</a>] _Frank, R., & Ueberhuber, C. W. (1977). [Iterated defect correction for the efficient solution of stiff systems of ordinary differential equations](https://doi.org/10.1007/BF01932286). BIT Numerical Mathematics, 17(2), 146-159._

[<a id="guettel13">Güttel13</a>] _Güttel, S., & Klein, G. (2013). Efficient high-order rational integration and deferred correction with equispaced data._

[<a id="christlieb09">Christlieb09</a>] _Christlieb, A., Ong, B., & Qiu, J. M. (2009). [Comments on high-order integrators embedded within integral deferred correction methods](https://doi.org/10.2140/camcos.2009.4.27). Communications in Applied Mathematics and Computational Science, 4(1), 27-56._

[<a id="christlieb10a">Christlieb10a</a>] _Christlieb, A., Ong, B., & Qiu, J. M. (2010). [Integral deferred correction methods constructed with high order Runge–Kutta integrators](https://doi.org/10.1090/S0025-5718-09-02276-5). Mathematics of Computation, 79(270), 761-783._

[<a id="christlieb10b">Christlieb10b</a>] _Christlieb, A. J., Macdonald, C. B., & Ong, B. W. (2010). [Parallel high-order integrators](https://doi.org/10.1137/09075740X). SIAM Journal on Scientific Computing, 32(2), 818-835._

[<a id="dutt00">Dutt00</a>]  _Dutt, A., Greengard, L., & Rokhlin, V. (2000). [Spectral deferred correction methods for ordinary differential equations](https://doi.org/10.1023/A:1022338906936). BIT Numerical Mathematics, 40(2), 241-266._

[<a id="hansen11">Hansen11</a>] _Hansen, A. C., & Strain, J. (2011). [On the order of deferred correction](https://doi.org/10.1016/j.apnum.2011.04.001). Applied numerical mathematics, 61(8), 961-973._

[<a id="kress02">Kress02</a>] _Kress, W., & Gustafsson, B. (2002). [Deferred correction methods for initial boundary value problems](https://doi.org/10.1023/A:1015113017248). Journal of scientific computing, 17(1), 241-251._

[<a id="rangan03">Rangan03</a>] _Rangan, A. V. (2003). Adaptive solvers for partial differential and differential-algebraic equations. University of California, Berkeley (PhD Thesis)._

[<a id="huang03">Huang06</a>] _Huang, J., Jia, J., & Minion, M. (2006). [Accelerating the convergence of spectral deferred correction methods](https://doi.org/10.1016/j.jcp.2005.10.004). Journal of Computational Physics, 214(2), 633-656._

[<a id="chu81">Chu81</a>] _Chu, K. W., & Spence, A. (1981). [Deferred correction for the integral equation eigenvalue problem](https://doi.org/10.1017/S0334270000002812). The ANZIAM Journal, 22(4), 474-487._

[<a id="geng85">Geng85</a>] _Geng, S. (1985). The deferred correction procedure for linear multistep formulas. Journal of Computational Mathematics, 41-49._

[<a id="bu12">Bu12</a>] _Bu, S., Huang, J., & Minion, M. (2012). [Semi-implicit Krylov deferred correction methods for differential algebraic equations](https://doi.org/10.1090/S0025-5718-2012-02564-6). Mathematics of Computation, 81(280), 2127-2157._