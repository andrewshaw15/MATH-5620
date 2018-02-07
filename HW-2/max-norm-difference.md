# Max Norm Difference

**Function Name:** calcMaxNormDiff

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function calculates the max norm of the difference of two vectors. This is especially useful in calculating the max norm of the error vector.

**Input:** This function takes as input the two vectors (here denoted as *approx* and *real* for convenience in calculating the error vector) and their size *n*.

**Output:** This function outputs the max norm of the difference of the two vectors.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "The max norm of the error vector (approx - real) is: " << calcMaxNormDiff(approx, real, n) << endl;
~~~~
For example, if the contents of *approx* are <1.5, 2.3, 2.8>, the contents of *real* are <1, 2, 3>, and *n* = 3, the function will produce:
~~~~
The max norm of the error vector (approx - real) is: 0.5
~~~~
**Implementation/Code:**
~~~~
double calcMaxNormDiff(vector<double> approx, vector<double> real, int n)
{
	vector<double> E(n); //error vector
	double max_norm = 0.; //max norm

	for (int i = 0; i < n; i++)
	{
		E[i] = abs(approx[i] - real[i]);
	}

	max_norm = *max_element(E.begin(), E.end());

	return max_norm;
}
~~~~
**Last Modified:** 6 Feb 18
