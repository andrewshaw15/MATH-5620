# Runge-Kutta 2

**Function Name:** RK2

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of a differential equation of the form *y' = f(y,t)* with intial condition *y(t0) = y0* at time *tFinal*.

**Input:** This function takes as input the number of time steps *n*, the initial time *t0*, the initial condition *y0*, the final time *tFinal*, and a vector representing *f(y,t)*

**Output:** This function returns the approximated solution of the equation at time *tFinal*.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "The solution is: y(" << tFinal << ") = " << RK2(n, t0, y0, tFinal, f) << endl;
~~~~
For example, if *n* = 12, *t0* = 0, *y0* = 0, *tFinal* = 0.006, and *f(y,t) = -1000y + 3000 - 2000e<sup>-t</sup>* the funtion would return
~~~~
The solution is: y(0.006) = 1.00643
~~~~
**Implementation/Code:** The following is the code for RK2():
~~~~
double RK2(int n, double t0, double y0, double tFinal, vector<double> f)
{
	double k = (tFinal - t0) / n;

	double y_star = y0 + ((k / 2) * ((-1000 * y0) + f[0]));
	double yFinal = y0 + (k * ((-1000 * y_star) + f[1]));

	for (int i = 2; i < 2 * n; i += 2)
	{
		y_star = yFinal + ((k / 2) * ((-1000 * yFinal) + f[i]));
		yFinal = yFinal + (k * ((-1000 * y_star) + f[i + 1]));
	}

	return yFinal;
}
~~~~
**Last Modified:** 28 Apr 18
