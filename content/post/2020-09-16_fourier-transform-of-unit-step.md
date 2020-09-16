---
title: "The Fourier transform of the Heaviside step function"
date: 2020-09-16T12:57:55-04:00
Description: ""
Tags: ["mathematics", "physics"]
Categories: []
DisableComments: false
---

The Heaviside step function shows up just about everywhere, with its integral representation and Fourier transform
often cropping up in quantum field theory and signal processing. These expressions often lack explanation, so the
purpose of this post is to illuminate their origins.

*Prerequisites:*
To understand this post you'll need to have a passing familiarity with Fourier transforms, distributions, and complex analysis.

*Recommended Reading:* [This excellent answer](https://math.stackexchange.com/questions/269809/heaviside-step-function-fourier-transform-and-principal-values)
by user Patch on the math StackExchange.


### The naive approach

As we know, the Fourier transform \\(\tilde{f}(k)\\) of a function \\(f(x)\\) is given by
$$\tilde{f}(k) = \int_{-\infty}^{\infty}f(x)e^{-ikx}\mathrm{d}x$$
This problem isn't hard---presumably, the transform of the Heaviside function is defined as
$$\tilde{\theta}(k) = \int_{-\infty}^{\infty}\theta(x)e^{-ikx}\mathrm{d}x.$$
However, there's a problem with this: the above integral does not converge. Explicitly, we have
$$\int_{-\infty}^{\infty}\theta(x)e^{-ikx}\mathrm{d}x = \lim_{a\to\infty}\int_0^ae^{-ikx}\mathrm{d}x = \lim_{a\to\infty}\frac{e^{-ikx}}{-ik}\Big|_{0}^{a} = \lim_{a\to\infty}\frac{1}{ik}(1 - e^{-ika}).$$
One way to skirt around this issue is to take the Fourier transform of something that is almost a step function,
then take the limit until the two functions are one and the same. Let's try the replacement
$$\theta(x) \to e^{-\varepsilon{x}}\theta(x)$$
with \\(\varepsilon > 0\\). With this new definition of \\(\theta(x)\\), the related Fourier transform becomes
$$\begin{aligned}
\tilde{\theta}(k) &= \int_{-\infty}^{\infty}e^{-\varepsilon{x}}\theta(x)e^{-ikx}\mathrm{d}x \\\ &= \lim_{a\to\infty}\int_0^ae^{-x(\varepsilon + ik)}\mathrm{d}x \\\ &= \lim_{a\to\infty}\frac{e^{-x(\varepsilon + ik)}}{-(\varepsilon + ik)}\Big|_0^a \\\ &= \lim_{a\to\infty}\frac{1}{\varepsilon + ik}(1 - e^{-a(\varepsilon + ik)}) \\\ &= \frac{1}{\varepsilon + ik}
\end{aligned}$$
Presumably we could then take \\(\lim_{\varepsilon\to0^+}\\) to recover the true Fourier transform of the step function.
But if that's the case, what's going on at \\(k = 0\\)?

### Distributions and test functions

The issue is that we're treating \\(\theta(x)\\) like a function, when really it's a distribution. From a 
physics or engineering point of view, this amounts to saying that \\(\theta(x)\\) is only defined when it's 
integrated against a test function, much like its cousin the Dirac delta \\(\delta(x)\\). Just as this
later distribution is defined by[^aside]
$$\int_{-\infty}^{\infty}\delta(x)f(x)\mathrm{d}x = f(0),$$
the step "function" is defined by
$$\int_{-\infty}^{\infty}\theta(x)f(x)\mathrm{d}x = \int_0^{\infty}f(x)\mathrm{d}x$$
in this framework. So what does \\(\tilde{\theta}(k)\\) do when applied to a test function? Let's assume this test function lives in 
Schwartz space, which means its derivative decays rapidly. Then we have
$$\int_{-\infty}^{\infty}\tilde{\theta}(k)f(k)\mathrm{d}k = \lim_{\varepsilon\to0^+}\int_{-\infty}^{\infty}\frac{1}{\varepsilon + ik}f(k)\mathrm{d}k = \lim_{\varepsilon\to0^+}\int_{-\infty}^{\infty}\frac{\varepsilon}{\varepsilon^2 + k^2}f(k) - \frac{ik}{\varepsilon^2 + k^2}f(k)\mathrm{d}k = \\, ?$$

We can break this into two integrals,
$$\begin{aligned}
\zeta_1 &= \lim_{\varepsilon\to0^+}\int_{-\infty}^{\infty}\frac{\varepsilon}{\varepsilon^2+k^2}f(k)\mathrm{d}k \\\ \zeta_2 &= \lim_{\varepsilon\to0^+}-i\int_{-\infty}^{\infty}\frac{k}{\varepsilon^2 + k^2}f(k)\mathrm{d}k
\end{aligned}$$
Within \\(\zeta_1\\) we recognize \\(\lim_{\varepsilon\to0^+}\varepsilon/(\varepsilon^2+k^2)\\) as the scaled, nascent delta function \\(\pi\delta(k)\\), and so
$$\zeta_1 = \int_{-\infty}^{\infty}\pi\delta(k)f(k)\mathrm{d}k = \pi f(0).$$
For \\(\zeta_2\\), it helps to rewrite it as
$$\zeta_2 = \lim_{\varepsilon\to0^+}-i\int_0^{\infty}\frac{kf(k) - kf(-k)}{\varepsilon^2 + k^2}\mathrm{d}k = -i\int_0^{\infty}\frac{f(k) - f(-k)}{k}\mathrm{d}k$$
which is the distributional definition of (minus \\(i\\) times) the Cauchy principal value of \\(1/x\\), i.e. 
$$\zeta_2 = -i\Big\[\mathrm{p.v.}\Big(\frac{1}{k}\Big)\Big\](f).$$
Combining these results gives the Fourier transform of the Heaviside step function
$$\tilde{\theta}(k) = \pi\delta(k) - i\\,\mathrm{p.v.}\frac{1}{k}$$


### An alternate representation of \\(\theta(x)\\) 

We've just found that
$$\tilde{\theta}(k) = \lim_{\varepsilon\to0^+}\frac{1}{\varepsilon + ik} = \pi\delta(k) - i\\,\mathrm{p.v.}\frac{1}{k}.$$
If we substitute the first of these into the definition of the inverse Fourier transform, we find
$$\theta(x) = \lim_{\varepsilon\to0^+}\frac{1}{2\pi}\int_{-\infty}^{\infty}\frac{e^{ikx}}{\varepsilon + ik}\mathrm{d}k = \lim_{\varepsilon\to0^+}\frac{-i}{2\pi}\int_{-\infty}^{\infty}\frac{e^{ikx}}{k - i\varepsilon}\mathrm{d}k$$
This is an interesting expression. How exactly does this give rise to \\(\theta(x)\\)? Recall the
[residue theorem](https://en.wikipedia.org/wiki/Residue_theorem) from complex analysis. It says that
a closed line integral in the complex plane is proportional to the sum of the residues of the poles
\\(a_k\\) enclosed by the contour \\(\Gamma\\), i.e.
$$\oint_{\Gamma}f(z)\mathrm{d}z = 2\pi i\sum_{k}\mathrm{Res}\big(f(a_k)\big)$$
Now, the integrand in the above representation of \\(\theta(x)\\) has a single pole at
\\(k = i\varepsilon\\) in the complex plane. Since this integrand is analytic, we may extend its
domain to the \\(\mathbb{C}\\). Furthermore, we may replace the integral \\(\int_{-\infty}^{\infty}\\)
with a contour integral enclosing half of the complex plane; when \\(x > 0\\), the contour includes
the real line and the upper semicircle at infinity. When \\(x < 0\\), the contour includes the real
line and the lower semicircle at infinity.[^jordan]

Since the integrand contains no poles within the lower half of the complex plane, \\(\theta(x) = 0\\)
for \\(x < 0\\). This is no longer the case when the contour encloses the upper half of the plane. Since
the residue of the integrand is \\(1\\) at the pole, we have 
$$\theta(x) = \lim_{\varepsilon\to0^+}\frac{-i}{2\pi}\oint_{\Gamma}\frac{e^{ikx}}{k - i\varepsilon}\mathrm{d}k = \frac{-i}{2\pi}\cdot2\pi i\\,\mathrm{Res}\big(f(i\varepsilon)\big) = 1$$

[^aside]: As an aside, \\(\delta(x)\\) and \\(\theta(x)\\) are related to each other via 
the distributional derivative \\(\mathrm{d}\theta(x)/\mathrm{d}x = \delta(x)\\). This
means that for a valid test function \\(g(x)\\),
$$\int_{-\infty}^{\infty}\theta(x)\frac{\mathrm{d}g(x)}{\mathrm{d}x}\mathrm{d}x = {-\int_{-\infty}^{\infty}\frac{\mathrm{d}\theta(x)}{\mathrm{d}x} g(x)\mathrm{d}x} = -\int_{-\infty}^{\infty}\delta(x)g(x)\mathrm{d}x = -g(0),$$
or, equivalently,
$$\int_{-\infty}^{\infty}\theta(x - y)\frac{\mathrm{d}g(y)}{\mathrm{d}y}\mathrm{d}y = -g(x)$$
which is the usual relationship between the integral of a function and convolution with the Heaviside
step function.

This representation of the step function (as a countour integral in the complex plane) is used
to encode time ordering in the [Feynman propagator](https://en.wikipedia.org/wiki/Propagator#Feynman_propagator)
in quantum field theory.

[^jordan]: These conditions are just applications of [Jordan's lemma](https://en.wikipedia.org/wiki/Jordan%27s_lemma).
