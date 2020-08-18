---
title: "The geometry of mechanics"
date: 2020-08-18T15:03:00
Description: ""
Tags: ["mechanics", "lagrangian", "hamiltonian", "geometry"]
Categories: []
DisableComments: false
---

If you've spent time with analytical mechanics, you've probably stumbled upon the concept of
a symplectic manifold. In particular, you've probably heard how Hamiltonian mechanics is naturally
described by a symplectic manifold. Unfortunately, many sources explaining why this is so are
opaque to the uninitiated or painfully slow to get to the point. I'll try to outline the geometric
 picture of mechanics using a combination of qualitative and quantitative arguments.

*Prerequisites:* To understand this post, you should be comfortable with differential geometry
and its two most popular notations: indicial notation and coordinate-free notation. You should
also be familiar with Lagrangian and Hamiltonian mechanics and the Poisson bracket formalism.

*Recommended Reading:* [The Geometry of Physics](https://www.cambridge.org/core/books/geometry-of-physics/94894F70DB22055BD7BC2B84C135ABAF)
by Theodore Frankel. [First Steps in Differential Geometry](https://www.springer.com/gp/book/9781461477310)
by Andrew McInerney. [Why symplectic geometry is the natural setting for classical mechanics](https://math.mit.edu/~cohn/Thoughts/symplectic.html) by Henry Cohn. [Symplectic geometry and classical mechanics](https://www.youtube.com/playlist?list=PLDfPUNusx1EoVnrQcCRishydtNBYU6A0c) by Tobias Osborne.

### The configuration space

We learn from Newton that we require three pieces of information to understand the evolution
of a system: (1) the position of the system's particles, (2) the velocity of those particles,
and (3) the forces in play.

Let's start with the first piece of information. We describe the positions of \\(N\\) particles
with a set of coordinates \\(q^i\\). If these particles are unconstrained, there are \\(3N\\) such coordinates. If
they are constrained (e.g. when describing a system of planar pendulums), there are less.
Whatever the case, we call this the configuration space of our system---it is a manifold
\\(\mathcal{M}\\). By construction, the positions of the particles of our system always lie within \\(\mathcal{M}\\).

The velocity of any one particle at a particular point \\(q_0\\) is described by 

$$\dot{q} = \frac{\mathrm{d}}{\mathrm{d}t}q(t)\Big|_{t_0, q(t_0) = q_0}$$

where \\(q(t)\\) is its path. This is exactly the definition of a tangent vector to \\(\mathcal{M}\\) at \\(q_0\\). More generally,
the velocities consistent with our configuration space are those tangent to the space at each point.

From this, we see that the first two pieces of information---the positions and velocities of all 
particles within the system---can be described by a single point in the tangent bundle \\(T\mathcal{M}\\).
In coordinate form this point would be described by \\( (q, \dot{q}) =
(q^1,\dots, q^M, \dot{q}^1, \dots, \dot{q}^M) \\). The forces of our system determine how this point moves
around in \\(T\mathcal{M}\\).

### The phase space

All these \\(q\\)'s and \\(\dot{q}\\)'s are reminiscent of the standard notation in Lagrangian mechanics,
and indeed this is where we're headed. The Lagrangian \\(\mathcal{L}(q, \dot{q})\\) is a function mapping 
\\(T\mathcal{M} \to \mathbb{R}\\). It endows our space with additional structure by constraining the
allowable system trajectories in \\(T\mathcal{M}\\). It does this by requiring these trajectories
be the ones that are stationary paths of the action \\(\int\mathrm{d}t\mathcal{L}\\).

Returning to \\(T\mathcal{M}\\), we recall that any tangent space \\(T_{q_0}\mathcal{M}\\)
has an associated dual space \\(T_{q_0}^*\mathcal{M}\\) called the cotangent space at \\(q_0\\).
This new space consists of one-forms---linear functionals---that map \\(T_{q_0}\mathcal{M} \to \mathbb{R}\\).
If we pick a basis for \\(T_{q_0}\mathcal{M}\\) labeled by \\( (\partial_{q^1}, \dots, \partial_{q^M}) \\),
there is an  associated dual basis labeled by \\( (\mathrm{d}q^1, \dots, \mathrm{d}q^M) \\)
satisfying \\(\mathrm{d}q^i(\partial_{q^j}) = \delta^i_j \\). In indicial notation, the tangent
space contains vectors with contravariant components \\(\dot{q}^i\\) and the cotanget space contains vectors
with covariant components \\(a_i\\). The big difference between these two types of components is how they
transform under a change of manifold coordinates.

A point absent from the above paragraph is how we go about mapping \\(T_{q_0}\mathcal{M} \to T^*_{q_0}\mathcal{M}\\).
There is no natural way to do this---we have to rely on some additional structure. Cue the Lagrangian.
Recall that the momentum conjugate to \\(q^i\\) at \\(q_0\\) is defined as

$$ p_i = \frac{\partial\mathcal{L(q, \dot{q})}}{\partial \dot{q}^i}\Big|_{q=q_0} $$

This is a local map taking vectors in the tangent space at \\(q_0\\) to one-forms in the dual space. We can do the
same at every point \\(q \in \mathcal{M}\\), thereby translating our system from \\(T\mathcal{M}\\)---the tangent
bundle---to \\(T^*\mathcal{M}\\)---the cotangent bundle. This is a manifold of its own. We will label it
\\(\mathcal{P}\\). A point in this manifold is described by \\( (q, p) = (q^1, \dots, q^M, p_1, \dots, p_M)\\). 
As the title of this section gives away, this is the system's phase space.

### The Hamiltonian

The most famous function that lives in phase space is the Hamiltonian \\(\mathcal{H}(q, p)\\). The Hamiltonian
constrains the possible system evolutions in \\(\mathcal{P}\\) just as the Lagrangian does in \\(T\mathcal{M}\\).
Naturally, these trajectories can be described as the integral curves of a vector field over \\(\mathcal{P}\\).
This field lives in \\(T\mathcal{P}\\) (or, equivalently, \\(TT^*\mathcal{M}\\)). What can we say about it?

For one, the instantaneous evolution of the system should only depend on the local change in energy \\(\mathrm{d}\mathcal{H}\\).
This means that a given vector \\(V_{(q, p)}\\) in \\(T_{(q, p)}\mathcal{P}\\) is informed by \\(\mathcal{d}\mathcal{H} \in T_{(q, p)}^*\mathcal{P}\\).
To translate between \\(V\\) and \\(\mathrm{d}\mathcal{H}\\), we can search for structures \\(\omega\\) or \\(\Omega\\) that satisfy

$$ \omega(V, W) = \mathrm{d}\mathcal{H}(W) \qquad \Omega(\mathrm{d}H, \mathrm{d}G) = V(G)$$

We'll go in search of \\(\omega\\), though we'll see what \\(\Omega\\) is later. In any case, both structures
must be linear if they are to capture the laws of mechanics.

We're looking for a two-form \\(\omega\\) that takes in a vector field and produces \\(\mathrm{d}\mathcal{H}\\).
In indicial notation this is \\(\omega_{ij}V^{i} = (\mathrm{d}\mathcal{H})_j\\). What do we know about mechanics that can constrain \\(\omega\\)?

First, the directional derivative of the Hamiltonian along \\(V\\) should be \\(0\\) by conservation of energy. This means

$$ V(\mathcal{H}) = \mathrm{d}\mathcal{H}(V) = \omega(V, V) = 0 $$
and the only way for this to be nontrivially true is if \\(\omega(V, W) = -\omega(W, V)\\). We also want
to be able to solve for \\(V\\) given \\(\mathcal{H}\\), so \\(\omega\\) should be nondegenerate. As a final requirement
we assert that physical laws shouldn't depend explicitly on time. This amounts to saying that \\(\omega\\) is left
unchanged when dragged along \\(V\\). But this is simply the Lie derivative of \\(\omega\\) with respect to \\(V\\),

$$ \mathcal{L}_V\omega = i_V\mathrm{d}\omega + \mathrm{d}(i_V\omega) = i_V\mathrm{d}\omega + \mathrm{d}(\mathrm{d}\mathcal{H}) = i_V\mathrm{d}\omega$$

and so \\(\mathrm{d}\omega\\) must be \\(0\\). To recap the above: we can associate a vector field
\\(V\\) to the differential of the Hamiltonian \\(\mathrm{d}\mathcal{H}\\) via a closed nondegenerate differential two-form.
This is exactly the definition of a symplectic form, so a Hamiltonian phase space \\(\mathcal{P}\\) is a symplectic manifold!

### Inverting the symplectic form

What if we had taken the other route and looked for \\(\Omega\\)? Consider the inverse of \\(\omega\\). In indicial notation, this has the property that

$$ -(\omega^{-1})^{ij}(\mathrm{d}\mathcal{H})_j = V^i $$

On the right side we have \\(V\\). When applied to a function \\(f\\), \\(V\\) describes its change over the system's
evolution, i.e. its change over time. On the left side we have a skew symmetric tensor that takes in the differential
of a function and combines it with the differential of the Hamiltonian. This sounds exactly like the Poisson bracket!
Let's define \\(\Omega\\) as \\(-\omega^{-1}\\) and denote the coordinates of \\(\mathcal{P}\\) as \\(z^\alpha\\) where[^index-confusion]

$$ z^{\alpha} = \begin{cases} q^\alpha, & \alpha = 1, \dots, M \\\ p_\alpha, & \alpha = M + 1, \dots, 2M\end{cases}$$

In this coordinate system, we know that \\(\Omega\\) takes the explicit form

$$ \Omega = \sum_{\alpha=1}^M\frac{\partial}{\partial z^{\alpha}} \otimes\frac{\partial}{\partial z^{\alpha+M}} - \frac{\partial}{\partial z^{\alpha+M}} \otimes \frac{\partial}{\partial z^{\alpha}} $$

or, in component form,

$$ (\omega^{-1})^{ij} = \begin{pmatrix}0 & -I_M \\\ I_M & 0 \end{pmatrix}$$

which immediately implies the component form of \\(\omega\\) is the same. The more common notation is

$$ \omega = \sum_{\alpha=1}^M \mathrm{d}z^{\alpha}\wedge\mathrm{d}z^{\alpha + M}$$

Most resources use \\(q\\)s and \\(p\\)s  and invoke the Einstein summation convention to write

$$ \omega = \mathrm{d}q^i \wedge \mathrm{d}p_i, $$

which is the negative exterior derivative of the [tautological one form](https://en.wikipedia.org/wiki/Tautological_one-form) \\(\theta = p_i\mathrm{d}q^i\\)
defined on \\(\mathcal{P}\\). In any case, we see that the Poisson bracket is intimately related to the symplectic form.

[^index-confusion]: We do this to avoid the confusion arising from the previously lowered \\(p\\) indices seemingly
becoming raised with the demotion of the \\(p\\)s to coordinates (as opposed to covariant tensor components).
