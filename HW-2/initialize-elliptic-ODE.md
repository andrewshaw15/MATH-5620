# Initialize Elliptic ODE

**Function Name:** initF

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:**

**Input:**

**Output:**

**Usage/Example:**

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
**Last Modified:** 30 Jan 18
