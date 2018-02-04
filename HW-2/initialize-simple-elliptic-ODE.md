# Initialize Simple Elliptic ODE

**Function Name:** initF

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function computes the vector *F* in the equation *AU = F*, which was derived from the simple elliptic equation *u"(x) = f(x)* in the region *a < x < b* with the boundary conditions *u(a) = u_a* and *u(b) = u_b*. The matrix *A* does not need to be computed, as the diagonal elements will always equal -2 and the off-diagonal elements will always equal 1 (assuming a centered difference approximation of *u"(x)* is used).

**Input:** This function requires as input the left and right bounds for *x* (*a* and *b*, respectively), the values of *u(x)* at the boundaries (*u(a)* and *u(b)*), the vector of values for *f(x)*, and the size *n* of *f*.

**Output:** This function returns a vector representing the vector *F*.

**Usage/Example:** This function may be called and its results displayed by the following:
~~~~
vector<double> F = initF(a, b, u_a, u_b, n, f);

cout << "The matrix F is:" << endl;
for (int i = 0; i < n; i++)
{
	cout << "F[" << i << "] = " << F[i] << endl;
}
~~~~
For example, if *a* = 0, *b* = 1, *u(a)* = 0, *u(b)* = 1, *n* = 3, and the contents of *f* are <25, 50, 75> the function will return:
~~~~
The matrix F is:
F[0] = 1.5625
F[1] = 3.125
F[2] = 3.6875
~~~~
**Implementation/Code:**
~~~~
vector<double> initF(double a, double b, double u_a, double u_b, int n, vector<double> f)
{
	double h = (b - a) / (n + 1); //mesh width

	vector<double> F(n);

	F[0] = (f[0] * pow(h, 2)) - u_a;

	for (int i = 1; i < n - 1; i++)
	{
		F[i] = f[i] * pow(h, 2);
	}

	F[n - 1] = (f[n - 1] * pow(h, 2)) - u_b;

	return F;
}
~~~~
**Last Modified:** 3 Feb 18
