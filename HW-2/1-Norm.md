# 1 Norm

**Function Name:** calc1Norm

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function calculates the 1 norm of a vector.

**Input:** The values that must be inputted into this function are the vector *v*, the step size between each vector element *h*, and the size *n* of the vector.

**Output:** This function returns the 1 norm of the vector.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "The 1-Norm of the vector is: " << calc1Norm(v, h, n) << endl;
~~~~
For example, if the contents of *v* are <1, 2, 3>, *h* = 0.25, and *n* = 3, the function would display:
~~~~
The 1-Norm of the vector is: 1.5
~~~~
**Implementation/Code:** The following is the code for calc1Norm():
~~~~
double calc1Norm(vector<double> v, double h, int n)
{
	double one_norm = 0.;

	for (int i = 0; i < n; i++)
	{
		one_norm += abs(v[i]);
	}

	one_norm *= h;

	return one_norm;
}
~~~~
**Last Modified:** 6 Feb 18
