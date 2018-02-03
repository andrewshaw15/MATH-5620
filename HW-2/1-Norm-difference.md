# 1 Norm Difference

**Function Name:** calc1NormDiff

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function is used to compute the 1 norm of the difference of two vectors. This is especially useful when computing the 1 norm of the error vector.

**Input:** This function takes as input the two vectors whose 1 norm of their difference is to be computed, the step size between each of the individual vector elements *h*, and the size of the vectors *n*.

**Output:** This function returns the 1 norm of the difference of the two inputted vectors.

**Usage/Example:** This code may be executed and the 1 norm of the vector difference displayed as follows:
~~~~
cout << calc1NormDiff(approx, real, h, n) << endl;
~~~~
**Implementation/Code:** The following is the code for calc1NormDiff():
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
**Last Modified:** 3 Feb 18
