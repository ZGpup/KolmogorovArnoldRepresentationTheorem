# A Guided Proof of the Kolmogorov Arnold Representation Theorem

By Zephyr Gilmore

The Kolmogorov Arnold Representation Theorem states that any continuous multivariate function can be written as the sum and composition of single variable functions. The result was first published in 1956, and was initially considered as a candidate method for constructing early neural networks, however, due to the methods used in the proof, computer implementation was never considered practical. In June 2024, a group published a method for constructing networks that is inspired by the Kolmogorov Arnold Representation Theorem. Their approach focuses on simplifying the functions used in the representation to make them computable, and therefore the networks they build are only loosely representative of the original theorem. That being said, the methods used in the original proof involve interesting mathematics and are worth understanding in their own right. Most publications of the original result are tricky to understand for someone just getting into mathematics. The easiest way to understand the tools developed in the proof is to simplify the problem, and then use visuals to accompany the mathematics. This paper proves a reduced result, and in doing so hopes to build intuition for understanding the tools used in the proof and to share the result with a broader mathematical audience. 

I focus on the claim that any two variable function $f(x,y)$ over the unit square can be written as, 

$$f(x,y) = \sum_{q=1}^5 \chi^q(\phi_1^q(x)+\phi_2^q(y))$$

Where $\chi^q, \phi_1^q, \phi_2^q$ are each continuous single variable functions. The proof is constructive, and will demonstrate exactly the steps to build this set of functions. For most of the proof, the construction is the same for each of the five values of $q$. When you see $\phi_1^q$ being referenced in the construction, it means we are doing the same thing for each $\phi_1^1, \phi_1^2, \dots$ and the value of $q$ is irrelevant. The proof will follow three parts.

**A tour of the proof:**

1) We will construct a sequence of tiles that cover the unit square. Each set of tiles in the sequence getting smaller and more refined.  For each $q$ we will construct a slightly different sequence of tiles. One such sequence of tiles might look like the following. 

[![Video Preview](https://img.youtube.com/vi/wn4_Y38mWOw/0.jpg)](www.youtube.com)

1) Using this sequence of tiles, we will construct $\phi_1^q(x)$ and $\phi_2^q(y)$ in such a way that the value of $\phi_1^q(x)+\phi_2^q(y)$ is unique over each tile. The reason for this specific construction will become obvious in the third step.  

2) Again using the sequence of tiles, we will construct $\chi^q(\phi_1^q(x)+\phi_2^q(y))$. Intuitively, one can think of this step as refining $\phi_1^q(x)+\phi_2^q(y)$ by controlling the values that it attains over each of the tiles. The method of this proof is to give us precise local control over the value of the function using the tiles. 

**1) Constructing the Grid:**

Now that the general format of the proof is hopefully clear, lets dive into the details. First, we will begin by constructing the grid system as proposed in part 1. The following videos describe this construction. 

<div style="text-align: center;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/bFVW1WmvpRU" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

Now we can take this structure of intervals created, $A_{k,p}^q$, and use them to make a tiling. Let $S_{k}^q = A_{k,1}^q\times A_{k,2}^q$ for all families $q$. This gives us five sets of intervals in $[0,1]\times[0,1]$, and for any point we have that it must be in at least four families in $A_{k,1}^q$, and four families in $A_{k,2}^q$, so it must be at any time covered by at least three families in $S_{k}^q$. The following animation shows how for $k=2$, we can stack the five families of tiles which will ensure that any point is in at least 3 of the 5 families. One could think of the gaps in between the tiles as roads and the gaps by the corners as intersections. If a point is in a road, then it will be in the gap of one of the families of intervals. If the point is in an intersection, it will be in the gap of two families of intervals, but a point could never be in more than 2 roads at the same time, so it must be inside of a block in the other 3 families. 

<div style="text-align: center;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/xi5LvWszp9U" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

For the rest of the proof, we will refer to these tiles as $S_{k,1_i,2_j}^q$, where $i$ is the x-coordinate of the tile, and $j$ is the y-coordinate of the tile. Hopefully the videos provided have given ample intuition for the construction of the desired grid system, now we can dive into the construction of the inner functions in step 2. 


**2) Constructing the Inner Functions**

In this sections we will construct a subsequence of the sequence of tiles $\{S_{k}^q\}_{k=1}^\infty$, we will call it  $\{S_{r}^q\}_{r=1}^\infty$. Using this sequence of tiles we will prove the following lemma.

*Lemma 1:* There exists a continuous function $\psi^q(x,y) = \phi_1^q(x) +\phi_2(y)$ that satisfies the following conditions for the sub-sequence of tiles. 
1) For all $r$ and $q$, $\psi^q(S_{k,1_i,2_j}^q) \cap \psi(S_{k,1_m,2_n}^q) = \emptyset$ for all $(i,j)\neq (n,m)$. 
2) The functions $\phi_p^q$ are non-decreasing and continuous. 

The proof of this lemma is best explained by the following video. The construction is proved with sufficient rigor in the video, but there are some supplemental details after to fill in any gaps.  

<div style="text-align: center;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/FWKZ0SEWdeM" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>


During the construction of our sequence of functions, we pick a new $\epsilon_i$ for each step, ensuring that $\epsilon_{i+1} < \frac{1}{2}\epsilon_i$ for all $i$, therefore $\epsilon_n < \frac{1}{2^n}\epsilon_1$. We also know that $||\phi_{i,p}^q - \phi_{i+1,p}^q|| < \epsilon_i$ since we always construct each function to be within the previous epsilon boundary. Using these facts we can show that the sequence is Uniformly Cauchy. 

We want to show that for any $\epsilon$, there is some $N$ such that $m,n >N$ implies $||\phi_{n,p}^q - \phi_{m,p}^q|| < \epsilon$. Assume that $n<m$, then we have that,
$$
\begin{aligned}
||\phi_{n,p}^q - \phi_{m,p}^q|| & = \sum_{i=n}^{m-1}||\phi_{i,p}^q - \phi_{i+1,p}^q ||  
 \leq \sum_{i=n}^{m-1} \epsilon_i 
 = \sum_{i=n}^{m-1} \frac{1}{2^i}\epsilon_1 
 < \frac{1}{2^{n-1}}\epsilon_1
\end{aligned}
$$
From here it is easy to see that by choosing sufficiently large $N$, the sequence must be uniformly cauchy, and therefore is uniformly convergent in $\mathbb{R}$. The construction of each $\phi_{r,p}^q$ means that they are clearly non-decreasing. Since we showed that for every $r$, the functions satisfy condition 1 for all smaller tiles, then we know that this limit function satisfies the condition for all possible $r$. Now that we have finished the construction of this inner function, we can begin to define $\chi^q$. 

**3) Constructing the Outer Functions**

Recall from before that when constructing the sequence of tilings, any point in the unit square will fall within at least 3 of the 5 families of tiles. This fact will now be crucial to finishing the proof. This section requires a bit of analysis, and this can make it harder to see the intuition behind the proof. Recall that we have five inner functions, one associated with each family of tiles, $$\psi^q(x,y) = \phi_{1}^q(x) + \phi_{2}^q(y)$$

Recall that the function we are trying to represent is $f(x,y)$. In a similar fashion to the last section, we will again pick a subsequence of the tiles. We will pick the sequence in such a way that every time we move to a smaller set of tiles, the function $f(x,y)$ fluctuates by only a small amount over each tile. Then we can define the outer function $\chi^q$, to output a fraction of the value of $f(x,y)$ over the center of each tile. When we do this, we will then know that at any point in the unit square, there will be at least three of the five functions $\chi^q$ such that that point is in their associated family of tiles. Since we picked the value of these $\chi^q$ to output a fraction of the correct value on these tiles, when we sum these three $\chi^q$ they will closely approximate the function. This process will be repeated, and we will show that the function created at the limit will be exactly our desired function $f(x,y)$. Now that we have some intuition, lets get into the math. 


For each of our tiles $S_{k}^q$, we will define $(x_{{c_k^q}},y_{{c_k^q}})$ to be the value at the center of the tile. Now we will construct a sequence of functions $\{g_i\}_{i=0}^\infty$. We will start by letting $g_0 = f(x,y)$ be the function we are trying to represent. Since $g_0$ is continuous and defined on a compact set then $g_0$ is both uniformly continuous and attains a maximum. Let $M_0$ be this maximum value, then since $g_0$ is uniformly continuous we can find some $\delta$ such that if $d((x,y),(x',y'))< \delta$, then we know $d(g(x,y), g(x',y'))< \frac{1}{6}M_0$. The choice of $\frac{1}{6}$ has to do with the fact that we have $5$ functions $\chi^q$, and we want the sum of them to be bounded by a quantity that goes to zero as we progress in the sequence. $\frac{1}{6}$ just happens to be the first easy fraction to write that will achieve this when summed five times.

Now, we will go through the procedure to pick the next element in the sequence $\{g_i\}_{i=0}^\infty$. We will start by picking the first set of tiles $k$ in the sequence, such that each tile $S_{k,1_i,2_j}^q$ has diameter less than $\delta$. In this case diameter is referring to the length of the longest edge of the rectangle. This means that our function $g_0$ will differ by less than $\frac{1}{6}M_0$ anywhere on the tile. Then we can define the function $\chi_1^q(x,y)$. We will do this piecewise on the values in $\psi^q(S_{k,1_i,2_j}^q)$,

$$
\chi_1^q(t) = \begin{cases} \frac{1}{3}g_0(x_{{c_k^q}},y_{{c_k^q}}) & t\in \psi^q(S_{k,1_i,2_j}^q) \\ \text{Connects linearly } & \text{Otherwise} \end{cases}
$$

Recall from part one that by construction, $\psi^q(S_{k,1_i,2_j}^q) \cap \psi^q(S_{k,1_n,2_m}^q) = \emptyset$ if $(i,j)\neq (n,m)$. This fact is now crucial for ensure that $\chi_q^1$ is well defined. Specifically notice that if $t\in \psi^q(S_{k,1_i,2_j}^q) \cap \psi^q(S_{k,1_n,2_m}^q)$, then the function $\chi_1^q$ will be assigned the value of $g_0$ at two different places (the center of each of the two tiles) which means it may not be well defined. Therefore the proof of *lemma 1* was crucial for this construction. Now, let 
$$f_1(x,y) = \sum_{i=1}^5\chi_1^q(\phi_1^q(x) + \phi_2^q(y))$$

This now concludes the construction of $\chi_1^q$. We will now show how to construct the next function $\chi_2^q$ in the sequence. Let $g_1 = g_0 - f_1$. Recall that any point $(x,y)$ is covered by tiles in at least 3 of the 5 families, for the sake of argument let the families which contain $(x,y)$ be families 1,2,3, then taking $||g_1|| = ||g_0-f_1||$, we can substitute for $f_1$ and split the sum into the set of tiles that contain our point and the set that do not.  

$$||g_0 - f_1|| = \max_{E^2} \left| g_o - \sum_{q=1}^3 \chi_1^q \left( \psi^q(x, y) \right) - \sum_{q=4}^5 \chi_1^q \left( \psi^q(x, y) \right) \right|$$
Then by the triangle inequality we have,
$$
\max_{E^2} \left| g_o - \sum_{q=1}^3 \chi_1^q \left( \psi^q(x, y) \right) + ( -\sum_{q=4}^5 \chi_1^q \left( \psi^q(x, y) \right)) \right|\\
\leq \max_{E^2} \left| g_o - \sum_{q=1}^3 \chi_1^q \left( \psi^q(x, y) \right) \right| + \max_{E^2} \left| \sum_{q=4}^5 \chi_1^q \left( \psi^q(x, y) \right) \right|\\
$$
Then since we know that the point $(x,y)$ is covered by the first 3 families, we can replace the first three $\chi_1^q$ with the value of $g_0$ at the center the three tiles that contain $(x,y)$. 
$$
= \max_{E^2} \left| g_o(x, y) - \sum_{q=1}^3 \frac{1}{3} g_o \left( x_{1c_1}^q, y_{2c_1}^q \right) \right| + \max_{E^2} \left| \sum_{q=4}^5 \chi_1^q \left( \psi^q(x, y) \right) \right|
$$

Now notice that by our choice of tiles size $(x,y)$ is within distance $\delta$ of the center of each of these tiles, so $d((x,y), (x_{1c_1}^q, y_{2c_1}^q))<\delta$. Then by uniform continuity, we have, $|g_0(x,y) - g_0(x_{1c_1}^q, y_{2c_1}^q)| < \frac{1}{6}M_0$. Then we can split up the first term into three groups, each less than $ \frac{1}{3}\cdot \frac{1}{6}M_0$

$$
= \max_{E^2} \left|3 \frac{1}{3} g_o(x, y) - \sum_{q=1}^3 \frac{1}{3} g_o \left( x_{1c_1}^q, y_{2c_1}^q \right) \right| + \max_{E^2} \left| \sum_{q=4}^5 \chi_1^q \left( \psi^q(x, y) \right) \right|\\
< \frac{3}{18}M_0 + \max_{E^2} \left| \sum_{q=4}^5 \chi_1^q \left( \psi^q(x, y) \right) \right|
$$
Finally, we know the right hand size is bounded by the maximum value that $\chi_1^q$ achieves. Since its maximum value is on some platform, and all platforms are bounded by $\frac{1}{3}g_0$, then we know $\chi_1^q$ is bounded by $\frac{1}{3}M_0$. So we then have, 
$$
\frac{1}{6}M_0 + \frac{2}{3}M_0 = \frac{5}{6}M_0
$$
So we get that $||g_1|| = ||g_0-f_1|| < \frac{5}{6}M_0$. notice then that $g_1$ is also a continuous function on a compact set, and it therefore uniformly continuous. In a similar manner we can pick $M_1 = ||g_1||$, and then let $\delta$ be small enough such that it satisfies uniform continuity for $\epsilon = \frac{1}{6}M_1$. By construction we must have $M_1 < \frac{5}{6}M_0$ since $||g_1||<\frac{5}{6}M_0$. We can then pick the next set of tiles with radius less than $\delta$, and repeat the same construction as before. This will yield $g_2 = g_1 - f_2$ such that $||g_2|| < \frac{5}{6}^2 M_0$. Repeating this process will yield a sequence of functions with $\chi_r^q < \frac{1}{3}||g_{r-1}|| <\frac{1}{3}(\frac{5}{6}^{r-1}M_0)$. Therefore the series converges to a limit function $\chi^q(\phi_1^q(x) + \phi_2^q(y))$ further notice that since this is true for all $q$, we get that $\sum_{r=1}^\infty \sum_{q=1}^5 \chi_r^q(\phi_1^q(x) + \phi_2^q(y))$ converges to $\sum_{q=1}^5 \chi^q(\phi_1^q(x) + \phi_2^q(y))$. We have now found the desired function, and it is left to show that it is equal to $f(x,y)$ as desired. 

Notice that we have $g_r = g_{r-1}-f_r$, therefore $f_r = g_{r-1}-g_r$. Then if we consider $||f_r||$ we obtain, 
$$||f_r|| = ||g_{r-1}-g_r|| \leq \frac{5}{6}^{r-1}M_0 + \frac{5}{6}^{r}M_0 < 2 \frac{5}{6}^{r-1}M_0$$
This bound ensures that the series $\sum_{r=1}^{\infty} f_r$ is absolutely convergent. Therefore we can take the series,
$$\sum_{r=1}^{\infty} f_r = \sum_{r=1}^{\infty} (g_{r-1}-g_r) = (g_0 - g_1) + (g_1 - g_2) + \dots$$
Then we get that every term besides $g_0$ cancels, so we have $\sum_{r=1}^\infty f_r = g_0 = f$. Then, since $f_r = \sum_{i=1}^5\chi_r^q(\phi_1^q(x) + \phi_2^q(y))$, we get $\chi^q(\phi_1^q(x) + \phi_2^q(y)) = f(x,y)$, completing the proof of the theorem.





### Bibliography

1. Aaron R Bragg. On the Kolmogorov-Arnold Representation Theorem for Continuous Functions. Wichita State University, 2016. Retrieved from https://soar.wichita.edu/server/api/core/bitstreams/59a5533a-8e8a-4f80-8de2-a0f5ff5b80dd/content.

2. Liu, Z., Wang, Y., Vaidya, S., Ruehle, F., Halverson, J., Soljačić, M., Hou, T. Y., & Tegmark, M. (2024). KAN: Kolmogorov-Arnold Networks. arXiv. Retrieved from https://arxiv.org/abs/2404.19756.









