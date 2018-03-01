# Five Point Laplacian - Conjugate Gradient

**Function Name:** fivePointLaplacian

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function computes the solution of the 2D Laplace equation *&Delta;u = sin(xy)* on the unit square with homogeneous Dirichlet boundary conditions using a five point stencil and the conjugate gradient method. This function uses two helper functions: initF() to initialize the right hand matrix (see [Initialize Five Point Matrix](https://andrewshaw15.github.io/MATH-5620/HW-3/initialize-five-point-laplacian)), and conjugateGradient() to implement the conjugate gradient method (see [Conjugate Gradient](https://andrewshaw15.github.io/MATH-5620/HW-4/conjugate-gradient)).

**Input:** This function takes as input vectors representing the boundary conditions (*u_top*, *u_bottom*, *u_left*, *u_right*) and their size *n*. Note that the vectors do not include the corner nodes.

**Output:** This function displays the solution of the Laplace equation.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
fivePointLaplacian(n, u_top, u_bottom, u_left, u_right);
~~~~
For example, if *n* = 5, *u_top* contains <1, 2, 3, 4, 5>, *u_bottom* contains <7, 8, 9, 10, 11>, *u_left* contains <1, 2, 3, 4, 5>, and *u_right* contains <7, 8, 9, 10, 11>, the function would display:
~~~~
The solution is:
1.98812 2.97855 3.97317 4.97341 5.98096
2.97855 3.962 4.95404 5.95667 6.97101
3.97317 4.95404 5.9477 6.95522 7.97404
4.97341 5.95667 6.95522 7.96772 8.98657
5.98096 6.97101 7.97404 8.98657 9.99922
~~~~
**Implementation/Code:** The following is the code for fivePointLaplacian():
~~~~
void fivePointLaplacian(int n, vector<double> u_top, vector<double> u_bottom, vector<double> u_left, vector<double> u_right)
{
	double h = 1. / (n + 1); //mesh size

	vector<vector<double>> f(n, vector<double>(n)); //array for forcing function

	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			f[i][j] = sin((i + 1) * (j + 1) * h);
		}
	}

	vector<vector<double>> T(n, vector<double>(n, 0)); //T sub-matrix
	vector<vector<double>> I(n, vector<double>(n, 0)); //I sub-matrix

	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			if (i == j) //diagonal
			{
				T[i][j] = -4.;
				I[i][j] = 1.;
			}
			else if (abs(i - j) == 1) //off-diagonal
			{
				T[i][j] = 1.;
			}
		}
	}

	vector<vector<double>> A(pow(n, 2), vector<double>(pow(n, 2), 0)); //A matrix

	for (int i = 0; i < pow(n, 2); i += n)
	{
		for (int j = 0; j < pow(n, 2); j += n)
		{
			if (i == j) //diagonal block
			{
				for (int a = 0; a < n; a++)
				{
					for (int b = 0; b < n; b++)
					{
						A[i + a][j + b] = T[a][b];
					}
				}
			}
			else if (abs(i - j) == n) //off-diagonal block
			{
				for (int a = 0; a < n; a++)
				{
					for (int b = 0; b < n; b++)
					{
						A[i + a][j + b] = I[a][b];
					}
				}
			}
		}
	}

	vector<double> F = initF(h, n, f, u_top, u_bottom, u_left, u_right);

	vector<vector<double>> U = conjugateGradient(h, pow(n, 2), F, A);

	cout << "The solution is:" << endl;
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			cout << U[i][j] << " ";
		}
		cout << endl;
	}
}
~~~~
**Last Modified:** 28 Feb 18
