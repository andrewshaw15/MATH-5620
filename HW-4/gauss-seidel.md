# Gauss-Seidel Method

**Function Name:** GaussSiedel

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function uses the Gauss-Seidel method to solve the 5 point Laplace equation *&Delta;u = f(x,y)* on the unit square with homogeneous Dirichlet boundary conditions. As a note, this method converges approximately twice as fast as the Jacobi iteration.

**Input:** This function takes as input the number of interior rows *n* and vectors representing the boundary conditions (*u_top*, *u_bottom*, *u_left*, and *u_right*). Note that these vectors do not include the corner nodes.

**Output:** This function displays the solution of the Laplace equation as an *n* x *n* matrix.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
GaussSeidel(n, u_top, u_bottom, u_left, u_right);
~~~~
For example, if *n* = 5, the contents of *u_top* are <1, 2, 3, 4, 5>, the contents of *u_bottom* are <7, 8, 9, 10, 11>, the contents of *u_left* are <1, 2, 3, 4, 5>, the contents of *u_right* are <7, 8, 9, 10, 11>, and *f(x,y) = sin(xy)*, the function would display:
~~~~
The solution is:
1.98812 2.97855 3.97317 4.97341 5.98096
2.97855 3.962 4.95404 5.95667 6.97101
3.97317 4.95404 5.9477 6.95522 7.97404
4.97341 5.95667 6.95522 7.96772 8.98657
5.98096 6.97101 7.97404 8.98657 9.99922
~~~~
**Implementation/Code:** The following is the code for GaussSeidel():
~~~~
void GaussSeidel(int n, vector<double> u_top, vector<double> u_bottom, vector<double> u_left, vector<double> u_right)
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

	vector<vector<double>> U(n + 2, vector<double>(n + 2, 0)); //solution with initial guess

	for (int k = 0; k < n; k++) //set up borders
	{
		U[0][k + 1] = u_top[k]; //top border
		U[n + 1][k + 1] = u_bottom[k]; //bottom border
		U[k + 1][0] = u_left[k]; //left border
		U[k + 1][n + 1] = u_right[k]; //right border
	}

	for (int k = 0; k < 1000; k++) //perform 1000 iterations
	{
		for (int i = 1; i <= n; i++)
		{
			for (int j = 1; j <= n; j++)
			{
				U[i][j] = 0.25 * (U[i - 1][j] + U[i + 1][j] + U[i][j - 1] + U[i][j + 1] - (pow(h, 2) * f[i - 1][j - 1]));
			}
		}
	}
	
	cout << "The solution is:" << endl;
	for (int i = 1; i < n + 1; i++)
	{
		for (int j = 1; j < n + 1; j++)
		{
			cout << U[i][j] << " ";
		}
		cout << endl;
	}
}
~~~~
**Last Modified:** 27 Feb 18
