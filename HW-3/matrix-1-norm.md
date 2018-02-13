# Matrix 1 Norm

**Function Name:** calcMatrix1Norm

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function computes the 1 norm of a matrix, or the maximum column sum.

**Input:** This function takes as input the matrix *A* with its *m* rows and *n* columns.

**Output:** This function outputs the 1 norm of the matrix.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
cout << "The 1-Norm of A is: " << calcMatrix1Norm(A, m, n) << endl;
~~~~
For example, if *A* contained <<1, 2, 3>, <4, 5, 6>> (hence *m* being 2 and *n* being 3), the function would return:
~~~~
The 1-Norm of A is: 9
~~~~
**Implementation/Code:** The following is the code for calcMatrix1Norm():
~~~~
double calcMatrix1Norm(vector<vector<double>> A, int m, int n)
{
	vector<double> maxCol(n, 0); //vector of column sums

	for (int i = 0; i < m; i++)
	{
		for (int j = 0; j < n; j++)
		{
			maxCol[j] += A[i][j];
		}
	}

	return *max_element(maxCol.begin(), maxCol.end());
}
~~~~
**Last Modified:** 12 Feb 18
