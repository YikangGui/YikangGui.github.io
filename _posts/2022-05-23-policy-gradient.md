# Policy Gradient

## Important Equations <a name="important-equations"></a>

$$
p_\theta(\tau)=p_\theta(s_1,a_1,\dots,s_T,a_T)=p(s_1)\prod_{t=1}^T\pi_\theta(a_t|s_t)p(s_{t+1}|s_t,a_t)\label{eq:*}
$$

$$
\begin{equation}
\begin{split}
\theta^* &=\arg\max_\theta E_{\tau\sim p_\theta(\tau)}\left[\sum_tr(s_t,a_t)\right]\\
&=\arg\max_\theta \sum_{t=1}^T E_{(s_t,a_t)\sim p_\theta(s_t,a_t)}\left[ r(s_t,a_t) \right]
\end{split}
\end{equation}
$$

$$
p((s_{t+1},a_{t+1})|(s_t,a_t)) = p(s_{t+1}|s_t,a_t)\pi_\theta(a_{t+1}|s_{t+1})
$$

### Definition: Q - function
$$
Q^\pi(s_t,a_t)=\sum_{t^\prime=t}^T E_{\pi_\theta}\left[ r(s_{t^\prime}, a_{t^\prime})|s_t,a_t \right]
$$

Total reward from taking $a_t$ in $s_t$

### Definition: Value function

$$
\begin{align}
V^\pi(s_t)&=\sum_{t^\prime=t}^T E_{\pi_\theta}\left[ r(s_{t^\prime}, a_{t^\prime})|s_t \right]\\
&=E_{a_t\sim \pi(a_t|s_t)}\left[ Q^\pi(s_t,a_t) \right]
\end{align}
$$

which means taking the expectation of the Q-function over the distribution of actions given the policy.

**Note:** $E_{s_1\sim p(s_1)}\left[ V^\pi(s_1)\right]$ is the RL objectives.

## Objective Function

$$ 
J(\theta)=E_{\pi}\left[ \sum_t r_t \right] \tag{1}\label{eq:objective}
$$

$\theta$ is the parameter of policy.

If we want to calculate the approximation of the objective function, we can sample trajectories from the policy to get the expectation.

$$J(\theta)\approx \frac{1}{N}\sum^N_{i=1} \sum_t r^i_t$$

This approximation is trivial and fast.

## Direct Policy Differentiation (REINFORCE) <a name='REINFORCE'></a>

We calculate the gradient directly from the objective function $\eqref{eq:objective}$

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
\begin{align}
\nabla_\theta J(\theta) &=\nabla_\theta \int p_\theta(\tau)r(\tau)d\tau\\
&= \int \nabla_\theta p_\theta(\tau)r(\tau)d\tau \\
&= \int p_\theta(\tau) \nabla_\theta \log p_\theta(\tau)r(\tau)d\tau\\
&=E_{\tau\sim p_\theta(\tau)}\left[\nabla_\theta\log p_\theta(\tau)r(\tau)\right]\\
&=E_{\tau\sim p_\theta(\tau)}\left[\left(\sum_{t=1}^T\nabla_\theta\log\pi_\theta(a_t|s_t)\right) \left(\sum_{t=1}^T r(s_t,a_t)\right)\right]\\
&\approx\frac{1}{N}\sum_{i=1}^N\left(\sum_{t=1}^T\nabla_\theta\log\pi_\theta(a_t^i|s_t^i)\right) \left(\sum_{t=1}^T r(s_t^i,a_t^i)\right) 
\end{align}
$$

