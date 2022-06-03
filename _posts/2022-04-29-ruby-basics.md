---
title:  "Ruby Basics"
image: assets/images/ruby-new.png
tags:
  - Ruby
---

In this article, we will get acquainted with the basic types of Ruby, consider the syntax and learn how to use them. 

All code will be entered in the interactive console - `irb`

### Ruby.new

Create new file **terminal.rb** with this code:

{% highlight ruby linenos %}
class Terminal
  attr_accessor :title
  
  def initialize(title = 'Awesome Term')
    @title = title
  end
  
  def run(command = nil)
    puts "Welcome to #{title}!"
    
    puts "Running your '#{command}' command..." if command
  end
end
{% endhighlight %}

**.rb** - is Ruby file extension

Now open the terminal and run `irb` command, you will see Ruby interactive command prompt. 

If you write `1 + 1` and press enter, Ruby will immediately execute your code and return the result:

{% highlight ruby %}
irb(main):001:0> 1 + 1
=> 2
{% endhighlight %}

Execute code from a file:

```ruby
irb(main)> require_relative 'terminal'

irb(main)> t1 = Terminal.new
irb(main)> t1.run 
=> Welcome to Awesome Term!

irb(main)> t2 = Terminal.new('Terminator')
irb(main)> t2.run
=> Welcome to Terminator!

irb(main)> t3 = Terminal.new
irb(main)> t3.title = "Just Term"
irb(main)> t3.run
=> Welcome to Just Term!

irb(main)> t4 = Terminal.new
irb(main)> t4.title = "Just Term"
irb(main)> t4.run("ls")
=> Welcome to Just Term!
=> Running your 'ls' command...
```

**require_relative** - Ruby method loads the file or library named *string* relative to the requiring file's path.

Class is a unique object in Ruby, we can declare it with a special keyword - **class**

```ruby 
def initialize (title)
```
- Is a special method in Ruby that allows us to specify the initial values of an object that we can transfer to 
```ruby
Terminal.new('My Term')
```

But the title argument is not stored anywhere yet.

You must assign a `@` variable for storage. (Instance Variables)

```ruby
class Terminal
  def initialize(title)
    @title = title
  end
end
```

> In the [first part](../install-ruby-with-asdf-on-fedora-linux) we installed Ruby in our system.

### Getters and Setters

Run `irb` and enter this code:

```ruby
class Terminal
 def initialize(title)
   @title = title
 end
end

irb(main)> Terminal.new("My Term")
```

In the console we will see what we got back:
```ruby
=> #<Terminal:0x00000000017be6b0 @title="My Term">
```

Call our Terminal object and get the title:

```ruby
irb(main)> t = Terminal.new('My Term')
irb(main)> puts t.title
```

**puts** - a method that returns values in the terminal for each new line.

Oops - we get an error...

```ruby
undefined method `title' for #<Terminal:0x0000000001667b40 @title="My Term"> (NoMethodError)
```

*Reason* - The object has no method title.

Create this method and return the title:

```ruby
class Terminal
 def initialize(title)
   @title = title
 end
  
 def title
   @title
 end
end
```

Once initialized we can use the title object as `@title`.

Let's call again:

```ruby
irb(main)> t = Terminal.new('My Term')
irb(main)> puts t.title
=> My Term
```

We can dynamically change the name:

```ruby
irb(main)> t = Terminal.new('My Term')
irb(main)> t.title = 'Some Term' 
irb(main)> puts t.title
=> Some Term
```

For this we need to add a new method
```ruby 
def title = (val)
```

New code looks like this:

```ruby
class Terminal

  def initialize(title)
    @title = title
  end
  
  def title
    @title
  end
  
  def title=(val)
    @title = val
  end
end

irb(main)> t = Terminal.new('My Term')
irb(main)> t.title = 'Some Term' 
irb(main)> puts t.title
=> Some Term
```

### **attr_reader**

To avoid always writing methods for initial values, Ruby has the method `attr_reader`:

```ruby
class Terminal
  attr_reader :title
  
  def initialize(title)
    @title = title
  end
end

irb(main)> t = Terminal.new('My Term')
irb(main)> puts t.title
=> My Term
```

### **attr_writer**

Instead of writing `def title = (val)` every time, Ruby has `attr_writer` method:

```ruby
class Terminal
  attr_reader :title
  attr_writer :title
  
  def initialize(title)
    @title = title
  end
end

irb(main)> t = Terminal.new
irb(main)> t.title = 'My New Term' 
irb(main)> puts t.title
=> My New Term
```

We can replace `attr_reader` and `attr_writer` with `attr_accessor`, which will add both actions. If they used, we no longer write the `@` symbol inside the object.

All methods that are in the object are called `Instance Methods`

### **method default value**

In the method we can define a default value:

```ruby
def initialize(title = 'Awesome Term')
end
```

If we didn't pass any value to the `Terminal.new`, the title would be set to "Awesome Term".

## Interpolation

Consider the method run (command = nil):

```ruby
def run(command = nil)
  puts "Welcome to #{title}!"
    
  puts "Running your '#{command}' command..." if command
end
```

Here we see an example of interpolation - `"# {any Ruby code here}”`

The `command` variable has a default value of nil, when something is passed in the method the code is called:

```ruby
puts "Running your '#{command}' command...
```

## Variables

```ruby
Local - name, age, lang
Instance - @name, @age, @lang
Class - @@name, @@age, @@lang
Global - $NAME, $AGE, $LANG
```

Variables can be of any type - string, array, tree, etc.

## **Strings**

```ruby
name = "Alex"
name = 'Alex'
```

With double quotes `""` - we can use interpolation, as well as special characters `\n` `\t` `\r`

```ruby
hello = "Hello,\nWorld"

puts hello
=> Hello,
=> World

hello = 'Hello,\nWorld'
puts hello

=> Hello,\nWorld
```

In single quotes, special characters don’t work, nor does interpolation. If there is a way, it is better to use single quotes `''`

```ruby
irb(main)> lang = 'ruby'

# Returns a new copy of the object
irb(main)> puts lang.upcase
=> RUBY

irb(main)> puts lang.capitalize
=> Ruby

irb(main)> puts lang
=> ruby

# If we want to directly change the lang object, we have to call it bang!
irb(main)> lang.upcase!

irb(main)> puts lang
=> Ruby

irb(main)> puts "Hello! " * 3
=> Hello! Hello! Hello!
```

### Concatenation

Concentration can be done by the `+` method.

```ruby
irb(main)> lang = 'ruby'
irb(main)> framework = "Rails"

irb(main)> new_str = lang.capitalize + ' on ' + framework

irb(main)> puts new_str
=> Ruby on Rails

irb(main)> puts new_str.length
=> 13

irb(main)> puts new_str.reverse
=> "sliaR no ybuR"

irb(main)> puts "#{lang} on #{framework}"
=> Ruby on Rails

irb(main)> str = 'Hello'
irb(main)> str = str + ', World'
irb(main)> puts str
=> Hello, World

# Short version
irb(main)> str = 'Hello'
irb(main)> str += ', World'
irb(main)> puts str
=> Hello, World
```

### **Integer and Float**

```ruby
irb(main)> counter = 300
irb(main)> counter = counter + 10
=> 310

irb(main)> counter += 100
=> 400

irb(main)> pi = 3.14

irb(main)> ten = 10
irb(main)> ten.to_f
=> 10.0
```

### Type Conversions

```ruby
irb(main)> age = "28"

irb(main)> puts age + 1
=> in '+': no implicit conversion of Integer into String (TypeError)

irb(main)> age = 28

irb(main)> puts age + "2"
=> in '+': String can't be coerced into Integer (TypeError)

irb(main)> age = 28

irb(main)> puts age + "1".to_i
=> 29

age = "28"
puts age + 1.to_s

=> 281
```

### **Symbols**

The symbols are identifiers, they have something in common with String.

```ruby
irb(main)> "hello".to_sym
=> :hello
```

Once stored in memory and does not change location in memory. The string always has a new address in memory.

```ruby
irb(main)> :hello.object_id
=> 2219548

irb(main)> :hello.object_id
=> 2219548

irb(main)> "hello".object_id
=> 280

irb(main)> "hello".object_id
=> 300
```

### **Boolean (FalseClass, TrueClass and NilClass)**

- `false` and `nil` are always **false**
- `true` and `0`, or *any variable* or object is **true**


### Array
A collection of different elements which can be of any type.

Array initialization:
```ruby
irb(main)> arr = []
irb(main)> arr = Array.new
irb(main)> arr = Array.new([])
irb(main)> arr = Array.new(nil)
irb(main)> arr = %w()
=> []

irb(main)> arr.class
=> Array
```

```ruby
irb(main)> [1, 2, "somestring"].length
=> 3

irb(main)> arr = ['Ruby', 'on', 'Rails', 7]
irb(main)> arr.join(' ')
=> Ruby on Rails 7
```

Array element indexes start at **0**
```ruby
irb(main)> arr = [1,2,3,4,5]

irb(main)> puts arr[0]
=> 1

irb(main)> puts arr[-1]
=> 5
```

If the array index is not found it returns nil
```ruby
irb(main)> arr = [1,2,3,4,5]
irb(main)> arr[9]
=> nil
```

Add to Array:
```ruby
irb(main)> arr = []
irb(main)> arr << 1
irb(main)> arr << 2
irb(main)> arr.push(9)
irb(main)> arr[5] = 10

irb(main)> puts arr

=> [1, 2, 9, nil, nil, 10] 

# Add to the beginning of the array
irb(main)> arr.unshift(5)
```

Remove from the array:
```ruby
irb(main)> arr = [1, 2, 3, 4, 5]

# Returns the last element and removes it from the array
irb(main)> arr.pop
=> 5

irb(main)> puts arr

=> [1, 2, 3, 4]

# Returns the first element and removes it from the array
irb(main)> arr.shift

=> 1

irb(main)> puts arr
=> [2, 3, 4]

irb(main)> arr = [1,2,3,4,5]

irb(main)> arr[0..3]

=> [1,2,3,4]
```


### Hash
A hash is a structure that is also called an associative array, but we can use any type of object in indexes.

The tree index name is unique.

Create a tree
```ruby
irb(main)> h = {}

irb(main)> h = Hash.new

# Hash default value
irb(main)> h = Hash.new(9)
irb(main)> h[:some_key]
=> 9
```

Return elements:
```ruby
irb(main)> h = {
irb(main)>   name: 'Alex',
irb(main)>   age: 28,
irb(main)>   langs: %w(Ruby Elixir Dart)
irb(main)> }

irb(main)> puts h[:name]
=> Alex

irb(main)> puts h[:age]
=> 28

irb(main)> puts h[:langs]
=> ['Ruby', 'Elixir', 'Dart']
```

Add new elements:
```ruby
irb(main)> h = {}

irb(main)> h[:name] = 'Alex'
irb(main)> h['age'] = 28

irb(main)> puts h
=> { :name => 'Alex', "age" => 28 }

irb(main)> puts h[:name]
=> Alex

# Returns nil because the key is stored as a string and we point to it as a symbol
irb(main)> puts h[:age]
=> nil

# key can be any object
irb(main)> h = { 1 => "one", 2 => "two" }

irb(main)> puts h[1]
=> one

irb(main)> puts [9]
=> nil
```

### Constants
Always starts with uppercase letters, the stored data does not change. (Changes but shows Ruby Warning)

```ruby
irb(main)> RUBY_VERSION = 3.0.1
irb(main)> SomeString = "hello"

irb(main)> SomeString = "changes"

=> warning: already initialized constant SomeString
```


### Range
```ruby
irb(main)> puts (1..10).to_a
=> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# include 5
irb(main)> (1..10) == 5
=> true
```


### Control Structures
**if** - is waiting for any object that will be true

```ruby
irb(main)> def check_version(version)
irb(main)>   if version > 2.6
irb(main)>     puts "Ok"
irb(main)>   elsif version >= 2.3 || version <= 2.5
irb(main)>     puts "Legacy"
irb(main)>   else
irb(main)>     puts "Very old"
irb(main)>   end
irb(main)> end
  
irb(main)> check_version(2.8)
=> Ok
```

**unless** - ends when it is false. (reverse version of if)

```ruby
irb(main)> is_eq = (1 == 2) # false

irb(main)> unless is_eq
irb(main)>   puts "enter unless block"
irb(main)> end

=> enter unless block
```

**case** - is a switch analog in other languages, but once entered in when it no longer goes to the next element.

```ruby
irb(main)> age = 28

irb(main)> case age
irb(main)>   when 1..18
irb(main)>     puts "<=18"
irb(main)>   when 19...31
irb(main)>   puts ">18"
irb(main)> else
irb(main)>   puts age
irb(main)> end

=> >18
```
