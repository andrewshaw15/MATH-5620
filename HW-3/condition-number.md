# Condition Number

**Function Name:** calcConditionNumber

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function calculates the condition number of a matrix. This function uses the two-norm and assumes that the matrix is normal. To find the maximum and minimum eigenvalues refer to [Power Method](https://andrewshaw15.github.io/MATH-5620/HW-3/power-method) and [Inverse Power Method](https://andrewshaw15.github.io/MATH-5620/HW-3/inverse-power-method), respectively. As a note, the relationship of the condition number to the size *n* of the matrix is *k = {1 + cos(&pi;/(n + 1))}/{1 + cos(n&pi;/(n + 1))}* for a tridiagonal, Toeplitz matrix ([Tridiagonal Matrix - Wikipedia](https://en.wikipedia.org/wiki/Tridiagonal_matrix) and [Condition Number - Wikipedia](https://en.wikipedia.org/wiki/Condition_number)).

**Input:** This function takes as input the maximum eigenvalue and the minimum eigenvalue of the matrix.

**Output:** This function returns the condition number of the matrix.

**Usage/Example:** This function may be called and its result displayed as follows:
~~~~
cout << "The condition number is: " << calcConditionNumber(lambda_max, lambda_min) << endl;
~~~~
For example, if the matrix is defined as that derived from the simple elliptic ODE *u" = f(x)*, that is *A* = <<-2, 1, 0>, <1, -2, 1>, <0, 1, -2>> (hence *&lambda;_max* = -3.41421 and *&lambda;_min* = -0.585786), the function will return:
~~~~
The condition number is: 5.82843
~~~~
**Implementation/Code:** The following is the code for calcConditionNumber():
~~~~
double calcConditionNumber(double lambda_max, double lambda_min)
{
	double k; //condition number

	k = abs(lambda_max / lambda_min);

	return k;
}
~~~~
**Last Modified:** 15 Feb 18
