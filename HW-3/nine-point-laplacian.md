# Laplacian Equation - 9 Point Stencil

**Function Name:** ninePointLaplacian

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function finds the solution of the 2D Laplace equation *&Delta;u = sin(xy)* on the unit square with homogeneous Dirichlet boundary conditions using LU Factorization by transforming the equation into *AU = F*. This function uses as helper functions initF() to initialize the right hand side (see [Initialize Nine Point Laplacian](https://andrewshaw15.github.io/MATH-5620/HW-3/initialize-nine-point-laplacian)) and a modified LUFactorization() to solve the linear system of equations (see [LU Factorization](https://andrewshaw15.github.io/MATH-5620/HW-2/LU-Factorization)).

**Input:** This function takes as input four vectors representing the boundary conditions (*u_left*, *u_right*, *u_top*, and *u_bottom*) and the number of interior rows *n*. It is important to note that *u_top* and *u_bottom* include the corner nodes while *u_left* and *u_right* do not.

**Output:** This function displays the result of the Laplace equation.

**Usage/Example:** This function may be called and its results diplayed as follows:
~~~~
ninePointLaplacian(n, u_top, u_bottom, u_left, u_right);
~~~~
For example, if *n* = 5, *u_top* contains <0, 1, 2, 3, 4, 5, 6>, *u_bottom* contains <6, 7, 8, 9, 10, 11, 12>, *u_left* contains <1, 2, 3, 4, 5>, and *u_right* contains <7, 8, 9, 10, 11> the function will display:
~~~~
The solution is:
1.98798 2.97824 3.97264 4.97263 5.98009
2.97824 3.96137 4.95309 5.95546 6.96981
3.97264 4.95309 5.94654 6.95411 7.97328
4.97263 5.95546 6.95411 7.9672 8.98677
5.98009 6.96981 7.97328 8.98677 10.0002
~~~~
**Implementation/Code:** The following is the code for ninePointLaplacian():
~~~~
void ninePointLaplacian(int n, vector<double> u_top, vector<double> u_bottom, vector<double> u_left, vector<double> u_right)
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
				T[i][j] = -20.;
				I[i][j] = 4.;
			}
			else if (abs(i - j) == 1) //off-diagonal
			{
				T[i][j] = 4.;
				I[i][j] = 1.;
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

	vector<vector<double>> U = LUFactorization(pow(n, 2), F, A);

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
**Last Modified:** 21 Feb 18
