# PHP Syntax Guide

PHP is a server-side scripting language and has integrations for standard web servers such as `apache` and `nginx`. Using a web server with PHP, it is possible to create dynamic web pages server-side.

## PHP Comments

```php
// this is a single line php comment

/*
 * this is a multiline
 * comment
 */
```

## PHP Variables
PHP variables are case-sensitive and are used to manage the program's state. A valid variable name starts with a letter or underscores, followed by any number of letters, numbers, or underscores.

```php
// dynamic variables (meaning they can be re-assigned)
$color = "red";

// store the value of color
$colorValue = $color;

// getting a reference to the color variable. This value may change based on the assignment of color.
$colorReference = &$color;

$color = "blue";

echo $colorValue; // red
echo $colorReference; // blue
```

## PHP Echo / Print
`echo` and `print` are used to output data. In a PHP script, echo will send data to `stdout` and on a PHP server it will appear in the server response.

```php
// These will all produce the same result. Echo can take a comma-separated list of arguments, but only one argument in brackets.

// comma-separated without parentheses
echo  "and a ", 1, 2, 3;

// just one parameter with parentheses
echo ("and a 123");   

print ("and a 123");
print  "and a 123";

// print will also return 1 making it suitable as an expression
$result = print "hello";
echo $result; // 1
```

## PHP Data Types

### Primitives
```php
$a_bool = true;   // a boolean
$a_str  = "foo";  // a string
$a_str2 = 'foo';  // a string
$an_int = 12;     // an integer

echo gettype($a_bool); // prints out:  boolean
echo gettype($a_str);  // prints out:  string
```

### Compound Types
PHP supports arrays, objects, callbacks, and array-like objects. Objects may define methods, static methods, and properties. PHP also supports class inheritance.

```php
// array
$trees = array("cedar", "pine", "spruce");
// associative array
$vegetation = array(
    "tree" => "cedar",
    "vegetable" => "carrots",
    "flower" => "tulip"
);
```

```php
// object

class Tree {

    public $name;

    function show_name() {
        echo $this->name;
    }

    function __construct($name) {
        $this->name = $name;
    }

}

// create an instance of a tree object
$tree = new Tree("cedar");
// access public method
$tree->show_name()

```
```php
// callable
function printCedarTree()
{
    echo "cedar";
}

function executeCallback($callback)
{
    $callback();
}

executeCallback('printCedarTree');
```

```php
// Iterable types. Iterable's must be an instance of an array or object implementing the Traversable interface or a generator. 


echo "from array", '<br>';
$treeArray = ['cedar', 'spruce', 'pine'];
foreach ($treeArray as $tree) {
    echo $tree, '<br>';
}

echo "from generator", '<br>';
function trees()
{
    yield 'cedar';
    yield 'spruce';
    yield 'pine';
}

foreach (trees() as $tree) {
    echo $tree, '<br>';
}
```

### Special Types
There are two special types, `NULL` and `resource`.

```php
// resources are references to external things such as files, databases, and network sockets.
$handle = fopen("c:\\folder\\resource.txt", "r"); // $handle is a resource type. The PHP engine will free the external resource once the variable goes out of scope. You may also free the resource manually.

// NULL is an unset variable or variable manually set to NULL.
$null = NULL

$undefinedVar == NULL // true

```



## PHP Strings

PHP has strings that support interpolation and verbatim strings.

```php

$cookie = "Chocolate Chip";
// string interpolation
echo "My cookie is $cookie\n"; // My cookie is Chocolate Chip

// here doc
echo <<<"EOL"
My cookie is $cookie
EOL; // My cookie is Chocolate Chip

// verbatim string
echo 'My cookie is $cookie'; // My cookie is $cookie
// nowdoc
echo <<<'EOL'
My cookie is $cookie
EOL; // My cookie is $cookie


// complex interpolation used for class properties, methods, and arrays.
// Example of calling a method on an instantiated object
class Cookie
{
    function chocolateChip(): string
    {
        return "Chocolate Chip";
    }
}

$cookie = new Cookie();
echo "My cookie is {$cookie->chocolateChip()}"

```

## PHP Numbers
PHP supports integer and float types.

```php
// integer types
$a = 1234; // decimal number
$a = 0123; // octal number (equivalent to 83 decimal)
$a = 0o123; // octal number (as of PHP 8.1.0)
$a = 0x1A; // hexadecimal number (equivalent to 26 decimal)
$a = 0b11111111; // binary number (equivalent to 255 decimal)
$a = 1_234_567; // decimal number (as of PHP 7.4.0)

$max_int = PHP_INT_MAX;
$min_int = PHP_INT_MIN;

// floating numbers

$a = 1.234; 
$b = 1.2e3; 
$c = 7E-10;
$d = 1_234.567; // as of PHP 7.4.0

```

## PHP Constants
Constants can be defined at compile time or dynamically at runtime.

```php
// defined at compile time
const TREE = "cedar";

// defined at runtime. This assignment not work inside class definitions.
define("TREE", "cedar");
```

## PHP Operators

### Arithmetic
```php

// add 
1 + 2; // 3

// subtract
2 - 1; // 1

// multiply
2 * 2; // 4

// divide
4 / 2; // 2

// modulus
4 % 2; // 0

// power
2 ** 4; // 16

// concatenate
2 . 4; // 24

```

### Arithmetic Assignment

```php
$a = 4;
$b = 2;

$a += $b; // a = a + b -> 6
$a -= $b; // a = a - b -> 2
$a *= $b; // a = a * b -> 8
$a /= $b; // a = a / b -> 2
$a %= $b; // a = a % b -> 0
$a **= $b; // a = a ** b -> 16
$a .= $b; // a = a . b -> 42
```

### Comparison

```php
$a == $b; // equality after type coercion
$a === $b; // equality without type coercion
$a != $b; // not equal with type coercion
$a !== $b; // not equal without type coercion
$a < $b; // $a less than $b
$a <= $b; // $a less than or equal to $b
$a >= $b; // $a greater than or equal to $b
$a <=> $b; // an int less than, equal to, or greater than zero when $a is less than, equal to, or greater than $b, respectively.

```

### Error Handling
The `@` symbol will silence errors from the evaluated expression after the symbol.

```php
$value = @$cache[$key]; // will not issue an error if the index $key doesn't exist.
```

### Execution
The backtick operator will execute a command identical to the `shell_exec()` function.
```php
$output = `ls -la`; // list files in the current directory
```

### Increment / Decrement

```php
$a = 1;
$b = ++$a; // $b == 2, $a == 2
$b = $a++; // $b == 1, $a == 2
$b = --$a; // $b == 0, $a == 0
$b = $a--; // $b == 1, $a == 0

```

### Logical Operators

```php

$a and $b; // true if $a and $b are both true
$a or $b; // true if $a or $b are true or both are true
$a xor $b; // true if $a or $b are true but not both
!$a; // true if $a is false or true if $a is false
$a && $b; // same as `and` but with a different operator precidence
$a && $b; // same as `or` but with a different operator precidence

// short circuiting
// foo() will never get called as those operators are short-circuit

$a = (false && foo());
$b = (true  || foo());
$c = (false and foo());
$d = (true  or  foo());

// operator precedence

// The result of the expression (false || true) is assigned to $e
// Acts like: ($e = (false || true))
$e = false || true;

// The constant false is assigned to $f before the "or" operation occurs
// Acts like: (($f = false) or true)
$f = false or true;
```

### Array Operators

```php
$a + $b; // Set union
$a == $b; // Set equality
$a != $b; // Sets are not equal

$a === $b; // Ordered Set equality and must be same type
$a !== $b; // Ordered Sets are not equal
```

### Instance Of
Check that variable is an instance of a class

```php
class MyClass
{
}

class NotMyClass
{
}
$a = new MyClass;

$a instanceof MyClass; // true
$a instanceof NotMyClass; // false
```

## PHP If & Else & Elseif
PHP supports an if conditional, one or more else if conditions, and else statements. There is also a shorthand ternary operator one may use for a conditional statement.

```php
$t = date("H");

if ($t < "10") {
  echo "Have a good morning!";
} elseif ($t < "20") {
  echo "Have a good day!";
} else {
  echo "Have a good night!";
}

// ternary operator
$marks=40;
echo $marks>=40 ? "pass" : "Fail"; // if true the return 'pass' else return 'Fail'
```

## PHP Functions
PHP supports many different types of functions and parameter declarations.

```php
// function with two parameters
function add($a, $b) {
    return $a + $b;
}

echo add(1, 2); // 3


// variadic function (variable number of parameters)
function sum(...$numbers) {
    $acc = 0;
    foreach ($numbers as $n) {
        $acc += $n;
    }
    return $acc;
}

echo sum(1, 2, 3, 4); // 10

// splat operator will expand an array into arguments
echo sum(...[1,2,3,4]); // 10

```

## PHP Arrays
PHP arrays can be thought of like arrays/objects in javascript, dictionaries in python. They hold a collection of values accessible by keys.

```php
$trees = array('cedar', 'pine', 'spruce');

// array literal
$trees = ['cedar', 'pine', 'spruce'];

// associative array
$pizza = [
    'size' => 'large',
    'kind' => 'barbeque chicken',
    'crust' => 'thin'
];

// accessing array elements

$array = array(
    "foo" => "bar",
    42    => 24,
    "multi" => array(
         "dimensional" => array(
             "array" => "foo"
         )
    )
);

$array["foo"]; // bar
$array[42]; // 24
$array["multi"]["dimensional"]["array"]; // foo

```
## PHP Loop

PHP supports conventional for and while loops, along with a shorthand for looping `iterable` type values.

```php
// echo numbers even numbers up to 10
for ($i = 1; $i <= 10; $i++) {
    if ($i % 2) {
        // short circuit the for loop and continue to the next iteration
        continue;
    }
    else {
        echo $i;
    }
}

// use a break statement to exit the loop
for ($i = 1; ; $i++) {
    if ($i > 10) {
        // exit for loop immediatly
        break;
    }
    echo $i;
}

// while loop echo numbers one through 10
$i = 1;
while ($i <= 10) {
    echo $i++; 
}

// do while loop echo numbers one through 10. The do statement will always run atleast once
$i = 1;
do {
    echo $i++;
} while ($i <= 10)

// using foreach in an array and mutating the values
$arr = array(1, 2, 3, 4);
foreach ($arr as &$value) {
    $value = $value * 2;
}
// $arr is now array(2, 4, 6, 8)

```

