# Full Elliptic ODE

**Function Name:** calcFullEllipticODE

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:**

**Input:**

**Output:**

**Usage/Example:**

**Implementation/Code:**
~~~~
void calcFullEllipticODE(int n, double a, double b, double u_a, double u_b, vector<double> f)
{
	srand(time(NULL));

	vector<vector<double>> A(n, vector<double>(n, 0)); //A matrix

	initA(A, n); //initialize A

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
