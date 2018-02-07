# Max Norm

**Function Name:** calcMaxNorm

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function calculates the max norm of a vector.

**Input:** This function takes as input a vector *v* and its size *n*.

**Output:** This function outputs the max norm of the vector.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "The max norm of the vector is: " << calcMaxNorm(v, n) << endl;
~~~~
For example, if the contents of *v* are <1, 2, 3> and *n* = 3, the function will output:
~~~~
The max norm of the vector is: 3
~~~~
**Implementation/Code:**
~~~~
double calcMaxNorm(vector<double> v, int n)
{
	for (int i = 0; i < n; i++)
	{
		v[i] = abs(v[i]);
	}
			      
	double max_norm = *max_element(v.begin(), v.end());

	return max_norm;
}
~~~~
**Last Modified:** 6 Feb 18
