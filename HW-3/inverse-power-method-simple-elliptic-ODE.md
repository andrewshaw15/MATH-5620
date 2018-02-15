# Smallest Eigenvalue - Simple Elliptic ODE

**Function Name:** inversePowerMethod_SimpleEllipticODE

**Author:** Andrew Shaw

**Language:** C++14

**Purpose/Description:** This function is the same as inversePowerMethod() (see [Inverse Power Method](https://andrewshaw15.github.io/MATH-5620/HW-3/inverse-power-method) but applied to the simple elliptic ODE *u" = f(x)*. Using the centered difference method to approximate *u"*, the matrix *A* in *AU = F* becomes the following: the diagonal terms are -2, the off-diagonal terms are 1, and all other terms are 0. As a note, the smallest eigenvalues are related to the size *n* of *A* by *&lambda; = -2 - 2cos(&pi;n/(n + 1))* ([Wikipedia](https://en.wikipedia.org/wiki/Tridiagonal_matrix)).

**Input:** This function takes as input the matrix *A* and its size *n*.

**Output:** This function returns the smallest eigenvalue of *A*.

**Usage/Example:** This function may be called and its result displayed as follows:
~~~~
cout << "The smallest eigenvalue is: " << inversePowerMethod_SimpleEllipticODE(A, n) << endl;
~~~~
For example, if *n* = 3 the function will return:
~~~~

~~~~
