# 1.8 — Whitespace and basic formatting

- **Whitespace** is a term that refers to **characters that are used for formatting purposes**. 
- In C++, this refers primarily to **spaces, tabs, and newlines**. 
- The C++ **compiler generally ignores whitespace**, with **a few minor exceptions (when processing text literals)**. 
- For this reason, we say that **C++ is a whitespace-independent language.**

Consequently, the **following statements all do the exact same thing**:

```cpp
std::cout << "Hello world!";

std::cout               <<            "Hello world!";

		std::cout << 		"Hello world!";

std::cout
	<< "Hello world!";
```

The **following functions all do the same thing**:

```cpp
int add(int x, int y) { return x + y; }

int add(int x, int y) {
    return x + y; }

int add(int x, int y)
{    return x + y; }

int add(int x, int y)
{
    return x + y;
}
```

One exception where the **C++ compiler *does* pay attention to whitespace is inside quoted text**, such as `"Hello world!"`.

```
"Hello world!"
```

is different than:

```
"Hello     world!"
```

and each prints out exactly as you’d expect.

**Newlines are not allowed in quoted text**:

```cpp
std::cout << "Hello
     world!"; // Not allowed!
```

**Quoted text separated by** nothing but **whitespace (spaces, tabs, or newlines)** will be **concatenated**:

```cpp
std::cout << "Hello "
     "world!"; // prints "Hello world!"
```

Another exception where the **C++ compiler pays attention to whitespace is with // comments**. **Single-line comments only last to the end of the line**. Thus doing something like this will get you in trouble:

```cpp
std::cout << "Hello world!"; // Here is a single-line comment
this is not part of the comment
```

## Basic formatting

- **C++ does not enforce any kind of formatting restrictions on the programmer**.
- Our basic rule of thumb is that **the best styles are the ones that produce the most readable code, and provide the most consistency**.

### Recommendations for basic formatting:

1. It’s fine to use either **tabs or spaces for indentation** (most **IDEs** have a setting where you **can convert a tab press into the appropriate number of spaces**). It ultimately comes down to **personal preference**.

2. There are **two acceptable styles for function braces**.
   - The Google C++ style guide recommends putting the opening curly brace on the same line as the statement.

   - The justification for this is that it reduces the amount of vertical whitespace (you aren’t devoting an entire line to nothing but the opening curly brace), so you can fit more code on a screen. More code on a screen makes the program easier to understand.

     ```cpp
     int main() {
     }
     ```
   - However, we prefer the common alternative, where the opening brace appears on its own line:

     ```cpp
     int main()
     {
     }

   - This enhances readability, and is less error prone since your brace pairs should always be indented at the same level. If you get a compiler error due to a brace mismatch, it’s very easy to see where.

3. Each statement within curly braces should start one tab in from the opening brace of the function it belongs to. For example:

   ```cpp
   int main()
   {
       std::cout << "Hello world!\n"; // tabbed in one tab (4 spaces)
       std::cout << "Nice to meet you.\n"; // tabbed in one tab (4 spaces)
   }
   ```

4. Lines should not be too long. 

   - Typically, 80 characters is the maximum length a line should be. 
   - If a line is going to be longer, it should be split (at a reasonable spot) into multiple lines.

   ```cpp
   int main()
   {
       std::cout << "This is a really, really, really, really, really, really, really, "
           "really long line\n"; // one extra indentation for continuation line
   
       std::cout << "This is another really, really, really, really, really, really, really, "
                    "really long line\n"; // text aligned with the previous line for continuation line
   
       std::cout << "This one is short\n";
   }
   ```

5. If a long line is split with an operator (eg. << or +), the operator should be placed at the beginning of the next line, not the end of the current line. Your lines should be no longer than 80 chars in length.

   - This helps make it clearer that subsequent lines are continuations of the previous lines, and allows you to align the operators on the left, which makes for easier reading.


   ```cpp
   std::cout << 3 + 4
       + 5 + 6
       * 7 * 8;
   ```

6. Use **whitespace** to make your code easier to read by **aligning values or comments or adding spacing between blocks of code**.

------

Harder to read:

```cpp
cost = 57;
pricePerItem = 24;
value = 5;
numberOfItems = 17;
```

Easier to read:

```cpp
cost          = 57;
pricePerItem  = 24;
value         = 5;
numberOfItems = 17;
```

------

Harder to read:

```cpp
std::cout << "Hello world!\n"; // cout lives in the iostream library
std::cout << "It is very nice to meet you!\n"; // these comments make the code hard to read
std::cout << "Yeah!\n"; // especially when lines are different lengths
```

Easier to read:

```cpp
std::cout << "Hello world!\n";                  // cout lives in the iostream library
std::cout << "It is very nice to meet you!\n";  // these comments are easier to read
std::cout << "Yeah!\n";                         // especially when all lined up
```

------

Harder to read:

```cpp
// cout lives in the iostream library
std::cout << "Hello world!\n";
// these comments make the code hard to read
std::cout << "It is very nice to meet you!\n";
// especially when all bunched together
std::cout << "Yeah!\n";
```

Easier to read:

```cpp
// cout lives in the iostream library
std::cout << "Hello world!\n";

// these comments are easier to read
std::cout << "It is very nice to meet you!\n";

// when separated by whitespace
std::cout << "Yeah!\n";
```

> If you are working in someone else’s code base, adopt their styles. It’s better to favor consistency than your preferences.