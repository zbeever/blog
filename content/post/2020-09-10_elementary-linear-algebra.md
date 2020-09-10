---
title: "Some proofs in elementary linear algebra"
date: 2020-09-10T09:00:00-04:00
Description: ""
Tags: ["mathematics"]
Categories: []
DisableComments: false
---

This semester, a controls class I'm enrolled in has promised to be proof-based. Writing proofs is not a
muscle I exercise often, so I figured it would be best to get back into things with some
proofs of elementary theorems in linear algebra. This is not going to be a particularly exciting post---it's mainly done for the benefit of myself.

*Prerequisites:* To understand this post, you should be familiar with linear algebra.

*Recommended Reading:* [Linear Algebra Done Right](http://linear.axler.net/)
by Sheldon Axler. [Finite Dimensional Linear Systems](https://epubs.siam.org/doi/book/10.1137/1.9781611973884?mobileUi=0&)
by Roger Brockett.

### Linear dependence and span

**Theorem**: *Given a vector space \\(V\\) over a field \\(\mathbb{F}\\) and a spanning set \\(V_0 = \lbrace v_1, \dots, v_n\rbrace\\) with \\(v_i \in V\\) for \\(i = 1,\dots,n\\), an arbitrary linearly
indepdendent set of vectors \\(U = \lbrace u_1, \dots, u_k\rbrace\\) with \\(u_j\in V\\) for \\(j=1,\dots,k\\) has at most \\(n\\) elements.*

Because the set \\(V_0\\) spans \\(V\\), we may express \\(u_1\\) in terms of the \\(n\\) vectors in \\(V_0\\),
$$ u_1 = \beta_1v_1 + \cdots + \beta_nv_n $$
where \\(\beta_i\in\mathbb{F}\\) are not all zero. Equivalently, we may express \\(v_1\\) in terms of \\(v_2, \dots, v_n\\) and \\(u_1\\) via[^labeling]
$$v_1 = \alpha_1u_1 + \beta_2v_2 + \cdots + \beta_nv_n$$
and so we may replace \\(v_1\\) in \\(V_0\\) with \\(u_1\\) and still span \\(V\\). We will define this new spanning set by
$$V_1 = \lbrace u_1, v_1, \dots, v_n \rbrace.$$
More generally, let
$$V_k = \lbrace u_1, \dots, u_k, v_{k+1}, \dots, v_n\rbrace$$
and assume it spans \\(V\\). Because this is a spanning set, we may write \\(u_{k+1}\\) in terms of the \\(n\\) vectors in \\(V_k\\) as
$$ u_{k+1}= \alpha_1u_1 + \cdots + \alpha_ku_k + \beta_{k+1}v_{k+1} + \cdots + \beta_nv_n.$$
Since the vectors \\(u_i\\) are linearly independent, the above expression must have at least one nonzero \\(\beta_i\\). Renaming the associated element \\(v_{k+1}\\), we can write
$$v_{k+1}= \alpha_1u_1 + \cdots + \alpha_ku_k + \alpha_{k+1}u_{k+1}+\beta_{k+2}v_{k+2} + \cdots + \beta_nv_n$$
and thus replace \\(v_{k+1}\\) with \\(u_{k+1}\\) to make a new spanning set
$$V_{k+1}= \lbrace u_1, \dots, u_k, u_{k+1}, v_{k+2}, \dots, v_n\rbrace$$
By induction, this process continues until we reach
$$V_n = \lbrace u_1, \dots, u_n \rbrace$$
and so the maximum number of elements in our linearly independent set \\(U\\) is \\(n\\). Were this not the case, then
by the assumption that \\(V_n\\) spans \\(V\\) we could write
$$ u_{n+1} = \alpha_1u_1 + \cdots + \alpha_nu_n,$$
for at least one nonzero \\(\alpha_i\\). This would contradict the assumption that \\(U\\) is linearly independent. Therefore, given an \\(n\\)-element spanning set of a vector space, we can find at most \\(n\\) linearly independent vectors within that space. \\(\square\\)

An immediate consequence of this is that all linearly independent sets that span the same vector space \\(V\\) contain the same number of elements. We call such a set a basis.

### The relationship between determinant, trace, and eigenvalues

**Lemma**: *The determinant of a matrix is given by the product of its eigenvalues.*

The eigenvalues \\(s_i\\) of a matrix \\(\mathbf{A}\\) satisfy

$$\det(\mathbf{A} - s\mathbf{I}) = 0.$$

This is a polynomial equation, and so by the fundamental theorem of algebra may be factored as

$$ \prod_{i} (s_i - s) = 0$$

where \\(s_i \in \mathbb{C}\\). From this, we see that

$$ \det(\mathbf{A}) = \lim_{s\to0}\det(\mathbf{A} - s\mathbf{I}) = \lim_{s\to0}\prod_{i}(s_i - s) = \prod_{i}s_i$$

i.e. the determinant of \\(\mathbf{A}\\) is given by the product of its eigenvalues. \\(\square\\)

**Lemma**: *The trace of a matrix is given by the sum of its eigenvalues.*

We begin by noticing that the trace of a product of three matrices is unchanged by a cyclic permutation[^perm], i.e.

$$\mathrm{Tr}(\mathbf{A}\mathbf{B}\mathbf{C}) = \mathrm{Tr}(\mathbf{B}\mathbf{C}\mathbf{A}) = \mathrm{Tr}(\mathbf{C}\mathbf{A}\mathbf{B}).$$

This is easily seen by framing the trace in indicial notation, in which case we have \\(\mathrm{Tr}(\mathbf{A}) = {A^i}_i\\) and so 

$${A^i}_j{B^j}_k{C^k}_i = {B^j}_k{C^k}_i{A^i}_j = {C^k}_i{A^i}_j{B^j}_k$$

where we have employed the Einstein summation convention.

We may put any matrix \\(\mathbf{A}\\) into Jordan normal form using a similarity transformation \\(\mathbf{P}\mathbf{A}\mathbf{P}^{-1}\\).
In this form, the eigenvalues appear along the main diagonal and so it is evident that

$$\mathrm{Tr}(\mathbf{P}\mathbf{A}\mathbf{P}^{-1}) = \sum_{i}s_i,$$

but by the above observation this is the same as

$$\mathrm{Tr}(\mathbf{A}\mathbf{P}^{-1}\mathbf{P}) = \mathrm{Tr}(\mathbf{A})$$

and the lemma is proved. \\(\square\\)

[^labeling]: All of these 're-expressions' involve possible relabellings. That is, the \\(u_i\\)s and \\(\beta_i\\)s in one step need not be the same \\(u_i\\)s and \\(\beta_i\\)s in the next.

[^perm]: More generally, the trace of the product of any number of matrices is invariant under cyclic permutation.
