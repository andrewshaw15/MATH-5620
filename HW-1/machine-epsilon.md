# Machine Epsilon

**Function Name:** calcMachEps

**Author:** Andrew Shaw

**Language:** C++14

**Description/Purpose:** This function will compute the double precision value for machine epsilon for any computer. Machine epsilon is the maximum relative error, or smallest incremental value a computer can recognize. Since this value can be different for every computer, it is recommended that this function be run on each computer to determine its machine epsilon.

**Input:** No input is required for this function.

**Output:** This function returns a double precision value representing the machine epsilon of the computer the function is run on.

**Usage/Example:** This function is called and the results displayed as follows:
~~~~
cout << "Machine Epsilon: " << calcMachEps() << endl;
~~~~
Sample output (results may vary on different computers):
~~~~
Machine Epsilon: 2.22045e-16
~~~~
This shows that approximately 16 decimal digits may be represented.

**Implementation/Code:** The following shows the code for calcMachineEpsilon():
~~~~
double calcMachEps()
{
	double epsilon = 1.0; //initial epsilon

	while (epsilon + 1 > 1) //while computer can differentiate between epsilon and 0
	{
		epsilon /= 2;
	}

	epsilon *= 2;

	return epsilon;
}
~~~~

**Last Modified:** 22 Jan 18
