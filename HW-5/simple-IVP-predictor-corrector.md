# Simple IVP - Predictor-Corrector

**Function Name:** simpleIVP_PC

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the equation *u' = &lambda;u* with *u(0) = &alpha;* at a specific time *t* using the four-step Adams-Bashforth method as a predictor and the four-step Adams-Moulton method as a corrector. Compare the solutions with [Simple IVP - Exact](https://andrewshaw15.github.io/MATH-5620/HW-5/simple-IVP-exact).

**Input:** This function takes as input the number of time steps *n*, the coefficient *&lambda;*, the initial condition *&alpha;*, and the time *t*.

**Output:** This function returns the approximated solution to the equation at the specified time *t*.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "u(" << t << ") = " << simpleIVP_PC(n, l, a, t) << endl;
~~~~
For example, if *n* = 3, 30, 300, and 3000, *&lambda;* = 1, *&alpha;* = 2, and *t* = 3, the function will return
~~~~
u(3) = 34.2444
u(3) = 37.4454
u(3) = 39.8581
u(3) = 40.1394
~~~~
As another example, if *n* = 3, 30, 300, and 3000, *&lambda;* = -, *&alpha;* = 2, and *t* = 3, the function will return
~~~~
u(3) = 0.0985243
u(3) = 0.0941469
u(3) = 0.0989054
u(3) = 0.099506
~~~~
Finally, if *n* = 3, 30, 300, and 3000, *&lambda;* = -100, *&alpha;* = 2, and *t* = 3, the function will return
~~~~
u(3) = 4.2572e+11
u(3) = -1.1479e+55
u(3) = -9.70911e-74
u(3) = 1.14744e-130
~~~~
**Implementation/Code:** The following is the code for simpleIVP_PC():
~~~~
double simpleIVP_PC(int n, double l, double a, double t)
{
	double k = t / n;

	double u1_p = a + (k * (l * a)); //first predictor step
	double u1 = a + ((k / 2) * ((l * a) + (l * u1_p))); //first corrector step
	double u2_p = u1 + ((k / 2) * ((-(l * a)) + (3 * (l * u1)))); //second predictor step
	double u2 = u1 + ((k / 12) * (-(l * a) + (8 * (l * u1)) + (5 * (l * u2_p)))); //second corrector step
	double u3_p = u2 + ((k / 12) * ((5 * (l * a)) - (16 * (l * u1)) + (23 * (l * u2)))); //third predictor step
	double u3 = u2 + ((k / 24) * ((l * a) - (5 * (l * u1)) + (19 * (l * u2)) + (9 * (l * u3_p)))); //third corrector step
	double u4_p = u3 + ((k / 24) * (-(9 * (l * a)) + (37 * (l * u1)) - (59 * (l * u2)) + (55 * (l * u3)))); //fourth predictor step
	double u4 = u3 + ((k / 720) * (-(19 * (l * a)) + (106 * (l * u1)) - (264 * (l * u2)) + (646 * (l * u3)) + (251 * (l * u4_p)))); //fourth corrector step

	for (int i = 4; i < n; i++)
	{
		u1_p = u1 + (k * (l * u1));
		u1 = u1 + ((k / 2) * ((l * u1) + (l * u1_p)));
		u2_p = u2 + ((k / 2) * ((-(l * u1)) + (3 * (l * u2))));
		u2 = u2 + ((k / 12) * (-(l * u1) + (8 * (l * u2)) + (5 * (l * u2_p))));
		u3_p = u3 + ((k / 12) * ((5 * (l * u1)) - (16 * (l * u2)) + (23 * (l * u3))));
		u3 = u3 + ((k / 24) * ((l * u1) - (5 * (l * u2)) + (19 * (l * u3)) + (9 * (l * u3_p))));
		u4_p = u4 + ((k / 24) * (-(9 * (l * u1)) + (37 * (l * u2)) - (59 * (l * u3)) + (55 * (l * u4))));
		u4 = u4 + ((k / 720) * (-(19 * (l * u1)) + (106 * (l * u2)) - (264 * (l * u3)) + (646 * (l * u4)) + (251 * (l * u4_p))));
	}

	if (n == 1)
	{
		return u1;
	}
	else if (n == 2)
	{
		return u2;
	}
	else if (n == 3)
	{
		return u3;
	}
	else
	{
		return u4;
	}
}
~~~~
**Last Modified:** 2 Apr 18
