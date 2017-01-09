# Ruby

## Syntax

* Never use `for`, unless you know exactly why. You can use `each` instead of `for`.

  ```ruby
  arr = [1, 2, 3]

  # bad
  for element in arr do
    puts element
  end

  # good
  arr.each { |element| puts element }
  ```

* Never use `then` for multi-line `if/unless`
  
  ```ruby
  # bad
  if some_condition then
    # do something
  end

  #good
  if some_condition
    # do something
  end
  ```

* Use ternary operator (`?:`) over `if/then/else/end` constructs for single line conditions.

  ```ruby
  # bad
  result = if some_condition then something else something_else end

  # good
  result = some_condition ? something : something_else
  ```

* Always use `&&` and `||` instead of `and` and `or` keywords.

* Avoid multi-line `?:`(ternary operator), use `if/unless` instead.

* For single `if/unless` bolck write it in a single line.

  ```ruby
  # bad
  if some_condition
    do_something
  end

  # good
  do_something if some_condition
  ```

* Never use `unless` with `else`. Write it inside `if-else` block
  
  ```ruby 
  # bad
  unless success?
    puts "failure"
  else
    puts "success"
  end

  # good
  if success?
    puts "success"
  else
    puts "failure"
  end
  ```

* Do not use parentheses around the condition of an `if/unless/while`.

  ```ruby
  # bad
  if (x > 5)
    # do something
  end
  
  # good
  if x > 5
    # do something
  end
  ```

* Avoid `return` where not required.
 
  ```ruby
  # bad
  def some_method(arr)
    return arr.size
  end
    
  # good
  def some_method(arr)
    arr.size
  end
  ```

* use `%w` freely.

  ```ruby
  # bad
  arr = ["one", "two", "three"]
  
  # good
  arr = %w(one two three)
  ```

## Naming

* use `snake_case` for methods and variables.

* use `CamelCase` for classes and modules.

* Constants are written in all uppercase with underscores to separate words. like: `A_CONST`

  
