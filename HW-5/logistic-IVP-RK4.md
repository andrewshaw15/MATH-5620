# Logistic IVP - RK4

**Function Name:** logisticIVP_RK4

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of the logistic equation *P' = &gamma;P - &beta;(P^2)* with *P(0) = P0* at a specified time *t*. Compare the solutions with [Logistic IVP - Exact](https://andrewshaw15.github.io/HW-1/logistic-IVP-exact).

**Input:** This function requires as input the number of time steps *n*, the coefficients *&gamma;* and *&beta;*, the initial condition *P(0)*, and the time *t*.

**Output:** This function returns the approximated solution of the logistic equation at time *t*.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "P(" << t << ") = " << logisticIVP_RK4(n, g, b, P0, t) << endl;
~~~~
For example, if *n* = 5, 50, 500, and 5000, *&gamma;* = 0.1, *&beta;* = 0.0001, *P(0)* = 25, and *t* = 5 the function would return
~~~~
P(5) = 40.5602
P(5) = 40.5602
P(5) = 40.5602
P(5) = 40.5602
~~~~
As another example, if *n* = 5, 50, 500, and 5000, *&gamma;* = 0.1, *&beta;* = 0.0001, *P(0)* = 40000, and *t* = 5 the function would return
~~~~
P(5) = -inf
P(5) = 2447.2
P(5) = 2447.19
P(5) = 2447.19
~~~~
**Implementation/Code:** The following is the code for logisticIVP_RK4():
~~~~
double logisticIVP_RK4(int n, double g, double b, double P0, double t)
{
	double k = t / n;

	double y1 = P0;
	double y2 = P0 + (0.5 * k * ((g * y1) - (b * pow(y1, 2))));
	double y3 = P0 + (0.5 * k * ((g * y2) - (b * pow(y2, 2))));
	double y4 = P0 + (k * ((g * y3) - (b * pow(y3, 2))));
	double P = P0 + ((k / 6) * (((g * y1) - (b * pow(y1, 2))) + (2 * ((g * y2) - (b * pow(y2, 2)))) + (2 * ((g * y3) - (b * pow(y3, 2)))) + ((g * y4) - (b * pow(y4, 2)))));

	for (int i = 1; i < n; i++)
	{
		y1 = P;
		y2 = P + (0.5 * k * ((g * y1) - (b * pow(y1, 2))));
		y3 = P + (0.5 * k * ((g * y2) - (b * pow(y2, 2))));
		y4 = P + (k * ((g * y3) - (b * pow(y3, 2))));
		P = P + ((k / 6) * (((g * y1) - (b * pow(y1, 2))) + (2 * ((g * y2) - (b * pow(y2, 2)))) + (2 * ((g * y3) - (b * pow(y3, 2)))) + ((g * y4) - (b * pow(y4, 2)))));
	}

	return P;
}
~~~~
**Last Modified:** 2 Apr 18
