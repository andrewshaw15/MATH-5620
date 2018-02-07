# Initialize Full Elliptic ODE

**Function Name:** initA

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function initializes the matrix *A* in *AU = F*, derived from the full elliptic ODE *(d/dx){k(x)u'} = f(x)* on the boundary *a < x < b* with boundary conditions *u(a) = u_a* and *u(b) = u_b*. Here, *k(x)* is a vector of size *n* whose elements are random integers between 10 and 50.

**Input:** This function takes as input the size *n* of *k* (the number of stencil points).

**Output:** This function outputs the matrix *A*.

**Usage/Example:** This function may be called and its results shown as follows:
~~~~
vector<vector<double>> A = initA(n);

cout << "The matrix A:" << endl;
for (int i = 0; i < n; i++)
{
	for (int j = 0; j < n; j++)
	{
		cout << A[i][j] << ' ';
	}
	cout << endl;
}
~~~~
For example, if *n* = 3 one possible result could be:
~~~~
The matrix A:
19 42 0
22 16 41
0 18 20
~~~~
**Implementation/Code:**
~~~~
vector<vector<double>> initA(int n)
{
	vector<vector<double>> A(n, vector<double>(n)); //A matrix

	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			if (i == j || abs(i - j) == 1)
			{
				A[i][j] = (rand() % 41) + 10; //random number between 10 and 50
			}
		}
	}

	return A;
}
~~~~
**Last Modified:** 6 Feb 18
