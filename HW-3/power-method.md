# Power Method

**Function Name:** powerMethod

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function uses the power method iteratively to compute the largest eigenvalue of a square matrix.

**Input:** This function takes as input the matrix *A* and its size *n*.

**Output:** This function returns the largest eigenvalue of the matrix.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "The largest eigenvalue is: " << powerMethod(A, n) << endl;
~~~~
For example, if *A* is the Hilbert matrix and *n* = 3, the function will output:
~~~~
The largest eigenvalue is: 1.40832
~~~~
**Implementation/Code:** The following is the code for powerMethod():
~~~~
double powerMethod(vector<vector<double>> A, int n)
{
	vector<double> b(n, 1); //initial vector
	vector<double> temp(n, 0); //temp vector to help with matrix multiplication
	double lambda_old = 1; //initial eigenvalue
	double lambda; //final eigenvalue

	for (int i = 0; i < n; i++) //temp=A*b
	{
		for (int j = 0; j < n; j++)
		{
			temp[i] += A[i][j] * b[j];
		}
	}

	for (int i = 0; i < n; i++) //replace temp with b and reset temp
	{
		b[i] = temp[i];
		temp[i] = 0;
	}
  
  //lambda is largest value (positive or negative)
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
				temp[i] += A[i][j] * b[j];
			}
		}

		for (int i = 0; i < n; i++) //set b=temp and reset temp
		{
			b[i] = temp[i];
			temp[i] = 0;
		}
    
    //lambda is largest value (positive or negative)
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

	return lambda;
}
~~~~
**Last Modified:** 13 Feb 18
