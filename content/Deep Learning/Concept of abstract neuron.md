#deeplearning   #Intermediate 

----

## Water in a Sink
A pipe is supplied with water at a given pressure $P$ and the knob $K$ can adjust $P$, providing a variable outgoing water flow at rate $r$. The knob influence rate by non-negative $w$.

$$P = r/w$$
Pipes pour water into tank where simultaneously, tank drained at a rate $R$.

**Problem**
Given the water pressure supplies $P_1,...,P_n$
How can one adjust the knobs $K_1,...,K_n$ such that after fixed interval of time $t$ there is predetermined volume $V$ of water in tank?

$$V = \left\{ \begin{array}{ c l }0 & \quad \textrm{if } R > \sum_{i=1}^{n} r_i \\(\sum_{i=1}^{n} r_i - R)t & \quad \textrm{otherwise}\end{array}\right.$$
Let's $K_i$ control $w_i$ so $ith$ pip supplies water at rate $r_i = P_iw_i$ and consider also *activation function*
$$\phi_t(x) = \left\{ \begin{array}{ c l }0 & \quad \textrm{if } x < 0 \\xt & \quad \textrm{otherwise}\end{array}\right.$$
where $t > 0$, Now, the volume $V$ can be written in terms $P_i, w_i, \phi_t$ as
$$V = \phi_t(\sum_{i=1}^nP_iw_i-R)t \space,\space where \space x=\sum_{i=1}^nP_iw_i-R$$
$R$ produces a horizontal shift for graph $\phi_t$ and in Neural Networks language it is called *bias*

The problem reduce to find solution of $V = \phi_t((\sum_{i=1}^n(P_iw_i-R))t$

Having unknown $R,w_i$. In practice it would suffice to obtain an approximation of the solution by choosing the controls $w_i$  and the bias $R$ that make this proximity function minimized
$$L(w_1,...,w_n,R) = \frac{1}{2}(\phi_t(\sum_{i=1}^{n}P_iw_i-R)-V)^2$$
other proximity functions can be also considered, for example,
$$L(w_1,...,w_n,R) = |\phi_t(\sum_{i=1}^{n}P_iw_i-R)-V|$$
Both $L$ functions are non-negative and vanish along the solution, They are also sometimes called *error functions*.

In practice we would like to learn from available data. We will provided with N training data
	$$(P^k, V_k), 1 \le k \le N, \space P^{k^T} = (P^{k}_{1},...,P^{k}_{n})$$
	The  forecast is given by $V = \phi_t((\sum_{i=1}^n(P_iw_i-R))t$. These are obtained by minimizing  the following cost function:
	$$C(w_1,...,w_n,R) = \frac{1}{2}\sum_{k=1}^{N}(\phi_t(P^{k^{T}}w-R)-V_k)^2$$ where $w^T = (w_1,...,w_n)$
**NOTE**
	- Error function (Loss function) compute the error for single training example
	- Cost function is average of loss function of training set
	- Some people call both of them error function, there terms are synonymous.