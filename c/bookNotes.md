<details open>
<summary><h1>Basics</h1></summary>

[The C Programming Language Book](https://seriouscomputerist.atariverse.com/media/pdf/book/C%20Programming%20Language%20-%202nd%20Edition%20(OCR).pdf)

Compile with the command cc hello.c 

Run with a.out 

```C
#include <stdio.h>
main()
{
	int fahr, celsius;
	int lower, upper, step;
	lower = 0; /* lower limit of temperature scale */
	upper = 300; /* upper limit */
	step = 20; /* step size */
	fahr = lower;
	printf("%s %s\n", Fahr, Celsius);
	while (fahr <= upper)
	{
		celsius = (5.0/9.0) * (fahr-32.0);
 		printf("%3.0f %6.1f\n", fahr, celsius);
 		fahr = fahr + step;
	}
}
```
OR
```C
#include <stdio.h>

#define LOWER 0 /* lower limit of table */
#define UPPER 300 /* upper limit */
#define STEP 20 /* step size */ 

main()
{
	int fahr;
	for (fahr = LOWER; fahr <= UPPER; fahr = fahr + STEP)
	{
 		printf("%3d %6.1f\n", fahr, (5.0/9.0)*(fahr-32));
	}
}
```

### Extern

An external variable must be defined, exactly once, outside of any function; this sets aside
storage for it.

The variable must also be declared in each function that wants to access it; this
states the type of the variable. The declaration may be an explicit extern statement or may be implicit from context.

## Arrays 

```C
int ndigit[10];
```

### Char arrays

```C
#include <stdio.h>
#define MAXLINE 1000 /* maximum input line length */

int getline(char line[], int maxline); //Supplying the size of an array is to set aside storage
void copy(char to[], char from[]);

/* print the longest input line */
main()
{
 	int len; /* current line length */
 	int max; /* maximum length seen so far */
 	char line[MAXLINE]; /* current input line */
 	char longest[MAXLINE]; /* longest line saved here */
 	max = 0;
 	while ((len = getline(line, MAXLINE)) > 0)
	{
 		if (len > max)
		{
 			max = len;
			copy(longest, line);
		}
	}
	if (max > 0) /* there was a line */
	{
		printf("%s", longest);
	}
 	return 0;
 }

/* getline: read a line into s, return length */
int getline(char s[],int lim)
{
 	int c, i;
 	for (i=0; i < lim-1 && (c=getchar())!=EOF && c!='\n'; ++i)
	{
 		s[i] = c;
	}
 	if (c == '\n')
	{
 		s[i] = c;
 		++i;
 	}
	s[i] = '\0';
 	return i;
} 

/* copy: copy 'from' into 'to'; assume to is big enough */
void copy(char to[], char from[])
{
	int i;
 	i = 0;
 	while ((to[i] = from[i]) != '\0')
	{
 		++i;
	}
 }
```

## Functions 

Definition:
```C
return-type function-name(parameter declarations, if any)
{
 	declarations
 	statements
} 
```

Example:
```C
#include <stdio.h>
int power(int m, int n); //forward declare

main()
{
	int i;
	for (i = 0; i < 10; ++i)
	{
 		printf("%d %d %d\n", i, power(2,i), power(-3,i));
	}
 	return 0;
}
/* power: raise base to n-th power; n >= 0 */
int power(int base, int n)
{
 	int p;
	for (p = 1; n > 0; --n)
	{
		p = p * base;
	}
	return p;
}
```

parameter names are optional in a function prototype:

```C
int power(int, int);
int power(); //old style, avoid
```

Typically, a return value of zero implies normal
termination; non-zero values signal unusual or erroneous termination conditions.

## String literals (printf)

* %d print as decimal integer
* %6d print as decimal integer, at least 6 characters wide
* %f print as floating point
* %6f print as floating point, at least 6 characters wide
* %.2f print as floating point, 2 characters after decimal point
* %6.2f print as floating point, at least 6 wide and 2 after decimal point 
* %o for octal
* %x for hexadecimal
* %c for character
* %s for character string
* %% for itself

## Char input output

```C
#include <stdio.h>
 /* copy input to output; 1st version */
 main()
 {
 int c;
 c = getchar();
//while ((c = getchar()) != EOF) 
	while (c != EOF) {
		putchar(c);
		c = getchar();
	}
}
```
</details>

<details open>
<summary><h1>Types, Operators and Expressions</h1>h1> </summary>

Names are made up of letters and digits; the first character must be a
letter. The underscore ``_'' counts as a letter

Traditional C practice is to use lower case for variable names, and
all upper case for symbolic constants. 

## Data types

There are only a few basic data types in C:

- **char** – a single byte, capable of holding one character in the local character set  
- **int** – an integer, typically reflecting the natural size of integers on the host machine (usually 16 or 32 bits)  
- **float** – single-precision floating point  
  - suffixes **f** or **F** indicate a float constant  
- **double** – double-precision floating point  

The size of these objects is machine-dependent. There are also arrays, structures and
unions of these basic types, pointers to them, and functions that return them.

Integer division truncates: any fractional part is discarded. 5/9 would be truncated to zero

### Type Qualifiers

A number of qualifiers can be applied to these basic types.

**short** and **long** apply to integers:

- `short int sh;`
- `long int counter;`

Suffixes **l** or **L** indicate a long constant.  
The word `int` can be omitted in such declarations, and typically it is:

- `short sh;`
- `long counter;`

### Signed and Unsigned

The qualifiers **signed** or **unsigned** may be applied to `char` or any integer type:

- `signed int sh;`
- `unsigned int counter;`

Suffixes **u** or **U** indicate an unsigned constant.

### Integer Constants

The value of an integer can be specified in octal or hexadecimal:

- A leading **0** (zero) on an integer constant means **octal**
- A leading **0x** or **0X** means **hexadecimal**

### Character constants

| Escape Sequence | Meaning                     |
|-----------------|-----------------------------|
| \a              | alert (bell) character      |
| \b              | backspace                   |
| \f              | formfeed                    |
| \n              | newline                     |
| \r              | carriage return             |
| \t              | horizontal tab              |
| \v              | vertical tab                |
| \\              | backslash                   |
| \?              | question mark               |
| \'              | single quote                |
| \"              | double quote                |
| \ooo            | octal number                |
| \xhh            | hexadecimal number          |


</details>
