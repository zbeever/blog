---
title: "The evolving Harris current sheet model"
date: 2020-08-15T12:57:55-04:00
draft: false
tags: ["space-physics", "electromagnetism"]
---

In many space physics papers investigating nonadiabatic current sheet scattering, the
simplified Harris model is used. In Cartesian coordinates, it takes on the simple form

$$\mathbf{B} = B_x\tanh\Big(\frac{z}{L}\Big)\hat{\mathbf{i}} + 0\hat{\mathbf{j}} + B_z\hat{\mathbf{k}}$$

where \\(L\\) parameterizes the current sheet thickness. This is nice approximation
for a relatively static magnetosphere, but it doesn't capture a thinning current sheet.
For that, we'll need to make the change \\(L=L(t)\\). In turn, this will induce an
electric field. What is the expression for that field?

### Deriving the induced electric field

The induced electric field is described by

$$\nabla\times{\mathbf{E}} = -\frac{\partial\mathbf{B}}{\partial t}.$$

The time derivative of the magnetic field is 

$$\frac{\partial\mathbf{B}}{\partial t} = B_x\mathrm{sech}^2\Big(\frac{z}{L(t)}\Big)\cdot\Big({-\frac{z}{L^2(t)}}\Big)\cdot\dot{L}(t)\hat{\mathbf{i}}$$

and so the only nonzero component of the curl equation is

$$\frac{\partial E_z}{\partial y} - \frac{\partial E_y}{\partial z} = -B_x\mathrm{sech}^2\Big(\frac{z}{L(t)}\Big)\cdot\frac{z}{L^2(t)}\cdot\dot{L}(t).$$

Because the Harris model has no component along the \\(y\\)-axis and doesn't depend
on the \\(y\\) coordinate, \\(\frac{\partial E_z}{\partial y} = 0\\) by symmetry. There
is no such restriction for \\(E_y\\), and so we may integrate to find[^limits]

$$E_y(z) = \int_{-\infty}^z B_x\mathrm{sech}^2\Big(\frac{z}{L(t)}\Big)\cdot\frac{z}{L^2(t)}\cdot\dot{L}(t)\mathrm{d}z.$$

Setting \\(u = z/L(t)\\) and \\(\mathrm{d}u = \mathrm{d}z/L(t)\\), this simplifies to

$$E_y(z) = B_x\dot{L}(t)\int_{-\infty}^{z/L(t)}\mathrm{sech}^2(u)\cdot u\mathrm{d}u.$$

We can integrate this by parts to get

$$E_y(z) = B_x\dot{L}(t)\Big(u\tanh(u)\Big|_{-\infty}^{z/L(t)} - \int_{-\infty}^{z/L(t)}\tanh(u)\mathrm{d}u\Big).$$

The remaining integral can be rewritten as

$$\int_{-\infty}^{z/L(t)}\tanh(u)\mathrm{d}u = \int_{-\infty}^{z/L(t)}\frac{\sinh(u)}{\cosh(u)}\mathrm{d}u = \int_{-\infty}^{z/L(t)}\mathrm{d}(\ln{\cosh(u)}) = \ln\cosh u\Big|_{-\infty}^{z/L(t)}.$$

Using the above, \\(E_y(z)\\) becomes

$$E_y(z) = B_x\dot{L}(t)\Big[\frac{z}{L(t)}\tanh\Big(\frac{z}{L(t)}\Big)- \ln\cosh\Big(\frac{z}{L(t)} \Big) + C\Big]$$

where \\(C\\) is given by

$$C = \lim_{u\to{-\infty}}\ln\cosh u - u\tanh u.$$

Since, by defintion, \\(\cosh u = \frac{e^u + e^{-u}}{2}\\) and \\(\tanh u = \frac{e^u - e^{-u}}{e^u + e^{-u}}\\), we can rewrite \\(C\\) as

$$\begin{aligned}
C &= \lim_{u\to{-\infty}}\ln\frac{e^{-u}}{2} + u\frac{e^{-u}}{e^{-u}} \\\ \\\ &= \lim_{u\to-\infty}-u + u - \ln 2 \\\ \\\ &= {-\ln 2}
\end{aligned}$$

The final expression for the induced field is given by

$$\mathbf{E}(z, t) = B_x\dot{L}(t)\Big[\frac{z}{L(t)}\tanh\Big(\frac{z}{L(t)}\Big)- \ln\cosh\Big(\frac{z}{L(t)} \Big) - \ln 2\Big]\hat{\mathbf{j}}$$
	
A question remains: the Harris model is formulated as an equilibrium solution to the Vlasov
equation. Is a time-dependent model physical? Intuitively, one would venture yes as long as
\\(\dot{L}(t)\\) is sufficiently slow. Certainly the above result captures the real
\\(y\\)-directed current found in the magnetosphere, so it is at least on the right track.
	
### Finding the field lines

The lines of force of a field are useful visualizations. Can we find an expression
for the field lines of the Harris current sheet?

The vector potential is defined (up to the addition of a gradient) by

$$\nabla \times {\mathbf{A}} = \mathbf{B}.$$

In component form, this is

$$\begin{aligned}
\frac{\partial A_z}{\partial y} - \frac{\partial A_y}{\partial z} &= B_x\tanh\Big(\frac{z}{L(t)}\Big) \\\ \\\ \frac{\partial A_x}{\partial z} - \frac{\partial A_z}{\partial x} &= 0 \\\ \\\ \frac{\partial A_y}{\partial x} - \frac{\partial A_x}{\partial y} &= B_z
\end{aligned}$$

By the same argument as in the last section, \\(\mathbf{A}\\) must be independent of \\(y\\),
and so these further reduce to

$$\begin{aligned}
\frac{\partial A_y}{\partial z} &= -B_x\tanh\Big(\frac{z}{L(t)}\Big) \\\ \\\ \frac{\partial A_y}{\partial x} &= B_z 
\end{aligned}$$

Integrating gives

$$\mathbf{A}(x, z, t) = \Big[{-B_xL(t)}\ln\cosh\Big(\frac{z}{L(t)}\Big)+B_zx\Big]\hat{\mathbf{j}}$$

It is well known that we can express the vector potential in terms of two scalar functions
\\(\alpha\\), \\(\beta\\) such that[^euler-potential]

$$\mathbf{A} = \alpha\nabla{\beta},$$

or, equivalently,

$$\mathbf{B} = \nabla{\alpha}\times\nabla{\beta}.$$

This second expression lends itself to a particularly nice geometrical interpretation: since
the gradient of a function is orthogonal to the level sets of that function, \\(\mathbf{B}\\)
must be directed along the intersection of the two implicit surfaces described by

$$\begin{aligned}
\alpha(x, y, z) &= \alpha_0 \\\ \\\ \beta(x, y, z) &= \beta_0
\end{aligned}$$

In the simple case of the Harris model, we can write these scalar functions by inspection,

$$\begin{aligned}
\alpha(x, z) &= -B_xL(t)\ln\cosh\Big(\frac{z}{L(t)}\Big) + B_zx \\\ \\\ \beta(y) &= y
\end{aligned}$$

Of course, these are not unique: we could add a constant to \\(\alpha\\) or any term \\(g\\)
to \\(\beta\\) that satisifes \\(\frac{\partial g}{\partial x} = -\frac{\partial g}{\partial z}\\).
In any case, for the surfaces described by \\(\alpha = \alpha_0\\) and \\(\beta = \beta_0\\), our
field lines are given by

$$\begin{aligned}
x &= \frac{\alpha_0}{B_z} + \frac{B_x}{B_z}L(t)\ln\cosh\Big(\frac{z}{L(t)}\Big) \\\ \\\ y &= \beta_0
\end{aligned}$$

### Forced mirroring

When the above model is used in a single particle simulation, there are only two qualitatively
distinct trajectories: those that become trapped in the current sheet and those that exit. In the 
magnetosphere, particles that exit from the current sheet have the chance to return for another
interaction --- provided they have not been scattered into the loss cone. To simulate multiple
current sheet crossings, we can strengthen the magnetic field far from the \\(x\\)-\\(y\\) plane
to force particle mirroring.[^nonadiabatic-results]

A modification that enables this behavior is

$$\mathbf{B}(x, z, t) = \Big[B_x\tanh\Big(\frac{z}{L(t)}\Big) + B_{\lambda}e^{-\lambda}\sinh^{2\gamma - 1}\Big(\frac{z}{R_E}\Big)\Big]\hat{\mathbf{i}} + B_z\hat{\mathbf{k}}.$$

where \\(\lambda \gg 1\\) and \\(\gamma \in \mathbb{N}\\). This modification strengthens the
magnetic field while maintaining the property \\(\nabla\cdot{\mathbf{B}}=0\\).
	
Through testing, \\(\lambda \approx 40\\) and \\(\gamma = 1 \\) yield decent results when
\\(B_\lambda = 1\\). With this value, \\(|\mathbf{B}|\\) begins to appreciably strengthen
around \\(z \approx \pm 20 R_E\\).
	
While this modification leaves the current sheet unchanged, the field lines far from the \\(x\\)-\\(y\\)
plane experience a large deformation. The vector potential becomes

$$\mathbf{A}(x, z, t) =  \Big[{-B_xL(t)}\ln\cosh\Big(\frac{z}{L(t)}\Big) - B_\lambda R_E e^{-\lambda}\cosh\Big(\frac{z}{R_E}\Big) + B_zx\Big]\hat{\mathbf{j}}$$

and so the obvious choices for the Euler potentials are

$$\begin{aligned}
\alpha(x, z) &= -B_xL(t)\ln\cosh\Big(\frac{z}{L(t)}\Big) - B_\lambda R_E e^{-\lambda}\cosh\Big(\frac{z}{R_E}\Big) + B_zx \\\ \\\ \beta(y) &= y
\end{aligned}$$

The field lines are then described by

$$\begin{aligned}
x &= \frac{\alpha_0}{B_z} + \frac{B_x}{B_z}L(t)\ln\cosh\Big(\frac{z}{L(t)}\Big) + \frac{B_x}{B_\lambda}R_E e^{-\lambda}\cosh\Big(\frac{z}{R_E}\Big) \\\ \\\ y &= \beta_0
\end{aligned}$$

[^limits]: The limits of integration are chosen so that the entire field contributes to \\(E_y\\) at the given \\(z\\). We arrive at the same result whether we set the lower limit to \\(\infty\\) or \\(-\infty\\).

[^euler-potential]: These are known as Euler potentials.

[^nonadiabatic-results]: This won't change the nonadiabatic scattering of the particles as this is a region of high adiabaticity.
