# Jacobi Iteration

**Function Name:** jacobiIteration

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:**

**Input:**

**Output:**

**Usage/Example:**

**Implementation/Code:**
~~~~
vector<double> jacobiIteration(int n, vector<double> F)
{
	vector<double> U(n, 1); //solution with initial guess of 1
	vector<vector<double>> A(n, vector<double>(n, 0)); //A matrix

	//initialize A matrix
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			if (i == j) //diagonals
			{
				A[i][j] = -2.;
			}
			else if (abs(i - j) == 1) //elements one away from diagonals
			{
				A[i][j] = 1.;
			}
		}
	}

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
**Last Modified:** 30 Jan 18
