# Runge-Kutta 4

**Function Name:** RK4

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of a differential equation of the form *y' = f(y,t)* with initial condition *y(t0) = y0* at time *tFinal*.

**Input:** This function takes as input the number of time steps *n*, the initial time *t0*, the initial condition *y0*, the final time *tFinal*, and a vector representing *f(y,t)*.

**Output:** This function returns the approximated solution of the equation at time *tFinal*.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "The solution is: y(" << tFinal << ") = " << RK4(n, t0, y0, tFinal, f) << endl;
~~~~
For example, if *n* = 12, *t0* = 0, *y0* = 0, *tFinal* = 0.006, and *f(y,t) = -1000y + 3000 - 2000e<sup>-t</sup>* the function would return
~~~~
The solution is: y(0.006) = 1.00749
~~~~
**Implementation/Code:** The following is the code for RK4():
~~~~
double RK4(int n, double t0, double y0, double tFinal, vector<double> f)
{
	double k = (tFinal - t0) / n;

	double y1 = y0;
	double y2 = y0 + ((k / 2) * ((-1000 * y1) + f[0]));
	double y3 = y0 + ((k / 2) * ((-1000 * y2) + f[1]));
	double y4 = y0 + (k * ((-1000 * y3) + f[1]));
	double yFinal = y0 + ((k / 6) * (((-1000 * y1) + f[0]) + (2 * ((-1000 * y2) + f[1])) + (2 * ((-1000 * y3) + f[1])) + ((-1000 * y4) + f[2])));

	for (int i = 2; i < 2 * n; i += 2)
	{
		y1 = yFinal;
		y2 = yFinal + ((k / 2) * ((-1000 * y1) + f[i]));
		y3 = yFinal + ((k / 2) * ((-1000 * y2) + f[i + 1]));
		y4 = yFinal + (k * ((-1000 * y3) + f[i + 1]));
		yFinal = yFinal + ((k / 6) * (((-1000 * y1) + f[i]) + (2 * ((-1000 * y2) + f[i + 1])) + (2 * ((-1000 * y3) + f[i + 1])) + ((-1000 * y4) + f[i + 2])));
	}

	return yFinal;
}
~~~~
**Last Modified:** 28 Apr 18
