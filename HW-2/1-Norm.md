# 1 Norm

**Function Name:** calc1Norm

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function calculates the 1 norm of a vector.

**Input:** The values that must be inputted into this function are the vector *v*, the step size between each vector element *h*, and the size of the vector *n*.

**Output:** This function returns the 1 norm of the vector.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << calc1Norm(v, h, n) << endl;
~~~~
**Implementation/Code:** The following is the code for calc1Norm():
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
**Last Modified:** 3 Feb 18
