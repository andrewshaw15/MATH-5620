# 2 Norm

**Function Name:** calc2Norm

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:**

**Input:**

**Output:**

**Usage/Example:**

**Implementation/Code:**
~~~~
double calc2Norm(vector<double> v, double h, int n)
{
	double two_norm = 0.;

	for (int i = 0; i < n; i++)
	{
		two_norm += pow(v[i], 2);
	}

	two_norm *= h;

	two_norm = sqrt(two_norm);

	return two_norm;
}
~~~~
**Last Modified:** 30 Jan 18
