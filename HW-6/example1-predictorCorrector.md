# Example 7.1 - Predictor-Corrector

**Function Name:** example1_PC

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of the equation *u' = -sin(t)* with *u(0) = 1* at time *T* = 2. The exact solution is *u = cos(t)*.

**Input:** This function takes as input the number of time steps *n*, the time step *k*, the initial condition *u(0)*, and a vector to represent *f(u,t)*.

**Output:** This function returns the approximated solution of the equation at *T* = 2.

**Usage/Example:** This function may be called and the exact solution and error may be shown as follows:
~~~~
cout << "u(" << T << ") = " << example1_PC(n, k, u0, f) << endl;
cout << "U(" << T << ") = " << cos(T) << endl;
cout << "Error = " << example1_PC(n, k, u0, f) - cos(T) << endl;
~~~~
For example, if *n* = 2000, *k* = 0.001, *u(0)* = 1, and *f(u,t) = -sin(t)* the function will return
~~~~
u(2) = -0.416147
U(2) = -0.416147
Error = 8.39329e-14
~~~~
**Implementation/Code:** The following is the code for example1_PC():
~~~~
double example1_PC(int n, double k, double u0, vector<double> f)
{
	double u1_p = u0 + (k * f[0]);
	double u1 = u0 + ((k / 2) * (f[0] + f[1]));
	double u2_p = u1 + ((k / 2) * (-f[0] + (3 * f[1])));
	double u2 = u1 + ((k / 12) * (-f[0] + (8 * f[1]) + (5 * f[2])));
	double u3_p = u2 + ((k / 12) * ((5 * f[0]) - (16 * f[1]) + (23 * f[2])));
	double u3 = u2 + ((k / 24) * (f[0] - (5 * f[1]) + (19 * f[2]) + (9 * f[3])));
	double u4_p = u3 + ((k / 24) * (-(9 * f[0]) + (37 * f[1]) - (59 * f[2]) + (55 * f[3])));
	double u4 = u3 + ((k / 720) * (-(19 * f[0]) + (106 * f[1]) - (264 * f[2]) + (646 * f[3]) + (251 * f[4])));

	for (int i = 1; i <= n - 4; i++)
	{
		u1_p = u1 + (k * f[i]);
		u1 = u1 + ((k / 2) * (f[i] + f[i + 1]));
		u2_p = u2 + ((k / 2) * (-f[i] + (3 * f[i + 1])));
		u2 = u2 + ((k / 12) * (-f[i] + (8 * f[i + 1]) + (5 * f[i + 2])));
		u3_p = u3 + ((k / 12) * ((5 * f[i]) - (16 * f[i + 1]) + (23 * f[i + 2])));
		u3 = u3 + ((k / 24) * (f[i] - (5 * f[i + 1]) + (19 * f[i + 2]) + (9 * f[i + 3])));
		u4_p = u4 + ((k / 24) * (-(9 * f[i]) + (37 * f[i + 1]) - (59 * f[i + 2]) + (55 * f[i + 3])));
		u4 = u4 + ((k / 720) * (-(19 * f[i]) + (106 * f[i + 1]) - (264 * f[i + 2]) + (646 * f[i + 3]) + (251 * f[i + 4])));
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
