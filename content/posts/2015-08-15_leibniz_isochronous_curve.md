---
title: "A derivation of the Leibniz isochronous curve"
date: 2020-08-15T12:43:36-04:00
draft: false
tags: ["mathematics", "physics", "variational-methods", "lagrangian"]
---

Recently, a friend of mine shared with me the idea of the Leibniz isochronous curve.
In words, this is the trajectory a frictionless object would follow if its vertical
velocity was left unchanged by a constant, downward force. Using the standard
\\(x\\)-\\(y\\) Cartesian axes, the curve is parameterized by

$$\begin{aligned}x &= x(t)\\\y &= -v_0t\end{aligned}$$

where \\(v_0\\) is positive. What is the exact expression for \\(x(t)\\)?

The Lagrangian approach is usually emphasized when there are obvious constraints,
so let's try that method here. Lets assume the trajectory can be written
\\(x = x(y(t))\\).

Using the usual \\(\mathcal{L} = T - V\\) for a point mass under the influence of gravity, we have

$$\begin{aligned}
\mathcal{L} &= \frac{1}{2}m(\dot{x}^2 + \dot{y}^2) - mgy \\\ \\\ &= \frac{1}{2}m\dot{y}^2\Big(\Big(\frac{\mathrm{d}x}{\mathrm{d}y}\Big)^2 + 1\Big) - mgy
\end{aligned}$$

The partial derivatives of this with respect to \\(y\\) and \\(\dot{y}\\) are

$$\begin{aligned}
\frac{\partial\mathcal{L}}{\partial y} &= m\dot{y}^2\frac{\mathrm{d}x}{\mathrm{d}y}\frac{\mathrm{d}^2x}{\mathrm{d}y^2} - mg \\\ \\\ \frac{\partial\mathcal{L}}{\partial \dot{y}} &= m\dot{y}\Big(\Big(\frac{\mathrm{d}x}{\mathrm{d}y}\Big)^2 + 1\Big)
\end{aligned}$$

and so the full Euler-Lagrange equation is

$$m\dot{y}^2\frac{\mathrm{d}x}{\mathrm{d}y}\frac{\mathrm{d}^2x}{\mathrm{d}y^2} - mg - m\ddot{y}\Big(\Big(\frac{\mathrm{d}x}{\mathrm{d}y}\Big)^2 + 1\Big) - 2m\dot{y}^2\frac{\mathrm{d}x}{\mathrm{d}y}\frac{\mathrm{d}^2x}{\mathrm{d}y^2} = 0.$$

There are a few things we can do to simplify this. For one, we can combine the first and last terms. On top of that, \\(\dot{y} = -v_0\\) and \\(\ddot{y} = 0\\). We also see that

$$ \frac{\mathrm{d}}{\mathrm{d}y} = \frac{\mathrm{d}t}{\mathrm{d}y}\frac{\mathrm{d}}{\mathrm{d}t} = -\frac{1}{v_0}\frac{\mathrm{d}}{\mathrm{d}t}.$$

Making the above substitutions (and writing everything in terms of \\(x\\) and \\(t\\)) reduces the Euler-Lagrange equation to 

$$-mv_0^2\cdot\frac{\dot{x}}{-v_0}\cdot\frac{\ddot{x}}{v_0^2} - mg = 0.$$

Canceling common factors and rewriting \\(\dot{x}\ddot{x}\\) as \\(\frac{1}{2}\frac{\mathrm{d}}{\mathrm{d}t}(\dot{x})^2\\) further simplifies this to

$$\frac{1}{2}\frac{\mathrm{d}}{\mathrm{d}t}(\dot{x}^2) = gv_0$$

which can be easily integrated to get

$$\dot{x}^2 = 2gv_0t.$$

We can take the square root and integrate again to arrive at 

$$x(t) = \frac{2}{3}\sqrt{2gv_ot^3}.$$

We're done! For ease of plotting, we can rewrite \\(t\\) in terms of \\(y\\) to get

$$y^3 = -\frac{9}{8}\frac{v_0^2}{g}x^2$$
