# Simple IVP - RK4

**Function Name:** simpleIVP_RK4

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of the equation *u' = &lambda;u* with *u(0) = &alpha;* at a specified time *t* using the four-stage Runge-Kutta method (RK4). Compare the solutions to [Simple IVP - Exact](https://andrewshaw15.github.io/MATH-5620/HW-5/simple-IVP-exact).

**Input:** This function takes as input the number of time steps *n*, the coefficient *&lambda;*, the initial conditions *&alpha;*, and the time *t*.

**Output:** This function returns the approximated solution of the above equation at time *t*.

**Usage/Example:** This function may be called and its results displayed as follows
~~~~
cout << "u(" << t << ") = " << simpleIVP_RK4(n, l, a, t) << endl;
~~~~
For example, if *n* = 3, 30, 300, and 3000, *&lambda;* = 1, *&alpha;* = 2, and *t* = 3 the function would return
~~~~
u(3) = 39.7316
u(3) = 40.171
u(3) = 40.1711
u(3) = 40.1711
~~~~
As another example, if *n* = 3, 30, 300, and 3000, *&lambda;* = -1, *&alpha;* = 2, and *t* = 3 the function would return
~~~~
u(3) = 0.105469
u(3) = 0.0995744
u(3) = 0.0995741
u(3) = 0.0995741
~~~~
Finally, if *n* = 3, 30, 300, and 3000, *&lambda;* = -100, *&alpha;* = 2, and *t* = 3 the function would return
~~~~
u(3) = 1.28471e+20
u(3) = 1.65128e+74
u(3) = 3.239e-128
u(3) = 1.02992e-130
~~~~
**Implementation/Code:** The following is the code for simpleIVP_RK4():
~~~~
double simpleIVP_RK4(int n, double l, double a, double t)
{
	double k = t / n;

	double y1 = a;
	double y2 = a + (0.5 * k * (l * y1));
	double y3 = a + (0.5 * k * (l * y2));
	double y4 = a + (k * (l * y3));
	double u = a + ((k / 6) * ((l * y1) + (2 * (l * y2)) + (2 * (l * y3)) + (l * y4)));

	for (int i = 1; i < n; i++)
	{
		y1 = u;
		y2 = u + (0.5 * k * (l * y1));
		y3 = u + (0.5 * k * (l * y2));
		y4 = u + (k * (l * y3));
		u = u + ((k / 6) * ((l * y1) + (2 * (l * y2)) + (2 * (l * y3)) + (l * y4)));
	}

	return u;
}
~~~~
**Last Modified:** 2 Apr 18
