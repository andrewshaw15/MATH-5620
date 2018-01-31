# 1 Norm Difference

**Function Name:** calc1NormDiff

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:**

**Input:**

**Output:**

**Usage/Example:**

**Implementation/Code:**
~~~~
double calc1NormDiff(vector<double> approx, vector<double> real, double h, int n)
{
	vector<double> E(n); //error vector
	double one_norm = 0.; //one norm

	for (int i = 0; i < n; i++)
	{
		E[i] = approx[i] - real[i];
		one_norm += E[i];
	}

	one_norm *= h;

	return one_norm;
}
~~~~
**Last Modified:** 30 Jan 18
