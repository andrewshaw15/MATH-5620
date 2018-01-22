# Absolute Error

**Function Name:** calcAbsError

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function calculates the absolute error of an approximated value when compared to the true value. Absolute error is the absolute value of the difference between the approximated value and the true value. This error will help determine how accurate an approximated solution is.

**Input:** Two values are needed as input for this function: the true value and the approximated value. The order that these numbers are inputted into the function does not matter.

**Output:** This function will output the absolute error of the values entered.

**Usage/Example:** The function may be called and the absolute error returned in the following fashion:
~~~~
cout << "Absolute Error: " << calcAbsErr(real, approx) << endl;
~~~~
For instance, if the values inputted were 4 and 3.5, the function would return
~~~~
Absolute Error: 0.5
~~~~
**Implementation/Code:** Below is the code for calcAbsError():
~~~~
double calcAbsErr(double real, double approx)
{
	return abs(approx - real);
}
~~~~
**Last Modified:** 22 Jan 18
