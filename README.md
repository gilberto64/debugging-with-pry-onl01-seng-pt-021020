ruby# Debugging with Pry

## Overview

We'll cover Pry, a type of REPL, and discuss how to install and use it to debug a program. 

## Objectives

1. Explain how Pry is a more flexible REPL than IRB. 
2. Install Pry on your computer. (already installed for IDE users)
3. Debug a program using binding.pry within the body of your file.

## What Is a REPL
 =>  7:     binding.pry
     8:     this_variable_hasnt_been_interpreted_yet = "The program froze before it could read me!" 
     9:     puts this_variable_hasnt_been_interpreted_yet
    10: end
[1] pry(main)> 
```

You have frozen your program *as it executes* and are now inside a REPL *inside your program*. You basically just stopped time! How cool is that?

5. In the terminal, in your pry console, type the variable name `inside_the_method` and hit enter. You should see a return value of `"We're inside the method"`

You are actually able to explore and manipulate the data *inside* the method in which you've placed your binding. 

Now, in the terminal, in your pry console, type the variable name `this_variable_hasnt_been_interpreted_yet`. You should see a return value of `nil`. That's because the binding you placed on line 7 actually froze the program on line 7 and the variable you just called hasn't been interpreted yet. Consequently, our REPL doesn't know about it. 
Now, in the terminal, type `exit`, and you'll leave your pry console and the program will continue to execute. 

## Instructions Part II: Using Pry to Debug

You can imagine how helpful it will be to use Pry to freeze programs and to "pry" methods open in order to solve tests and debug your code. Let's walk through an example together. In this repository that you've forked and cloned down onto your computer, you'll see a `spec` folder containing a file `pry_debugging_spec.rb`. This is a test for the file `lib/pry_debugging.rb`. 

In `pry_debugging.rb`, we have a broken method. Run `learn` to see the failing test. 

Oh no! A broken program! Luckily, we have Pry required at the top of our `spec/pry_debugging_spec.rb` file, and we know how to use it. Let's place a `binding.pry` right before the `end` keyword like this. 

```ruby
def plus_two(num)
    num + 2
    num 
    binding.pry
end
```

Now, run the test suite again and drop into your Pry console. Your terminal should look like this: 

```ruby
From: /Users/sophiedebenedetto/Desktop/Dev/Ruby-Methods_and_Variables/pry-readme/lib/pry_debugging.rb @ line 4 Object#plus_two:

    1: def plus_two(num)
    2:  num + 2
    3:  num 
 => 4:  binding.pry
    5: end

[1] pry(#<RSpec::ExampleGroups::PlusTwo>)>
```

The test is calling our `plus_two` method with the argument, `num`,  the value of `num` set to `3`, and the expected return value of `5`. We remember that the return value of a method in Ruby is generally the value of the last line of the method. Let's check our current return value by typing `num` into our Pry console. You should see something like this: 

```ruby
[1] pry(#<RSpec::ExampleGroups::PlusTwo>)> num
=> 3
[2] pry(#<RSpec::ExampleGroups::PlusTwo>)> 
```

By checking the value of the variable on the last line of our method inside our pry console, we can see that `num` is set to `3` and therefore the method is returning `3`. 

How can we fix this method so that it behaves in the expected way? This method is called `plus_two` and the test is expecting a return value of `5`, given a `num` of `3`. Looks like our method should return the *sum* of the original number (`3`) plus 2. But our method, as it currently stands, is returning the original number. Play around with it inside your Pry console and get the test to pass. Remember to type `exit` in your terminal and then remove your `binding.pry` when you think your test will pass. 

Once you have your test passing, make sure the `binding.pry` line has been removed and add commit and push your changes. Then open a pull request. 


## Resources 

* [Pry documentation](http://pryrepl.org/)

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/debugging-with-pry' title='Debugging with Pry'>Debugging with Pry</a> on Learn.co and start learning to code for free.</p>
