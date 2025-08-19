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

---

### Project 2

> 2. Write a program that computes the volume of a sphere with a 10-meter radius, using the formula $v = 4/3 \pi r^3$.
>    Write the fraction $4/3$ as `4.0f/3.0f`. (Try writing it as `4/3`. What happens?)
>
> **_Hint:_** C doesn't have an exponentiation operator, so you'll need to multiply $r$ by itself twice to get $r^3$.

### Solution

```c++
#define PI 3.141592f
#include <stdio.h>

int main(void)
{
    const float radius = 10.0f;
    const float volume = (4.0f / 3.0f) * PI * (radius * radius * radius);

    printf("The volume of a %.0f-meter sphere is %.0fm. \n", radius, volume);

    return 0;
}
```

### Answer

C resolves $4/3$ to 1 rather than 1.3333 etc. This is because C applies integer division and truncates the decimal point, when both numbers are defined as whole numbers (integers).

---

### Project 3

> 3. Modify the program of Programming Project 2 so that it prompts the user to enter the radius of the sphere.

### Solution

```c++
#define PI 3.141592f
#include <stdio.h>

int main(void)
{
    float radius;

    printf("Enter radius: ");
    scanf("%f", &radius);

    const float volume = (4.0f / 3.0f) * PI * (radius * radius * radius);

    printf("The volume of a %.0f-meter sphere is %.0fm. \n", radius, volume);

    return 0;
}
```

> [!Note]
> The **input** isn't validated at this point. The user could enter anything (including strings), which would result in `undefined` behavior. This will be addressed in later projects.

---

### Project 4

> 4. Write a program that asks the user to enter a dollars-and-cents amount, then displays the amount with 5% tax added: <br> > `Enter an amount: 100.00` <br> > `With tax added: $105.00`

### Solution

```c++
#include <stdio.h>

int main(void)
{
    float amount, taxRate = 0.05f;

    printf("Enter an amount: ");
    scanf("%f", &amount);

    printf("With tax added: $%.2f.\n", (amount + (amount * taxRate)));

    return 0;
}
```

---

### Project 5

> 5. Write a program that asks the user to enter a value for $x$ and then displays the value of the polynomial: <br> > $3x^5 + 2x^4 - 5x^3 -x^2 + 7x - 6$
>
> **_Hint:_** C doesn't have an exponentiation operator, so you'll need to multiply $x$ by itself repeatedly in order to compute the power of $x$.

### Solution

```c++
#include <stdio.h>

int main(void)
{
    int x;

    printf("Enter the value of x: ");
    scanf("%d", &x);

    int pValue = 3 * (x * x * x * x * x) + 2 * (x * x * x * x ) - 5 * (x * x * x ) - (x * x) + 7 * x - 6;

    printf("The value of the polynomial is %d.\n", pValue);

    return 0;
}
```

---

### Project 6

> 6. Modify the program of Programming Project 5, so the polynomial is evaluated using the following formula: <br> > $((((3x+2)x - 5)x - 1) x + 7)x - 6$
>
> Note that the modified program does fewer multiplications. This technique for evaluation polynomials is known as **_Horner's rule_**.

### Solution

```c++
#include <stdio.h>

int main(void)
{
    int x;

    printf("Enter the value of x: ");
    scanf("%d", &x);

    int pValue = ((((3 * x + 2) * x - 5) * x - 1) * x + 7) * x - 6;

    printf("The value of the polynomial is %d.\n", pValue);

    return 0;
}
```

---

### Project 7

> 7. Write a program that asks the user to enter a US dollar amount and shows them how to pay that amount using the smallest number of $20, £10, $5 and $1 bills: <br> > `Enter a dollar amount: 93` <br> > `$20 bills: 4` <br> > `$10 bills: 1` <br> > `$5 bills: 0` <br> > `$1 bills: 3`
>
> **_Hint_**: Divide the amount by 20 to determine the number of $20 bills needed, and then reduce the amount by the total of the $20 bills. Repeat with the other bill sizes. Be sure to use integers values throughout, not floating-point numbers.

### Solution

```c++
#include <stdio.h>

int dispense(int *dollarAmount, int billValue)
{
    int numberOfBills = *dollarAmount / billValue;
    *dollarAmount -= (numberOfBills * billValue);

    return numberOfBills;
}

int main(void)
{
    int dollarAmount;
    printf("Enter the dollar amount: ");
    scanf("%d", &dollarAmount);

    int numberOfTwentyBills = dispense(&dollarAmount, 20);
    printf("$%d bills: %d \n", 20, numberOfTwentyBills);

    int numberOfTenBills = dispense(&dollarAmount, 10);
    printf("$%d bills: %d \n", 10, numberOfTenBills);

    int numberOfFiveBills = dispense(&dollarAmount, 5);
    printf("$%d bills: %d \n", 5, numberOfFiveBills);

    printf("$1 bills: %d \n" , dollarAmount);

    return 0;
}
```

> [!Note]
> The above program implementation uses more advanced concepts, including `pointers` and `functions`. This is not explicitly covered in the C fundmentals chapter.

---

### Project 8

> 8. Write a program that calculates the remaining balance on a loan, after the first, second and third monthly repayments. <br> <br>
> `Enter the amount of the loan: 20000` <br>
> `Enter the interest rate: 6.0` <br>
> `Enter monthly repayment: 386.66` <br> <br>
> `Balance remaining after first payment: $19713.34` <br>
> `Balance remaining after second payment: $19425.25` <br>
> `Balance remaining after third payment: $19135.71` <br> <br>
> Display each balance with two digits after the decimal point. _Hint_: Each month the balance is decreased by the amount of the payment, but increased by the balance times the monthly interest rate. To find the monthly interest rate, convert the interest rate to a percentage and divide it by 12.

### Solution

```c++
#include <stdio.h>

void calculateBalance (float *loanAmount, float repaymentAmount, float monthlyRate)
{
    float interest = *loanAmount * monthlyRate;
    *loanAmount -= repaymentAmount;
    *loanAmount += interest;
}

int main(void)
{
    float loanAmount, interestRate, repaymentAmount;
    printf("Enter loanAmount: ");
    scanf("%f", &loanAmount);

    printf("Enter interestRate: ");
    scanf("%f", &interestRate);

    printf("Enter repaymentAmount: ");
    scanf("%f", &repaymentAmount);

    float monthlyRate = (interestRate / 100) / 12;
    calculateBalance(&loanAmount, repaymentAmount, monthlyRate);
    printf("Balance remaining after first payment: : $%.2f\n", loanAmount);

    calculateBalance(&loanAmount, repaymentAmount, monthlyRate);
    printf("Balance remaining after second payment: : $%.2f\n", loanAmount);

    calculateBalance(&loanAmount, repaymentAmount, monthlyRate);
    printf("Balance remaining after third payment: : $%.2f\n", loanAmount);

    return 0;
}
```

> [!Note]
> The above program implementation uses more advanced concepts, including `pointers` and `functions`. This is not explicitly covered in the C fundmentals chapter.

---
