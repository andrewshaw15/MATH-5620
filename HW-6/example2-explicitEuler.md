# Example 7.2 - Explicit Euler

**Function Name:** example2_explicitEuler

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of *u' = &lambda;(u - cos(t)) - sin(t)* at time *T = 2* with initial condition *u(0) = 1*. The exact solution is *u = cos(t)*.

**Input:** This function takes as input the number of time steps *n*, the step size *k*, the initial condition *u(0)*, the coefficient *&lambda;*, and the function *f(u,t)* represented as a vector.

**Output:** This function returns the approximated solution at time *T*.

**Example/Usage:** This function may be called and the exact solution and error displayed as follows:
~~~~
cout << "u(" << T << ") = " << example2_explicitEuler(n, k, u0, l, f2) << endl;
cout << "U(" << T << ") = " << cos(T) << endl;
cout << "Error = " << example2_explicitEuler(n, k, u0, l, f2) - cos(T) << endl;
~~~~
For example, if *n* = 2000, *k* = 0.001, *&lambda;* = -10, *u(0)* = 1, and *f(u,t)* is the *t*-dependent components from the equation the function will return
~~~~
u(2) = -0.416163
U(2) = -0.416147
Error = -1.61161e-05
~~~~
**Implementation/Code:** The following is the code for example2_explicitEuler():
~~~~
double example2_explicitEuler(int n, double k, double u0, double l, vector<double> f)
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
