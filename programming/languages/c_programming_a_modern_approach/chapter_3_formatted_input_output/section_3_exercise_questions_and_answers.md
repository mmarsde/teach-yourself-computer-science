## Exercises:
## Section 3
### Exercise 1 - Section 3.1
> What output do the following calls to `printf` produce?
> 1. `printf("%6d,%4d", 86, 1040);`
> 2. `printf("%12.5e", 30.253);`
> 3. `printf("%.4f", 83.162);`
> 4. `printf("%-6.2g", .0000009979);`

### Answer
> ___NOTE___: Format strings adhere to the following conversion format: `%m.pX` or `%-m.pX`  
> 1. m = minimum field width 
> 2. p = precision 
> 3. X = conversion specifier
> 4. If there is a '-' (minus) before the 'm' specifier, white space is added to the right of the format string to fill any unused placeholder values, resulting in a left justified format string.

1. `printf("%6d,%4d", 86, 1040);` prints the following output (note `#` represents whitespace):
   1. `####86,1040`. Both integers are printed in decimal format in the format string, as denoted by the `d` for the conversion (`X`) specifier. 
   2. The first `m` specifier requires 6 placeholder values in total, for the first input number. Because the first number only contains 2 digits, the remaining 4 placeholders are padded with white space to the left (i.e. the resulting number is right justified).
   3. The second `m` specifier requires 4 placeholder values in total, for the second input number. Because the second number already contains 4 digits, no additional whitespace is added.
2. `printf("%12.5e", 30.253);` prints the following output (note `#` represents whitespace):
   1. `#3.02530e+01`
   2. The input float number is printed using exponential notation in the format string, as denoted by the `e` for the conversion (`X`) specifier.
   3. The `m` specifier requires 12 placeholder values in total.
   4. The `p` specifier requires 5 placeholder values after the decimal point.
   5. Because the output value results in 11 occupied placeholder values, the remaining placeholder value is padded with a single whitespace to the left. (i.e. the resulting number is right justified)
3. `printf("%.4f", 83.162);` prints the following output:
   1. `83.1620`
   2. The input float value is printed in float format in the format string, as denoted by the `f` for the conversion (`X`) specifier.
   3. The `p` specifier requires 4 placeholder values after the decimal point.
   4. Because the input value only supplies 3 values after the decimal point, an additional zero is added to fill the remaining placeholder value.
4. `printf("%-6.2g", .0000009979);` prints the following output (note `#` represents whitespace):
   1. `1e-06#`
   2. The float input is printed using exponential format, as denoted by the `g` for the conversion (`X`) specifier.
   3. `g` conversion specifiers are typically used when the size of the input is not known at runtime (so can print in either decimal or exponential format).
   4. The format string requires a total field width (`m`) of 6, a precision (`p`) of 2 places after the decimal point and any unused placeholder values should be filled with whitespace to the right. (i.e. the resulting number is left justified).
   5. Because the resulting output only filled 5 of the required placeholders, the remaining placeholder was padded with whitespace to the right.

___

### Exercise 2 - Section 3.1

> Write calls to `printf` that display a `float` variable `x` in the following formats.
> 1. Exponential notation; left-justified in a field size of 8; one digit after the decimal point. 
> 2. Exponential notation; right-justified in a field size of 10; six digits after the decimal point.
> 3. Fixed decimal notation; left-justified in a field size of 8; three digits after the decimal point.
> 4. Fixed decimal notation; right-justified in a field size of 6; zero digits after the decimal point.

### Answer
```c++
#include <stdio.h>

int main(void) {
    const float x = 12.2;

    // Exponential notation; left-justified in a field size of 8; one digit after the decimal point.
    printf("%-8.1e\n", x);
    // output: "1.2e+01 "

    // Exponential notation; right-justified in a field size of 10; six digits after the decimal point.
    printf("%10.6e\n", 30.253);
    // output: "1.220000e+01"

    // Fixed decimal notation; left-justified in a field size of 8; three digits after the decimal point.
    printf("%-8.3f\n", x);
    // output: "12.200  "

    // Fixed decimal notation; right-justified in a field size of 6; no digits after the decimal point.
    printf("%6.0f\n", x);
    // output: "    12"

    return 0;
}
```
___

### Exercise 3 - Section 3.2
> For each of the following pairs of `scanf` format strings, indicate whether or not the two strings are equivalent. If they're not, show how they can be distinguished.
> 1. `"%d"` versus `"%d "`
> 2. `"%d-%d-%d"` versus `"%d -%d -%d"`
> 3. `"%f` versus `"%f "`
> 4. `"%f,%f"` versus `"%f, %f"`

### Answer
 1. `"d%"` and `"d% "` are __not__ equivalent. For `"d%"`, `scanf` stores the first `integer` input it finds to an output variable e.g. `&value`  and immediately terminates, (provided it meets the `conversion specifier` requirements). By constrast, with `"d% "`,`scanf` will store the first `integer` input it finds into a named variable e.g. `&value` (provided it meets the `conversion specifier` requirements), places any "whitespace" characters (spaces, newline characters, tabs etc) it encounters back onto the input buffer (which is excluded/ignored from further processing) and continues to scan until it finds the next non whitespace character, before terminating.
 2. `"%d-%d-%d"` and `"%d -%d -%d"` produce equivalent output. The only difference with `"%d -%d -%d"` is that whitespace is effectively ignored/placed back onto the input buffer.
 3. `"f%"` and `"f% "` are __not__ equivalent. For `"f%"`, `scanf` stores the first `float` input it finds to an output variable e.g. `&value`  and immediately terminates, (provided it meets the `conversion specifier` requirements). By constrast, with `"f% "`,`scanf` will store the first `float` input it finds into a named variable e.g. `&value` (provided it meets the `conversion specifier` requirements), places any "whitespace" characters (spaces, newline characters, tabs etc) it encounters back onto the input buffer (which is excluded/ignored from further processing) and continues to scan until it finds the next non whitespace character, before terminating.
 4. `"%f,%f"` and `"%f, %f"` produce equivalent output. The only difference with `"%f, %f"`  is that whitespace is effectively ignored/placed back onto the input buffer.

 ### Exercise 4 - Section 3.2
 > Suppose we call `scanf` as follows:
 >
 > `scanf("%d%f%d", &i, &x, &j);`
 >
 > If the user enters
 >
 > `10.3 5 6`
 >
 > what will be the values of `i`, `x` and `j`? (Assume that `i` and `j` are `int` variables and `x` is a `float` variable.) 

### Answer

```c++
#include <stdio.h>

int main(void) 
{    
    int i, j;
    float x;

    scanf("%d%f%d", &i, &x, &j);
    //input: 10.3 5 6

    printf("%d%f%d\n", i, x, j);
    //Output: 10 0.300000 5

    return 0;
}
```

### Explanation:

`scanf` attempts to map the first input sequence to an `int` variable (`i`), but it encounters `10.3`. `10` is mapped to `i` and `.3` is placed back onto the input buffer for further processing. `scanf` attempts to map the next input sequence to the float variable (`x`), which is `.3`. This is mapped as `0.300000` (padded out to 6 decimal places, as is the default behavior). `scanf` skips any whitespace and attempts to map the next input sequence to the final `int` variable (`j`). `5` is mapped to `j` and `scanf` terminates at the next non-whitespace character, which is `6`.  

### Exercise 5 - Section 3.2
> Suppose we call `scanf` as follows:
>
> `scanf("%f%d%f", &x, &i, &y);`
>
> if the user enters:
>
> `12.3 45.6 789`
> 
> what will be the values of `x`, `i`, and `y` after the call? (Assume that `x` and `y` are `float` variables and `i` is an `int` variable.)

### Answer

```c++
#include <stdio.h>

int main(void) 
{    
    float x, y;
    int i;

    scanf("%f%d%f", &x, &i, &y);
    //input: 12.3 45.6 789
    
    printf("%f %d %f", x, i, y);
    //output: 12.300000 45 0.600000

    return 0;
}
```

### Explanation:

`scanf` maps the first input sequence `12.3` to the `float` variable `x`, but pads the floating point out to 6 decimal places (as per the default behavior in the absence of a `precision` specifier). `scanf` attempts to map the next input sequence to the `int` variable `i`, but encounters `45.6`. `45` is mapped to `i` and `.6` is placed back onto the input buffer for further processing. `scanf` attempts to map the next input sequence to the final `float` variable `y`. `.6` is mapped as `0.600000` (padded with 6 decimal places as per the default behavior) to `y` and `scanf` continues to scan until it terminates at the next sequence of non-whitespace characters, which is `789`.

### Exercise 6 - Section 3.2
> Show how to modify the `addfrac.c` of Section 3.2 so that the user is allowed to enter fractions that contain spaces before and after each `/` character.

### Answer

```c++
/* Adds two fractions, but doesn't reduce to the lowest terms. */
#include <stdio.h>

int main(void)
{
    int num1, denom1, num2, denom2, result_num, result_denom;

    printf("Enter the first fraction: ");
    fflush(stdout); // keeps user input on the same line
    scanf("%d / %d", &num1, &denom1);

    printf("Enter the second fraction: ");
    fflush(stdout); // keeps user input on the same line
    scanf("%d / %d", &num2, &denom2);

    result_num = num1 * denom2 + num2 * denom1;
    result_denom = denom1 * denom2;

    printf("The sum is: %d/%d\n", result_num, result_denom);

    return 0;
}

```
Spaces are added as part of the format string in the `scanf` calls, before and after the `/` characters.
> Output:
> 
> Enter the first fraction: 1 / 2 <br>
> Enter the second fraction: 1 / 6 <br>
> The sum is: 8/12