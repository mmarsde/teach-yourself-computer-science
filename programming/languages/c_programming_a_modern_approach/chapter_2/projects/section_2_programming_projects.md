## Programming Projects:

## Section 2
### Project 1
> 1. Write a program that uses `printf` to display the following picture on the screen:

              *
             *
            *
       *   *
        * *
         *

### Solution
```c++
#include <stdio.h>

int main(void) 
{
    printf("        *\n");
    printf("       *\n");
    printf("      *\n");
    printf(" *   *\n");
    printf("  * *\n");
    printf("   *\n");
    
    return 0;
}
```
___
### Project 2
> 2. Write a program that computes the volume of a sphere with a 10-meter radius, using the formula $v = 4/3 \pi r^3$. 
> Write the fraction $4/3$ as `4.0f/3.0f`. (Try writing it as `4/3`. What happens?)
>
> ___Hint:___ C doesn't have an exponentiation operator, so you'll need to multiply $r$ by itself twice to get $r^3$.

### Solution
```c++
#define PI 3.141592f
#include <stdio.h>

int main(void) {
    const float radius = 10.0f;
    const float volume = (4.0f / 3.0f) * PI * (radius * radius * radius);

    printf("The volume of a %.0f-meter sphere is %.0fm. \n", radius, volume);
    return 0;
}
```
### Answer
C resolves 4/3 to 1 rather than 1.3333 etc. This is because C applies integer division and truncates the decimal point, when both numbers are defined as whole numbers (integers).
___