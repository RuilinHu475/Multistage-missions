# Reference trajectories and disturbance specifications

Simulation settings accompanying **Augmented Predictive and Sliding-Mode Control for Cooperative Trajectory Tracking of Underactuated USV-AUV Systems in Multistage Missions**.

[Download the PDF version](simulation_setup.pdf)

## Reference trajectories

The USV follows a counterclockwise circle with periodically varying tangential speed:

$$
\begin{aligned}
\boldsymbol p_{d,u}(t)&=
R\begin{bmatrix}\cos\vartheta_d(t)\\1+\sin\vartheta_d(t)\end{bmatrix},\\
\dot{\vartheta}_d(t)&=\frac{2\pi}{300}
\left[1+0.454\sin\left(\frac{\pi t}{25}\right)
-0.09\cos\left(\frac{2\pi t}{25}\right)\right],\\
R&=26.26\ {\rm m},\qquad \vartheta_d(0)=-\frac{\pi}{2}.
\end{aligned}
$$

The AUV horizontal reference is the transmitted USV position, with the position reference given by

$$
\boldsymbol p_{d,a}(t_k)=
\begin{bmatrix}x_u(t_k)\\y_u(t_k)\\z_d(t_k)\end{bmatrix}.
$$

Its depth reference is

$$
z_d(t)=\begin{cases}
-\zeta(t),&0\leq t<100,\\
-18,&100\leq t<200,\\
-18+\zeta(t-200),&200\leq t\leq300.
\end{cases}
$$

where

$$
\begin{aligned}
\zeta(\tau)&=0.25\int_0^\tau
c\left(\frac{s}{28}\right)c\left(\frac{100-s}{28}\right)\,{\rm d}s,\\
c(r)&=\begin{cases}
0,&r<0,\\
\dfrac{1-\cos(\pi r)}{2},&0\leq r\leq1,\\
1,&r>1.
\end{cases}
\end{aligned}
$$

The search, operation, and return stages occupy 0-100 s, 100-200 s, and 200-300 s, respectively. The prescribed working depth is 18 m below the surface.

## Environmental disturbances

For the USV,

$$
\boldsymbol d_u(t)=\begin{bmatrix}
1.3+2\sin(0.02t)+1.5\sin(0.1t)\\
0.6\sin(0.3t+\pi/6)\\
-\sin(0.09t+\pi/3)-4\sin(0.01t)
\end{bmatrix}.
$$

For the AUV,

$$
\begin{aligned}
\boldsymbol d_a(t)&=0.05\begin{bmatrix}
m_{a11}d(t)\\m_{a22}d(t)\\m_{a33}d(t)\\m_{a55}d(t)\\m_{a66}d(t)
\end{bmatrix},\\
d(t)&=\sin(0.02t+\pi/3).
\end{aligned}
$$

The coefficients $m_{a11}$, $m_{a22}$, $m_{a33}$, $m_{a55}$, and $m_{a66}$ are the corresponding diagonal entries of the AUV inertia matrix.

| Vehicle | Disturbance component order |
|---|---|
| USV | Surge force, sway force, yaw moment |
| AUV | Surge force, sway force, heave force, pitch moment, yaw moment |

Time is in seconds, positions are in metres, force components are in N, and moment components are in N m.
