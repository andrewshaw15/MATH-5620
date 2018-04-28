# Beam-Warming

**Function Name:** beamWarming

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of the advection equation *u<sub>t</sub> + au<sub>x</sub> = 0* with initial condition *u(x,0) = f(x)* and periodic boundary condition *u(0,t) = u(L,t) = g(t)* on the boundary *0 &le; x &le; L* at position *X* and time *T*.

**Input:** This function takes as input the coefficient *a*, the length *L*, the number of interior nodes (plus the end point) *i*, the position *X*, the final time *T*, the number of time steps *n*, a vector representing the initial condition *f(x)*, and a vector representing the boundary condition *g(t)*.

**Output:** This function returns the approximated solution of the advection equation at position *X* and time *T*.

**Usage/Example:** This function may be called and its results displayed as follows (*X* is passed in as *X - 1* for vector indexing compatability):
~~~~
cout << "U(" << X << "," << T << ") = " << beamWarming(a, L, i, X - 1, T, n, f, g) << endl;
~~~~
For example, if *a* = 2, *L* = 10, *i* = 100, *X* = 6.5, *T* = 5, *n* = 5000, *f(x)* is *0.5Lx - x<sup>2</sup>* for *0 &le; x &le; 0.5L* and 0 elsewhere, and *g(t)* is *f(x)* as it translates to the right the function would return
~~~~
U(6.5,5) = 6.25512e-15
~~~~
**Implementation/Code:** The following is the code for beamWarming():
~~~~
double beamWarming(double a, double L, int i, double X, double T, int n, vector<double> f, vector<double> g)
{
	double h = L / i; //mesh spacing
	double k = T / n; //time step

	vector<double> U(i - 1);
  
	U[0] = f[1] - (((a * k) / (2 * h)) * ((3 * f[1]) - (4 * f[0]) + f[i - 1])) + ((pow(a * k, 2) / (2 * pow(h, 2))) * (f[1] - (2 * f[0]) + f[i - 1]));
	for (int j = 1; j < i - 1; j++)
	{
		U[j] = f[j + 1] - (((a * k) / (2 * h)) * ((3 * f[j + 1]) - (4 * f[j]) + f[j - 1])) + ((pow(a * k, 2) / (2 * pow(h, 2))) * (f[j + 1] - (2 * f[j]) + f[j - 1]));
	}

	for (int t = 1; t < n; t++)
	{
		U[0] = U[0] - (((a * k) / (2 * h)) * ((3 * U[0]) - (4 * g[t]) + U[i - 2])) + ((pow(a * k, 2) / (2 * pow(h, 2))) * (U[0] - (2 * g[t]) + U[i - 2]));
		U[1] = U[1] - (((a * k) / (2 * h)) * ((3 * U[1]) - (4 * U[0]) + g[t])) + ((pow(a * k, 2) / (2 * pow(h, 2))) * (U[1] - (2 * U[0]) + g[t]));
		for (int j = 2; j < i - 2; j++)
		{
			U[j] = U[j] - (((a * k) / (2 * h)) * ((3 * U[j]) - (4 * U[j - 1]) + U[j - 2])) + ((pow(a * k, 2) / (2 * pow(h, 2))) * (U[j] - (2 * U[j - 1]) + U[j - 2]));
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
**Last Modified:** 28 Apr 18
