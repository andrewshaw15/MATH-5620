# 1 Norm

**Function Name:** calc1Norm

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:**

**Input:**

**Output:**

**Usage/Example:**

**Implementation/Code:**
~~~~
double calc1Norm(vector<double> v, double h, int n)
{
	double one_norm = 0.;

	for (int i = 0; i < n; i++)
	{
		one_norm += v[i];
	}

	one_norm *= h;

	return one_norm;
}
~~~~
**Last Modified:** 30 Jan 18
