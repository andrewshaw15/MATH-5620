# Vibration Test

**Function Name:** calcY

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function determines the analytical solution of the equation *my" + cy' + ky = f(t)* when *f(t)* = 0. This function will be used as a standard when methods of estimating integrals numerically are explored.

**Input:** This function requires six input values: *m*, *c*, *k*, *y(0)*, *v(0)*, and *t*. The value *m* may represent the mass of the spring-mass-damper system, *c* the damping coefficient, *k* the spring constant, *y(0)* the initial position, *v(0)* the initial velocity, and *t* the time at which the position *y* is desired to be known.

**Output:** This function returns the position *y* of the spring-mass-damper system at time *t*.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "y(" << t << ") = " << calcY(m, c, k, y0, v0, t) << endl;
~~~~
For instance, if *m* = 10, *c* = 200, *k* = 1000, *y(0)* = 2, *v(0)* = 5, and *t* = 7, the result would be
~~~~
y(7) = 7.03655e-29
~~~~
**Implementation/Code:** The following is the code for the function calcY()
~~~~
double calcY(double m, double c, double k, double y0, double v0, double t)
{
	double wn = sqrt(k / m); //natural frequency
	double cc = 2 * m * wn; //critical damping constant
	double z = c / cc; //damping ratio

	if (z < 1) //underdamped case
	{
		double wd = wn * sqrt(1 - pow(z, 2)); //damped frequency
		double C1 = y0; //constant found with initial conditions
		double C2 = (v0 + (z * wn * y0)) / wd; //constant found with initial conditions

		return (exp(-z * wn * t) * ((C1 * cos(wd * t)) + (C2 * sin(wd * t))));
	}
	else if (z == 1) //critically damped case
	{
		double C1 = y0; //constant found with initial conditions
		double C2 = v0 + (wn * y0); //contant found with initial conditions

		return (exp(-wn * t) * (C1 + (C2 * t)));
	}
	else //overdamped case
	{
		double C1 = ((y0 * wn * (z + sqrt(pow(z, 2) - 1))) + v0) / (2 * wn * sqrt(pow(z, 2) - 1)); //constant found with initial conditions
		double C2 = ((-y0 * wn * (z - sqrt(pow(z, 2) - 1))) - v0) / (2 * wn * sqrt(pow(z, 2) - 1)); //constant found with initial conditions

		return ((C1 * exp((-z + sqrt(pow(z, 2) - 1)) * wn * t)) + (C2 * exp((-z - sqrt(pow(z, 2) - 1)) * wn * t)));
	}
}
~~~~
**Last Modified:** 22 Jan 18
