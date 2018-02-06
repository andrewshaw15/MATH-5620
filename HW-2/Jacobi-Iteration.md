# Jacobi Iteration

**Function Name:** jacobiIteration

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function uses Jacobi Iteration to solve *AU = F* from either the simple elliptic ODE (refer to [Initialize Simple Elliptic ODE](https://andrewshaw15.github.io/MATH-5620/HW-2/initialize-simple-elliptic-ODE) for *F* initialization) or from the full elliptic ODE (refer to [Initialize Full Elliptic ODE](https://andrewshaw15.github.io/MATH-5620/HW-2/initialize-full-elliptic-ODE) for *F* and *A* documentation).

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
vector<double> jacobiIteration(vector<double> F, int n, vector<vector<double>> A)
{
	vector<double> U(n, 1); //solution with initial guess of 1

	vector<double> U_old(n, 1.); //vector to store old values
	vector<double> relErr(n, 1.); //vector of relative errors

	for (int i = 0; i < n; i++)
	{
		U[i] = F[i];

		for (int j = 0; j < n; j++)
		{
			if (i != j)
			{
				U[i] -= A[i][j] * U[j];
			}
		}

		U[i] /= A[i][i];

		relErr[i] = ((U[i] - U_old[i]) / U[i]) * 100.;

		U_old[i] = U[i]; //update old values
	}

	int numIterations = 1;

	//iterate until max relative error is less than 1% or # iterations exceeds 1000
	while (*max_element(relErr.begin(), relErr.end()) >= 1. && numIterations < 1000)
	{
		for (int i = 0; i < n; i++)
		{
			U[i] = F[i];

			for (int j = 0; j < n; j++)
			{
				if (i != j)
				{
					U[i] -= A[i][j] * U[j];
				}
			}

			U[i] /= A[i][i];

			relErr[i] = ((U[i] - U_old[i]) / U[i]) * 100.;

			U_old[i] = U[i]; //update old values
		}

		numIterations++;
	}

	return U;
}
~~~~
**Last Modified:** 6 Feb 18
