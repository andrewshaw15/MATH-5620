# Example 7.1 - Implicit Euler

**Function Name:** example1_implicitEuler

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of *u' = -sin(t)* with *u(0) = 1* at *T = 2*. The exact solution is *u = cos(t)*. As a note, it would appear that the error increases by a factor of ten if *k* is increased by a factor of ten.

**Input:** This function takes as input the number of time steps *n*, the step size *k*, the initial condition *u(0)*, and a vector representing *f(u,t)*.

**Output:** This function returns the approximation of the equation at time *T*.

**Usage/Example:** This function may be called and the exact solution and error shown as follows:
~~~~
cout << "u(" << T << ") = " << example1_implicitEuler(n, k, u0, f) << endl;
cout << "U(" << T << ") = " << cos(T) << endl;
cout << "Error = " << example1_implicitEuler(n, k, u0, f) - cos(T) << endl;
~~~~
For example, if *n* = 2000, *k* = 0.001, *u(0)* = 1, and *f(u,t) = -sin(t)* the function will return
~~~~
u(2) = -0.416601
U(2) = -0.416147
Error = -0.000454531
~~~~
If *n* = 200, *k* = 0.01, *u(0)* = 1, and *f(u,t) = -sin(t)* the function will return
~~~~
u(2) = -0.420682
U(2) = -0.416147
Error = -0.00453469
~~~~
If *n* = 20, *k* = 0.1, *u(0)* = 1, and *f(u,t) = -sin(t)* the function will return
~~~~
u(2) = -0.460431
U(2) = -0.416147
Error = -0.0442846
~~~~
If *n* = 2, *k* = 1, *u(0)* = 1, and *f(u,t) = -sin(t)* the function will return
~~~~
u(2) = -0.750768
U(2) = -0.416147
Error = -0.334622
~~~~
**Implementation/Code:** The following is the code for example1_implicitEuler():
~~~~
double example1_implicitEuler(int n, double k, double u0, vector<double> f)
{
	double u = u0 + (k * f[0]);

	for (int i = 1; i < n; i++)
	{
		u += k * f[i];
	}

	return u;
}
~~~~
**Last Modified:** 10 Apr 18
