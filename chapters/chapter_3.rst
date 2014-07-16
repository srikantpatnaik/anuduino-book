Arduino Programming Language
============================

Variables
---------

As the name suggests, variable is an entity that may vary during
program execution. Variable names are names given to locations in
memory. These locations can contain integer , real or character
constants. The rules for constructing variable names of all types
are the same. These rules are given below.

Rules for Constructing Variable Names
(a) A variable name is any combination of 1 to 31 alphabets,
digits or underscores. Some compilers allow variable names
whose length could be up to 247 characters. Still, it would be
safer to stick to the rule of 31 characters. Do not create
unnecessarily long variable names as it adds to your typing
effort.

(b) The first character in the variable name must be an alphabet or
underscore.

(c) No commas or blanks are allowed within a variable name.

(d) No special symbol other than an underscore (as in gross_sal)
can be used in a variable name.

Example::
	si_int
	m_hra
	pop_e_89

The following code declares a variable named 'inputVariable' and
assigns it the value obtained from the digital input pin 0.


.. code-block:: c

	int inputVariable;

	void setup()
	{
	pinMode(0,INPUT);
	}

	void loop()
	{
	inputVariable=digitalRead(0);
	}

**NOTE** : Make sure you give descriptive names for variables for
better understanding and debugging.

A variable has to be declared before it can be used.It can be declared
at the start of the program outside all the functions(called global
variables) or can be declared within the functions(called local variables).
Global variables can be accessed throughout the program whereas local
variables are accessible only within the functions in which they are declared.

The variable 'inputVariable' declared above is a global variable.


Constants
---------

Constant is a bit like a variable declaration except the value cannot be
changed.

The const keyword is to declare a constant, as shown below::

	int const a = 1;
	const int a = 2;

**Note** :

    You can declare the const before or after the type. Choose one an stick to it.
    It is usual to initialise a const with a value as it cannot get a value any
    other way.
    The rules of declaring constants is same as that of variables.

The anuduino programming language has a few pre-defined values which are called
constants. They are used to make the program easier to read. They are classified
in groups

TRUE/FALSE
~~~~~~~~~~

These are boolean constants that define logic levels. FALSE is easily defined as
zero(0) while TRUE is defined as 1 but can be anything else other than zero. So,
in boolean sense -2, 7 ..454 are all TRUE.

HIGH/LOW
~~~~~~~~

These constants are used to define pin levels and are used to read and write to
digital pins. HIGH is defined as logic level 1, ON or 5 volts while LOW is defined
as logic level 0, OFF or 0 volts.

digitalWrite(0,HIGH);

INPUT/OUTPUT
~~~~~~~~~~~~

These are the constants used with the pinMode() function(explained later) to define
the mode of the digital pin as INPUT or OUTPUT. ::

	pinMode(0,OUTPUT)


Datatypes
---------

Datatypes are the means to identify the type of data and the associated operations of
handling it.The datatypes supported in DigiSpark are :

integer(int), float(float), double(double), character(char)

- **Int (integer)**  The main workhorse, stores a number in 2 bytes (16 bits). Has
  no decimal places and will store a value between -32,768 and 32,767
- **long (long)** Used when an integer is not large enough. Takes 4 bytes (32 bits) of
  RAM and has a range between -2,147,483,648 and 2,147,483,647.
- **boolean (boolean)** A simple True or False variable. Useful because it only uses
  one bit of RAM
- **Float (float)** Used for floating point math (decimals). Takes 4 bytes (32 bits)
  of RAM and has a range between -3.4028235E+38 and 3.4028235E+38
- **Char (character)** Stores one character using the ASCII code(i.e. ‘A’=65).
  Uses one byte (8 bits) of RAM. The Anuduino handles strings as an array of chars.


Keywords
--------

Keywords are the words whose meaning has already been explained to the to the
computer. The keywords cannot be used as variable names because if we do
so we are trying to assign a new meaning to the keyword, which is not allowed
by the computer. However, it would be safer not to mix up the variable names and
the keywords. The keywords are also called ‘Reserved words’.

**Examples** : for, int, float, while, break, switch etc


Structure
---------

The basic structure of the anuduino programming is fairly simple and runs in atleast
two parts. These two required parts, or functions enclose blocks of statements.

.. code-block:: c

	void setup()
	{
	 statements;
	}

	void loop()
	{
	 statements;
	}

Where setup() is the preparation and loop() is the execution. Both functions are required
for the program to work.

The setup() function should follow the declaration of any variables at the very beginning
of the program. It is the first function to run in any program just like the main()
function in C. It is run only once and is used to set pinMode and initialise serial
communication.

The loop functions follows next and includes the code to be executed continuously- reading
inputs, triggering outputs etc. This function is the core of all anuduino programs and
does bulk of the work.

setup
~~~~~

The setup() function is called once when the program starts. It is used to begin serial
communication and set pinmodes. It must be included in the program even if there are no
statements to run.


.. code-block:: c

	void setup()
	{
	 pinMode(0,OUTPUT); //setting PB0 as output pin
	}

loop()
~~~~~~

After calling the setup() function, the loop() function does precisely what its name
suggests, and loops consecutively, allowing the program to change, respond and control
the anuduino board.

.. code-block:: c

	/*program to toggle the PB0 output*/
	void loop()
	{
	 digitalWrite(0,HIGH)//turns PB0 on
	 delay(1000);
	 digitalWrite(0,LOW);//turns PB0 off
	 delay(1000);
	}


Curly braces
------------

The curly braces just define the beginning and end of function blocks and statement blocks
such as void loop() functions and if and for statements.


.. code-block:: c

	type function()
	{
	statements;
	}

The opening curly brace { must be always followed be a closing curly brace }. This is often
referred to as braces being balanced. Unbalanced braces can lead to cryptic, impenetrable
errors that are often hard to track down in a large program.


Semicolon
---------

A semicolon must be used at the end of the statement and to separate elements in a program.
It is used to separate elements in a for loop.

.. code-block:: c

	int x=10; //declares a variable 'x' with an integer value 10

**Note** : Forgetting to add semicolon at the end of a statement may result in compile time
           errors. This error may be sometimes obvious and sometimes difficult to track down.


Comments
--------

Single line comments
~~~~~~~~~~~~~~~~~~~~

Single line comments begin with // and end with the next line of code. They donot takeup any
memory space.

//this is a single line comment

Single line comments are often used after a valid statement to provide information about what
the statement accomplishes or to provide a future reminder.


Multi-line comments
~~~~~~~~~~~~~~~~~~~

Blocks comments or multi-line comments are areas of text ignored by the compiler and are used
for large text descriptions of code and comments that help others understand parts of the
program. They begin with /\* and end with \*/ and can span multiple times.

/\* This is the starting of multi-line comment
This is the ending of multi-line comment\*/


Operators
---------

An operator is a symbol that tells the compiler to perform specific mathematical or logical
manipulations. Aniduino programming language is rich in built-in operators and provides the
following types of operators:

- Arithmetic Operators

- Relational Operators

- Logical Operators

- Bitwise Operators

- Assignment Operators


Arithmetic operators
~~~~~~~~~~~~~~~~~~~~

**+**	Adds two operands ::

        A + B will give 30

**-**	Subtracts second operand from the first::

        A - B will give -10

*****	Multiplies both operands::

        A * B will give 200

**/**	Divides numerator by de-numerator::

        B / A will give 2

**%**	Modulus Operator and remainder of after an integer division::

        B % A will give 0

**++**	Increments operator increases integer value by one::

        A++ will give 11

**--**	Decrements operator decreases integer value by one::

        A-- will give 9


Relational operators
~~~~~~~~~~~~~~~~~~~~

**==**	Checks if the values of two operands are equal or not, if yes then condition becomes true. ::

        (A == B) is not true.

**!=**	Checks if the values of two operands are equal or not, if values are not equal then condition becomes true. ::

        (A != B) is true.

**>**	Checks if the value of left operand is greater than the value of right operand, if yes then condition becomes true.::

        (A > B) is not true

**<**	Checks if the value of left operand is less than the value of right operand, if yes then condition becomes true. ::

        (A < B) is true.

**>=**	Checks if the value of left operand is greater than or equal to the value of right operand, if yes then condition becomes true. ::

        (A >= B) is not true.

**<=**	Checks if the value of left operand is less than or equal to the value of right operand, if yes then condition becomes true. ::

        (A <= B) is true.


Logical operators
~~~~~~~~~~~~~~~~~

**&&**	Called Logical AND operator. If both the operands are non-zero, then condition becomes true. ::

        (A && B) is false.

**||**	Called Logical OR Operator. If any of the two operands is non-zero, then condition becomes true.::

        (A || B) is true.

**!**	Called Logical NOT Operator. Use to reverses the logical state of its operand. If a condition is true then Logical NOT operator will make false. ::

        !(A && B) is true.


Bitwise operators
~~~~~~~~~~~~~~~~~

**&**	Binary AND Operator copies a bit to the result if it exists in both operands. (A & B) will give 12, which is 0000 1100

**|**	Binary OR Operator copies a bit if it exists in either operand. (A | B) will give 61, which is 0011 1101

**^**	Binary XOR Operator copies the bit if it is set in one operand but not both. (A ^ B) will give 49, which is 0011 0001

**~**	Binary Ones Complement Operator is unary and has the effect of 'flipping' bits. (~A ) will give -61, which is 1100 0011 in 2's complement form.

**<<**	Binary Left Shift Operator. The left operands value is moved left by the number of bits specified by the right operand. ::

 	       A << 2 will give 240 which is 1111 0000

**>>**	Binary Right Shift Operator. The left operands value is moved right by the number of bits specified by the right operand. ::

       	      A >> 2 will give 15 which is 0000 1111


Assignment operators
~~~~~~~~~~~~~~~~~~~~

**=**	Simple assignment operator, Assigns values from right side operands to left side  operand. ::

                C = A + B will assign value of A + B into C

**+=**	Add AND assignment operator, It adds right operand to the left operand and assign the result to left operand. ::

	        C += A is equivalent to C = C + A

**-=**	Subtract AND assignment operator, It subtracts right operand from the left operand and assign the result to left operand. ::

	        C -= A is equivalent to C = C - A

***=**	Multiply AND assignment operator, It multiplies right operand with the left operand and assign the result to left operand.::

        	C \*= A is equivalent to C = C \* A

**/=**	Divide AND assignment operator, It divides left operand with the right operand and assign the result to left operand. ::

	        C /= A is equivalent to C = C / A

**%=**	Modulus AND assignment operator, It takes modulus using two operands and assign the result to left operand. ::

	        C %= A is equivalent to C = C % A

**<<=**	Left shift AND assignment operator. ::

        	C <<= 2 is same as C = C << 2

**>>=**	Right shift AND assignment operator. ::

	        C >>= 2 is same as C = C >> 2

**&=**	Bitwise AND assignment operator. ::

	        C &= 2 is same as C = C & 2

**^=**	bitwise exclusive OR and assignment operator. ::

        	C ^= 2 is same as C = C ^ 2

**|=**	bitwise inclusive OR and assignment operator. ::

	        C \|= 2 is same as C = C | 2


Control structures
-------------------

Decision control structures
~~~~~~~~~~~~~~~~~~~~~~~~~~~

We all need to alter our actions in the face of changing circumstances. Same way even
the microcontroller has to decide its response to these changes. A decision control
instruction can be implemented in C using:

(a) The if statement
(b) The if-else statement

(a) The if statement
^^^^^^^^^^^^^^^^^^^^

The general form of if statement looks like this:

if ( this condition is true )
execute this statement ;

The keyword if tells the compiler that what follows is a decision control instruction.
The condition following the keyword if is always enclosed within a pair of parentheses.
If the condition, whatever it is, is true, then the statement is executed. If the
condition is not true then the statement is not executed; instead the program skips past it.

(b) The if-else statement
^^^^^^^^^^^^^^^^^^^^^^^^^

The if statement by itself will execute a single statement, or a group of statements,
when the expression following if evaluates to true. It does nothing when the expression
evaluates to false. Can we execute one group of statements if the expression evaluates to
true and another group of statements if the expression evaluates to false? Of course!.
This is possible by the if-else statement.

The general form of if-else statement is :

.. code-block:: c

	if( this condition is true)
	execute this statement ;
	else
	execute this statement ;

Apart from these, We can have a lot of variations in the if statements. The if statements
could be nested as well.

The if statement can take any of the following forms:

(a)

.. code-block:: c

     if ( condition )
     	do this ;

(b)

.. code-block:: c

 if ( condition )
    {
     do this ;
     and this ;
    }

(c)

.. code-block:: c

 if ( condition )
     do this ;
    else
     do this ;

(d)

.. code-block:: c

	if ( condition )
	    {
	     do this ;
	     and this ;
	    }
	    else
	    {
	     do this ;
	     and this ;
	    }

(e)

.. code-block:: c

   if ( condition )
    do this ;
    else
    {
      if ( condition )
       do this ;
      else
      {
       do this ;
       and this ;
      }
    }

(f)

.. code-block:: c

 if ( condition )
    {
     if ( condition )
      do this ;
     else
     {
      do this ;
      and this ;
     }
    }
    else
     do this ;


Loop control structures
~~~~~~~~~~~~~~~~~~~~~~~

The versatility of the microcontroller lies in its ability to perform a set of
instructions repeatedly. This involves repeating some portion of the program
either a specified number of times or until a particular condition is being
satisfied. This repetitive o peration is done throug h a loop control instruction.
There are three methods by way of which we can repeat a part of a
program. They are:

(a) Using a for statement
(b) Using a while statement
(c) Using a do-while statement

(a) for statement
^^^^^^^^^^^^^^^^^

The for allows us to specify three things about
a loop in a single line:

(a) Setting a loop counter to an initial value.

(b) Testing the loop c ounter to determine whether its value has
reached the number of repetitions desired.

(c) Increasing the value of loop counter eac h time the program
segment within the loop has been executed.

The general form of for statement is as under:

.. code-block:: c

	for ( initialise counter ; test counter ; increment counter )
	  {
	  do this ;
	  and this ;
	  and this ;
	  }

Example :

.. code-block:: c

	for(int i=0;i<1000;i++)
	{
	 digitalWrite(0,HIGH);
	}
	digitalWrite(0,LOW);

The above program gives a low output at PB0 pin when i becomes 1000.
Before this, the PB0 pin is high.

(b) while statement
^^^^^^^^^^^^^^^^^^^

The basic structure is

.. code-block:: c

	while ( condition )
	{
	  Code to execute while the condition is true
	}

The true represents a boolean expression which could be x == 1 or while ( x != 7 )
(x does not equal 7). It can be any combination of boolean statements that are legal.
Even, (while x ==5 || v == 7) which says execute the code while x equals five or
while v equals 7. Notice that a while loop is like a stripped-down version of a for
loop-- it has no initialization or update section. However, an empty condition is not
legal for a while loop as it is with a for loop.

(c) do-while statement
^^^^^^^^^^^^^^^^^^^^^^

do-while loops are useful for things that want to loop at least once. The structure is

.. code-block:: c

	do
	{
	 statements;
	} while ( condition );

Notice that the condition is tested at the end of the block instead of the beginning,
so the block will be executed at least once. If the condition is true, we jump back
to the beginning of the block and execute it again. A do..while loop is almost the
same as a while loop except that the loop body is guaranteed to execute at least once.
A while loop says "Loop while the condition is true, and execute this block of code",
a do..while loop says "Execute this block of code, and then continue to loop while
the condition is true".


(c) Case control structures
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The control statement that allows us to make a decision from the number of choices is
called a switch, or more correctly a switch-case-default, since these three keywords
go together to make up the control statement. They most often appear as follows:

.. code-block:: c

	switch ( integer expression )
	{
	  case constant 1 :
			   do this ;
	  case constant 2 :
			   do this ;
	  case constant 3 :
			   do this ;
	  default :
		   do this ;
	}

The integer expression following the keyword switch is any C expression that will
yield an integer value. It could be an integer constant like 1, 2 or 3, or an expression
that evaluates to an integer. The keyword case is followed by an integer or a character
constant. Each constant in each case must be different from all the others. The “do this”
lines in the above form of switch represent any valid C statement.

What happens when we run a program containing a switch? First, the integer expression
following the keyword switch is evaluated. The value it gives is then matched, one by one,
against the constant values that follow the case statements. When a match is found, the
program executes the statements following that case, and all subsequent case and default
statements as well. If no match is found with any of the case statements, only the
statements following the default are executed.

Consider the following program:

.. code-block:: c

	void loop( )
	{
	 if(Serial.available())
	  i=serial.read();
	 switch ( i )
	  {
	    case 1 : digitalWrite(1,HIGH);

	    case 2 : digitalWrite(2,HIGH);

	    case 3 : digitalWrite(3,HIGH);

	    default : digitalWrite(0,HIGH);
	  }
	}

The output of this program would be:

All 1,2,3 and 0 high if i is 1
2,3 and 0 high if i is 2
3 and 0 if i is 3
0 high if i!= 1,2 or 3


The output is definitely not what we expected! We didn’t expect the second, third
and default case in the above output. The program executes case 2 and 3 and the default
case. Well, yes. We said the switch executes the case where a match is found and all
the subsequent cases and the default as well.
If you want that only case 2 should get executed, it is upto you to
get out of the switch then and there by using a break statement.
The following example shows how this is done. Note that there is
no need for a break statement after the default, since the control
comes out of the switch anyway.

.. code-block:: c

	void loop( )
	{
	 if(serial.available())
	  i=serial.read();
	 switch ( i )
	  {
	    case 1 : digitalWrite(1,HIGH);
		     break;
	    case 2 : digitalWrite(2,HIGH);
		     break;
	    case 3 : digitalWrite(3,HIGH);
		     break;
	    default : digitalWrite(0,HIGH);
	  }
	}


The output of this program would be:

PB1 high if i is 1
PB2 high if i is 2
PB3 high if i is 3


Predefined functions
--------------------

Digital input/Output functions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

pinMode()
^^^^^^^^^

Used in the setup() function to configure a specified pin to behave either as an
INPUT or an OUTPUT.

*Syntax*
 pinMode(pin, mode);

*Example*
 pinMode(0,OUTPUT); //sets the pin PB0 as an output pin

**digitalRead(pin)**

Reads the value from a specified digital pin with the result either as HIGH or LOW.

*Syntax*
digitalRead(pin);

"Example*

.. code-block:: c

	int i=digitalRead(1); //i is 1 if PB1 is HIGH or 0 if PB1 is LOW.

digitalWrite()
^^^^^^^^^^^^^^

outputs either logic level HIGH or LOW at specified digital pin.

*Syntax*
digitalWrite(pin, mode);

*Example*
digitalWrite(3,HIGH); //makes the PB3 pin high


Analog input/output functions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Anuduino is a digital machine but it has the ability to operate in the analog
realm (through tricks)

analogWrite()
^^^^^^^^^^^^^

*Syntax*
analogWrite(pin, value);

*Example*
analogWrite(0, 255);//writes the analog value of 255 to PB0

Some of the Anuduio pins support PWM (0,1). This turns the pin ON and OFF very quickly
making it act like an analog output. The value is any number between 0( 0% duty cycle ~0V)
and 255 (100% duty cycle ~5V).

analogRead()
^^^^^^^^^^^^

When the analog input pins are set to input you can read their voltage. A value between
0 ( for 0 volts) and 1024( for 5 volts) will be returned.

*Syntax*
analogRead(pin);

*Example*
analogRead(0); //reads the analog value from PB0


Miscellaneous functions
~~~~~~~~~~~~~~~~~~~~~~~

pulseIn()
^^^^^^^^^

Reads a pulse (either HIGH or LOW) on a pin. For example, if value is HIGH, pulseIn()
waits for the pin to go HIGH, starts timing, then waits for the pin to go LOW and stops
timing. Returns the length of the pulse in microseconds. Gives up and returns 0 if no
pulse starts within a specified time out.

The timing of this function has been determined empirically and will probably show errors
in longer pulses. Works on pulses from 10 microseconds to 3 minutes in length.

*Syntax*
pulseIn(pin, value)
pulseIn(pin, value, timeout)

*Parameter*
pin: the number of the pin on which you want to read the pulse. (int)
value: type of pulse to read: either HIGH or LOW. (int)
timeout (optional): the number of microseconds to wait for the pulse to start;
default is one second (unsigned long)

Returns the length of the pulse (in microseconds) or 0 if no pulse started before the
timeout (unsigned long)

Example:

.. code-block:: c

	int pin = 0;
	unsigned long duration;

	void setup()
	{
	  pinMode(pin, INPUT);
	}

	void loop()
	{
	  duration = pulseIn(pin, HIGH);
	}

delayMicroseconds()
^^^^^^^^^^^^^^^^^^^

Pauses the program for the amount of time (in microseconds) specified as parameter.
There are a thousand microseconds in a millisecond, and a million microseconds in a second.
For delays longer than a few thousand microseconds, you should use delay() instead.

*Syntax*
delayMicroseconds(us)

*Parameters*
us: the number of microseconds to pause (unsigned int)

*Example*

.. code-block:: c

	int outPin = 3;                 // digital pin 3

	void setup()
	{
	  pinMode(outPin, OUTPUT);      // sets the digital pin as output
	}

	void loop()
	{
	  digitalWrite(outPin, HIGH);   // sets the pin on
	  delayMicroseconds(50);        // pauses for 50 microseconds
	  digitalWrite(outPin, LOW);    // sets the pin off
	  delayMicroseconds(50);        // pauses for 50 microseconds
	}

configures pin number 3 to work as an output pin. It sends a train of pulses with
100 microseconds period.

delay()
^^^^^^^

Pauses the program for the amount of time (in miliseconds) specified as parameter. (There are 1000 milliseconds in a second.)

*Syntax*
delay(ms)

*Parameters*
ms: the number of milliseconds to pause (unsigned long)

Example:

.. code-block:: c


	int ledPin = 13;                 // LED connected to digital pin 13

	void setup()
	{
	  pinMode(ledPin, OUTPUT);      // sets the digital pin as output
	}

	void loop()
	{
	  digitalWrite(ledPin, HIGH);   // sets the LED on
	  delay(1000);                  // waits for a second
	  digitalWrite(ledPin, LOW);    // sets the LED off
	  delay(1000);                  // waits for a second
	}
