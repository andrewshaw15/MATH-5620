# Initialize Full Elliptic ODE

**Function Name:** initA

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:**

**Input:**

**Output:**

**Usage/Example:**

**Implementation/Code:**
~~~~
void initA(vector<vector<double>>& A, int n)
{
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
}
~~~~
**Last Modified:** 30 Jan 18
