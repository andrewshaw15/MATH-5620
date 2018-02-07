# Jacobi Iteration

**Function Name:** jacobiIteration

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function uses Jacobi Iteration to solve *AU = F* from either the simple elliptic ODE (refer to [Initialize Simple Elliptic ODE](https://andrewshaw15.github.io/MATH-5620/HW-2/initialize-simple-elliptic-ODE) for *F* initialization) or from the full elliptic ODE (refer to [Initialize Full Elliptic ODE](https://andrewshaw15.github.io/MATH-5620/HW-2/initialize-full-elliptic-ODE) for *F* and *A* initialization).

**Input:** This function takes as input the matrix *A*, the vector *F*, and their size *n*.

**Output:** This function returns a vector representing the solution.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
vector<double> U = jacobiIteration(n, F, A);

cout << "The solution is:" << endl;
for (int i = 0; i < n; i++)
{
	cout << "U[" << i + 1 << "] = " << U[i] << endl;
}
~~~~
For example, if *n* = 3, the contents of *F* are <1.5625, 3.125, 3.6875>, and the elements of *A* are -2 on the diagonals, 1 on the off-diagonals, and 0 elsewhere, the function outputs:
~~~~
The solution is:
U[1] = -3.62073
U[2] = -5.71448
U[3] = -4.70099
~~~~
**Implementation/Code:**
~~~~
vector<double> jacobiIteration(int n, vector<double> F, vector<vector<double>> A)
{
	vector<double> temp(n); //temporary vector to help with math

	vector<double> U(n, 1); //solution with initial guess of 1

	int numIterations = 1;

	line:

	for (int i = 0; i < n; i++)
	{
		temp[i] = F[i];

		for (int j = 0; j < n; j++)
		{
			if (i != j)
			{
				temp[i] -= A[i][j] * U[j];
			}
		}
	}

	for (int i = 0; i < n; i++)
	{
		U[i] = temp[i] / A[i][i];
	}

	numIterations++;

	if (numIterations < 100)
	{
		goto line;
	}

	return U;
}
~~~~
**Last Modified:** 6 Feb 18
