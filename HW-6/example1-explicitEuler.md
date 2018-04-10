# Example 7.1 - Explicit Euler

**Function Name:** example1_explicitEuler

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function approximates the solution of *u' = -sin(t)* with *u(0) = 1* at time *T = 2* with step size *k = 0.001* (thus the number of steps *n* = 2000). The exact solution is *u = cos(t)*, and the exact solution at time *T* with the error is given in the examples below.

**Input:** This function takes as input the number of time steps *n*, the step size *k*, the initial condition *u(0)*, and the function *f(u,t)* represented as a vector.

**Output:** This function returns the approximation to the differential equation at time *T*.

**Example/Usage:** This function may be called and the exact solution and error displayed as follows:
~~~~
cout << "u(" << T << ") = " << example1_explicitEuler(n, k, u0, f1) << endl;
cout << "U(" << T << ") = " << cos(T) << endl;
cout << "Error = " << example1_explicitEuler(n, k, u0, f1) - cos(T) << endl;
~~~~
For example, if the values for *n*, *k*, *u(0)*, *f(u,t)*, and *T* are used as described above, the function will return
~~~~
u(2) = -0.415692
U(2) = -0.416147
Error = 0.000454767
~~~~
**Implementation/Code:** The following is the code for example1_explicitEuler():
~~~~
double example1_explicitEuler(int n, double k, double u0, vector<double> f)
{
	double u = u0 + (k * f[0]);

	for (int i = 1; i < n; i++)
	{
		u += (k * f[i]);
	}

	return u;
}
~~~~
**Last Modified:** 10 Apr 18
