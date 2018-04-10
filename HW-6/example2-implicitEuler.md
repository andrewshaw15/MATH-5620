# Example 7.2 - Implicit Euler

**Function Name:** example2_implicitEuler

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of *u' = &lambda;(u - cos(t)) - sin(t)* with *u(0) = 1* at *T = 2*. The exact solution is *u = cos(t)*. As a note, it would appear that the error increases roughly by a factor of ten as *k* increases by a factor of ten, reaching a limit of ~0.001.

**Input:** This function takes as input the number of steps *n*, the step size *k*, the initial condition *u(0)*, and a vector representing *f(u,t)*.

**Output:** This function returns the approximated solution of the equation at *T* = 2.

**Usage/Example:** This function may be called and the exact answer and error shown as follows:
~~~~
cout << "u(" << T << ") = " << example2_implicitEuler(n, k, u0, l, f) << endl;
cout << "U(" << T << ") = " << cos(T) << endl;
cout << "Error = " << example2_implicitEuler(n, k, u0, l, f) - cos(T) << endl;
~~~~
For example, if *n* = 2000, *k* = 0.001, *u(0)* = 1, and *f(u,t) = -&lambda;cos(t) - sin(t)* the function would return
~~~~
u(2) = -0.416131
U(2) = -0.416147
Error = 1.60836e-05
~~~~
If *n* = 200, *k* = 0.01, *u(0)* = 1, and *f(u,t) = -&lambda;cos(t) - sin(t)* the function would return
~~~~
u(2) = -0.415987
U(2) = -0.416147
Error = 0.000159373
~~~~
If *n* = 20, *k* = 0.1, *u(0)* = 1, and *f(u,t) = -&lambda;cos(t) - sin(t)* the function would return
~~~~
u(2) = -0.414699
U(2) = -0.416147
Error = 0.0014478
~~~~
If *n* = 2, *k* = 1, *u(0)* = 1, and *f(u,t) = -&lambda;cos(t) - sin(t)* the function would return
~~~~
u(2) = -0.415015
U(2) = -0.416147
Error = 0.00113137
~~~~
**Implementation/Code:** The following is the code for example2_implicitEuler():
~~~~
double example2_implicitEuler(int n, double k, double u0, int l, vector<double> f)
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
