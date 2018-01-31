# 2 Norm Difference

**Function Name:** calc2NormDiff

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:**

**Input:**

**Output:**

**Usage/Example:**

**Implementation/Code:**
~~~~
double calc2NormDiff(vector<double> approx, vector<double> real, double h, int n)
{
	vector<double> E(n); //error vector
	double two_norm = 0.; //two norm

	for (int i = 0; i < n; i++)
	{
		E[i] = approx[i] - real[i];
		two_norm += pow(E[i], 2);
	}

	two_norm *= h;

	two_norm = sqrt(two_norm);

	return two_norm;
}
~~~~
**Last Modified:** 30 Jan 18
