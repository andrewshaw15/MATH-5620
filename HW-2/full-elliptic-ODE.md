# Full Elliptic ODE

**Function Name:** calcFullEllipticODE

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function solves the full elliptic ODE *(d/dx){k(x)u'} = f(x)* on the boundary *a < x < b* with boundary conditions *u(a) = u_a* and *u(b) = u_b*. Here, *k(x)* is defined as a vector of size *n* whose elements are random integers from 10 to 50. The full elliptic ODE is transformed into *AU = F* (refer to [Initialize Full Elliptic ODE](https://andrewshaw15.github.io/MATH-5620/HW-2/initialize-full-elliptic-ODE) for *A* initialization and [Initialize Simple Elliptic ODE](https://andrewshaw15.github.io/MATH-5620/HW-2/initialize-simple-elliptic-ODE) for *F* initialization) and solved using the Thomas Algorithm (see [Thomas Algorithm](https://andrewshaw15.github.io/MATH-5620/HW-2/thomas-algorithm)), LU Factorization (see [LU Factorization](https://andrewshaw15.github.io/MATH-5620/HW-2/LU-Factorization)), and Jacobi Iteration (see [Jacobi Iteration](https://andrewshaw15.github.io/MATH-5620/HW-2/Jacobi-Iteration)).

**Input:** This function takes as input the left and right boundaries (*a* and *b*, respectively), the values of *u(x)* at the boundaries (*u_a* and *u_b*), the vector of *f* values, the matrix *A*, and the size *n* of *f* and *A*.

**Output:** This function displays the solution of the full elliptic ODE as calculated by the three methods described above.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
calcFullEllipticODE(n, a, b, u_a, u_b, f, A);
~~~~
For example, a possible output of the function if *n* = 3, *a* = 0, *b* = 1, *u_a* = 2.5, *u_b* = 5, and the contents of *f* are <0.025, 0.05, 0.075> (remembering the contents of *A* are determined randomly) could be:
~~~~
Thomas Algorithm Solution:
U(1) = -1.42885
U(2) = 1.71812
U(3) = -0.676774

LU Factorization Solution:
U(1) = -1.42885
U(2) = 1.71812
U(3) = -0.676774

Jacobi Iteration Solution:
U(1) = -1.42607
U(2) = 1.70075
U(3) = -0.675582
~~~~
**Implementation/Code:**
~~~~
void calcFullEllipticODE(int n, double a, double b, double u_a, double u_b, vector<double> f, vector<vector<double>> A)
{
	vector<double> F = initF(a, b, u_a, u_b, n, f);

	vector<double> U_TA = thomasAlgorithm(n, F, A); //Thomas Algorithm Solution

	cout << "Thomas Algorithm Solution:" << endl;
	for (int i = 0; i < n; i++)
	{
		cout << "U(" << i + 1 << ") = " << U_TA[i] << endl;
	}
	cout << endl;

	vector<double> U_LUF = LUFactorization(n, F, A);

	cout << "LU Factorization Solution:" << endl;
	for (int i = 0; i < n; i++)
	{
		cout << "U(" << i + 1 << ") = " << U_LUF[i] << endl;
	}
	cout << endl;

	vector<double> U_JI = jacobiIteration(n, F, A);

	cout << "Jacobi Iteration Solution:" << endl;
	for (int i = 0; i < n; i++)
	{
		cout << "U(" << i + 1 << ") = " << U_JI[i] << endl;
	}
	cout << endl;
}
~~~~
**Last Modified:** 6 Feb 18 
