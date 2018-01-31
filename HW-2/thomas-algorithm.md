# Thomas Algorithm

**Function Name:** thomasAlgorithm

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:**

**Input:**

**Output:**

**Usage/Example:**

**Implementation/Code:**
~~~~
vector<double> thomasAlgorithm(int n, vector<double> F)
{
	vector<double> lA(n, -1.); //lower diagonal elements of A
	vector<double> dA(n, 2.); //diagonal elements of A
	vector<double> uA(n, -1.); //upper diagonal elements of A

	lA[0] = 0;
	uA[n - 1] = 0;

	vector<double> U(n); //solution

	for (int i = 1; i < n; i++) 
	{
		//decomposition
		lA[i] /= dA[i - 1];
		dA[i] -= lA[i] * uA[i - 1];

		//forward substitution
		F[i] -= lA[i] * F[i - 1];
	}

	//back substitution
	U[n - 1] = F[n - 1] / dA[n - 1];

	for (int i = n - 2; i >= 0; i--)
	{
		U[i] = (F[i] - (uA[i] * U[i + 1])) / dA[i];
	}
	
	return U;
}
~~~~
**Last Modified:** 30 Jan 18
