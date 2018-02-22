# Initialize 9 Point Laplacian

**Function Name:** initF

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function computes the right hand side of the equation *AU = F*, derived from the Laplacian equation *&Delta;u = f(x,y)* with nine stencil points.

**Input:** This function takes as input the step size h, the vectors representing the boundary conditions (*u_top*, *u_bottom*, *u_left*, and *u_right*), the number of interior rows n, and a matrix representing the forcing function f(x,y) at each discrete point. It is important to note that *u_top* and *u_bottom* include the corner nodes while *u_left* and *u_right* do not.

**Output:** This function returns a vector representing *F* in the matrix equation and displays its values.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
vector<double> F = initF(h, n, f, u_top, u_bottom, u_left, u_right);
~~~~
For example, if *n* = 5, *h* = 1/6, *u_top* contains <0, 1, 2, 3, 4, 5, 6>, *u_bottom* contains <6, 7, 8, 9, 10, 11, 12>, *u_left* contains <1, 2, 3, 4, 5>, *u_right* contains <7, 8, 9, 10, 11>, and *f = sin(xy)* the function would display:
~~~~
F contains:
F(1) = -11.9724
F(2) = -11.9455
F(3) = -17.9201
F(4) = -23.8969
F(5) = -65.8766
F(6) = -11.9455
F(7) = 0.103062
F(8) = 0.140245
F(9) = 0.16199
F(10) = -47.8341
F(11) = -17.9201
F(12) = 0.140245
F(13) = 0.166249
F(14) = 0.15155
F(15) = -53.9003
F(16) = -23.8969
F(17) = 0.16199
F(18) = 0.15155
F(19) = 0.0762121
F(20) = -60.0318
F(21) = -65.8766
F(22) = -47.8341
F(23) = -53.9003
F(24) = -60.0318
F(25) = -120.142
~~~~
**Implementation/Code:** The following is the code for initF():
~~~~
vector<double> initF(double h, int n, vector<vector<double>> f, vector<double> u_top, vector<double> u_bottom, vector<double> u_left, vector<double> u_right)
{
	vector<double> F(pow(n, 2)); //right hand side of equation
	vector<vector<double>> temp(n, vector<double>(n)); //2D representation of F

	//initialize corners
	temp[0][0] = (f[0][0] * 6 * pow(h, 2)) - u_top[0] - (4 * u_top[1]) - u_top[2] - (4 * u_left[0]) - u_left[1]; //top left corner
	temp[0][n - 1] = (f[0][n - 1] * 6 * pow(h, 2)) - u_top[n - 1] - (4 * u_top[n]) - u_top[n + 1] - (4 * u_right[0]) - u_right[1]; //top right corner
	temp[n - 1][n - 1] = (f[n - 1][n - 1] * 6 * pow(h, 2)) - u_right[n - 2] - (4 * u_right[n - 1]) - u_bottom[n + 1] - (4 * u_bottom[n]) - u_bottom[n - 1]; //bottom right corner
	temp[n - 1][0] = (f[n - 1][0] * 6 * pow(h, 2)) - u_left[n - 2] - (4 * u_left[n - 1]) - u_bottom[0] - (4 * u_bottom[1]) - u_bottom[2]; //bottom left corner

	//initialize edges
	for (int k = 1; k < n - 1; k++)
	{
		temp[0][k] = (f[0][k] * 6 * pow(h, 2)) - u_top[k] - (4 * u_top[k + 1]) - u_top[k + 2]; //top edge
		temp[n - 1][k] = (f[n - 1][k] * 6 * pow(h, 2)) - u_bottom[k] - (4 * u_bottom[k + 1]) - u_bottom[k + 2]; //bottom edge
		temp[k][0] = (f[k][0] * 6 * pow(h, 2)) - u_left[k - 1] - (4 * u_left[k]) - u_left[k + 1]; //left edge
		temp[k][n - 1] = (f[k][n - 1] * 6 * pow(h, 2)) - u_right[k - 1] - (4 * u_right[k]) - u_right[k + 1]; //right edge
	}

	//initialize interior
	for (int i = 1; i < n - 1; i++)
	{
		for (int j = 1; j < n - 1; j++)
		{
			temp[i][j] = f[i][j] * 6 * pow(h, 2);
		}
	}

	int k = 0; //helper variable to transform temp to F

	//transform temp (2D) to F (1D)
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			F[k++] = temp[i][j];
		}
	}

	cout << "F contains:" << endl;
	for (int i = 0; i < pow(n, 2); i++)
	{
		cout << "F(" << i + 1 << ") = " << F[i] << endl;
	}

	return F;
}
~~~~
**Last Modified:** 21 Feb 18
