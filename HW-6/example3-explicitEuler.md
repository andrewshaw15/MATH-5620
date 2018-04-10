# Example 7.3 - Explicit Euler

**Function Name:** example3_explicitEuler

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of the problem *u' = &lambda;(u - cos(t)) - sin(t)* with *u(0) = 1* at time *T = 2*. The exact solution is *u = cos(t)*.

**Input:** This function takes as input the number of time steps *n*, the step size *k*, the initial condition *u(0)*, the coefficient *&lambda;*, and the function *f(u,t)*.

**Output:** This function returns the approximated solution at time *T*.

**Usage/Example:** The function may be called and the exact solution and error displayed as follows:
~~~~
cout << "u(" << T << ") = " << example3_explicitEuler(n, k, u0, l, f) << endl;
cout << "U(" << T << ") = " << cos(T) << endl;
cout << "Error = " << example3_explicitEuler(n, k, u0, l, f) - cos(T) << endl;
~~~~
For example, if *n* = 2000, *k* = 0.001, *u(0)* = 1, *&lambda;* = -2100, and *f(u,t)* is the *t*-dependent portion from the equation the function will return
~~~~
u(2) = -1.45252e+76
U(2) = -0.416147
Error = -1.45252e+76
~~~~
**Implementation/Code:** The following is the code for example3_explicitEuler():
~~~~
double example3_explicitEuler(int n, double k, double u0, double l, vector<double> f)
{
	double u = u0 + (k * ((l * u0) + f[0]));

	for (int i = 1; i < n; i++)
	{
		u += (k * ((l * u) + f[i]));
	}

	return u;
}
~~~~
**Last Modified:** 10 Apr 18
