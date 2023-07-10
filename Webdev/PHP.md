# PHP basics

A boiled down introduction and future reference. Sources used for these notes: Bro Code's tutorial on YouTube and [Wikiversity](https://en.wikiversity.org/wiki/PHP)

## Variables

PHP datatypes are dynamic. it has strings, integers, float, booleans, etc.

```php
<?php
 $name = "Passarinho";
 $age = 21;
 echo "I'm {$name}<br>And I turned {$age} last sunday";
?>
```

## Arrays

### Numeric arrays

```php
$users = array(
 0 => 'Michael',
 1 => 'Dwight',
 2 => 'Jim'
);
```

To access data from this array: `$users[0]`

### Associative arrays

```php
$trainer = array(
 'name' => 'Ben',
 'age' => 14,
 'pokemon' => 'Mudkip'
);
```

To access data from this array: `$trainer['name']`

### Multidimensional arrays

```php
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

```php
function greet($name) {
 echo 'Hi, ' . $name;
}          # ^ concatenation
```

Calling a function: `<?php greet('Joe'); ?>`

## Scope

Contrary to other programming languages, variables outside a function cannot be used inside of it. This can be mitigated with the keyword `global`:

```php
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

Assuming that there is the following `<form>` tag in an HTML file with login inputs: **`<form action="index.php" method="get">`** which has an `<input>` with a name attribute "username".

To get the value submitted, we can type **`$username = $_GET["username"]`**. It can store many values, like an array.

Since the method is `get`, any information submitted using `$_GET` is appended to the URL, making it not a safe choice for sensitive data. We can change that with `$_POST`: **`<form action="index.php" method="post">`** so it doesn't happen. It now goes to the body of the HTTP request instead.

+ $_GET can get bookmarked, $_POST can't
+ $_GET can be cached, $_POST cannot
+ $_POST doesn't have a char limit, $_GET does

### An implementation example: circumference calculator

```php
<form action="index.php" method="post">
 <label>radius:</label>
 <input type="text" name="radius">
 <input type="submit" value="calculate">
</form>
...
<?php
 $radius = $_POST["radius"];
 $circumference = null;

 $circumference = 2 * pi() * $radius;

 echo"Circumference = {$circumference}cm <br>";
?>
```

## Dealing with conditions

### if statements

Syntax:

`if ($age >= 18){echo "You may enter";}`

Other keywords are: `elseif` and `else`

### Logical operators

The typical stuff (same as in C):

or: `||`

and: `&&`

not: `!`

### switch

Syntax:

```php
$grade = "B";
switch($grade){
 case "A":
  echo "You did great";
  break;
 case "B":
  echo "You did good";
  break;
 default:
  echo "You can do better";
}
```

## isset() and empty()

`isset()` returns *true* if a variable is declared and not null

`empty()` returns *true* if a variable is not declared, `false`, `null` or `""`

```php
# only computes when the user clicks the submit button
if(isset($_POST["login"]))
{
 username = $_POST["username"]
 password = $_POST["password"]

 if(empty($username)) {echo "Username is missing";}
 elseif(empty($password)) {echo "Password is missing";}
 
 else {echo "Hello {$username}";}
}
```

## [String functions](https://www.w3schools.com/php/php_ref_string.asp)

There are quite a few! There's a link above to an extensive table of them. But some of the most common are:

`strlen(string)` returns the length

`str_replace(old, new, string)` returns the modified string with swapped characters

`strtolower(string)` and `strtoupper(string)` transform to lowercase and uppercase, respectively

`trim(string)` gets rid of spaces before and after (`' hi there  '` returns 'hi there')

## Sanitizing and validating inputs

To prevent users from injecting code into the HTML via input boxes or getting unwanted/incompatible inputs, these can be done:

### Sanitizing/filtering

```php
if(isset($_POST["login"]))
{
 # sanitizing special characters (that could mess with the HTML)
 $username = filter_input(INPUT_POST, "username", FILTER_SANITIZE_SPECIAL_CHARS);
 
 # filtering inputs and returning only integer values
 $age = filter_input(INPUT_POST, "age", FILTER_SANITIZE_NUMBER_INT);

 # filters out all the illegal characters for an email address
 $email = filter_input(INPUT_POST, "email", FILTER_SANITIZE_EMAIL);
}
```

### Validating

While `SANITIZE` filters characters, `VALIDATE` returns an empty value if the input is not valid.

```php
if(isset($_POST["login"]))
{
 $age = filter_input(INPUT_POST, "age", FILTER_VALIDATE_INT);

 $email = filter_input(INPUT_POST, "email", FILTER_VALIDATE_EMAIL);

 if (empty($age)) {
  echo "Invalid age";
 }

 if (empty($email)) {
  echo "Invalid email";
 }
}
```

## Importing other files: Include

In the following code, the HTML files are rendered on the same page:

```php
<?php
 include("header.html")
?>

# ...code for the body...

<?php
 include("footer.html")
?>
```

It's a good way to reutilize code over several pages!

## Cookies

Syntax

`setcookie(name, value, expire, path, domain, secure, httponly);`

Implementation

```php
setcookie("food", "pizza", time() + (86400 * 2), "/");
```

Printing all the cookies

```php
foreach($_COOKIE as $key => $value){
 echo"{$key} = {$value} <br>";
}
```

## Sessions
