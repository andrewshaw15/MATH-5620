# Heat Equation - Implicit Euler

**Function Name:** heatEquation_implicitEuler

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of the heat equation *u<sub>t</sub> = &kappa;u<sub>xx</sub>* with the initial condition *u(x,0) = f(x)* and boundary conditions *u(0,t) = g<sub>0</sub>(t)* and *u(L,t) = g<sub>L</sub>(t)* for *t > 0* on the interval *0 &le; x &le; L* at position *X* at time *T*.

**Input:** This function takes as input the coefficient *&kappa;*, the length *L*, the number of interior nodes (plus the end node) *i*, the position *X*, the final time *T*, the number of time steps *n*, a vector representing *f(x)*, and two vectors representing *g<sub>0</sub>(t)* and *g<sub>L</sub>(t)*.

**Output:** This function returns the approximated solution of the heat equation at position *X* and time *T*.

**Usage/Example:** This function may be called and its results displayed as follows (*X* is passed as *X* - 1 for vector index compatability):
~~~~
cout << "U(" << X << "," << T << ") = " << heatEquation_implicitEuler(K, L, i, X - 1, T, n, f, g0, gL) << endl;
~~~~
For example, if *&kappa;* = 0.835; *L* = 10; *i* = 100; *X* = 6.5; *T* = 5; *n* = 5000; *f(x)* is 100 at *x* = 0, 50 at *x = L*, and 0 elsewhere; *g<sub>0</sub>(t)* = 100; and *g<sub>L</sub>(t)* = 50 the function will return
~~~~
U(6.5,5) = 14.6344
~~~~
As another example, if *&kappa;* = 0.835; *L* = 10; *i* = 100; *X* = 6.5; *T* = 5; *n* = 500; *f(x)* is 100 at *x* = 0, 50 at *x = L*, and 0 elsewhere; *g<sub>0</sub>(t)* = 100; and *g<sub>L</sub>(t)* = 50 the function will return
~~~~
U(6.5,5) = 14.6326
~~~~
As another example, if *&kappa;* = 0.835; *L* = 10; *i* = 100; *X* = 6.5; *T* = 5; *n* = 50; *f(x)* is 100 at *x* = 0, 50 at *x = L*, and 0 elsewhere; *g<sub>0</sub>(t)* = 100; and *g<sub>L</sub>(t)* = 50 the function will return
~~~~
U(6.5,5) = 14.6145
~~~~
Finally, if *&kappa;* = 0.835; *L* = 10; *i* = 100; *X* = 6.5; *T* = 5; *n* = 5; *f(x)* is 100 at *x* = 0, 50 at *x = L*, and 0 elsewhere; *g<sub>0</sub>(t)* = 100; and *g<sub>L</sub>(t)* = 50 the function will return
~~~~
U(6.5,5) = 14.4341
~~~~
**Implementation/Code:** The following is the code for heatEquation_implicitEuler():
~~~~
double heatEquation_implicitEuler(double K, double L, int i, double X, double T, int n, vector<double> f, vector<double> g0, vector<double> gL)
{
	double h = L / i; //mesh spacing
	double k = T / n; //time step
	double a = (K * k) / pow(h, 2);

	vector<double> U(i - 1); //vector of interior node solutions for each time step

	//Thomas Algorithm
	vector<double> w(i - 1); //sub-diagonal elements vector

	w[0] = 0;
	for (int j = 1; j < i - 1; j++)
	{
		w[j] = -a;
	}

	vector<double> x(i - 1); //diagonal elements vector

	for (int j = 0; j < i - 1; j++)
	{
		x[j] = 1 + (2 * a);
	}

	vector<double> y(i - 1); //super-diagonal elements vector

	for (int j = 0; j < i - 2; j++)
	{
		y[j] = -a;
	}
	y[i - 2] = 0;

	vector<double> z(i - 1); //right hand side vector

	z[0] = f[1] + (a * g0[1]);
	for (int j = 1; j < i - 2; j++)
	{
		z[j] = f[j + 1];
	}
	z[i - 2] = f[i - 1] + (a * gL[1]);

	for (int j = 1; j < i - 1; j++)
	{
		w[j] = w[j] / x[j - 1];
		x[j] = x[j] - (w[j] * y[j - 1]);
		z[j] = z[j] - (w[j] * z[j - 1]);
	}

	U[i - 2] = z[i - 2] / x[i - 2];

	for (int j = i - 3; j >= 0; j--)
	{
		U[j] = (z[j] - (y[j] * U[j + 1])) / x[j];
	}

	for (int t = 1; t < n; t++) //time step
	{
		//reset matrix elements
		w[0] = 0;
		for (int j = 1; j < i - 1; j++)
		{
			w[j] = -a;
		}

		for (int j = 0; j < i - 1; j++)
		{
			x[j] = 1 + (2 * a);
		}

		for (int j = 0; j < i - 2; j++)
		{
			y[j] = -a;
		}
		y[i - 2] = 0;

		//recalculate right hand side vector
		z[0] = U[0] + (a * g0[t + 1]);
		for (int j = 1; j < i - 2; j++)
		{
			z[j] = U[j];
		}
		z[i - 2] = U[i - 2] + (a * gL[t + 1]);

		for (int j = 1; j < i - 1; j++)
		{
			w[j] = w[j] / x[j - 1];
			x[j] = x[j] - (w[j] * y[j - 1]);
			z[j] = z[j] - (w[j] * z[j - 1]);
		}

		U[i - 2] = z[i - 2] / x[i - 2];

		for (int j = i - 3; j >= 0; j--)
		{
			U[j] = (z[j] - (y[j] * U[j + 1])) / x[j];
		}
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
**Last Modified:** 24 Apr 18
