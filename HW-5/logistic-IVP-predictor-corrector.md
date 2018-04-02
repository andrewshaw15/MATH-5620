# Logistic IVP - Predictor-Corrector

**Function Name:** logisticIVP_PC

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function approximates the solution of the logistic equation *P' = &gamma;P - &beta;(P^2)* with *P(0) = P0* at a specific time *t*. Compare the solutions with [Logistic IVP - Exact](https://andrewshaw15.github.io/MATH-5620/HW-1/logistic-IVP-exact).

**Input:** This function takes as input the number of time steps *n*, the coefficients *&gamma;* and *&beta;*, the initial condition *P(0)*, and the time *t*.

**Output:** This function returns the approximated solution to the logistic equation at time *t*.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "P(" << t << ") = " << logisticIVP_PC(n, g, b, P0, t) << endl;
~~~~
For example, if *n* = 5, 50, 500, and 5000, *&gamma;* = 0.1, *&beta;* = 0.0001, *P(0)* = 25, and *t* = 5 the function would return
~~~~
P(5) = 40.4624
P(5) = 40.5185
P(5) = 40.5557
P(5) = 40.5598
~~~~
As another example, if *n* = 5, 50, 500, and 5000, *&gamma;* = 0.1, *&beta;* = 0.0001, *P(0)* = 40000, and *t* = 5 the function would return
~~~~
P(5) = -inf
P(5) = 2417.36
P(5) = 2442.84
P(5) = 2446.73
~~~~
**Implementation/Code:** The following is the code for logisticIVP_PC():
~~~~
double logisticIVP_PC(int n, double g, double b, double P0, double t)
{
	double k = t / n;

	double P1_p = P0 + (k * ((g * P0) - (b * pow(P0, 2)))); //first predictor step
	double P1 = P0 + ((k / 2) * (((g * P0) - (b * pow(P0, 2))) + ((g * P1_p) - (b * pow(P1_p, 2))))); //first corrector step
	double P2_p = P1 + ((k / 2) * (-((g * P0) - (b * pow(P0, 2))) + (3 * ((g * P1) - (b * pow(P1, 2)))))); //second predictor step
	double P2 = P1 + ((k / 12) * (-((g * P0) - (b * pow(P0, 2))) + (8 * ((g * P1) - (b * pow(P1, 2)))) + (5 * ((g * P2_p) - (b * pow(P2_p, 2)))))); //second corrector step
	double P3_p = P2 + ((k / 12) * ((5 * ((g * P0) - (b * pow(P0, 2)))) - (16 * ((g * P1) - (b * pow(P1, 2)))) + (23 * ((g * P2) - (b * pow(P2, 2)))))); //third predictor step
	double P3 = P2 + ((k / 24) * (((g * P0) - (b * pow(P0, 2))) - (5 * ((g * P1) - (b * pow(P1, 2)))) + (19 * ((g * P2) - (b * pow(P2, 2)))) + (9 * ((g * P3_p) - (b * pow(P3_p, 2)))))); //third corrector step
	double P4_p = P3 + ((k / 24) * (-(9 * ((g * P0) - (b * pow(P0, 2)))) + (37 * ((g * P1) - (b * pow(P1, 2)))) - (59 * ((g * P2) - (b * pow(P2, 2)))) + (55 * ((g * P3) - (b * pow(P3, 2)))))); //fourth predictor step
	double P4 = P3 + ((k / 720) * (-(19 * ((g * P0) - (b * pow(P0, 2)))) + (106 * ((g * P1) - (b * pow(P1, 2)))) - (264 * ((g * P2) - (b * pow(P2, 2)))) + (646 * ((g * P3) - (b * pow(P3, 2)))) + (251 * ((g * P4_p) - (b * pow(P4_p, 2)))))); //fourth corrector step

	for (int i = 4; i < n; i++)
	{
		P1_p = P1 + (k * ((g * P1) - (b * pow(P1, 2))));
		P1 = P1 + ((k / 2) * (((g * P1) - (b * pow(P1, 2))) + ((g * P1_p) - (b * pow(P1_p, 2)))));
		P2_p = P2 + ((k / 2) * (-((g * P1) - (b * pow(P1, 2))) + (3 * ((g * P2) - (b * pow(P2, 2))))));
		P2 = P2 + ((k / 12) * (-((g * P1) - (b * pow(P1, 2))) + (8 * ((g * P2) - (b * pow(P2, 2)))) + (5 * ((g * P2_p) - (b * pow(P2_p, 2))))));
		P3_p = P3 + ((k / 12) * ((5 * ((g * P1) - (b * pow(P1, 2)))) - (16 * ((g * P2) - (b * pow(P2, 2)))) + (23 * ((g * P3) - (b * pow(P3, 2))))));
		P3 = P3 + ((k / 24) * (((g * P1) - (b * pow(P1, 2))) - (5 * ((g * P2) - (b * pow(P2, 2)))) + (19 * ((g * P3) - (b * pow(P3, 2)))) + (9 * ((g * P3_p) - (b * pow(P3_p, 2))))));
		P4_p = P4 + ((k / 24) * (-(9 * ((g * P1) - (b * pow(P1, 2)))) + (37 * ((g * P2) - (b * pow(P2, 2)))) - (59 * ((g * P3) - (b * pow(P3, 2)))) + (55 * ((g * P4) - (b * pow(P4, 2))))));
		P4 = P4 + ((k / 720) * (-(19 * ((g * P1) - (b * pow(P1, 2)))) + (106 * ((g * P2) - (b * pow(P2, 2)))) - (264 * ((g * P3) - (b * pow(P3, 2)))) + (646 * ((g * P4) - (b * pow(P4, 2)))) + (251 * ((g * P4_p) - (b * pow(P4_p, 2))))));
	}

	if (n == 1)
	{
		return P1;
	}
	else if (n == 2)
	{
		return P2;
	}
	else if (n == 3)
	{
		return P3;
	}
	else
	{
		return P4;
	}
}
~~~~
**Last Modified:** 2 Apr 18
