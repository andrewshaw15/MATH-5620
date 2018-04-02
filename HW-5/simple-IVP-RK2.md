# Simple IVP - RK2

**Function Name:** simpleIVP_RK2

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of the equation *u' = &lambda;u* with *u(0) = &alpha;* at a specific time *t* using the two-stage Runge-Kutta method (RK2). Compare the solutions to [Simple IVP - Exact](https://andrewshaw15.github.io/MATH-5620/HW-5/simple-IVP-exact).

**Input:** This function takes as input the number of time steps *n*, the coefficient *&lambda;*, the initial condition *&alpha;*, and the time *t*.

**Output:** This function returns the approximated solution to the above equation at time *t*.

**Usage/Example:** The function may be called and its results displayed as follows
~~~~
cout << "u(" << t << ") = " << simpleIVP_RK2(n, l, a, t) << endl;
~~~~
For example, if *n* = 3, 30, 300, and 3000, *&lambda;* = 1, *&alpha;* = 2, and *t* = 3, the function would return
~~~~
u(3) = 31.25
u(3) = 39.9851
u(3) = 40.1691
u(3) = 40.1711
~~~~
As another example, if *n* = 3, 30, 300, and 3000, *&lambda;* = -1, *&alpha;* = 2, and *t* = 3, the function would return
~~~~
u(3) = 0.25
u(3) = 0.100112
u(3) = 0.0995792
u(3) = 0.0995742
~~~~
Finally, if *n* = 3, 30, 300, and 3000, *&lambda;* = -100, *&alpha;* = 2, and *t* = 3, the function would return
~~~~
u(3) = 2.35442e+11
u(3) = 4.83666e+48
u(3) = 9.81819e-91
u(3) = 1.76509e-130
~~~~
**Implementation/Code:** The following is the code for simpleIVP_RK2():
~~~~
double simpleIVP_RK2(int n, double l, double a, double t)
{
	double k = t / n;

	double u_star = a + (0.5 * k * (l * a));
	double u = a + (k * (l * u_star));

	for (int i = 1; i < n; i++)
	{
		u_star = u + (0.5 * k * (l * u));
		u = u + (k * (l * u_star));
	}

	return u;
}
~~~~
**Last Modified:** 2 Apr 18
