# Matrix Max Norm

**Function Name:** calcMatrixMaxNorm

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function calculates the max norm of a matrix, or the maximum row sum.

**Input:** This function takes as input the matrix *A* with its size (*m* rows and *n* columns).

**Output:** This function returns the max norm of the matrix.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "The Max Norm of A is: " << calcMatrixMaxNorm(A, m, n) << endl;
~~~~
For example, if *A* contains <<1, 2, 3>, <4, 5, 6>> (hence *m* = 2 and *n* = 3), the function would return:
~~~~
The Max Norm of A is: 15
~~~~
**Implementation/Code:** The following is the code for calcMatrixMaxNorm():
~~~~
double calcMatrixMaxNorm(vector<vector<double>> A, int m, int n)
{
	vector<double> maxRow(m, 0); //vector of row sums

	for (int i = 0; i < m; i++)
	{
		for (int j = 0; j < n; j++)
		{
			maxRow[i] += A[i][j];
		}
	}

	return *max_element(maxRow.begin(), maxRow.end());
}
~~~~
**Last Modified:** 12 Feb 18
