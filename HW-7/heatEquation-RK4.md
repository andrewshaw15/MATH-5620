# Heat Equation - Runge-Kutta 4

**Function Name:** heatEquation_RK4

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of the heat equation *u<sub>t</sub> = &kappa;u<sub>xx</sub>* with initial condition *u(x,0) = f(x)* and boundary conditions *u(0,t) = g<sub>0</sub>(t)* and *u(L,t) = g<sub>L</sub>(t)* for *t > 0* on the interval *0 &le; x &le; L* at position *X* and time *T*.

**Input:** This function takes as input the coefficient *&kappa;*, the length *L*, the number of interior nodes (plus the final node) *i*, the position *X*, the final time *T*, the number of time steps (including the final one) *n*, a vector representing the initial condition *f(x)*, and vectors representing the boundary conditions *g<sub>0</sub>(t)* and *g<sub>L</sub>(t)*.

**Output:** This function approximates the solution of the heat equation at position *X* and time *T*.

**Usage/Example:** This function may be called and its results displayed as follows (*X* - 1 is passed in for *X* for vector index compatability):
~~~~
cout << "U(" << X << "," << T << ") = " << heatEquation_RK4(K, L, i, X - 1, T, n, f, g0, gL) << endl;
~~~~
For example, if *&kappa;* = 0.835; *L* = 10; *i* = 100; *X* = 6.5; *T* = 5; *n* = 5000; *f(x)* is 100 at *x* = 0, 50 at *x = L*, and 0 elsewhere; *g<sub>0</sub>(t)* = 100; and *g<sub>L</sub>(t)* = 50 the function will return
~~~~
U(6.5,5) = 11.6592
~~~~
**Implementation/Code:** The following is the code for heatEquation_RK4():
~~~~
double heatEquation_RK4(double K, double L, int i, double X, double T, int n, vector<double> f, vector<double> g0, vector<double> gL)
{
	double k = T / n; //time step
	double h = L / i; //mesh spacing
	double a = (k * K) / pow(h, 2);

	vector<double> y1(i - 1);

	for (int j = 0; j < i - 1; j++)
	{
		y1[j] = f[j + 1];
	}

	vector<double> y2(i - 1);

	y2[0] = f[1] + ((a / 2) * (f[0] - (2 * y1[0]) + y1[1]));
	for (int j = 1; j < i - 2; j++)
	{
		y2[j] = f[j + 1] + ((a / 2) * (y1[j - 1] - (2 * y1[j]) + y1[j + 1]));
	}
	y2[i - 2] = f[i - 1] + ((a / 2) * (y1[i - 3] - (2 * y1[i - 2]) + f[i]));

	vector<double> y3(i - 1);

	y3[0] = f[1] + ((a / 2) * (g0[1] - (2 * y2[0]) + y2[1]));
	for (int j = 1; j < i - 2; j++)
	{
		y3[j] = f[j + 1] + ((a / 2) * (y2[j - 1] - (2 * y2[j]) + y2[j + 1]));
	}
	y3[i - 2] = f[i - 1] + ((a / 2) * (y2[i - 3] - (2 * y2[i - 2]) + gL[1]));

	vector<double> y4(i - 1);

	y4[0] = f[1] + (a * (g0[1] - (2 * y3[0]) + y3[1]));
	for (int j = 1; j < i - 2; j++)
	{
		y4[j] = f[j + 1] + (a * (y3[j - 1] - (2 * y3[j]) + y3[j + 1]));
	}
	y4[i - 2] = f[i - 1] + (a * (y3[i - 3] - (2 * y3[i - 2]) + gL[1]));

	vector<double> U(i - 1);

	U[0] = f[1] + ((a / 6) * ((f[0] - (2 * y1[0]) + y1[1]) + (2 * (g0[1] - (2 * y2[0]) + y2[1])) + (2 * (g0[1] - (2 * y3[0]) + y3[1])) + (g0[2] - (2 * y4[0]) + y4[1])));
	for (int j = 1; j < i - 2; j++)
	{
		U[j] = f[j + 1] + ((a / 6) * ((y1[j - 1] - (2 * y1[j]) + y1[j + 1]) + (2 * (y2[j - 1] - (2 * y2[j]) + y2[j + 1])) + (2 * (y3[j - 1] - (2 * y3[j]) + y3[j + 1])) + (y4[j - 1] - (2 * y4[j]) + y4[j + 1])));
	}
	U[i - 2] = f[i - 1] + ((a / 6) * ((y1[i - 3] - (2 * y1[i - 2]) + f[i]) + (2 * (y2[i - 3] - (2 * y2[i - 2]) + gL[1])) + (2 * (y3[i - 3] - (2 * y3[i - 2]) + gL[1])) + (y4[i - 3] - (2 * y4[i - 2]) + gL[2])));

	for (int t = 2; t < 2 * n; t += 2)
	{
		for (int j = 0; j < i - 1; j++)
		{
			y1[j] = U[j];
		}

		y2[0] = U[0] + ((a / 2) * (g0[t] - (2 * y1[0]) + y1[1]));
		for (int j = 1; j < i - 2; j++)
		{
			y2[j] = U[j] + ((a / 2) * (y1[j - 1] - (2 * y1[j]) + y1[j + 1]));
		}
		y2[i - 2] = U[i - 2] + ((a / 2) * (y1[i - 3] - (2 * y1[i - 2]) + gL[t]));

		y3[0] = U[0] + ((a / 2) * (g0[t + 1] - (2 * y2[0]) + y2[1]));
		for (int j = 1; j < i - 2; j++)
		{
			y3[j] = U[j] + ((a / 2) * (y2[j - 1] - (2 * y2[j]) + y2[j + 1]));
		}
		y3[i - 2] = U[i - 2] + ((a / 2) * (y2[i - 3] - (2 * y2[i - 2]) + gL[t + 1]));

		y4[0] = U[0] + (a * (g0[t + 1] - (2 * y3[0]) + y3[1]));
		for (int j = 1; j < i - 2; j++)
		{
			y4[j] = U[j] + (a * (y3[j - 1] - (2 * y3[j]) + y3[j + 1]));
		}
		y4[i - 2] = U[i - 2] + (a * (y3[i - 3] - (2 * y3[i - 2]) + gL[t + 1]));

		U[0] = U[0] + ((a / 6) * ((g0[t] - (2 * y1[0]) + y1[1]) + (2 * (g0[t + 1] - (2 * y2[0]) + y2[1])) + (2 * (g0[t + 1] - (2 * y3[0]) + y3[1])) + (g0[t + 2] - (2 * y4[0]) + y4[1])));
		for (int j = 1; j < i - 2; j++)
		{
			U[j] = U[j] + ((a / 6) * ((y1[j - 1] - (2 * y1[j]) + y1[j + 1]) + (2 * (y2[j - 1] - (2 * y2[j]) + y2[j + 1])) + (2 * (y3[j - 1] - (2 * y3[j]) + y3[j + 1])) + (y4[j - 1] - (2 * y4[j]) + y4[j + 1])));
		}
		U[i - 2] = U[i - 2] + ((a / 6) * ((y1[i - 3] - (2 * y1[i - 2]) + gL[t]) + (2 * (y2[i - 3] - (2 * y2[i - 2]) + gL[t + 1])) + (2 * (y3[i - 3] - (2 * y3[i - 2]) + gL[t + 1])) + (y4[i - 3] - (2 * y4[i - 2]) + gL[t + 2])));
	}

	if (round(fmod(X, h)) == 0) //X is on interior node
	{
		return U[X / h];
	}
	else //interpolate
	{
		return (U[floor(X / h)] + (((U[ceil(X / h)] - U[floor(X / h)]) * (X - (h * floor(X / h)))) / ((h * ceil(X / h)) - (h * floor(X / h)))));
	}
}
~~~~
**Last Modified:** 25 Apr 18
