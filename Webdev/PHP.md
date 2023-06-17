# PHP basics
Sources used for these notes: Bro Code's tutorial on YouTube and [Wikiversity](https://en.wikiversity.org/wiki/PHP)

## Variables
PHP datatypes are inferred and dynamic. it has strings, integers, float, booleans, etc.

```
<?php
	$name = "Passarinho";
	$age = 21;
	echo "I'm {$name}<br>And I turned {$age} last sunday";
?>
```

## Arrays
### Numeric arrays
```
$users = array(
	0 => 'Michael',
	1 => 'Dwight',
	2 => 'Jim'
);
```
To access data from this array: `$users[0]`

### Associative arrays
```
$trainer = array(
	'name' => 'Ben',
	'age' => 14,
	'pokemon' => 'Mudkip'
);
```
To access data from this array: `$trainer['name']`

### Multidimensional arrays
```
$trainer = array(
	'name' => 'Ben',
	'age' => 14,
	'pokemon' => array(
		0 => 'Mudkip',
		1 => 'Bagon',
		2 => 'Mareep',
		3 => 'Nincada',
		4 => 'Sentret',
		5 => 'Eevee',
		6 => 'Murkrow'
	) // now Ben has a whole team!
);
```
To access data from this array: `$trainer['pokemon'][2]`

## Functions
Declaring a funtion:

```
function greet($name) {
	echo 'Hi, ' . $name;
}			  # ^ concatenation
```
Calling a function: `<?php greet('Joe'); ?>`

## Scope
Contrary to other programming languages, variables outside a function cannot be used inside of it. This can be mitigated with the keyword `global`:
```
$var = 'Test';
function test()
{
 	global $var;
 	echo $var;
}
test();
?>
```

Another way to do that is to use the `$GLOBALS` array: `$GLOBALS['var'] = 'something';`

To be able to use a variable created *inside* a function, we use the `static` keyword.

## $_GET and $_POST
Assuming that there is the following `<form>` tag in an HTML file with login inputs: **`<form action="index.php" method="get">`**

To get the value submitted, we can type **`$username = $_GET["username"]`**. It can store many values, like an array.

Since the method is `get`, any information submitted using `$_GET` is appended to the URL, making it not a safe choice for sensitive data.

We can change that with `$_POST`: **`<form action="index.php" method="post">`** so it doesn't happen. It goes to the body of the HTTP request.

+ $_GET can get bookmarked, $_POST can't
+ $_GET can be cached, $_POST cannot
+ $_POST doesn't have a char limit, $_GET does

An implementation example from Wikiversity's Web Design course:
```

```
