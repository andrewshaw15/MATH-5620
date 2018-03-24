# Simple IVP - Exact

**Function Name:** simpleIVP

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function calculates the exact solution of the equation *u' = &lambda;u* with the initial condition *u(0) = &alpha;* at a specific time *t*. This function is used as a standard for functions that approximate the solution

**Input:** This function takes as input the coefficient *&lambda;*, the initial condition *&alpha;*, and the time *t*.

**Output:** This function outputs the exact solution of the equation at time *t*.

**Usage/Example:** This function may be called and its solution displayed as follows:
~~~~
cout << "u(" << t << ") = " << simpleIVP(l, a, t) << endl;
~~~~
For example, if *&lambda;* = 1, *&alpha;* = 2, and *t* = 3, the function would return
~~~~
u(3) = 40.1711
~~~~
As another example, if *&lambda* = -1, *&alpha;* = 2, and *t* = 3, the function would return
~~~~
u(3) = 0.0995741
~~~~
And finally, if *&lambda;* = -100, *&alpha;* = 2, and *t* = 3, the function would return
~~~~
u(3) = 1.02964e-130
~~~~
**Implementation/Code:** The following is the code for simpleIVP():
~~~~
double simpleIVP(double l, double a, double t)
{
	return (a * exp(l * t));
}
~~~~
**Last Modified:** 24 Mar 18
