# Example 7.2 - Runge-Kutta 4

**Function Name:** example2_RK4

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution to the equation *u' = &lambda(u - cos(t)) - sin(t)* with *u(0) = 1* at time *T = 2*. The exact solution is *u = cos(t)*.

**Input:** This function takes as input the number of time steps *n*, the time step *k*, the initial condition *u(0)*, the coefficient *&lambda;*, and a vector representing *f(u,t)*. Note that odd indices indicate half-step values while even indices indicate full-step values.

**Output:** This function returns the approximate solution of the equation at time *T* = 2.

**Usage/Example:** This function may be called and the exact solution and error displayed as follows:
~~~~
cout << "u(" << T << ") = " << example2_RK4(n, k, u0, l, f) << endl;
cout << "U(" << T << ") = " << cos(T) << endl;
cout << "Error = " << example2_RK4(n, k, u0, l, f) - cos(T) << endl;
~~~~
For example, if *n* = 2000, *k* = 0.001, *u(0)* = 1, *&lambda;* = -10, and *f(u,t) = -&lambda;cos(t) - sin(t)* the function would return
~~~~
u(2) = -0.415844
U(2) = -0.416147
Error = 0.000303133
~~~~
**Implementation/Code:** The following is the code for example2_RK4():
~~~~
double example2_RK4(int n, double k, double u0, int l, vector<double> f)
{
	double y1 = u0;
	double y2 = u0 + ((k / 2) * ((l * y1) + f[0]));
	double y3 = u0 + ((k / 2) * ((l * y2) + f[1]));
	double y4 = u0 + (k * ((l * y3) + f[1]));
	double u = u0 + ((k / 6) * (((l * y1) + f[0]) + (2 * ((l * y2) + f[1])) + (2 * ((l * y3) + f[1])) + ((l * y4) + f[2])));

	for (int i = 2; i < 2 * n; i += 2)
	{
		y1 = u;
		y2 = u + ((k / 2) * ((l * y1) + f[i]));
		y3 = u + ((k / 2) * ((l * y2) + f[i + 1]));
		y4 = u + (k * ((l * y3) + f[i + 1]));
		u = u + ((k / 6) * (((l * y1) + f[i]) + (2 * ((l * y2) + f[i + 1])) + (2 * ((l * y3) + f[i + 1])) + ((l * y4) + f[i + 2])));
	}

	return u;
}
~~~~
**Last Modified:** 10 Apr 18
