# Inverse Power Method

**Function Name:** inversePowerMethod

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function computes the smallest eigenvalue of a square matrix. The algorithm is the same as the power method, but the inverse of *A* is used instead of *A*. This function uses LU Factorization to find the inverse of the given *A* matrix (see [LU Factorization](https://andrewshaw15.github.io/MATH-5620/HW-2/LU-Factorization)).

**Input:** This function takes as input the matrix *A* and its size *n*.

**Output:** This function returns the smallest eigenvalue of the matrix.

**Example/Usage:** This function may be called and its result displayed as follows:
~~~~
cout << "The smallest eigenvalue is: " << inversePowerMethod(A, n) << endl;
~~~~
For example, if *n* = 3 and *A* contains <<3.556, -1.778, 0>, <-1.778, 3.556, -1.778>, <0, -1.778, 3.556>> the function will return
~~~~
The smallest eigenvalue is: 1.04153
~~~~
**Implementation/Code:** The following is the code for inversePowerMethod():
~~~~
double inversePowerMethod(vector<vector<double>> A, int n)
{
	//find transpose of inverse of A (has same eigenvalues as inverse of A)
	vector<vector<double>> A_i(n, vector<double>(n)); //A inverse transpose
	vector<double> F(n, 0); //vector to help find A inverse transpose

	for (int i = 0; i < n; i++)
	{
		fill(F.begin(), F.end(), 0);
		F[i] = 1;

		A_i[i] = LUFactorization(n, F, A);
	}

	vector<double> b(n, 1); //initial vector
	vector<double> temp(n, 0); //temp vector to help with matrix multiplication
	double lambda_old = 1; //initial eigenvalue
	double lambda; //final eigenvalue

	for (int i = 0; i < n; i++) //temp=A*b
	{
		for (int j = 0; j < n; j++)
		{
			temp[i] += A_i[i][j] * b[j];
		}
	}

	for (int i = 0; i < n; i++) //replace temp with b and reset temp
	{
		b[i] = temp[i];
		temp[i] = 0;
	}

	if (*max_element(b.begin(), b.end()) >= abs(*min_element(b.begin(), b.end())))
	{
		lambda = *max_element(b.begin(), b.end());
	}
	else
	{
		lambda = *min_element(b.begin(), b.end());
	}

	for (int i = 0; i < n; i++) //pull out largest b[i]
	{
		b[i] /= lambda;
	}

	int iterations = 1;

	double error = abs((lambda - lambda_old) / lambda) * 100; //relative error

	while (error >= 1 || iterations < 100) //while error is greater than 1% or max iterations reached
	{
		lambda_old = lambda; //update lambda

		for (int i = 0; i < n; i++) //temp=A*b
		{
			for (int j = 0; j < n; j++)
			{
				temp[i] += A_i[i][j] * b[j];
			}
		}

		for (int i = 0; i < n; i++) //set b=temp and reset temp
		{
			b[i] = temp[i];
			temp[i] = 0;
		}

		if (*max_element(b.begin(), b.end()) >= abs(*min_element(b.begin(), b.end())))
		{
			lambda = *max_element(b.begin(), b.end());
		}
		else
		{
			lambda = *min_element(b.begin(), b.end());
		}

		for (int i = 0; i < n; i++) //pull out largest b[i]
		{
			b[i] /= lambda;
		}

		iterations++;

		error = abs((lambda - lambda_old) / lambda) * 100; //update relative error
	}
	
	lambda = 1 / lambda;

	return lambda;
}
~~~~
**Last Modified:** 15 Feb 18
