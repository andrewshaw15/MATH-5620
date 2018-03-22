# Logistic Differential Equation Test

**Function Name:** calcP

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function gives the analytical solution to the logistic differential equation *P'(t) = aP - b(P^2)*. This function will be used as a standard of comparison against later functions that will find approximate solutions to the above equation.

**Input:** This function requires four inputs: *a*, *b*, *P(0)*, and *t*, where *a* and *b* are the constant coefficients in the equation, *P(0)* is the initial condition (the value of *P* when *t* = 0), and *t* is the time at which the value of *P* is to be known.

**Output:** This function returns the value of *P* at the specified time *t* with the inputted *a* and *b* values.

**Usage/Example:** This function may be called and the value of *P* at time *t* displayed as follows:
~~~~
cout << "P(" << t << ") = " << calcP(alpha, beta, P0, t) << endl;
~~~~
For instance, if *a* = 4.2, *b* = 1.3, *P(0)* = 2.7, and *t* = 5, the function would return
~~~~
P(5) = 3.23077
~~~~
**Implementation/Code:** The following illustrates the function calcP()
~~~~
double calcP(double alpha, double beta, double P0, double t)
{
	return (alpha / (beta - ((beta - (alpha / P0)) * exp(-alpha * t))));
}
~~~~
**Last Modified:** 22 Jan 18
