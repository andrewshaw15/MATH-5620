# Predictor-Corrector

**Function Name:** PC

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of a differential equation of the form *y' = f(y,t)* with initial condition *y(t0) = y0* at time *tFinal*.

**Input:** This function takes as input the number of time steps *n*, the intial time *t0*, the initial condition *y0*, the final time *tFinal*, and a vector representing *f(y,t)*.

**Output:** This function returns the approximated solution to the equation at time *tFinal*.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "The solution is: y(" << tFinal << ") = " << PC(n, t0, y0, tFinal, f) << endl;
~~~~
For example, if *n* = 12, *t0* = 0, *y0* = 0, *tFinal* = 0.006, and *f(y,t) = -1000y + 3000 - 2000e<sup>-t</sup>* the function will return
~~~~
The solution is: y(0.006) = 1.00586
~~~~
**Implementation/Code:** The following is the code for PC():
~~~~
double PC(int n, double t0, double y0, double tFinal, vector<double> f)
{
	double k = (tFinal - t0) / n;

	double y1_p = y0 + (k * ((-1000 * y0) + f[0]));
	double y1 = y0 + ((k / 2) * (((-1000 * y0) + f[0]) + ((-1000 * y1_p) + f[1])));
	double y2_p = y1 + ((k / 2) * (-((-1000 * y0) + f[0]) + (3 * ((-1000 * y1) + f[1]))));
	double y2 = y1 + ((k / 12) * (-((-1000 * y0) + f[0]) + (8 * ((-1000 * y1) + f[1])) + (5 * ((-1000 * y2_p) + f[2]))));
	double y3_p = y2 + ((k / 12) * ((5 * ((-1000 * y0) + f[0])) - (16 * ((-1000 * y1) + f[1])) + (23 * ((-1000 * y2) + f[2]))));
	double y3 = y2 + ((k / 24) * (((-1000 * y0) + f[0]) - (5 * ((-1000 * y1) + f[1])) + (19 * ((-1000 * y2) + f[2])) + (9 * ((-1000 * y3_p) + f[3]))));
	double y4_p = y3 + ((k / 24) * (-(9 * ((-1000 * y0) + f[0])) + (37 * ((-1000 * y1) + f[1])) - (59 * ((-1000 * y2) + f[2])) + (55 * ((-1000 * y3) + f[3]))));
	double y4 = y3 + ((k / 720) * (-(19 * ((-1000 * y0) + f[0])) + (106 * ((-1000 * y1) + f[1])) - (264 * ((-1000 * y2) + f[2])) + (646 * ((-1000 * y3) + f[3])) + (251 * ((-1000 * y4_p) + f[4]))));

	for (int i = 5; i < n; i++)
	{
		y1_p = y1 + (k * ((-1000 * y1) + f[i - 4]));
		y1 = y1 + ((k / 2) * (((-1000 * y1) + f[i - 4]) + ((-1000 * y1_p) + f[i - 3])));
		y2_p = y2 + ((k / 2) * (-((-1000 * y1) + f[i - 4]) + (3 * ((-1000 * y2) + f[i - 3]))));
		y2 = y2 + ((k / 12) * (-((-1000 * y1) + f[i - 4]) + (8 * ((-1000 * y2) + f[i - 3])) + (5 * ((-1000 * y2_p) + f[i - 2]))));
		y3_p = y3 + ((k / 12) * ((5 * ((-1000 * y1) + f[i - 4])) - (16 * ((-1000 * y2) + f[i - 3])) + (23 * ((-1000 * y3) + f[i - 2]))));
		y3 = y3 + ((k / 24) * (((-1000 * y1) + f[i - 4]) - (5 * ((-1000 * y2) + f[i - 3])) + (19 * ((-1000 * y3) + f[i - 2])) + (9 * ((-1000 * y3_p) + f[i - 1]))));
		y4_p = y4 + ((k / 24) * (-(9 * ((-1000 * y1) + f[i - 4])) + (37 * ((-1000 * y2) + f[i - 3])) - (59 * ((-1000 * y3) + f[i - 2])) + (55 * ((-1000 * y4) + f[i - 1]))));
		y4 = y4 + ((k / 720) * (-(19 * ((-1000 * y1) + f[i - 4])) + (106 * ((-1000 * y2) + f[i - 3])) - (264 * ((-1000 * y3) + f[i - 2])) + (646 * ((-1000 * y4) + f[i - 1])) + (251 * ((-1000 * y4_p) + f[i]))));
	}

	if (n == 1)
	{
		return y1;
	}
	else if (n == 2)
	{
		return y2;
	}
	else if (n == 3)
	{
		return y3;
	}
	else
	{
		return y4;
	}
}
~~~~
**Last Modified:** 28 Apr 18
