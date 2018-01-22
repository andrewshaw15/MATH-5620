# Relative Error

**Function Name:** calcRelErr

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** The purpose of this function is to calculate the relative error of an approximated value when compared to the true value. The relative error is the absolute error divided by the true value and is a way to determine the accuracy of an approximated value.

**Input:** This function requires to inputs: the true value and the approximated value (in that order).

**Output:** This function returns the relative error of the approximated value.

**Usage/Example:** This function may be called and the relative error displayed as follows:
~~~~
cout << "Relative Error: " << calcRelErr(real, approx) << endl;
~~~~
For instance, if the real value was 4 and the approximated value was 3.5, the function would return
~~~~
Relative Error: 0.125
~~~~
**Implementation/Code:** Below is the function calcRelErr()
~~~~
double calcRelErr(double real, double approx)
{
	return abs((approx - real) / real);
}
~~~~
**Last Modified:** 22 Jan 18
