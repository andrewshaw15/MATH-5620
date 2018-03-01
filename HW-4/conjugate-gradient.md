# Conjugate Gradient Method

**Function Name:** conjugateGradient

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function calculates the solution of a system of linear equations *AU = F* using the conjugate gradient method. As a note, this method will converge in at most *n* iterations, where *n* is the size of the matrix, not accounting for round-off error. Even with round-off error, this method will converge significantly faster than Jacobi or Gauss-Seidel. This function uses three helper functions: calc2Norm() to calculate the vector two norm (see [2 Norm](https://andrewshaw15.github.io/MATH-5620/HW-2/2-Norm)), matrixMultiply() to multiply a matrix with a vector, and vectorMultiply() to multiply two vectors together.

**Input:** This function takes as input the matrix *A*, the vector *F*, and their size *n*.

**Output:** This function returns and displays a vector representing the solution of the linear system of equations.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
vector<double> U = conjugateGradient(n, F, A);
~~~~
For example, if *n* = 5, *A* contains <<-2, 1, 0, 0, 0>, <1, -2, 1, 0, 0>, <0, 1, -2, 1, 0>, <0, 0, 1, -2, 1>, <0, 0, 0, 1, -2>>, and *F* contains <1, 2, 4, 8, 16>, the function will display:
~~~~
The solution is:
U(1) = -9.5
U(2) = -18
U(3) = -24.5
U(4) = -27
U(5) = -21.5
~~~~
**Implementation/Code:** The following is the code for conjugateGradient():
~~~~
vector<double> conjugateGradient(int n, vector<double> F, vector<vector<double>> A)
{
	double h = 1. / (n + 1);

	vector<double> U(n, 0); //solution vector with initial guess
	vector<double> r_old(n); //original residual vector
	vector<double> p_old(n); //original search direction

	vector<double> temp = matrixMultiply(A, U, n); //helper vector

	for (int i = 0; i < n; i++)
	{
		r_old[i] = F[i] - temp[i];
	}

	p_old = r_old;

	double error = calc2Norm(r_old, h, n);

	double iter = 0;

	while(error > (error / 10) && iter < 1000)
	{
		vector<double> w = matrixMultiply(A, p_old, n); //helper vector
		
		//double a = ((r_old^T) * r_old)/((p_old^T) * w);
		double a = vectorMultiply(r_old, r_old, n) / vectorMultiply(p_old, w, n);

		//U = U + (a * p_old);
		for (int i = 0; i < n; i++)
		{
			U[i] = U[i] + (a * p_old[i]);
		}

		vector<double> r(n); //new residual vector
		//r = r_old - (a * w);
		for (int i = 0; i < n; i++)
		{
			r[i] = r_old[i] - (a * w[i]);
		}

		error = calc2Norm(r, h, n);

		//double b = ((r^T) * r)/((r_old^T) * r_old);
		double b = vectorMultiply(r, r, n) / vectorMultiply(r_old, r_old, n);

		vector<double> p(n); //new search direction
		//p = r + (b * p_old);
		for (int i = 0; i < n; i++)
		{
			p[i] = r[i] + (b*p_old[i]);
		}

		r_old = r; //update r
		p_old = p; //update p

		iter++;
	}

	cout << "The solution is:" << endl;
	for (int i = 0; i < n; i++)
	{
		cout << "U(" << i + 1 << ") = " << U[i] << endl;
	}

	return U;
}

double calc2Norm(vector<double> v, double h, int n)
{
	double two_norm = 0.;

	for (int i = 0; i < n; i++)
	{
		two_norm += pow(v[i], 2);
	}

	two_norm *= h;

	two_norm = sqrt(two_norm);

	return two_norm;
}

vector<double> matrixMultiply(vector<vector<double>> A, vector<double> v, int n)
{
	vector<double> u(n, 0); //solution

	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			u[i] += A[i][j] * v[j];
		}
	}

	return u;
}

double vectorMultiply(vector<double> v, vector<double> w, int n)
{
	double u = 0; //solution

	for (int i = 0; i < n; i++)
	{
		u += v[i] * w[i];
	}

	return u;
}
~~~~
**Last Modified:** 28 Feb 18
