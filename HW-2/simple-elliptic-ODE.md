# Simple Elliptic ODE

**Function Name:** calcSimpleEllipticODE

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:**

**Input:**

**Output:**

**Usage/Example:**

**Implementation/Code:**
~~~~
void calcSimpleEllipticODE(int n)
{
	const double PI = 3.14159265;

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
**Last Modified:** 1 Feb 18
