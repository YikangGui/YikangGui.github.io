# Policy Gradient
## Objective Function
$$J(\theta)=E_{\pi}\left[ \sum_t r_t \right]$$
$\theta$ is the parameter of policy.

If we want to calculate the approximation of the objective function, we can sample trajectories from the policy to get the expectation.

$$J(\theta)\approx \frac{1}{N}\sum^N_{i=1} \sum_t r^i_t$$

This approximation is trivial and fast.

## Direct Policy Differentiation
$$
\begin{align}
J(\theta) &= E_{\tau\sim p_\theta(\tau)}\left[ r({\tau}) \right]\\
&=\int p_\theta(\tau)r(\tau)d\tau\\
\end{align}
$$

where $r(\tau)=\sum_{t=1}^T r(s_t,a_t)$

$$
\begin{align}
\nabla_\theta J(\theta) &=\nabla_\theta \int p_\theta(\tau)r(\tau)d\tau\\
&= \int \nabla_\theta p_\theta(\tau)r(\tau)d\tau\\
&= \int p_\theta(\tau) \nabla_\theta \log p_\theta(\tau)r(\tau)d\tau \\
\end{align}
$$
