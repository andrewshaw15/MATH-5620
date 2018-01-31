# LU Factorization

**Function Name:** LUFactorization

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:**

**Input:**

**Output:**

**Usage/Example:**

**Implementation/Code:**
~~~~
vector<double> LUFactorization(int n, vector<double> F)
{
	vector<double> U(n); //solution
	vector<vector<double>> A(n, vector<double>(n)); //A matrix
	
	for (int i = 0; i < n; i++) //initialize A matrix
	{
		for (int j = 0; j < n; j++)
		{
			if (i == j) //diagonal terms
			{
				A[i][j] = -2.;
			}
			else if (abs(i - j) == 1) //terms next to diagonals
			{
				A[i][j] = 1.;
			}
		}
	}

	//decompose A matrix
	for (int i = 0; i < n - 1; i++)
	{
		for (int j = i + 1; j < n; j++)
		{
			double c = A[j][i] / A[i][i]; //factor
			A[j][i] = c;

			for (int k = i + 1; k < n; k++)
			{
				A[j][k] -= c * A[i][k];
			}
		}
	}

	//substitution phase
	double s; //sum

	for (int i = 1; i < n; i++)
	{
		//forward substitution
		s = F[i];

		for (int j = 0; j < i; j++)
		{
			s -= A[i][j] * F[j];
		}

		F[i] = s;

		//back substitution
		U[n - 1] = F[n - 1] / A[n - 1][n - 1];

		for (int i = n - 2; i >= 0; i--)
		{
			s = 0;

			for (int j = i + 1; j < n; j++)
			{
				s += A[i][j] * U[j];
			}

			U[i] = (F[i] - s) / A[i][i];
		}
	}

	return U;
}
~~~~
**Last Modified:** 30 Jan 18
