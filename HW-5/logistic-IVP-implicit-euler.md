# Logistic IVP - Implicit Euler

**Function Name:** logisticIVP_implicitEuler

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of the logistic equation *P' = &gamma;P - &beta;(P^2)* with *P(0) = P0* at a specified time *t* using the implicit Euler method. Compare the solutions to [Logistic IVP - Exact](https://andrewshaw15.github.io/MATH-5620/HW-1/logistic-IVP-exact).

**Input:** This function takes as input the number of time steps *n*, the coefficients *&gamma;* and *&beta;*, the initial condition *P(0)*, and the time *t*.

**Output:** This function returns the approximated solution to the logistic equation at time *t*.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "P(" << t << ") = " << logisticIVP_implicitEuler(n, g, b, P0, t) << endl;
~~~~
For example, if *n* = 5, 50, 500, and 5000, *&gamma;* = 0.1, *&beta;* = 0.0001, *P(0)* = 25, and *t* = 5 the function will return
~~~~
P(5) = 41.5406
P(5) = 40.6519
P(5) = 40.5693
P(5) = 40.5611
~~~~
As another example, if *n* = 5, 50, 500, and 5000, *&gamma;* = 0.1, *&beta;* = 0.0001, *P(0)* = 40000, and *t* = 5 the function will return
~~~~
P(5) = 3539.55
P(5) = 2553.51
P(5) = 2457.94
P(5) = 2448.26
~~~~
**Implementation/Code:** The following is the code for logisticIVP_implicitEuler():
~~~~
double logisticIVP_implicitEuler(int n, double g, double b, double P0, double t)
{
	double k = t / n;
	
	//quadratic formula        v-<- tried -sqrt(...) here and P returned undefined
	double P = (-(1 - (k * g)) + sqrt(pow((1 - (k * g)), 2) - (4 * (k * b) * (-P0)))) / (2 * k * b);

	for (int i = 1; i < n; i++)
	{
		P = (-(1 - (k * g)) + sqrt(pow((1 - (k * g)), 2) - (4 * (k * b) * (-P)))) / (2 * k * b);
	}

	return P;
}
~~~~
**Last Modified:** 2 Apr 18
