# Implicit Euler

**Function Name:** implicitEuler

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of a differential equation of the form *y' = f(y,t)* with initial condition *y(t0) = y0* at time *tFinal*.

**Input:** This function takes as input the number of time steps *n*, the intial time *t0*, the initial condition *y0*, the final time *tFinal*, and a vector representing *f(y,t)*.

**Output:** This function returns the approximated solution of the equation at time *tFinal*.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "The solution is: y(" << tFinal << ") = " << implicitEuler(n, t0, y0, tFinal, f) << endl;
~~~~
For example, if *n* = 12, *t0* = 0, *y0* = 0, *tFinal* = 0.006, and *f(y,t) = -1000y + 3000 - 2000e<sup>-t</sup>* the function would return
~~~~
The solution is: y(0.006) = 0.992293
~~~~
**Implementation/Code:** The following is the code for implicitEuler():
~~~~
double implicitEuler(int n, double t0, double y0, double tFinal, vector<double> f)
{
	double k = (tFinal - t0) / n; //time step

	double yFinal = (y0 + (k * f[0])) / (1 + (1000 * k)); //final solution

	for (int i = 1; i < n; i++)
	{
		yFinal = (yFinal + (k * f[0])) / (1 + (1000 * k));
	}

	return yFinal;
}
~~~~
**Last Modified:** 28 Apr 18
