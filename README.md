# README

*This project has been created as part of the 42 curriculum by ecantu-p*

# Description

The goal of this project is to recode printf() in my own ft_printf() function and in the way discover variadic functions in C.
Function prototype:
`int ft_printf(const char *, ...);`

| Program Name | libftprintf.a |
| --- | --- |
| Turn in files | Makefiles, *.h,  * / *.h, *.c, * / *.c |
| Makefile | NAME, all, clean, fclean, re |
| External functs. | malloc |
|  | free |
|  | write |
|  | va_start |
|  | va_arg |
|  | va_copy |
|  | va_end |
| Libft authorized | Yes |
| Description | Write a library that contains ft_printf(), a function that will mimic the original printft(). |

### Variadic Functions

“C allows you to define functions that you can call with a variable number of arguments. These are sometimes called variadic functions. Such functions require a fixed number of mandatory arguments, followed by a variable number of optional arguments. Each such function must have at least one mandatory argument. The types of the optional arguments can also vary. The number of optional arguments is either determined by the values of the mandatory arguments or by a special value that terminates the list of optional arguments.
The best-known examples of variadic functions in C are the standard library functions printf() and scanf(). Each of these two functions has one mandatory argument: the format string. The conversion specifiers in the format string determine the number and the types of the optional arguments.
For each mandatory argument, the function head shows an appropriate parameter, as in ordinary function declarations. These are followed in the parameter list by a comma and an ellipsis (…), which stands for the optional arguments.
Internally, variadic functions access any optional arguments through an object with the type va_list, which contains the argument information. An object of this type—also called an argument pointer—contains at least the position of one argument on the stack. The argument pointer can be advanced from one optional argument to the next, allowing a function to work through the list of optional arguments. The type va_list is defined in the header file stdarg.h.
When you write a function with a variable number of arguments, you must define an argument pointer with the type va_list in order to read the optional arguments. In the following description, the va_list object is named argptr. You can manipulate the argument pointer using four macros, which are defined in the header file stdarg.h:

void va_start(va_list argptr, lastparam);
The macro va_start initializes the argument pointer argptr with the position of the first optional argument. The macro’s second argument must be the name of the function’s last named parameter. You must call this macro before your function can use the optional arguments.

type va_arg(va_list argptr, type);
The macro va_arg expands to yield the optional argument currently referenced by argptr, and also advances argptr to reference the next argument in the list. The second argument of the macro va_arg is the type of the argument being read.

void va_end(va_list argptr);
When you have finished using an argument pointer, you should call the macro va_end. If you want to use one of the macros va_start or va_copy to reinitialize an argument pointer that you have already used, then you must call va_end first.

void va_copy(va_list dest, va_list src);
The macro va_copy initializes the argument pointer dest with the current value of src. You can then use the copy in dest to access the list of optional arguments again, starting from the position referenced by src.

va_list
Functions with variable numbers of arguments use an object of the type va_list to access their optional arguments. Such an object is commonly called an argument pointer, as it serves as a reference to a list of optional arguments.” (Prinz and Crawford, 2016)

### Requirements

- Do not implement the buffer management of the original `printf()`
- The function should handle the following conversions *(Text in italics is from the printf(3) description)*:
    - `%c` Prints a single character. *If no **l** modifier is present, the int argument is converted to an unsigned char, and the resulting character is written.*
    - `%s` Prints a string (as defined by the common C convention). *If no l modifier is present: The const char * argument is expected to be a pointer to an array of character type (pointer to a string). Characters from the array are written up to (but not including) a terminating null byte ('\0')…*
    - `%p` The void *pointer argument has to printed in hexadecimal format.*(as if by **%#x** or **%#lx**)*
    - `%d` Prints a decimal (base 10) number. *The int argument is converted to signed decimal notation. The precision, if any, gives the minimum number of digits that must appear; if the converted value requires fewer digits, it is padded on the left with zeros. The default precision is 1. When 0 is printed with an explicit precision 0, the output is empty.*
    - `%i` Prints an integer in base 10. *The int argument is converted to signed decimal notation. The precision, if any, gives the minimum number of digits that must appear; if the converted value requires fewer digits, it is padded on the left with zeros. The default precision is 1. When 0 is printed with an explicit precision 0, the output is empty.*
    - `%u` Prints a unsigned decimal (base 10) number. *The unsigned int argument is converted to unsigned octal (**o**), unsigned decimal (**u**), or unsigned hexadecimal (**x** and **X**) notation.*
    - `%x` Prints a number in hexadecimal (base 16) lowercase format. *The unsigned int argument is converted to unsigned octal (**o**), unsigned decimal (**u**), or unsigned hexadecimal (**x** and **X**) notation.*
    - `%X` Prints a number in hexadecimal (base 16) uppercase format. *The unsigned int argument is converted to unsigned octal (**o**), unsigned decimal (**u**), or unsigned hexadecimal (**x** and **X**) notation.*
    - `%%` Prints a percent sign.  *A '%' is written. No argument is converted. The complete conversion specification is '%%'.*
- Your function will be compared against the original printf().
- You must use the command ar to create your library. Using the libtool command is forbidden.
- Your libftprintf.a has to be created at the root of your repository.
- Your header file must be named ft_printf.h and must contain the prototype of
your ft_printf() function.

### Function printf

- Description
    
    The functions in the **printf**() family produce output according to a *format* as described below**. printf()** writes the output to *stdout.*
    
- Format
   Every `printf()` call contains a ***format control string*** that describes the output format. The format control string consit of:
   
   -  *Conversion specifiers:*
      - `%` plus
      - flags in the following order:
         - `-`
         - `+`
         - `' '`
         - `#`
         - `0`
      - field width 
         - an integers to specify the number of bytes to write.
      - precisions
         - an integer to specify the precision to print. This precision is based on the literal character of the conversion specifier. Each one has a different behaviour. See bonus for details
      -literal characters:
         - as described above, in our implementation case: `c`, `s`, `p`, `d`, `i`, `u`, `x`, `X`, `%`
    
    
- Return value
    
    Upon successful return, these functions return the number of characters printed (excluding the null byte used to end output to strings). ***strlen()***
    If an output error is encountered, a negative value is returned.
    
### Allowed Functions

- malloc: The **malloc**() function allocates *size* bytes and returns a pointer to the allocated memory. *The memory is not initialized*. If *size* is 0, then **malloc**() returns either NULL, or a unique pointer value that can later be successfully passed to **free**().
`void *malloc(size_t size);`
- free: The **free**() function frees the memory space pointed to by *ptr*, which must have been returned by a previous call to **malloc**(), **calloc**() or **realloc**(). Otherwise, or if *free(ptr)* has already been called before, undefined behavior occurs. If *ptr* is NULL, no operation is performed.
`void free(void *ptr);`
- write: The *write*() function shall attempt to write *nbyte* bytes from the buffer pointed to by *buf* to the file associated with the open file descriptor, *fildes*.
`ssize_t write(int *fildes***, const void ****buf***, size_t** *nbyte***);**`
- va_start:  The **va_start**() macro initializes *ap* for subsequent use by **va_arg**() and **va_end**(), and must be called first. 
The argument *last* is the name of the last argument before the variable argument list, that is, the last argument of which the calling function knows the type.
Because the address of this argument may be used in the **va_start**() macro, it should not be declared as a register variable, or as a function or an array type.
**`void va_start(va_list** *ap***,** *last***);**`
- va_arg: The **va_arg**() macro expands to an expression that has the type and value of the next argument in the call. The argument *ap* is the *va_list ap* initialized by **va_start**(). Each call to **va_arg**() modifies *ap* so that the next call returns the next argument. The argument *type* is a type name specified so that the type of a pointer to an object that has the specified type can be obtained simply by adding a * to *type*.
The first use of the **va_arg**() macro after that of the **va_start**() macro returns the argument after *last*. Successive invocations return the values of the remaining arguments.
If there is no next argument, or if *type* is not compatible with the type of the actual next argument (as promoted according to the default argument promotions), random errors will occur.
If *ap* is passed to a function that uses **va_arg(***ap***,***type***)** then the value of *ap* is undefined after the return of that function.
`*type* **va_arg(va_list** *ap***,** *type***);**`
- va_copy: The **va_copy**() macro copies the (previously initialized) variable argument list *src* to *dest*. The behavior is as if **va_start**() were applied to *dest* with the same *last* argument, followed by the same number of **va_arg**() invocations that was used to reach the current state of *src*.
An obvious implementation would have a *va_list* be a pointer to the stack frame of the variadic function. In such a setup (by far the most common) there seems nothing against an assignment 

   `va_list aq = ap;`

   Unfortunately, there are also systems that make it an array of pointers (of length 1), and there one needs

   `va_list aq;`

   `*aq = *ap;`

   Finally, on systems where arguments are passed in registers, it may be necessary for **va_start**() to allocate memory, store the arguments there, and also an indication of which argument is next, so that **va_arg**() can step through the list. Now **va_end**() can free the allocated memory again. To accommodate this situation, C99 adds a macro **va_copy**(), so that the above assignment can be replaced by

   ```c
   va_list aq;
   va_copy(aq, ap);
   ...
   va_end(aq);
   ``` 
   
   Each invocation of **va_copy**() must be matched by a corresponding invocation of **va_end**() in the same function. Some systems that do not supply **va_copy**() have **__va_copy** instead, since that was the name used in the draft proposal.

- va_end: Each invocation of **va_start**() must be matched by a corresponding invocation of **va_end**() in the same function. After the call **va_end(***ap***)** the variable *ap* is undefined. Multiple traversals of the list, each bracketed by **va_start**() and **va_end**() are possible. **va_end**() may be a macro or a function.

# Instructions

1. To evaluate this project first you must have cloned its git repository.
2. There is a Make file to build the library. The folloging rules are available to build the library:
*all*, *clean*, *fclean* and *re*.
    1. make *all*: Builds the library form 0.
    2. make *clean*: Removes the object files.
    3. make *fclean*: Removes additional to *clean* the static library file.
    4. make *re*: Runs *clean* and rebuilds the library.
    
    After building the library, verify the c files agains norminette.
    
3. Verify Norminette.
4. Comment out the main program to evaluate
5. Compile and verify with:
    1. `cc -Wall -Wextra -Werrror ft_printf.c libftprintf.a`
    

# Resources

- Deitel, Paul, and Harvey Deitel. *C How to program*. Pearson Education Limited, 2023.
- Kernighan, Brian W., and Dennis M. Ritchie. *The C programming language*. Pearson Educación, 1988.
- Prinz, Peter, and Tony Crawford. *C in a Nutshell*. " O'Reilly Media, Inc.", 2016.
- The GNU C library *(glibc)* manual. Reference manual version 2.42 [https://sourceware.org/glibc/manual/][https://sourceware.org/glibc/manual/]
- Function library manual: [https://linux.die.net/man/3/](https://linux.die.net/man/3/)
    
    https://linux.die.net/man/3/printf
    
    https://linux.die.net/man/3/malloc
    
    https://linux.die.net/man/3/write
    
    https://linux.die.net/man/3/va_start
    
- va_start examples
    
    https://www.tutorialspoint.com/c_standard_library/c_macro_va_start.htm
    

```c
#include <stdio.h>
#include <stdarg.h>
int sum(int count, ...) {
   va_list args;
   int tot = 0;
   
   // Set the va_list variable with the last fixed argument
   va_start(args, count);
   
   // Retrieve the arguments and calculate the sum
   for (int i = 0; i < count; i++) {
      tot = tot + va_arg(args, int);
   }
   
   // use the va_end to clean va_list variable
   va_end(args);
   
   return tot;
}

int main() {
   // Call the sum, with number of arguments
   printf("Sum of 3, 5, 7, 9: %d\n", sum(4, 3, 5, 7, 9));
   printf("Sum of 1, 2, 3, 4, 5: %d\n", sum(5, 1, 2, 3, 4, 5));
   return 0;
}
```

```c
#include <stdio.h>
#include <stdarg.h>
int cnt(int count, ...) {
   va_list args;
   int num_of_arg = 0;

   // Set the va_list variable with the last fixed argument
   va_start(args, count);

   // Retrieve the arguments and count the arguments
   for (int i = 0; i < count; i++) {
      num_of_arg= num_of_arg + 1;
   }    
   // use the va_end to clean va_list variable
   va_end(args);

   return num_of_arg;
}

int main() {
   // Call the sum, with number of arguments
   printf("Number of arguments: %d\n", cnt(4, 3, 5, 7, 9));
   printf("Number of arguments: %d\n", cnt(5, 1, 2, 3, 4, 5));
   return 0;
}
```

```c
#include <stdio.h>
#include <stdarg.h>
#include <stdlib.h>
#include <string.h>

char* concatenate(int count, ...) {
   va_list args;
   int length = 0;
   
   // calculate length
   va_start(args, count);
   for (int i = 0; i < count; i++) {
      length = length + strlen(va_arg(args, char*));
   }
   va_end(args);

   // Allocate memory for the result string
   char *res = (char*)malloc(length + 1);
   if (!res) {
      return NULL;
   }

   // Concatenate the strings
   // Initialize result as an empty string
   res[0] = '\0';
   va_start(args, count);
   for (int i = 0; i < count; i++) {
      strcat(res, va_arg(args, char*));
   }
   va_end(args);

   return res;
}
int main() {
   char *res = concatenate(3, "Hello, ", "tutorialspoint", "Mexico");
   if (res) {
      printf("%s\n", res);
      //free the alocated memory
      free(res);
   }
   return 0;
}
```

### Google Ai
AI was utilized to clarify the makefile instructions. Specifically why using `$(MAKE) -C 000_libft` did not linked libft library to libprintft library. It turn out it cannot be done. The way to doit was to include the *.c files at the libprintf Makefile. 

# Additional Sections

## Chosen Algorithm

After Kernighan and Ritchie, 1988:

```c
#include<stdio.h>
#include<stdarg.h>

void minprintf(char *fmt, ...)
{
  va_list ap;
  char    *p;
  char    *sval;
  int     ival;
  double  dval;
  
  va_start(ap, fmt);
  
  for(p=fmt; *p; p++)
  {
    if(*p != '%')
    {
      putchar(*p);
      continue;
    }
    switch (*++p)
    {
      case 'd':
        ival = va_arg(ap, int);
        printf("%d", ival);
        break;
      case 'f':
        dval = va_arg(ap, double);
        printf("%f", dval);
        break;
      case 's':
        for (sval = va_arg(ap, char*); *sval; sval++)
          putchar(*sval);
        break;
      default:
        putchar(*p);
        break;      
    }   
  }
  va_end(ap);
}

int main() {
  minprintf("The first value:%d, the second value:%d", 433, 344);
  printf("\n");
  minprintf("The first value:%f, the second value:%f", 5.44, 4.55);
  printf("\n");
  minprintf("The first str:%s, the second str:%s", "Start", "End");
  printf("\n");
  return 0;
}
```

## Data Structure
```c
typedef struct s_ftprintf
{
	char			*str;
	unsigned int	count;
	int				fcs_minus;
	int				fcs_plus;
	int				fcs_space;
	int				fcs_hash;
	int				fcs_zero;
	unsigned int	fcs_fw;
	int				fcs_pcs;
	unsigned int	fcs_pcs_len;
	char			fcs_conv_spc;
	signed int		ival;
	unsigned int	uval;
	unsigned int	xval;
}					t_ftprintf;
```

# Bonus

## Requirements

- Manage any combination of the follwing flags:
    - ‘-0.’  
    - The field: minimum width under all conversions
- Manage the following flags
   The character % is followed by zero or more of the following flags:
   - \#  *The value should be converted to an "alternate form". For **o** conversions, the first character of the output string is made zero (by prefixing a 0 if it was not zero already). For **x** and **X** conversions, a nonzero result has the string "0x" (or "0X" for **X** conversions) prepended to it.*
   - ‘ ‘ *(empty space) A blank should be left before a positive number (or empty string) produced by a signed conversion.*
   - \+ *A sign (+ or -) should always be placed before a number produced by a signed conversion. By default a sign is used only for negative numbers. A **+** overrides a space if both are used.*

## Theory

After *Dietel and Dietel, 2023* p503 and *glibc* 12.12 Formatted Output.

| Flag | Description | Remarks | Eval |
| --- | --- | --- | --- |
| - (minus sign) | Left-align the output within the specified field. | Not in the project scope | |
| + | Display a plus sign preceding positive values and a minus sign preceding negative values. | Evaluate these two together | |
| space | Print a space before a positive value not printed with the + flag. | Evaluate these two together | |
| # | Prefix 0x or 0X to the output value when used with the hexadecimal conversion specifiers x or X. | Only for x and X | |
| 0 (Zero) | Pad a field with leading zeros. | printf("%+09d\n", 452);  printf("%09d\n", 452);|+00000452 000000452 |

- Precision

   - ***Integers*** Indicates the minimum number of digits to be printed. If the printed value contains fewer digits than the specified precision and the precision value has a leading zero on decimal point, zeros are prefixed to the printed value until the total number of digits is equivalent in the precision value. If neither a zero nor a decimal point is present in the precision value, spaces are inserted instead. ***The default value is `1`. ***
   - ***Strings*** When precision is used with conversion specified `s`, the precision is the maximum number of characters written from the begginning of the string. 
   - ***Float points and scientific notation*** This are not part of the project scope, therefore the precision part is not implemented. Just consider that this is another case that do not follows the ***Integer*** rule.
   - ***USAGE*** to use precision, place a decimal point `.` followed by an integer representing the precision between the percent sign and the conversion specifier:

      - eg. 1:   `printf("%9.4d\n", 873);`

         |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
         |--|--|--|--|--|--|--|--|--|
         ||||||0|8|7|3|
      
         In this example, we have a filed with of 9 positions, with a precision of 4. This means that it should consider 9 positions and write 4 bytes. Because the argument only has 3, it add a fourth byte with a value of '0' or 48 in ascii.
         This means, that after the %, it needs to be check for a numeric value, that needs to be transform to an integer. Therefore `ft_isnum(char)`, then `ft_atoi(*ptr(char*))` to convert the number, the number can be bigger than a digit. 

      ---
      **There is a special case that is out of the scope of this project**
      - eg. 2: `printf("%*.*d\n", 9, 4, 873);`
         |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
         |--|--|--|--|--|--|--|--|--|
         ||||||0|8|7|3|

         This displays the same result, only that the field width and the precision are passed as wildcards. 

      ---
   - Special case with minus and precision.

      - eg. 3:   `printf("-%9.4d\n", 873);`

         |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
         |--|--|--|--|--|--|--|--|--|
         |0|8|7|3||||||
         
         This example demostrates the use of the `-` flag with the same filed with and precision on the previous examples. The *minus* flag aligns the string to the left. 
         The quantity of spaces is the same 9 and the precision is 4. 

         **This means that for the `-` flag to work, it needs a field with. Otherwise makes no sense.**
   - Precision and 0 pading. 
      Precision `.` and cero padding `0` does not work together. Is either one or the other.
      The default behaviour is as Precision. In other words, precision has precedence to cero pading. 

- Zero padding special case:`0`.
   
    In addition to precision, zero padding does not work in conjuction with `-` (minus). The default behaviour is *minus*. <u>However the compiler will NOT compile. </u>

- Minus `-` and plus `+` together. 
   There is no difference on which appears first, this means that `+-` is equal to `-+`.
   
   
   `printf("%-+9.4d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  |+|0|3|7|8|||||

   `printf("%+-9.4d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  |+|0|3|7|8|||||

## Examples:
  `printf("%9.4d\n", 873);`

   |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
   |--|--|--|--|--|--|--|--|--|
   ||||||0|8|7|3|

  `printf("%-9.4d\n", 873);`
   |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
   |--|--|--|--|--|--|--|--|--|
   |0|8|7|3||||||
  ---

  
  `printf("%9.4d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  ||||||0|3|7|8|

  `printf("%+9.4d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  |||||+|0|3|7|8|

  `printf("% 9.4d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  ||||||0|3|7|8|
  ---
  
  `printf("%-9.4d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  |0|3|7|8||||||

  `printf("%-+9.4d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  |+|0|3|7|8|||||

  `printf("%- 9.4d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  | |0|3|7|8|||||
  ---
  
  `printf("%+-9.4d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  |+|0|3|7|8|||||

  `printf("%+9.4d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  |||||+|0|3|7|8|
  ---
  
  `printf("%09.4d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  ||||||0|3|7|8|

  `printf("%+09.4d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  |||||+|0|3|7|8|

  `printf("% 09.4d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  ||||||0|3|7|8|

  ---
  `printf("%09d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  |0|0|0|0|0|0|3|7|8|

  `printf("%+09d\n", 378);`
  |*1*|*2*|*3*|*4*|*5*|*6*|*7*|*8*|*9*|
  |--|--|--|--|--|--|--|--|--|
  |+|0|0|0|0|0|3|7|8|
