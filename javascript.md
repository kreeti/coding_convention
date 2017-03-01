# JavaScript

# Naming

* Variable declarations should always be made using var to not declare them as global variables.

  # Bad
  function sum(x, y) {
    result = x + y;
    return result;
  }

  # Good
  function sum(x, y) {
    var result = x + y;
    return result;
  }


* use camelCase for variables and functions.

* Constants (like PI) are written in UPPERCASE.

* JavaScript files should have a .js extension.

* Constructors intended for use UpperCamelCase.


# Syntax

* Always end a simple statement with a semicolon.

* In case of object use colon plus one space between each property and its value.

* In case of keys in object use quotes around string values, not around numeric values.

* Do not add a comma after the last property-value pair of an object.

* For understandability try to declare all variables at the top.

* To check both data type and values use '==='.

  # Bad
  var a = "5";
  var b = 5;

  if (a==b && typeof(a) == typeof(b)) {
    // do something
  }
  
  # Good
  var a = "5";
  var b = 5;

  if (a===b) {
    // do something  
  }

# Programming

* Use 2 space indentation.

* Always put spaces around operators ( = + - * / ), and after commas.

* Always put the opening brace on the same line as the previous statement.

  # Bad
  function func()
  {
    return
    {
      "name": "Xyz"
    };
  }  

  # Good
  function func () {
    return {
      "name": "Xyz"
    };
  }


* The closing brace should be on the same indent as the original function call.

  # Bad
  function func() {
    return {
             "name": "Xyz"
           };
  }

  # Good
  function func() {
    return {
      "name": "Xyz"
    };
  }

* Use ternary operator (`?:`) over `if/else` constructs for single line conditions.

* Don't use an empty line at the beginning or end of methods, blocks or conditionals.
  Use an empty line between methods, blocks and conditionals.

  # bad
  if some_condition {

    // do something
  }

  # good
  if some_condition {
    // do something
  }

  # bad
  [2, 3, 4].map( function check(x) { return x*2; })
  if some_condition {
    // do some thing
  }

  # good
  [2, 3, 4].map( function check(x) { return x*2; })

  if some_condition {
    // do some thing
  }


* When a conditional is too long to fit on one line, successive lines must be indented one extra level to distinguish them from the body.

  # bad
  if ( firstCondition() && secondCondition() &&
       thirdCondition() ) {
    doStuff();
  }

  # good
  if ( firstCondition() && secondCondition() &&
         thirdCondition() ) {
    doStuff();
  }


* Switch cases are allowed to share the same code block. 
  Example: 
  switch (some_condition) {
    case 4:
    case 5:
       // do something
       break; 
  }    

* Javascript array can have data of different data types.
  Example: 
  var a = [1,"a",2]; 

