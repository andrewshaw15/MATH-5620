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
For example, if *n* = 8, *t0* = 0, *y0* = 1, *tFinal* = 4, and *f(t,y) = -2(y^3) + 12(y^2) - 20y +8.5*, the function would return:
~~~~
The solution is: y(4) = 7
~~~~
**Implementation/Code:** The following is the code for explicitEuler():
~~~~
double explicitEuler(int n, double t0, double y0, double tFinal, vector<double> f)
{
	double k = (tFinal - t0) / n; //time step

	double yFinal = y0 + (k * f[0]); //final solution

	for (int i = 1; i < n; i++)
	{
		yFinal += (k * f[i]);
	}

	return yFinal;
}
~~~~
**Last Modified:** 20 Mar 18
