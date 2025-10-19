## Programming Projects:

## Section 3

### Project 1
> 1. Write a program that accepts a date from the user in the form `mm/dd/yyyy` and then displays it in the form `yyyymmdd` : <br>
> `Enter a date (mm/dd/yyyy): 2/17/2011` <br>
> `You entered the date 20110217`

### Solution

```c++
#include <stdio.h>

int main(void)
{
    int day, month, year;

    printf("Enter a date (mm/dd/yyyy): ");
    fflush(stdout);
    
    scanf("%02d/%02d/%4d", &day, &month, &year);

    printf("You entered the date %4d%02d%02d\n", year, month, day);

    return 0;
}
```
> Output: <br>
> Enter a date (mm/dd/yyyy): 12/9/1989 <br>
> You entered the date 19890912 <br>