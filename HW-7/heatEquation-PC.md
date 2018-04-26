# Heat Equation - Predictor-Corrector

**Function Name:** heatEquation_PC

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of the heat equation *u<sub>t</sub> = &kappa;u<sub>xx</sub>* with initial condition *u(x,0) = f(x)* and boundary conditions *u(0,t) = g<sub>0</sub>(t)* and *u(L,t) = g<sub>L</sub>(t)* for *t > 0* on the interval *0 &le; x &le; L* at position *X* and time *T*.

**Input:** This function takes as input the coefficient *&kappa;*, the length *L*, the number of interior nodes (including the end node) *i*, the position *X*, the final time *T*, the number of time steps (including the final one) *n*, a vector representing the initial condition *f(x)*, and vectors representing the boundary conditions *g<sub>0</sub>(t)* and *g<sub>L</sub>(t)*.

**Output:** This function returns the approximated solution of the heat equation at position *X* and time *T*.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "U(" << X << "," << T << ") = " << heatEquation_PC(K, L, i, X, T, n, f, g0, gL) << endl;
~~~~
For example, if *&kappa;* = 0.835; *L* = 10; *i* = 100; *X* = 6.5; *T* = 5; *n* = 5000; *f(x)* is 100 at *x* = 0, 50 at *x = L*, and 0 elsewhere; *g<sub>0</sub>(t)* = 100; and *g<sub>L</sub>(t)* = 50 the function will return
~~~~
U(6.5,5) = 15.2592
~~~~
**Implementation/Code:** The following is the code for heatEquation_PC():
~~~~
double heatEquation_PC(double K, double L, int i, double X, double T, int n, vector<double> f, vector<double> g0, vector<double> gL)
{
	double k = T / n;
	double h = L / i;
	double a = (k * K) / pow(h, 2);

	vector<double> u1_p(i + 1); //first prediction

	u1_p[0] = g0[1]; //boundary condition
	for (int j = 1; j < i; j++)
	{
		u1_p[j] = f[j] + (a * (f[j - 1] - (2 * f[j]) + f[j + 1]));
	}
	u1_p[i] = gL[1]; //boundary condition

	vector<double> u1(i + 1); //first correction

	u1[0] = u1_p[0]; //boundary condition
	for (int j = 1; j < i; j++)
	{
		u1[j] = f[j] + ((a / 2) * ((f[j - 1] - (2 * f[j]) + f[j + 1]) + (u1_p[j - 1] - (2 * u1_p[j]) + u1_p[j + 1])));
	}
	u1[i] = u1_p[i]; //boundary condition

	vector<double> u2_p(i + 1); //second prediction

	u2_p[0] = g0[2]; //boundary condition
	for (int j = 1; j < i; j++)
	{
		u2_p[j] = u1[j] + ((a / 2) * (-(f[j - 1] - (2 * f[j]) + f[j + 1]) + (3 * (u1[j - 1] - (2 * u1[j]) + u1[j + 1]))));
	}
	u2_p[i] = gL[2]; //boundary condition

	vector<double> u2(i + 1); //second correction

	u2[0] = u2_p[0]; //boundary condition
	for (int j = 1; j < i; j++)
	{
		u2[j] = u1[j] + ((a / 12) * (-(f[j - 1] - (2 * f[j]) + f[j + 1]) + (8 * (u1[j - 1] - (2 * u1[j]) + u1[j + 1])) + (5 * (u2_p[j - 1] - (2 * u2_p[j]) + u2_p[j + 1]))));
	}
	u2[i] = u2_p[i]; //boundary condition

	vector<double> u3_p(i + 1); //third prediction

	u3_p[0] = g0[3]; //boundary condition
	for (int j = 1; j < i; j++)
	{
		u3_p[j] = u2[j] + ((a / 12) * ((5 * (f[j - 1] - (2 * f[j]) + f[j + 1])) - (16 * (u1[j - 1] - (2 * u1[j]) + u1[j + 1])) + (23 * (u2[j - 1] - (2 * u2[j]) + u2[j + 1]))));
	}
	u3_p[i] = gL[3]; //boundary condition

	vector<double> u3(i + 1); //third correction

	u3[0] = u3_p[0]; //boundary condition
	for (int j = 1; j < i; j++)
	{
		u3[j] = u2[j] + ((a / 24) * ((f[j - 1] - (2 * f[j]) + f[j + 1]) - (5 * (u1[j - 1] - (2 * u1[j]) + u1[j + 1])) + (19 * (u2[j - 1] - (2 * u2[j]) + u2[j + 1])) + (9 * (u3_p[j - 1] - (2 * u3_p[j]) + u3_p[j + 1]))));
	}
	u3[i] = u3_p[i]; //boundary condition

	vector<double> u4_p(i + 1); //fourth prediction

	u4_p[0] = g0[4]; //boundary condition
	for (int j = 1; j < i; j++)
	{
		u4_p[j] = u3[j] + ((a / 24) * (-(9 * (f[j - 1] - (2 * f[j]) + f[j + 1])) + (37 * (u1[j - 1] - (2 * u1[j]) + u1[j + 1])) - (59 * (u2[j - 1] - (2 * u2[j]) + u2[j + 1])) + (55 * (u3[j - 1] - (2 * u3[j]) + u3[j + 1]))));
	}
	u4_p[i] = gL[4]; //boundary condition

	vector<double> u4(i + 1); //fourth correction

	u4[0] = u4_p[0]; //boundary condition
	for (int j = 1; j < i; j++)
	{
		u4[j] = u3[j] + ((a / 720) * (-(19 * (f[j - 1] - (2 * f[j]) + f[j + 1])) + (106 * (u1[j - 1] - (2 * u1[j]) + u1[j + 1])) - (264 * (u2[j - 1] - (2 * u2[j]) + u2[j + 1])) + (646 * (u3[j - 1] - (2 * u3[j]) + u3[j + 1])) + (251 * (u4_p[j - 1] - (2 * u4_p[j]) + u4_p[j + 1]))));
	}
	u4[i] = u4_p[i]; //boundary condition

	for (int t = 5; t < n; t++)
	{
		u1_p[0] = g0[t - 3]; //boundary condition
		for (int j = 1; j < i; j++)
		{
			u1_p[j] = u1[j] + (a * (u1[j - 1] - (2 * u1[j]) + u1[j + 1]));
		}
		u1_p[i] = gL[t - 3]; //boundary condition

		u1[0] = u1_p[0]; //boundary condition
		for (int j = 1; j < i; j++)
		{
			u1[j] = u1[j] + ((a / 2) * ((u1[j - 1] - (2 * u1[j]) + u1[j + 1]) + (u1_p[j - 1] - (2 * u1_p[j]) + u1_p[j + 1])));
		}
		u1[i] = u1_p[i]; //boundary condition

		u2_p[0] = g0[t - 2]; //boundary condition
		for (int j = 1; j < i; j++)
		{
			u2_p[j] = u2[j] + ((a / 2) * (-(u1[j - 1] - (2 * u1[j]) + u1[j + 1]) + (3 * (u2[j - 1] - (2 * u2[j]) + u2[j + 1]))));
		}
		u2_p[i] = gL[t - 2]; //boundary condition

		u2[0] = u2_p[0]; //boundary condition
		for (int j = 1; j < i; j++)
		{
			u2[j] = u2[j] + ((a / 12) * (-(u1[j - 1] - (2 * u1[j]) + u1[j + 1]) + (8 * (u2[j - 1] - (2 * u2[j]) + u2[j + 1])) + (5 * (u2_p[j - 1] - (2 * u2_p[j]) + u2_p[j + 1]))));
		}
		u2[i] = u2_p[i]; //boundary condition

		u3_p[0] = g0[t - 1]; //boundary condition
		for (int j = 1; j < i; j++)
		{
			u3_p[j] = u3[j] + ((a / 12) * ((5 * (u1[j - 1] - (2 * u1[j]) + u1[j + 1])) - (16 * (u2[j - 1] - (2 * u2[j]) + u2[j + 1])) + (23 * (u3[j - 1] - (2 * u3[j]) + u3[j + 1]))));
		}
		u3_p[i] = gL[t - 1]; //boundary condition

		u3[0] = u3_p[0]; //boundary condition
		for (int j = 1; j < i; j++)
		{
			u3[j] = u3[j] + ((a / 24) * ((u1[j - 1] - (2 * u1[j]) + u1[j + 1]) - (5 * (u2[j - 1] - (2 * u2[j]) + u2[j + 1])) + (19 * (u3[j - 1] - (2 * u3[j]) + u3[j + 1])) + (9 * (u3_p[j - 1] - (2 * u3_p[j]) + u3_p[j + 1]))));
		}
		u3[i] = u3_p[i]; //boundary condition

		u4_p[0] = g0[t]; //boundary condition
		for (int j = 1; j < i; j++)
		{
			u4_p[j] = u4[j] + ((a / 24) * (-(9 * (u1[j - 1] - (2 * u1[j]) + u1[j + 1])) + (37 * (u2[j - 1] - (2 * u2[j]) + u2[j + 1])) - (59 * (u3[j - 1] - (2 * u3[j]) + u3[j + 1])) + (55 * (u4[j - 1] - (2 * u4[j]) + u4[j + 1]))));
		}
		u4_p[i] = gL[t]; //boundary condition

		u4[0] = u4_p[0]; //boundary condition
		for (int j = 1; j < i; j++)
		{
			u4[j] = u4[j] + ((a / 720) * (-(19 * (u1[j - 1] - (2 * u1[j]) + u1[j + 1])) + (106 * (u2[j - 1] - (2 * u2[j]) + u2[j + 1])) - (264 * (u3[j - 1] - (2 * u3[j]) + u3[j + 1])) + (646 * (u4[j - 1] - (2 * u4[j]) + u4[j + 1])) + (251 * (u4_p[j - 1] - (2 * u4_p[j]) + u4_p[j + 1]))));
		}
		u4[i] = u4_p[i]; //boundary condition
	}

	if (n == 1)
	{
		if (round(fmod(X, h)) == 0) //X is on interior node
		{
			return u1[X / h];
		}
		else //interpolate
		{
			return (u1[floor(X / h)] + (((u1[ceil(X / h)] - u1[floor(X / h)]) * (X - (h * floor(X / h)))) / ((h * ceil(X / h)) - (h * floor(X / h)))));
		}
	}
	else if (n == 2)
	{
		if (round(fmod(X, h)) == 0) //X is on interior node
		{
			return u2[X / h];
		}
		else //interpolate
		{
			return (u2[floor(X / h)] + (((u2[ceil(X / h)] - u2[floor(X / h)]) * (X - (h * floor(X / h)))) / ((h * ceil(X / h)) - (h * floor(X / h)))));
		}
	}
	else if (n == 3)
	{
		if (round(fmod(X, h)) == 0) //X is on interior node
		{
			return u3[X / h];
		}
		else //interpolate
		{
			return (u3[floor(X / h)] + (((u3[ceil(X / h)] - u3[floor(X / h)]) * (X - (h * floor(X / h)))) / ((h * ceil(X / h)) - (h * floor(X / h)))));
		}
	}
	else
	{
		if (round(fmod(X, h)) == 0) //X is on interior node
		{
			return u4[X / h];
		}
		else //interpolate
		{
			return (u4[floor(X / h)] + (((u4[ceil(X / h)] - u4[floor(X / h)]) * (X - (h * floor(X / h)))) / ((h * ceil(X / h)) - (h * floor(X / h)))));
		}
	}
}
~~~~
**Last Modified:** 25 Apr 18
