# Explicit Euler

**Function Name:** explicitEuler

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function uses the explicit Euler method to solve the equation *y' = f(t,y)* with *y(t0) = y0*. As a note, this function may be easily adapted to solve a system of *m* equations.

**Input:** This function takes as input the number of time steps *n*, the initial time *t0*, the initial value *y0*, the final time *tFinal*, and a vector representing the values of *f(t,y)*.

**Output:** This function returns the final value *yFinal* evaluated at *tFinal*.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "The solution is: y(" << tFinal << ") = " << explicitEuler(n, t0, y0, tFinal, f) << endl;
~~~~
For example, if *n* = 12, *t0* = 0, *y0* = 0, *tFinal* = 0.006, and *f(t,y) = -1000y + 3000 - 2000e<sup>-t</sup>*, the function would return:
~~~~
The solution is: y(0.006) = 1.00973
~~~~
**Implementation/Code:** The following is the code for explicitEuler():
~~~~
double explicitEuler(int n, double t0, double y0, double tFinal, vector<double> f)
{
	double k = (tFinal - t0) / n; //time step

	double yFinal = y0 + (k * ((-1000 * y0) + f[0])); //final solution

	for (int i = 1; i < n; i++)
	{
		yFinal += (k * ((-1000 * yFinal) + f[i]));
	}

	return yFinal;
}
~~~~
**Last Modified:** 28 Apr 18
