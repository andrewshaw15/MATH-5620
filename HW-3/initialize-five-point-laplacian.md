# Initialize 5 Point Laplacian

**Function Name:** initF

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function computes the right hand side of the equation *AU = F*, derived from the Laplacian equation *&Delta;u = f(x,y)* with five stencil points.

**Input:** This function takes as input the step size *h*, the vectors representing the boundary conditions (*u_top*, *u_bottom*, *u_left*, and *u_right*), and their size *n*, along with a matrix representing the forcing function *f(x,y)* at each discrete point.

**Output:** This function returns a vector representing *F* in the matrix equation and displays its values.

**Usage/Example:** This function may be called and its results displayed as follows:
~~~~
vector<double> F = initF(h, n, f, u_top, u_bottom, u_left, u_right);
~~~~
For example, if *h* = 1/6, *n* = 5, *f* = *sin(xy)*, *u_top* contained <1, 2, 3, 4, 5>, *u_left* contained <1, 2, 3, 4, 5>, *u_bottom* contained <7, 8, 9, 10, 11>, and *u_right* contained <7, 8, 9, 10, 11>, the function would return:
~~~~
F contains:
F(1) = -1.99539
F(2) = -1.99091
F(3) = -2.98668
F(4) = -3.98282
F(5) = -11.9794
F(6) = -1.99091
F(7) = 0.0171769
F(8) = 0.0233742
F(9) = 0.0269983
F(10) = -7.97235
F(11) = -2.98668
F(12) = 0.0233742
F(13) = 0.0277082
F(14) = 0.0252583
F(15) = -8.98338
F(16) = -3.98282
F(17) = 0.0269983
F(18) = 0.0252583
F(19) = 0.012702
F(20) = -10.0053
F(21) = -11.9794
F(22) = -7.97235
F(23) = -8.98338
F(24) = -10.0053
F(25) = -22.0237
~~~~
**Implementation/Code:** The following is the code for initF():
~~~~
vector<double> initF(double h, int n, vector<vector<double>> f, vector<double> u_top, vector<double> u_bottom, vector<double> u_left, vector<double> u_right)
{
	vector<double> F(pow(n, 2)); //right hand side of equation
	vector<vector<double>> temp(n, vector<double>(n)); //2D representation of F

	//initialize corners
	temp[0][0] = (f[0][0] * pow(h, 2)) - u_top[0] - u_left[0]; //top left corner
	temp[0][n - 1] = (f[0][n - 1] * pow(h, 2)) - u_top[n - 1] - u_right[0]; //top right corner
	temp[n - 1][n - 1] = (f[n - 1][n - 1] * pow(h, 2)) - u_bottom[n - 1] - u_right[n - 1]; //bottom right corner
	temp[n - 1][0] = (f[n - 1][0] * pow(h, 2)) - u_bottom[0] - u_left[n - 1]; //bottom left corner

	//initialize edges
	for (int k = 1; k < n - 1; k++)
	{
		temp[0][k] = (f[0][k] * pow(h, 2)) - u_top[k]; //top edge
		temp[n - 1][k] = (f[n - 1][k] * pow(h, 2)) - u_bottom[k]; //bottom edge
		temp[k][0] = (f[k][0] * pow(h, 2)) - u_left[k]; //left edge
		temp[k][n - 1] = (f[k][n - 1] * pow(h, 2)) - u_right[k]; //right edge
	}

	//initialize interior
	for (int i = 1; i < n - 1; i++)
	{
		for (int j = 1; j < n - 1; j++)
		{
			temp[i][j] = f[i][j] * pow(h, 2);
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
**Last Modified:** 20 Feb 18
