# Max Norm

**Function Name:** calcMaxNorm

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:**

**Input:**

**Output:**

**Usage/Example:**

**Implementation/Code:**
~~~~
double calcMaxNorm(vector<double> v)
{
	double max_norm = *max_element(v.begin(), v.end());

	return max_norm;
}
~~~~
**Last Modified:** 30 Jan 18
