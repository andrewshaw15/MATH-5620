# Thomas Algorithm

**Function Name:** thomasAlgorithm

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function uses the Thomas Algorithm to solve the equation *AU = F* derived from either the simple elliptic ODE (refer to [Initialize Simple Elliptic ODE](https://andrewshaw15.github.io/MATH-5620/HW-2/initialize-simple-elliptic-ODE) for *F* initialization) or from the full elliptic ODE (refer to [Initialize Full Elliptic ODE](https://andrewshaw15.github.io/MATH-5620/HW-2/initialize-full-elliptic-ODE) for *F* and *A* initializations).

**Input:** This function takes as input the matrix *A*, the vector *F*, and their size *n*.

**Output:** This function outputs a vector representing the solution.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
vector<double> U = thomasAlgorithm(n, F, A);

cout << "The solution is:" << endl;
for (int i = 0; i < n; i++)
{
	cout << "U[" << i + 1 << "] = " << U[i] << endl;
}
~~~~
For example, if *n* = 3, the contents of *F* are <1.5625, 3.125, 3.6875>, and the elements of *A* are -2 on the diagonal, 1 on the off-diagonals, and 0 elsewhere, the function would output:
~~~~
The solution is:
U[1] = -3.65625
U[2] = -5.75
U[3] = -4.71875
~~~~
**Implementation/Code:**
~~~~
vector<double> thomasAlgorithm(int n, vector<double> F, vector<vector<double>> A)
{
	vector<double> lA(n); //lower diagonal elements of A
	vector<double> dA(n); //diagonal elements of A
	vector<double> uA(n); //upper diagonal elements of A
	
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			if (i == j) //diagonal term
			{
				dA[i] = A[i][j];
			}
			else if (i - j == 1) //lower diagonal term
			{
				lA[i] = A[i][j];
			}
			else if (j - i == 1) //upper diagonal term
			{
				uA[i] = A[i][j];
			}
		}
	}

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
**Last Modified:** 6 Feb 18
