# Policy Gradient

## Important Equations 
$$
\begin{equation}
p_\theta(s_1,a_1,\dots,s_T,a_T)=p(s_1)\prod_{t=1}^T\pi_\theta(a_t|s_t)p(s_{t+1}|s_t,a_t)
\end{equation}
$$

## Objective Function

$$ 
J(\theta)=E_{\pi}\left[ \sum_t r_t \right] \tag{1}\label{eq:1}
$$

$\theta$ is the parameter of policy.

If we want to calculate the approximation of the objective function, we can sample trajectories from the policy to get the expectation.

$$J(\theta)\approx \frac{1}{N}\sum^N_{i=1} \sum_t r^i_t$$

This approximation is trivial and fast.

## Direct Policy Differentiation

We calculate the gradient directly from the objective function $\eqref{eq:1}$

$$
\begin{equation*}
\begin{split}
J(\theta) &= E_{\tau\sim p_\theta(\tau)}\left[ r({\tau}) \right]\\
&=\int p_\theta(\tau)r(\tau)d\tau\\
\end{split}
\end{equation*}
$$

where $r(\tau) = \sum_{t=1}^T r(s_t,a_t)$

$$
\begin{align*}
\nabla_\theta J(\theta) &=\nabla_\theta \int p_\theta(\tau)r(\tau)d\tau\\
&= \int \nabla_\theta p_\theta(\tau)r(\tau)d\tau \\
&= \int p_\theta(\tau) \nabla_\theta \log p_\theta(\tau)r(\tau)d\tau \tag{2}\label{eq:2}
\end{align*}
$$

test ref $\eqref{eq:2}$
1
11
11
11
11
11
11
11
11
11
11
11
11
11
11
11
11
1
1
11
11
11
11
11
11
11
11
11
11
11
11
11
11
11
11
1
1
11
11
11
11
11
11
11
11
11
11
11
11
11
11
11
11
1
1
11
11
11
11
11
11
11
11
11
11
11
11
11
11
11
11
1
1
11
11
11
11
11
11
11
11
11
11
11
11
11
11
11
11
1
$\eqref{eq:1}$