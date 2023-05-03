Download Link: https://assignmentchef.com/product/solved-cs2211a-lab-no-9-introduction-to-c
<br>
The objective of this lab is to practice:  o <strong>C Preprocessor </strong>o <strong>Makefile </strong>

If you would like to leave, and at least 30 minutes have passed, raise your hand and wait for the TA.

Show the TA what you did. If, and only if, you did a reasonable effort during the lab, he/she will give you the lab mark.

<strong>========================================================================== </strong>

<strong><em>In this lab, you should decide on the correct responses before running the code to test the real result. </em></strong>

<ol>

 <li>Write parameterized macros that compute the following values.

  <ul>

   <li>The cube of x.</li>

   <li>The remainder when n is divided by 4.</li>

   <li>1 if the product of x and y is less than 100, 0</li>

   <li>The number of elements in a one-dimensional array (see the discussion of the sizeof operator in Section 8.1) <em>Write a program to test these macros. </em>Do your macros always work? If not, describe what arguments would make them fail.</li>

  </ul></li>

</ol>




Hint: What will happen if the provided argument(s) have side effect?

<ol start="2">

 <li>Show what the following program will look like after preprocessing. You may <strong>ignore</strong> any lines added to the program as a result of including the &lt; h&gt; header. What will be the output of this program?</li>

</ol>




#include &lt;stdio.h&gt;

#define N 100




void f(void);




int main(void)

{   f(); # ifdef N

#  undef N   #   endif   return 0;

}




void f(void)

{

#if defined(N)

printf(“N is %d
”, N);

#else

printf(“N is undefined
”);

#endif

}




<ol start="3">

 <li>Let TOUPPER be the following macro:</li>

</ol>

#define TOUPPER(c) (‘a’ &lt;= (c) &amp;&amp; (c) &lt;= ‘z’? (c) – ‘a’ + ‘A’: (c))

Let s be a string and let i be an int variable.

Show the output produced by each of the following program fragments.

<ul>

 <li>strcpy(s, “abcde”); i=0;</li>

</ul>

putchar(TOUPPER(s[++i]));     putchar(‘
’);




<ul>

 <li>strcpy(s, “01234”); i=0;</li>

</ul>

putchar(TOUPPER(s[++i]));     putchar(‘
’);

Did you get the results that you expected? If not, explain why?

<ol start="4">

 <li>C compilers usually provide some method of specifying the value of a macro at the time a program is compiled. This ability makes it easy to change the value of a macro without editing any of the program’s files. Most compilers (including gcc) support the -D option, which allows the value of a macro to be specified on the command line, i.e., <em>defines</em> a macro as if by using #define. Many compilers also support the -U option, which <em>undefines</em> a macro as if by using #undef.</li>

</ol>

Type the following program:




#include &lt;stdio.h&gt;




#ifdef DEBUG

#define PRINT_DEBUG(n) printf(“Value of ” #n “: %d
”, n)

#else

#define PRINT_DEBUG(n)

#endif

int main(void)

{

int i = 1, j = 2, k = 3;




#ifdef DEBUG

printf(“DEBUG is defined:
”);

#else

printf(“DEBUG is not defined:
”);

#endif




PRINT_DEBUG(i);

PRINT_DEBUG(j);

PRINT_DEBUG(k);

PRINT_DEBUG(i + j); PRINT_DEBUG(2 * i + j – k); return 0;

}

<ul>

 <li>Compile and the run this program without using any option during compilation</li>

 <li>Compile and the run this program using the following options during compilation:

  <ol>

   <li>-DDEBUG=1</li>

   <li>–DDEBUG</li>

  </ol></li>

</ul>

<ul>

 <li>-Ddebug=1 iv. –Ddebug</li>

</ul>

What are the differences between the five runs? Why?







<ol start="5">

 <li>The following are two C programs (<strong>addition.c</strong> and <strong>add_fun.c</strong>) and one header file (<strong>add_fun.h</strong>).</li>

</ol>




<strong><u>addition.c</u></strong> #include &lt;stdio.h&gt;

#include &lt;stdlib.h&gt;

#include “add_fun.h”




int main(int argc, char *argv[])

{

int operand1, operand2, result;




// check to make sure that we have the correct number or arguments     if(argc != 3)

{ // print an error message and exit

printf(“Usage: %s operand1 operand2
”, argv[0]);

// return with  unsuccessful status       return 1;

}




// convert the arguments from array of characters to integer     operand1 = atoi(argv[1]);     operand2 = atoi(argv[2]);




// perform the addition operation     result = add(operand1, operand2);




// print the result

printf(”       Result = %d

”, result);




// return with a successful status     return 0;

}

<strong><u>add_fun.c</u></strong>

#include “add_fun.h”




int add(int op1, int op2)

{

int sum;




sum = op1 + op2;




return sum;

}

<strong><u>add_fun.h</u></strong>

int add(int op1, int op2);










To automatically  build and test these C programs, you need to have a <strong>makefile</strong>.   The following is a suggested <strong>makefile</strong>.










<strong><u>makefile</u></strong>

#format is target-name: target dependencies

#{-tab-}actions




# MACRO definitions

CC  = gcc

CFLAG = -std=c99 -Wall




# All Targets all: addition




#Executable addition depends on the files addition.o add_fun.o addition: addition.o add_fun.o

$(CC) $(CFLAG) -o addition addition.o add_fun.o




# addition.o depends on the source and header files

addition.o: addition.c add_fun.h     $(CC) $(CFLAG) -c addition.c




# add_fun.o depends on the source and header files

add_fun.o: add_fun.c add_fun.h     $(CC) $(CFLAG) -c add_fun.c




# test cases test: addition     addition 1 2     addition 6 7     addition 11 2




#Clean the build directory clean:

rm -f *.o addition




download all these 4 files and do the following experimentations

<strong><em>(you should expect he answer before executing the command)</em></strong>:

<ul>

 <li>make</li>

 <li>make clean</li>

 <li>make all</li>

 <li>make all</li>

 <li>make clean</li>

 <li>make addition</li>

 <li>make addition</li>

 <li>rm addition.o</li>

 <li>make</li>

 <li>rm add_fun.o</li>

 <li>make</li>

 <li>touch addition.h</li>

 <li>make</li>

 <li>touch add_fun.c</li>

 <li>make</li>

 <li>touch add_fun.h</li>

 <li>make</li>

 <li>make test</li>

 <li>make clean</li>

 <li>make test</li>

</ul>