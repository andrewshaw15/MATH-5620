# Heat Equation - Explicit Euler

**Function Name:** heatEquation_explicitEuler

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of the heat equation *u<sub>t</sub> = &kappa;u<sub>xx</sub>* with initial condition *u(x,0) = f(x)* and boundary conditions *u(0,t) = g<sub>0</sub>(t)* and *u(L,t) = g<sub>L</sub>(t)* for *t > 0* where *0 <= x <= L*.

**Input:** This function takes as input the coefficient *&kappa;*, the right bound *L*, the number of spatial points *i*, the point of interest *X*, the time of interest *T*, the number of time steps *n*, a vector representing the initial condition *f(x)*, and vectors representing the boundary conditions *g<sub>0</sub>(t)* and *g<sub>L</sub>(t)*.

**Output:** This function returns the approximated solution of the heat equation at point *X* and time *T*.

**Usage/Example:** This function may be called and the results displayed as follows:
~~~~
cout << "U(" << X << "," << T << ") = " << heatEquation_explicitEuler(K, L, i, X, T, n, f, g0, gL) << endl;
~~~~
For example, if *&kappa;* = 0.835; *L* = 10; *i* = 100; *X* = 6.5; *T* = 5; *n* = 5000; *f(x)* is 100 at *x* = 0, 50 at *x = L*, and 0 elsewhere; *g<sub>0</sub>(t)* = 100; and *g<sub>L</sub>(t)* = 50 the function will return
~~~~
U(6.5,5) = 15.4561
~~~~
**Implementation/Code:** The following is the code for heatEquation_explicitEuler():
~~~~
double heatEquation_explicitEuler(double K, double L, int i, double X, double T, int n, vector<double> f, vector<double> g0, vector<double> gL)
{
	double h = L / i; //mesh spacing
	double k = T / n; //time step
	double a = (K * k) / pow(h, 2);

	vector<double> U(i + 1); //vector of solutions for each time step

	for (int j = 0; j <= n; j++) //time step
	{
		for (int l = 0; l <= i; l++) //mesh spacing
		{
			if (j == 0) //initial condition
			{
				U[l] = f[l];
			}
			else
			{
				if (l == 0) //left boundary condition
				{
					U[l] = g0[j];
				}
				else if (l == i) //right boundary condition
				{
					U[l] = gL[j];
				}
				else //interior nodes
				{
					U[l] += a * (U[l - 1] - (2 * U[l]) + U[l + 1]);
				}
			}
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
**Last Modified:** 21 Apr 18
