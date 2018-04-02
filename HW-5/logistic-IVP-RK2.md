# Logistic IVP - RK2

**Function Name:** logisticIVP_RK2

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of the logistic equation *P' = &gamma;P - &beta;(P^2)* with *P(0) = P0* at a specific time *t* using the two-stage Runge-Kutta method (RK2). Compare the solutions with [Logistic IVP - Exact](https://andrewshaw15.github.io/MATH-5620/HW-1/logistic-IVP-exact).

**Input:** This function takes as input the number of time steps *n*, the coefficients *&gamma;* and *&beta;*, the initial condition *P(0)*, and time *t*.

**Output:** This function returns the approximated solution of the logistic equation at time *t*.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "P(" << t << ") = " << logisticIVP_RK2(n, g, b, P0, t) << endl;
~~~~
For example, if *n* = 5, 50, 500, and 5000, *&gamma;* = 0.1, *&beta;* = 0.0001, *P(0)* = 25, and *t* = 5 the function would return
~~~~
P(5) = 40.5342
P(5) = 40.5599
P(5) = 40.5602
P(5) = 40.5602
~~~~
As another example, if *n* = 5, 50, 500, and 5000, *&gamma;* = 0.1, *&beta;* = 0.0001, *P(0)* = 40000, and *t* = 5 the function would return
~~~~
P(5) = -3.58657e+227
P(5) = 2461.83
P(5) = 2447.29
P(5) = 2447.19
~~~~
**Implementation/Code:** The following is the code for logisticIVP_RK2():
~~~~
double logisticIVP_RK2(int n, double g, double b, double P0, double t)
{
	double k = t / n;

	double P_star = P0 + (0.5 * k * ((g * P0) - (b * pow(P0, 2))));
	double P = P0 + (k * ((g * P_star) - (b * pow(P_star, 2))));

	for (int i = 1; i < n; i++)
	{
		P_star = P + (0.5 * k * ((g * P) - (b * pow(P, 2))));
		P = P + (k * ((g * P_star) - (b * pow(P_star, 2))));
	}

	return P;
}
~~~~
**Last Modified:** 2 Apr 18
