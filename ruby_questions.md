
# Ruby Questions

#### What is a class?

A class is a blueprint/recipe from which an object is created. It contains both variables and methods. Classes can inherit other classes, and thus include their variables and methods. 

#### What is the difference between a class and a module?

A module holds a collection of methods that can be used across classes. It cannot be instantiated in the way a class can. Modules are added using the include keyword,
they cannot be inherited like classes.

#### What is an object?

An object is an instantiated class. It has a state and a set of behaviours. State is set by object variables and behaviour is set by object methods. Object variables are typically only modified via the objects methods, this process is called data encapsulation. 

#### How would you declare and use a constructor in Ruby?

```
	class Whatever
		def initialize(food,drink)
			@food=food
			@drink=drink
		end
	end
```		

Most languages have the “new” keyword which Ruby doesn’t have, instead it has the new method. Where Whatever.new(“pizza”,”coke") is used. 

#### How would you create getter and setter methods in Ruby?

attr_accessor:  variableName -creates getter and setter methods
attr_reader: variableName -creates getter methods only
attr_writer:  variableName -creates setter methods only

the above code creates the following
```
#a getter

def name
	@name
end

#setter
def name=(n)
	@name=n
end
```


#### Describe the difference between class and instance variables?

Class variables have only one copy which is shared between all the objects of a Class, whereas each object has its own copy of instance variables. 

#### What are the three levels of method access control for classes and what do they signify?

The three levels of method access control are private, protected and public. Private means the methods can only be accessed by the class itself. Protected means the methods can only b accessed by the class and any subclasses, and public mean that the methods can be accessed by everyone.

#### What does ‘self’ mean?

Self refers to the object that is currently being acted on. When you use self in a method definition ie. def self.updateScore() you are creating a class method. 

#### Explain how (almost) everything is an object in Ruby.

Ruby doesn’t have any primitives like other languages e.g. (int,char), everything that sits on the right hand side of an assignment statement will be an object. Also In ruby every statement or expression evaluates to a single object.

#### Explain what singleton methods are. What is Eigenclass in Ruby?


Ruby doesn’t have class methods so it uses singleton methods instead. Singleton methods are methods that live in the singleton class and are only available for a single object, unlike regular instance methods that are available to all instances of the class. A singleton method is a method that is defined on an instance as opposed to a method defined in a class where the method would be available on all instances.

Eigenclass is another name for the singleton class. 
```
	class << self
	#class methods here
	end
```


#### Describe Ruby method lookup path.

When you call a method Ruby has a specific sequence in how it searches for it.
First it looks to see if there are any singleton methods, then any modules which extends the singleton (rare), instance methods in a class, mixed in modules ( modules that have been included), before searching any parent classes for instance methods/modules until it reaches the top of the inheritance chain.

#### Describe available Ruby callbacks. How can we use them in practice?

A callback is a block of code, that is passed to a method as an argument. 

#### What is the difference between Proc and lambda?

Taken from Stack Overflow -> Short answer: What matters is what return does: lambda returns out of itself, and proc returns out of itself AND the function that called it.

What is less clear is why you want to use each. lambda is what we expect things should do in a functional programming sense. It is basically an anonymous method with the current scope automatically bound. Of the two, lambda is the one you should probably be using.

Proc, on the other hand, is really useful for implementing the language itself. For example you can implement "if" statements or "for" loops with them. Any return found in the proc will return out of the method that called it, not the just the "if" statement. This is how languages work, how "if" statements work, so my guess is Ruby uses this under the covers and they just exposed it because it seemed powerful.

You would only really need this if you are creating new language constructs like loops, if-else constructs, etc.








