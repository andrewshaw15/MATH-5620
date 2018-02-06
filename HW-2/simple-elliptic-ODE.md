# Simple Elliptic ODE

**Function Name:** calcSimpleEllipticODE

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function solves the simple elliptic ODE *u" = f(x)* on the interval 0 *< x <* 1 with *u(0)* = 2.5, *u(1)* = 5.0, and *f(x) = sin(&pi;x)* using the Thomas Algorithm (refer to [Thomas Algorithm](https://andrewshaw15.github.io/MATH-5620/HW-2/thomas-algorithm)), LU Factorization (refer to [LU Factorization](https://andrewshaw15.github.io/MATH-5620/HW-2/LU-Factorization)), and Jacobi Iteration (refer to [Jacobi Iteration](https://andrewshaw15.github.io/MATH-5620/HW-2/Jacobi-Iteration)). See [Initialize Simple Elliptic ODE](https://andrewshaw15.github.io/MATH-5620/HW-2/initialize-simple-elliptic-ODE) for transforming *u" = f(x)* to *AU = F*.

**Input:** This function takes as input the size *n* of *f* (the number of stencil points).

**Output:** This function displays three vectors representing the solutions obtained via the three methods described above.

**Usage/Example:** This code may be called and its results displayed as follows:
~~~~
calcSimpleEllipticODE(n);
~~~~
For example, if *n* = 3, the function outputs:
~~~~
Thomas Algorithm Solution:
U(1) = 3.04956
U(2) = 3.64331
U(3) = 4.29956

LU Factorization Solution:
U(1) = 3.04956
U(2) = 3.64331
U(3) = 4.29956

Jacobi Iteration Solution:
U(1) = 3.0315
U(2) = 3.62525
U(3) = 4.29053
~~~~
**Implementation/Code:**
~~~~
void calcSimpleEllipticODE(int n)
{
	vector<vector<double>> A(n, vector<double>(n, 0)); //A matrix

	//initialize A
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			if (i == j) //diagonal terms
			{
				A[i][j] = -2.;
			}
			else if (abs(i - j) == 1) //off diagonal terms
			{
				A[i][j] = 1.;
			}
		}
	}

	double a = 0.; //left boundary
	double b = 1.; //right boundary
	double u_a = 2.5; //value at left boundary
	double u_b = 5.0; //value at right boundary
	vector<double> f(n); //forcing function values (sin(pi*x))

	double h = (b - a) / (n + 1); //mesh size

	for (int i = 0; i < n; i++)
	{
		f[i] = sin(PI * (i + 1) * h);
	}

	vector<double> F = initF(a, b, u_a, u_b, n, f); //Set up right hand side

	vector<double> U_TA = thomasAlgorithm(n, F, A); //Thomas Algorithm Solution

	cout << "Thomas Algorithm Solution:" << endl;
	for (int i = 0; i < n; i++)
	{
		cout << "U(" << i + 1 << ") = " << U_TA[i] << endl;
	}
	cout << endl;

	vector<double> U_LUF = LUFactorization(n, F, A); //LU Factorization Solution

	cout << "LU Factorization Solution:" << endl;
	for (int i = 0; i < n; i++)
	{
		cout << "U(" << i + 1 << ") = " << U_LUF[i] << endl;
	}
	cout << endl;

	vector<double> U_JI = jacobiIteration(n, F, A); //Jacobi Iteration Solution

	cout << "Jacobi Iteration Solution:" << endl;
	for (int i = 0; i < n; i++)
	{
		cout << "U(" << i + 1 << ") = " << U_JI[i] << endl;
	}
	cout << endl;
}
~~~~
**Last Modified:** 6 Feb 18
