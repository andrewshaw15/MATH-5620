# Logistic IVP - Exact

**Function Name:** logisticIVP

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function gives the analytical solution to the logistic differential equation *P'(t) = &gamma;P - &beta;(P^2)* at a time *t*. This function will be used as a standard of comparison against later functions that will find approximate solutions to the above equation.

**Input:** This function requires four inputs: *&gamma;*, *&beta;*, *P(0)*, and *t*, where *&gamma;* and *&beta;* are the constant coefficients in the equation, *P(0)* is the initial condition (the value of *P* when *t* = 0), and *t* is the time at which the value of *P* is to be known.

**Output:** This function returns the value of *P* at the specified time *t* with the inputted *&gamma;* and *&beta;* values.

**Usage/Example:** This function may be called and the value of *P* at time *t* displayed as follows:
~~~~
cout << "P(" << t << ") = " << logisticIVP(g, b, P0, t) << endl;
~~~~
For instance, if *&gamma;* = 0.1, *&beta;* = 0.0001, *P(0)* = 25, and *t* = 5, the function would return
~~~~
P(5) = 3.23077
~~~~
As another example, if *&gamma;* = 0.1, *&beta;* = 0.0001, *P(0)* = 40000, and *t* = 5, the function would return
~~~~
P(5) = 2447.19
~~~~
**Implementation/Code:** The following illustrates the function logisticIVP()
~~~~
double logisticIVP(double g, double b, double P0, double t)
{
	return (g / (b - ((b - (g / P0)) * exp(-g * t))));
}
~~~~
**Last Modified:** 24 Mar 18
