# Simple IVP - Explicit Euler

**Function Name:** simpleIVP_explicitEuler

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function uses the explicit Euler method to solve *u' = &lambda;u* with *u(0) = &alpha;* at a specified time *t*. Compare the results to [Simple IVP - Exact](https://andrewshaw15.github.io/MATH-5620/HW-5/simpleIVP-exact).

**Input:** This function takes as input the number of time steps *n*, the initial value *&alpha;*, the constant coefficient *&lambda;*, and the time *t*.

**Output:** This function returns the value of *u* at time *t*.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "u(" << t << ") = " << simpleIVP_explicitEuler(n, a, l, t) << endl;
~~~~
For example, if *n* = 3, 30, 300, and 3000, *&lambda;* = 1, *&alpha;* = 2, and *t* = 3 the function will return
~~~~
u(3) = 16
u(3) = 34.8988
u(3) = 39.5769
u(3) = 40.1109
~~~~
As another example, if *n* = 3, 30, 300, and 3000, *&lambda;* = -1, *&alpha;* = 2, and *t* = 3 the function will return
~~~~
u(3) = 0
u(3) = 0.0847823
u(3) = 0.0980818
u(3) = 0.0994248
~~~~
Finally, if *n* = 3, 30, 300, and 3000, *&lambda;* = -100, *&alpha;* = 2, and *t* = 3 the function will return
~~~~
u(3) = -1.9406e+06
u(3) = 8.47823e+28
u(3) = 0
u(3) = 1.06797e-137
~~~~
**Implementation/Code:** The following is the code for simpleIVP_explicitEuler():
~~~~
double simpleIVP_explicitEuler(int n, double a, double l, double t)
{
	double k = t / n; //time step

	double u = a + (k * (l * a));

	for (int i = 1; i < n; i++)
	{
		u += (k * (l * u));
	}

	return u;
}
~~~~
**Date Modified:** 27 Mar 18
