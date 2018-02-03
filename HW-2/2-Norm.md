# 2 Norm

**Function Name:** calc2Norm

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function calculates the 2 norm of a vector.

**Input:** This function takes as input the vector *v*, the step size between each of the vector's elements *h*, and the size of the vector *n*.

**Output:** This function returns the 2 norm of the vector.

**Usage/Example:** This function may be called and its result displayed as follows:
~~~~
cout << calc2Norm(v, h, n) << endl;
~~~~
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
**Last Modified:** 3 Feb 18
