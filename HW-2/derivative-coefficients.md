# Derivative Coefficients

**Function Name:** calCoeff

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function calculates the coefficients for finite difference approximations of the *k*th derivative of a function *u(x)* evaluated at a value *xBar*.

**Input:** This function requires as input the derivative to be approximated *k*, the value *xBar* at which this derivative is to be evaluated, the vector of *x* values, and the size *n* of the vector *x*.

**Output:** This function returns a vector representing the coefficients for the finite difference approximation.

**Usage/Example:** The function may be called and the coefficient vector displayed as follows:
~~~~
vector<double> c = calcCoeff(k, xBar, x, n);

cout << "The coefficients are:" << endl;
for (int i = 0; i < n; i++)
{
	cout << "C" << i << " = " << c[i] << endl;
}
~~~~
For example, if *k* = 1, *xBar* = 2, the contents of *x* are <2, 1, 0>, and *n* = 3, the result would be:
~~~~
The coefficients are:
C0 = 1.5
C1 = -2
C2 = 0.5
~~~~
**Implementation/Code:**
~~~~
vector<double> calcCoeff(int k, double xBar, vector<double> x, int n)
{
	vector<vector<double>> A(n, vector<double>(n, 1)); //matrix A

	vector<double> xRow(n); //displacements

	for (int i = 0; i < n; i++)
	{
		xRow[i] = x[i] - xBar;
	}

	for (int i = 1; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			A[i][j] = pow(xRow[j], i) / calcFac(i);
		}
	}

	vector<double> B(n, 0); //right hand side vector
	B[k] = 1.;

	vector<double> C(n); //coefficients vector

	//find A^-1 (C = (A^-1)*B)
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

	//substitution
	double s; //sum

	for (int i = 1; i < n; i++)
	{
		//forward substitution
		s = B[i];

		for (int j = 0; j < i; j++)
		{
			s -= A[i][j] * B[j];
		}

		B[i] = s;

		//back substitution
		C[n - 1] = B[n - 1] / A[n - 1][n - 1];

		for (int i = n - 2; i >= 0; i--)
		{
			s = 0;

			for (int j = i + 1; j < n; j++)
			{
				s += A[i][j] * C[j];
			}

			C[i] = (B[i] - s) / A[i][i];
		}
	}

	return C;
}

double calcFac(double i) //helper function to calculate factorial
{
	if (i < 2.)
	{
		return 1.;
	}

	return (i * calcFac(i - 1.));
}
~~~~
**Last Modified:** 3 Feb 18
