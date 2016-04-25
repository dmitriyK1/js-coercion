
https://davidwalsh.name/fixing-coercion
http://getify.github.io/coercions-grid
http://jsperf.com/triple-equals-vs-double-equals/5
http://jscoercion.qfox.nl/
http://webreflection.blogspot.com/2010/10/javascript-coercion-demystified.html

Explicit coercion \ Implicit coercion

Use only one form of coercion ( Number vs + operator )

Abstract operations:
    ToString
    ToNumber
    ToBoolean
    ToPrimitive ( when converting objects; uses valueOf > toString )
               
String( [] )                  ''
String( [1,2,3] )             '1,2,3'
String( [null, undefined] )   ','
String( [ [], [], [] ] )      ',,'
String( [,,,,] )              ',,,'        // trailing comma is allowed in array but ignored [ 1, 2, 3, ]


function stringification is a browser implementation-dependent

Number( '' )                 0       
Number( '0' )                0
Number( '-0' )               -0
Number( '009' )              9
Number( '3.14159' )          3.14159
Number( '0.' )               0
Number( '.0' )               0
Number( '.' )                NaN
Number( '0xaf' )             0

Number( true )               1
Number( false )              0
Number( null )               0
Number( undefined )          NaN

Number( obj ) > ToPrimitive > .valueOf > .toString ( if valueOf doesn't return a primitive / value )

Number( [''] )               0        // .toValue returns [''] so fallback to .toString used which returns '', Number('') === 0
Number( ['0'] )              0
Number( ['-0'] )             -0
Number( [null] )             0
Number( [undefined] )        0
Number( [1, 2, 3] )          NaN
Number( [[[[[[]]]]]] )       0

date = new Date

date + 1 = 'string date value1'             // Date uses toString > valueOf fallback

Falsy values
    ''
    0, +0, -0
    false
    null
    undefined
    NaN


Implicit coercion
    "123" - 0               // 123
    "123" - ""              // 123

if ( "" == false )         // empty string converted to 0, false converted to 0

if ( "123" == false )      // 123 == 1 > false

if ( [] == false )         // '' == false > 0 == 0

Never use 
    == true
    == false

[] == ![]
    "" == false
        0 == 0

==   allows coercion, slower
===  disallows coercion, faster

~ hides a leaky abstraction of -1 in .indexOf()

<, >      always uses coercion, no strict form 

String('abc')          instanceof String         // false
(new String('abc'))    instanceof String         // true

3 > 2 > 1           // false
