# Bonus: Blocks vs. Procs vs. Lambdas, a.k.a. "Closures" in Ruby

## What is a Closure?

A closure is a block of functional code with variables that are bound to the environment that the closure is called in.

A closure has a few important properties:

  * it can be passed around like an object (but that does not necessarily mean it is an object, as we'll discuss below),
  * a closure can be defined in one scope and be called in a completely different scope,
  * it remembers the variables within its scope at the time of creation; when it's called, it can access those variables even if they might not be in that current scope—meaning that a closure retains knowledge of its lexical environment at the time that it was defined.

## Blocks

Blocks are a simple form of a closure in Ruby. Unlike basically everything else in Ruby, **blocks are not objects**.

Blocks are constructed with a `do...end` or with `{}`. 

You should already be familiar with blocks from working with iterators and enumerators.

Here are two familiar examples of blocks:

The `.each` enumerator method accepts a block as an argument and calls the given block once for each element in the collection.

```ruby
array.each do |x|
  puts x
end

#or

array.each { |x| puts x } 
```

You might have seen this within an RSpec test; the `before(:each)` method is given a block to which it yields for each of the tests within the same context.

```ruby
before(:each) do 
  @language = "Ruby"
end
```

## Procs

Procs are a type of closure in Ruby that behave very similarly to blocks but with a few key differences:

  * a proc can be assigned to a local variable,
  * a proc instance is executed by calling the `call` method on it, and
  * more than one proc can be passed to a method.

But essentially, **a proc is a block turned into an object by being assigned to an instance of the Proc class.**

Therefore, the creation of a proc looks very similar to the instantiation of a class.

Here we're assigning a block to an instance of the Proc class and assigning it to a variable. Then we're calling the method `.call` on it:

```ruby
greeting = Proc.new { "Hello!" }

greeting.call
=> "Hello!"
```

Procs can also accept arguments that are passed into the `.call` method:

```ruby
greeting = Proc.new { |name| "Hello, #{name}!" }

greeting.call("Amanda")
=> "Hello, Amanda!"
```

## Lambdas

A lambda isn't that much different than a proc in functionality.

Here's a lambda being passed to the enumerator each. The `&` before it turns it into a block, which each expects as an argument.

```ruby
plus_one = lambda { |n| puts n + 1 }

array = [1, 2, 3]

array.each(&plus_one)
=> 2
=> 3
=> 4
```

A lambda can also be declared in this funny way:

```ruby
plus_one = ->(n) { puts n + 1 }
```

Lambdas and procs are used almost interchangeably, but there are a few differences between the two: 

* lambdas expect a certain amount of arguments and check for them; procs just returns `nil` for the missing argument, but do not throw an error
* they return differently: lambdas return to the calling method and procs return immediately without going back to the caller—essentially, lambdas behave more like method calls: you can think of them as anonymous functions

## Closing Thoughts

If this is confusing to you, particularly the procs and lambdas, don't worry! Procs and lambdas are awesome and enable you to write interesting, powerful code. However, day to day you won't be working with them a whole lot. Blocks, however, you will interact with every day. Focus on getting to know them the best.

## Resources

* [The Difference between Procs and Lambdas](http://www.skorks.com/2010/05/ruby-procs-and-lambdas-and-the-difference-between-them/)
* [Jim Weirich on Procs and Lambdas](https://gist.github.com/mislav/4508988)

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/ruby-closures-readme' title='Bonus: Blocks vs. Procs vs. Lambdas, a.k.a. "Closures" in Ruby'>Bonus: Blocks vs. Procs vs. Lambdas, a.k.a. "Closures" in Ruby</a> on Learn.co and start learning to code for free.</p>
