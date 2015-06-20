Object To Objects
=================

Summary
-------

Objects are always passed by reference, not by value. This means you always have shared state when passing objects around.
Shared state is one of the main culprits for unnecessary or incidental complexity. Complexity is bad.

re-But...tals
-------------

- "But I use value objects!" Good for you, that is not actually OOP though.

- "But all my objects are immutable." Yup, same as value objects. See above.

- "OOP is the future!". Carnegie Melloin disagrees, they don't actually offer OOP as a course anymore. OO Design does 
  have merit. But you should probably check out this Functional Programming thing.

In the wild
-----------

- [DateTime](http://php.net/manual/en/class.datetimeimmutable.php), part of PHP. There is now also an ImmutableDateTime. Guess why.

- [PSR-7: URI interface](http://www.php-fig.org/psr/psr-7/#3.5-psr\http\message\uriinterface) ->withPort(80) - this is good.

Elaboration
-----------

Complexity is the main problem with software development. It is always better to keep things simple. Simple is not easy.
It may be more difficult to understand or longer to type. But a simple solution means less ties, less connections to
other parts of a program. We already know this. That is why global variables are considered bad, any part of your program
can change one and a totally unrelated part ( or so you thought ) will suddenly behave differently. This is also why we
use dependency injection ( note: not service locators, there is a difference ).

Using basic types PHP gives you a great boon, called 'pass by value'. So if I call a function with a variable and the 
function changes that variable and returns, your variable hasn't changed. The function changed its own internal copy of 
the variable. Whatever happens inside the function is of no concern to you. You can use the function as a black box. This works
for booleans, integers, floats, strings and even arrays. *But not for objects*.

Objects are always passed by reference (Well.. actually it's something almost like a reference but slightly different, 
doesn't matter for this case). This means that if you pass objects as arguments, the object can be changed by the function
without your intention or knowledge. One of the more surprising examples is calling a 'print' method that takes a 
DateTime object as argument. The naive implementation then sets a timezone in the DateTime object to make sure that
you print it correctly and then returns. Now your timezone is changed. This is why they made a ImmutableDateTime. Instead
you could also just use an integer, unix has been doing this successfully for some time now.

Does this mean I should never use objects? No, it doesn't. Objects and classes do give you room to structure your program
better and make it simpler. But you should use these rules of thumb:

- Parameters to any function are method should be basic types
- If you absolutely must have an object as parameter, make sure it is immutable. Or better yet, have (static) transformation
  functions that create a new instance for each change, making the objects immutable value objects and you can almost
  have polymorphism a la carte.
- If you can't have it be immutable, redesign your program
- If you can't do that ( it happens ), make it explicit
