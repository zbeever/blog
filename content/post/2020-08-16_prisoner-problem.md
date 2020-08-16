+++
title = "The prisoner problem (no, not that one)"
date = 2020-08-16T05:15:31-04:00
images = []
tags = ["mathematics"]
categories = []
draft = false
+++

During her Master's program, my girlfriend signed up for a Putnam Competition preparation course.
She doesn't have a background in math, but she thought it would be fun---and it was! There were
lots of interesting practice problems we solved together and this was my favorite.

*Prerequisites:* To understand this post, you should have some knowledge of modular arithmetic.

*Recommended Reading:* The [Putnam Competition website](https://www.maa.org/math-competitions/putnam-competition).

### The setup

Imagine a room with \\(N\\) prisoners. They are going to play a game for their freedom.
They can talk amongst themselves and come up with a strategy before the game starts,
but as soon as it begins they are immobile and unable to communicate. Here it is:

All the prisoners close their eyes. Upon opening them, they find a hat has been placed
on top of each of their heads. On each hat is a number from the set \\(\lbrace 1, 2, \dots, N\rbrace\\).
*These numbers can be repeated!* So, for example, in a game with \\(4\\) prisoners the hats might read \\(1, 1, 3, 4\\) or \\(2, 1, 4, 3\\) or \\(4, 4, 4, 4\\).

Now, each prisoner must write down a guess of the number on *their* hat. If *one* prisoner guesses
correctly, all are free to go. Can you find a way to guarantee their freedom? Think about it for
a while before reading on.

### The solution

Admittedly, the prerequisites list in the introduction gives you a major hint. Ignore that for now.
How would you go about solving this?

It's natural to try a small version of the problem, say for \\(N = 2\\) or \\(N = 3\\). Doing so makes
you realize you can't rely on any particular ordering of the prisoners. There's just too much variation.
Let's forget about what any particular prisoner can calculate and instead look at invariant quantities,
i.e. those quantities that are fixed for a given game.

Labeling each number \\(n_i\\), where \\(i \in \lbrace1, 2, \dots, N\rbrace\\), the two obvious invariant
quantities are

$$S = \sum_{i=1}^N n_i$$

and

$$P = \prod_{i=1}^N n_i$$

The first is simpler than the second, so let's focus on it and play around. The sum of all prisoners'
numbers is nice, but prisoner \\(i\\) doesn't have access to it. The next best thing---which is all
prisoner \\(i\\) has access to---is

$$S_i = S - n_i$$

i.e. the sum of all numbers minus their own. We'd like to turn this into a guess of some number
between \\(1\\) and \\(N\\). An easy way to do this is with modular arithmetic, so let's investigate

$$S - n_i\pmod{N}$$

Clearly \\(n_i\\) will be unaffected by this operation unless \\(n_i = N\\), in which case
\\(n_i = 0 \pmod{N}\\). On the other hand, \\(S\\) will always be affected, and moreover \\(S\pmod{N}\\)
will take on the same value for every prisoner. Here's the key insight: if we make any one-to-one mapping
from \\(\lbrace 1, 2, \dots, N \rbrace\\) to the prisoners (e.g. have them form a line and remember
their place), we can use their newly assigned number \\(l_i\\) to cancel \\(S\pmod{N}\\), leaving
only \\(n_i = n_i \pmod{N}\\) in its place! That is, prisoner \\(i\\) writes down

$$l_i - (S - n_i) \mod N$$

for their guess, with the special case of \\(0\\) being interpreted as \\(N\\). This works because
\\(S \pmod{N}\\) is between \\(0\\) and \\(N - 1\\), inclusive. The prisoner \\(i\\) whose assigned
number is \\(l_i = S \pmod{N}\\) (and there will be such a prisoner) is actually evaluating \\(n_i\pmod{N}\\).

Try this for yourself. If you've got Numpy installed, the following code runs a simulation of the game with \\(N\\) prisoners.

{{< highlight python "linenos=table, linenostart=1" >}}
import numpy as np

N = 10

prisoner_numbers = np.random.default_rng().integers(0, N, N) + 1
line_numbers     = np.arange(1, N + 1)

S      = np.sum(prisoner_numbers)
S_i    = S - prisoner_numbers
mod_op = np.mod(line_numbers - S_i, N)
guess  = np.where(mod_op == 0, N, mod_op)

correct_guess = np.argwhere(guess == prisoner_numbers)[0, 0]

print(f'Prisoner {correct_guess + 1} correctly guessed their number. S: {S}, S_i: {S_i[correct_guess]}, l_i: {line_numbers[correct_guess]}, n_i: {prisoner_numbers[correct_guess]}')
{{< / highlight >}}
