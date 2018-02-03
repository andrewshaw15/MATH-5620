# 2 Norm Difference

**Function Name:** calc2NormDiff

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function calculates the 2 norm of the difference of two vectors. This is especially useful in calculating the 2 norm of the error vector.

**Input:** This function requires as input the two vectors, the step size between each vector element *h*, and the size of the vectors *n*.

**Output:** This function returns the 2 norm of the difference of the two vectors.

**Usage/Example:** This function may be called and its result displayed as follows:
~~~~
cout << calc2NormDiff(approx, real, h, n) << endl;
~~~~
**Implementation/Code:** The following is the code for calc2NormDiff():
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
**Last Modified:** 3 Feb 18
