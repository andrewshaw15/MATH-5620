# Max Norm Difference

**Function Name:** calcMaxNormDiff

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:**

**Input:**

**Output:**

**Usage/Example:**

**Implementation/Code:**
~~~~
double calcMaxNormDiff(vector<double> approx, vector<double> real, int n)
{
	vector<double> E(n); //error vector
	double max_norm = 0.; //max norm

	for (int i = 0; i < n; i++)
	{
		E[i] = approx[i] - real[i];
	}

	max_norm = *max_element(E.begin(), E.end());

	return max_norm;
}
~~~~
**Last Modified:** 30 Jan 18
