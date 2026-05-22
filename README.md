# Self-Similar Solutions to the Thin-Film Equation

This notebook investigates the numerical construction of self-similar source-type solutions to the one-dimensional thin-film equation. The thin-film equation describes how a fluid that is very thin in height compared to the length travels over time on a one-dimensional flat solid surface. We consider the source-type thin-film equation

$$
\begin{aligned}
\partial_t u
&=
-\partial_x\left(|u|^n \partial_x^3 u\right),
\qquad x\in\mathbb{R}, \quad & t>0,
\\
u(x,0)
&=
c\delta(x),
\qquad & x\in\mathbb{R},
\end{aligned}
$$

where $u(x,t)$ denotes the film height and $n>0$ is the mobility exponent.

The solution is expected to have the self-similar form 

$$
u(x,t) = t^{-\alpha}f(\mu), \qquad \mu = xt^{-\alpha}, \qquad \alpha=\frac{1}{n+4}.
$$

Substituting this into the thin-film equation reduces the PDE to the nonlinear ODE

$$
\begin{aligned}
& (|f(\mu)|^nf'''(\mu))' = \alpha (\mu f(\mu))', \qquad & \text{for } -\infty < \mu < \infty, \\
& \mu f(\mu) \to 0, \qquad & \text{as } \mu \to \pm \infty.
\end{aligned}
$$

Exploiting the scaling properties of the equation and rescaling the variables reduces the ODE to

$$
\begin{cases}
u^{n-1}u^{\prime\prime\prime} = x,
& u>0,
\quad 0<x<a,
\\
u(0)=1,
\quad
u^\prime(0)=0,
\\
u(a)=0,
\quad
u^\prime(a)=0.
\end{cases}
$$

The solution is symmetric and strictly decreasing on the interval $0<x<a$. A nontrivial compactly supported solution exists and is unique only for $0<n<3$.

The goal is to numerically construct compactly supported, symmetric, nonnegative self-similar solutions satisfying the required boundary and mass conditions.

<br>
<br>

To numerically construct the self-similar solution, we note that the location of the free boundary $x=a$ is unknown beforehand. Therefore, the problem is a free-boundary problem: both the solution $u(x)$ and the endpoint $a$ satisfying

$$
u(a)=0,
\qquad
u'(a)=0
$$

must be determined simultaneously.

To overcome this difficulty, the nonlinear boundary value problem is reformulated as a shooting problem. Instead of prescribing the free boundary location $a$, we prescribe an initial curvature parameter $\gamma$ and solve the corresponding initial value problem

$$
\begin{cases}
u''' = xu^{1-n},
& u>0,
\qquad x>0,
\\
u(0)=1,
\qquad
u'(0)=0,
\qquad
u''(0)=-\gamma,
\end{cases}
$$

where $\gamma>0$ is the shooting parameter.

For each choice of $\gamma$, the resulting initial value problem is integrated numerically. Depending on the value of $\gamma$, the solution may:
- remain positive,
- become negative,
- or touch zero with the desired free-boundary behavior.

The correct value of $\gamma$ is determined using a bisection-based shooting procedure. Two initial values $\gamma_-$ and $\gamma_+$ are chosen such that the corresponding solutions exhibit qualitatively different behavior. For example:
- $\gamma_-$ produces a solution for which there exists a point $b$ satisfying $u(b)=0$ and $u'(b)<0$,
- $\gamma_+$ produces a solution for which there exists a point $b$ satisfying $u(b)>0$ and $u'(b)=0$.

The interval $[\gamma_+,\gamma_-]$ is repeatedly refined until the critical value of $\gamma$ producing the desired compactly supported self-similar solution is obtained.

<br>
<br>

This project was developed as part of my bachelor thesis at TU Delft.

- [Self-Similar Solutions to the Thin-Film Equation](thesis/Bachelor_Thesis_Yordi_Boesveld.pdf)

## Implemented Methods

- Shooting method for the nonlinear free-boundary problem
- Bisection method for determining the shooting parameter
- Numerical ODE integration
- Free-boundary detection
- Rescaling to satisfy the prescribed mass

## Results

The notebook contains:

- Numerical self-similar profiles for multiple values of $n$
- Compactly supported thin-film solutions
- Visualization of the free-boundary location
- Comparison of solution behavior for different mobility exponents
- Plots of the constructed droplet profiles

The experiments illustrate how the mobility exponent affects the shape, support, and spreading behavior of the self-similar thin-film solution.

## Running the Project

The project was developed and tested using Python 3.12. Install the required packages: pip install -r requirements.txt

Open the notebook:

jupyter notebook notebooks/helmholtz_iterative_solvers.ipynb

Run all notebook cells sequentially to reproduce the numerical experiments and self-similar solution figures.
