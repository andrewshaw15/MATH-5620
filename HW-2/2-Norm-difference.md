# 2 Norm Difference

**Function Name:** calc2NormDiff

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function calculates the 2 norm of the difference of two vectors. This is especially useful in calculating the 2 norm of the error vector.

**Input:** This function requires as input the two vectors (here called *approx* and *real* for convenience in calculating the error vector), the step size between each vector element *h*, and the size *n* of the vectors.

**Output:** This function returns the 2 norm of the difference of the two vectors.

**Usage/Example:** This function may be called and its result displayed as follows:
~~~~
cout << "The 2-Norm of the error vector (approx - real) is: " << calc2NormDiff(approx, real, h, n) << endl;
~~~~
For example, if the contents of *approx* are <1.5, 2.3, 2.8>, the contents of *real* are <1, 2, 3>, *h* = 0.25, and *n* = 3, the function would output:
~~~~
The 2-Norm of the error vector (approx - real) is: 0.308221
~~~~
**Implementation/Code:** The following is the code for calc2NormDiff():
~~~~
double calc2NormDiff(vector<double> approx, vector<double> real, double h, int n)
{
	vector<double> E(n); //error vector
	double two_norm = 0.; //two norm

	for (int i = 0; i < n; i++)
	{
		E[i] = abs(approx[i] - real[i]);
		two_norm += pow(E[i], 2);
	}

	two_norm *= h;

	two_norm = sqrt(two_norm);

	return two_norm;
}
~~~~
**Last Modified:** 6 Feb 18
