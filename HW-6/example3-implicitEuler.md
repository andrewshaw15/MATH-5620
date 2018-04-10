# Example 7.3 - Implicit Euler

**Function Name:** example3_implicitEuler

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of *u' = &lambda;(u - cos(t)) - sin(t)* with *u(0) = 1* at *T* = 2. The exact solution is *u = cos(t)*. As a note, the error appears to increase roughly by a factor of ten as *k* is increased by a factor of ten, approaching a limit as *k* increases.

**Input:** This function takes as input the number of time steps *n*, the time step *k*, the initial condition *u(0)*, the coefficient *&lambda;*, and a vector representing *f(u,t)*.

**Output:** This function returns the approximation to the equation at *T* = 2.

**Example/Usage:** This function may be called and the exact solution and error displayed as follows:
~~~~
cout << "u(" << T << ") = " << example3_implicitEuler(n, k, u0, l, f) << endl;
cout << "U(" << T << ") = " << cos(T) << endl;
cout << "Error = " << example3_implicitEuler(n, k, u0, l, f) - cos(T) << endl;
~~~~
For example, if *n* = 2000, *k* = 0.001, *u(0)* = 1, *&lambda;* = -10, and *f(u,t) = -&lambda;cos(t) - sin(t)* the function would return
~~~~
u(2) = -0.416147
U(2) = -0.416147
Error = 9.89072e-08
~~~~
If *n* = 200, *k* = 0.01, *u(0)* = 1, *&lambda;* = -10, and *f(u,t) = -&lambda;cos(t) - sin(t)* the function would return
~~~~
u(2) = -0.416146
U(2) = -0.416147
Error = 9.82566e-07
~~~~
If *n* = 20, *k* = 0.1, *u(0)* = 1, *&lambda;* = -10, and *f(u,t) = -&lambda;cos(t) - sin(t)* the function would return
~~~~
u(2) = -0.416138
U(2) = -0.416147
Error = 9.16804e-06
~~~~
If *n* = 2, *k* = 1, *u(0)* = 1, *&lambda;* = -10, and *f(u,t) = -&lambda;cos(t) - sin(t)* the function would return
~~~~
u(2) = -0.416124
U(2) = -0.416147
Error = 2.2356e-05
~~~~
**Implementation/Code:** The following is the code for example3_implicitEuler():
~~~~
double example3_implicitEuler(int n, double k, double u0, int l, vector<double> f)
{
	double u = (u0 + (k * f[0])) / (1 - (k * l));

	for (int i = 1; i < n; i++)
	{
		u = (u + (k * f[i])) / (1 - (k * l));
	}

	return u;
}
~~~~
**Last Modified:** 10 Apr 18
