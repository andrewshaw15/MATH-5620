# LU Factorization

**Function Name:** LUFactorization

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function uses LU Factorization to solve *AU = F* derived from the either the simple elliptic ODE (refer to [Initialize Simple Elliptic ODE](https://andrewshaw15.github.io/MATH-5620/HW-2/initialize-simple-elliptic-ODE) for *F* initialization) or from the full elliptic ODE (refer to [Initialize Full Elliptic ODE](https://andrewshaw15.github.io/MATH-5620/HW-2/initialize-full-elliptic-ODE) for *F* and *A* initialization).

**Input:** This function requires for input the matrix *A*, the vector *F*, and their size *n*.

**Output:** This function outputs a vector representing the solution.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
vector<double> U = LUFactorization(n, F, A);

cout << "The solution is:" << endl;
for (int i = 0; i < n; i++)
{
	cout << "U[" << i + 1 << "] = " << U[i] << endl;
}
~~~~
For example, if *n* = 3, the contents of *F* are <1.5625, 3.125, 3.6875>, and the elements of *A* are -2 on the diagonal, 1 on the off-diagonals, and 0 elsewhere the function will display:
~~~~
The solution is:
U[1] = -3.65625
U[2] = -5.75
U[3] = -4.71875
~~~~
**Implementation/Code:**
~~~~
vector<double> LUFactorization(int n, vector<double> F, vector<vector<double>> A)
{
	vector<double> U(n); //solution

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
**Last Modified:** 6 Feb 18
