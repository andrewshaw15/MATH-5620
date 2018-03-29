# Simple IVP - Implicit Euler

**Function Name:** simpleIVP_implicitEuler

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function approximates the solution of the equation *u' = &lambda;u* with *u(0) = &alpha;* at a specified time *t*. Compare the solutions with [Simple IVP - Exact](https://andrewshaw15.github.io/MATH-5620/HW-5/simple-IVP-exact).

**Input:** This function takes as input the number of time steps *n*, the coefficient *&lambda;*, the initial condition *&alpha;*, and the time *t*.

**Output:** This function returns the approximated solution of the equation.

**Example/Usage:** This function may be called and its results displayed as follows:
~~~~
cout << "u(" << t << ") = " << simpleIVP_implicitEuler(n, l, a, t) << endl;
~~~~
For example, if *n* = 3, 30, 300, and 3000, *&lambda;* = 1, *&alpha;* = 2, and *t* = 3, the function would return
~~~~
u(3) = inf
u(3) = 47.1796
u(3) = 40.7823
u(3) = 40.2314
~~~~
As another example, if *n* = 3, 30, 300, and 3000, *&lambda;* = -1, *&alpha;* = 2, and *t* = 3, the function would return
~~~~
u(3) = 0.25
u(3) = 0.114617
u(3) = 0.101069
u(3) = 0.0997235
~~~~
Finally, if *n* = 3, 30, 300, and 3000, *&lambda;* = -100, *&alpha;* = 2, and *t* = 3, the function would return
~~~~
u(3) = 1.94118e-06
u(3) = 1.14617e-31
u(3) = 9.81819e-91
u(3) = 1.32732e-124
~~~~
**Implementation/Code:** The following is the code for simpleIVP_implicitEuler():
~~~~
double simpleIVP_implicitEuler(int n, double l, double a, double t)
{
	double k = t / n;

	//u = u_old + k(lu) -> u(1 - kl) = u_old -> u = u_old / (1 - kl)
	double u = a / (1 - (k * l));

	for (int i = 1; i < n; i++)
	{
		u = u / (1 - (k * l));
	}

	return u;
}
~~~~
**Last Modified:** 29 Mar 18
