## Exercises:
## Section 2
### Question 1 - Section 2.1
### Create and run Kernighan and Richie's famous "hello, world" program:
```c++
#include <stdio.h>

int main(void) 
{
    printf("hello, world\n");
} 
```
### Do you get a warning message from the compiler? If so, what's needed to make it go away?

### Answer
   - Whether you get a warning message depends on your compiler settings. If you are using the `C89` standard, in combination
   with the GCC compiler argument `-Wall` (causes the compiler to raise a warning message if it detects possible errors), you'll get the following compiler __warning__ message: ` warning: control reaches end of non-void function [-Wreturn-type]`.
   This is because the `main` function expects a return type of `int` to determine whether it's reached the end of the function call.
   - To fix the compiler warning, include the following statement ___after___ `printf("hello, world\n");`. This will cause the program to terminate successfully:
     - `return 0;`
   - Compiler command with the `-Wall` argument specified: `gcc  -Wall -std=c89 -o hello_world.o hello_world.c`
____     
### Question 2 - Section 2.2
### Consider the following program:
```c++
#include <stdio.h>

int main(void) 
{
    printf("Parkinson's Law:\nWork expands to ");
    printf("fill the time\n");
    printf("available for it's completion\n");
    return 0;
} 
```
### a) Identify the directives and statements in this program.
### Answer 
   - There are ___four statements___ in this program (all terminated by a semicolon). The first 3 statements calls the `printf` 
   function from the standard IO library `<stdio.h>` to print a series of formatted string literals to the terminal. The 
   last statement returns the integer value `0` to the operating system, terminating the program and indicating successful
   execution.
   The statements are as follows:
     - `printf("Parkinson's Law:\nWork expands to ");`
     - `printf("fill the time\n");`
     - `printf("available for it's completion\n");`
     - `return 0;`
   - There is ___one  directive___ in this program. Directives are used by the preprocessor to copy dependencies into the `main` program
   (such as code from the standard and/or custom libraries or translations of computed values), prior to compilation. 
   They are prefixed with `#` and declared at the top of the program. The directive included in this program is:
     - `#include <stdio.h>`


### b) What output does the program produce?
### Answer
   - Upon execution, the following output is produced: <br>
`Parkinson's Law:` <br>
`Work expands to fill the time` <br>
`vailable for it's completion` <br>
<br>

`Process finished with exit code 0`

   - The first statement prints the string literal `"Parkinson's Law:"` followed by a new line `\n`. This moves the cursor
   to a new line in the terminal, before printing the next string literal `"Work expands to "`. The proceeding statements
   print the remaining string literals followed by a new line.
   
____

### Question 3 - Section 2.4
### Condense the `dweight.c` program by:
#### 1. Replacing the assignments to `height`, `length`, and `width` with initializers.
#### 2. Removing the `weight` variable, instead calculating `(volume + 165) / 166` within the last `printf` statement.
### Answer

```c++
#include <stdio.h>

int main(void)  
{
    //variable declarations and initializers
    int height = 8, length = 12, width = 10, volume = height * length * width;

    printf("Dimensions: %dx%dx%d\n", height, length, width);
    printf("Volume (cubic inches): %d\n", volume);
    printf("Dimensional weight (pounds): %d\n", (volume + 165) / 166 );

    return 0; 
}
```
> **_NOTE:_**
> Although not explicitly requested in the question, `volume` can also be declared with an initializer.
___
### Question 4 - Section 2.4
### Write a program that declares several `int` and `float` variables, without initializing them and print their values. Is there a pattern to them? (usually there isn't.)
### Answer - `variables.c`

```c++
#include <stdio.h>
int main(void) {
    int a, b, c, d;
    float e, f, g, h;

    printf("Uninitialized integer variables: %d,%d,%d,%d\n", a, b, c, d);
    printf("Uninitialized float variables: %f,%f,%f,%f\n", e, f, g, h);

    return 0;
}
```
- The return values for the integer variables (when uninitialized) are typically random. Example output `32543,-1410159648,0,0`. The values are considered to be `indeterminate`, because C does not automatically assign `0` to local variables. Whatever bits happen to be in the memory location being accessed, is what gets returned in the `printf` statement at runtime. 
- The return values for the float variables (when uninitialized) are typically random, for the same reason mentioned above. 
___
### Question 5 - Section 2.7
### Which of the following are not legal C identifiers?
#### a) 100_bottles
#### b) _100_bottles
#### c) one_hundred_bottles
#### d) bottles_by_the_hundred_
### Answer 
- `_100_bottles`, `one_hundred_bottles`, `bottles_by_the_hundred_` are all considered valid `C identifiers`, because they satisfy the following requirements:
  - They either begin with an alphanumeric character or an underscore `_`.
- `100_bottles` is considered an invalid `C identifier`, because it begins with a digit. 
___
### Question 6 - Section 2.7
### Why is it not a good idea for an identifier to contain more than one adjacent underscore (as in current__balance for example)?
### Answer
- Identifiers containing double underscores **could potentially** cause conflicts with reserved identifiers used in the C standard library. It is not considered good practice.
- `7.1.3 Reserved identifiers - All identifiers that begin with an underscore and either an uppercase letter or another underscore are always reserved for any use. ISO 9899:2011 §7.1.3 ¶1 #1`
___
### Question 7 - Section 2.7
### Which of the following are keywords in C?
#### a) `for`
#### b) `If`
#### c) `main`
#### d) `printf`
#### e) `while`
### Answer
`for` and `while` are recognised as keywords by the C compiler and cannot be used for naming identifiers.
`printf` and `main` are ___function identifiers___ recognised by the C standard, but are not language ___keywords___.
`If` is not recognised as a reserved keyword by the compiler, because C is a case-sensitive language. By contrast, `if` (all in lowercase) is considered a valid C keyword.
___
### Question 8 - Section 2.8
### How many tokens are there in the following statement? 
#### `answer=(3*q-p*p)/3;`
### Answer
There are 14 tokens in the statement, comprising variables (`answer`, `q`, `p`), operators (`=`, `()`, `*` `-` and `/`), operands (`3`) and punctuation (`;`).
Tokens can be separated by white space for readability, provided it doesn't change the semantics of the statement.
___
### Question 9 - Section 2.8
### Insert spaces between the tokens in Exercise 8 to make the statement easier to read.
### Answer
`answer = ( 3*q - p*p ) / 3;`
___
### Question 10 - Section 2.8
### In the `dweight.c` program (Section 2.4), which spaces are essential?
### Answer
The essential spaces in the `dweight.c` program are the ones separating the reserved keywords, so the compiler can distinguish them.
Removing the spaces between keywords, would alter their semantics, meaning the compiler would not recognise them.
- `int height;` and other variable declarations etc.
- `return 0;`
___
