# Logistic IVP - Explicit Euler

**Function Name:** logisticIVP_explicitEuler

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function uses the explicit Euler method to approximate the solution of the logistic equation *P' = &gamma;P - &beta;(P^2)* with *P(0) = P0* at a specified time *t*. Compare the solutions to [Logistic IVP - Exact](https://andrewshaw15.github.io/MATH-5620/HW-1/logistic-IVP-exact).

**Input:** This function requires as input the number of time steps *n*, the coefficients *&gamma;* and *&beta;*, the initial condition *P0*, and the time *t*.

**Output:** This function returns the approximated solution of the logistic equation.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "P(" << t << ") = " << logisticIVP_explicitEuler(n, P0, g, b, t) << endl;
~~~~
For example, if *n* = 5, 50, 500, and 5000, *&gamma;* = 0.1, *&beta;* = 0.0001, *P0* = 25, and *t* = 5, the function would return
~~~~
P(5) = 39.7102
P(5) = 40.4698
P(5) = 40.5511
P(5) = 40.5593
~~~~
As another example, if *n* = 5, 50, 500, and 5000, *&gamma;* = 0.1, *&beta;* = 0.0001, *P0* = 40000, and *t* = 5, the function would return
~~~~
P(5) = -2.28592e+21
P(5) = 2334.4
P(5) = 2436.38
P(5) = 2446.11
~~~~
**Implementation/Code:** The following is the code for logisticIVP_explicitEuler():
~~~~
double logisticIVP_explicitEuler(int n, double P0, double g, double b, double t)
{
	double k = t / n; //time step

	double P = P0 + (k * ((g * P0) - (b * pow(P0, 2))));

	for (int i = 1; i < n; i++)
	{
		P += (k * ((g * P) - (b * pow(P, 2))));
	}

	return P;
}
~~~~
**Last Modified:** 29 Mar 18
