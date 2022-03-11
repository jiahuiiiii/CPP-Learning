# 2.3 — Introduction to function parameters and arguments

- We could have a function return a value back to the function’s caller. 
- We used that to create a modular *getValueFromUser* function that we used in this program:

```cpp
#include <iostream>

int getValueFromUser()
{
 	std::cout << "Enter an integer: ";
	int input{};
	std::cin >> input;

	return input;
}

int main()
{
	int num { getValueFromUser() };

	std::cout << num << " doubled is: " << num * 2 << '\n';

	return 0;
}
```

- What if we wanted to put the output line into its own function as well? You might try something like this:

```cpp
#include <iostream>

int getValueFromUser()
{
 	std::cout << "Enter an integer: ";
	int input{};
	std::cin >> input;

	return input;
}

// This function won't compile
void printDouble()
{
	std::cout << num << " doubled is: " << num * 2 << '\n';
}

int main()
{
	int num { getValueFromUser() };

	printDouble();

	return 0;
}
```

- This **won’t compile**, because **function *printDouble* doesn’t know what identifier *num* is.** 
- **Function *printDouble*** doesn’t have a way to **access the value the user entered**.

- We need some way to **pass the value of variable *num* to function *printDouble*** so that ***printDouble* can use that value in the function body**.

## Function parameters and arguments

- It is useful to be able to **pass information *to* a function being called**, so that **the function has data to work with**. 
- For example, if we wanted to write a **function to add two numbers**, we need some way to **tell the function which two numbers to add when we call it**. We do that via **function parameters and arguments**.

- A **function parameter** is **a variable used in a function.** 
- Function parameters **work almost identically to variables defined inside the function**, but with one difference: **they are always initialized with a value provided by the caller of the function**.

- Function parameters are **defined in the function declaration** by placing them **in between the parenthesis after the function identifier**, with **multiple parameters being separated by commas**.

```cpp
// This function takes no parameters
// It does not rely on the caller for anything
void doPrint()
{
    std::cout << "In doPrint()\n";
}

// This function takes one integer parameter named x
// The caller will supply the value of x
void printValue(int x)
{
    std::cout << x  << '\n';
}

// This function has two integer parameters, one named x, and one named y
// The caller will supply the value of both x and y
int add(int x, int y)
{
    return x + y;
}
```

- An **argument** is a **value that is passed *from* the caller *to* the function when a function call is made**:

```cpp
doPrint(); // this call has no arguments
printValue(6); // 6 is the argument passed to function printValue()
add(2, 3); // 2 and 3 are the arguments passed to function add()
```

- Note that **multiple arguments are also separated by commas**.

### How parameters and arguments work together

- When a function is called, all of **the parameters of the function are created as variables**
- The **value of each of the arguments is *copied* into the matching parameter**. 
- This process is called **pass by value**.

For example:

```cpp
#include <iostream>

// This function has two integer parameters, one named x, and one named y
// The values of x and y are passed in by the caller
void printValues(int x, int y)
{
    std::cout << x << '\n';
    std::cout << y << '\n';
}

int main()
{
    printValues(6, 7); // This function call has two arguments, 6 and 7

    return 0;
}
```

- When function *printValues* is called with arguments *6* and *7*, *printValues*‘s parameter *x* is created and initialized with the value of *6*, and *printValues*‘s parameter *y* is created and initialized with the value of *7*.

```
6
7
```

- Note that **the number of arguments must generally match the number of function parameters.**
- The **argument passed to a function can be any valid expression** (as the **argument is essentially just an initializer for the parameter**, and **initializers can be any valid expression**).

### Fixing our challenge program

We now have the tool we need to fix the program we presented at the top of the lesson:

```cpp
#include <iostream>

int getValueFromUser()
{
 	std::cout << "Enter an integer: ";
	int input{};
	std::cin >> input;

	return input;
}

void printDouble(int value) // This function now has an integer parameter
{
	std::cout << value << " doubled is: " << value * 2 << '\n';
}

int main()
{
	int num { getValueFromUser() };

	printDouble(num);

	return 0;
}
```

- In this program, **variable *num* is first initialized with the value entered by the user**. 
- Then, function *printDouble* is called, and **the value of argument *num* is copied into the *value* parameter of function *printDouble***. 
- Function *printDouble* then uses the value of parameter *value*.

### Using return values as arguments

- We can see that v**ariable *num* is only used once, to transport the return value of function *getValueFromUser* to the argument of the call to function *printDouble***.

We can **simplify** the above example slightly as follows:

```cpp
#include <iostream>

int getValueFromUser()
{
 	std::cout << "Enter an integer: ";
	int input{};
	std::cin >> input;

	return input;
}

void printDouble(int value)
{
	std::cout << value << " doubled is: " << value * 2 << '\n';
}

int main()
{
	printDouble(getValueFromUser());

	return 0;
}
```

- Now, we’re **using the return value of function *getValueFromUser* directly as an argument to function *printDouble***。

### How parameters and return values work together

- By **using both parameters and a return value**, we can create **functions that take data as input**, **do some calculation with it**, and r**eturn the value to the caller**.

```cpp
#include <iostream>

// add() takes two integers as parameters, and returns the result of their sum
// The values of x and y are determined by the function that calls add()
int add(int x, int y)
{
    return x + y;
}

// main takes no parameters
int main()
{
    std::cout << add(4, 5) << '\n'; // Arguments 4 and 5 are passed to function add()
    return 0;
}
```

```
9
```

In pictorial format:

![img](https://www.learncpp.com/images/CppTutorial/Chapter2/ParametersReturn.png?ezimgfmt=rs:441x251/rscb2/ng:webp/ngcb2)

### More examples

```cpp
#include <iostream>

int add(int x, int y)
{
    return x + y;
}

int multiply(int z, int w)
{
    return z * w;
}

int main()
{
    std::cout << add(4, 5) << '\n'; // within add() x=4, y=5, so x+y=9
    std::cout << add(1 + 2, 3 * 4) << '\n'; // within add() x=3, y=12, so x+y=15

    int a{ 5 };
    std::cout << add(a, a) << '\n'; // evaluates (5 + 5)

    std::cout << add(1, multiply(2, 3)) << '\n'; // evaluates 1 + (2 * 3)
    std::cout << add(1, add(2, 3)) << '\n'; // evaluates 1 + (2 + 3)

    return 0;
}
```

```
9
15
10
7
6
```

## Conclusion

- **Function parameters and return values** allows us to write functions that can **perform tasks and return retrieved results back to the caller** without knowing what the specific inputs or outputs are ahead of time.