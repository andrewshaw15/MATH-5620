# Example 7.2 - Predictor-Corrector

**Function Name:** example2_PC

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the equation *u' = &lambda;(u - cos(t)) - sin(t)* with *u(0)* = 1 at time *T* = 2. The exact solution is *u = cos(t)*.

**Input:** This function takes as input the number of time steps *n*, the time step *k*, the initial condition *u(0)*, the coefficient *&lambda;*, and a vector representing *f(u,t)*.

**Output:** This function returns the approximated solution of the equation at *T* = 2.

**Usage/Example:** This function may be called and the exact solution and error displayed as follows:
~~~~
cout << "u(" << T << ") = " << example2_PC(n, k, u0, l, f) << endl;
cout << "U(" << T << ") = " << cos(T) << endl;
cout << "Error = " << example2_PC(n, k, u0, l, f) - cos(T) << endl;
~~~~
For example, if *n* = 2000, *k* = 0.001, *u(0)* = 1, *&lambda;* = -10, and *f(u,t) = -&lambda;cos(t) - sin(t)* the function would return
~~~~
u(2) = -0.416364
U(2) = -0.416147
Error = -0.000217144
~~~~
**Implementation/Code:** The following is the code for example2_PC():
~~~~
double example2_PC(int n, double k, double u0, int l, vector<double> f)
{
	double u1_p = u0 + (k * ((l * u0) + f[0]));
	double u1 = u0 + ((k / 2) * (((l * u0) + f[0]) + ((l * u1_p) + f[1])));
	double u2_p = u1 + ((k / 2) * (-((l * u0) + f[0]) + (3 * ((l * u1) + f[1]))));
	double u2 = u1 + ((k / 12) * (-((l * u0) + f[0]) + (8 * ((l * u1) + f[1])) + (5 * ((l * u2_p) + f[2]))));
	double u3_p = u2 + ((k / 12) * ((5 * ((l * u0) + f[0])) - (16 * ((l * u1) + f[1])) + (23 * ((l * u2) + f[2]))));
	double u3 = u2 + ((k / 24) * (((l * u0) + f[0]) - (5 * ((l * u1) + f[1])) + (19 * ((l * u2) + f[2])) + (9 * ((l * u3_p) + f[3]))));
	double u4_p = u3 + ((k / 24) * (-(9 * ((l * u0) + f[0])) + (37 * ((l * u1) + f[1])) - (59 * ((l * u2) + f[2])) + (55 * ((l * u3) + f[3]))));
	double u4 = u3 + ((k / 720) * (-(19 * ((l * u0) + f[0])) + (106 * ((l * u1) + f[1])) - (264 * ((l * u2) + f[2])) + (646 * ((l * u3) + f[3])) + (251 * ((l * u4_p) + f[4]))));

	for (int i = 1; i <= n - 4; i++)
	{
		u1_p = u1 + (k * ((l * u1) + f[i]));
		u1 = u1 + ((k / 2) * (((l * u1) + f[i]) + ((l * u1_p) + f[i + 1])));
		u2_p = u2 + ((k / 2) * (-((l * u1) + f[i]) + (3 * ((l * u2) + f[i + 1]))));
		u2 = u2 + ((k / 12) * (-((l * u1) + f[i]) + (8 * ((l * u2) + f[i + 1])) + (5 * ((l * u2_p) + f[i + 2]))));
		u3_p = u3 + ((k / 12) * ((5 * ((l * u1) + f[i])) - (16 * ((l * u2) + f[i + 1])) + (23 * ((l * u3) + f[i + 2]))));
		u3 = u3 + ((k / 24) * (((l * u1) + f[i]) - (5 * ((l * u2) + f[i + 1])) + (19 * ((l * u3) + f[i + 2])) + (9 * ((l * u3_p) + f[i + 3]))));
		u4_p = u4 + ((k / 24) * (-(9 * ((l * u1) + f[i])) + (37 * ((l * u2) + f[i + 1])) - (59 * ((l * u3) + f[i + 2])) + (55 * ((l * u4) + f[i + 3]))));
		u4 = u4 + ((k / 720) * (-(19 * ((l * u1) + f[i])) + (106 * ((l * u2) + f[i + 1])) - (264 * ((l * u3) + f[i + 2])) + (646 * ((l * u4) + f[i + 3])) + (251 * ((l * u4_p) + f[i + 4]))));
	}

	if (n == 1)
	{
		return u1;
	}
	else if (n == 2)
	{
		return u2;
	}
	else if (n == 3)
	{
		return u3;
	}
	else
	{
		return u4;
	}
}
~~~~
**Last Modified:** 10 Apr 18
