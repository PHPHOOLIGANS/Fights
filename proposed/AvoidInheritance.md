Avoid Inheritance, Really, Please
=================================

Summary
-------

Inheritance is bad. It creates brittle connections, bound at write-time (before compile-time, if we had such a thing).
It adds API surface (extends allows access to protected stuff) that developers forget is an API. Everybody already
agrees that composition is better, use dependency injection. Use constructor-only dependency injection. Don't use service
locators, don't pass a DI object to a constructor.

PHP is not Java. Java is not OO. Java should not exist, use Scala instead if you must.

Re-But..tals
------------

- I actually have no idea why anyone still wants to do this... can't imagine.. sorry

In the wild
-----------

- Zend
- Symphony
- PHPStorm 8 and PHPUnit 4.6. Try it.
- PHPCR...

Elaboration
-----------

We've been using the OO paradigm now for almost 50 years. There is actually quite a bit of knowledge on what works, and
what doesn't. People have been saying stuff like 'SOLID' (look it up) for some time now. But what they all point to is
that inheritance makes for brittle software, software that is resistant to change. Whenever you create a class tree, you
create a taxonomy, usually a strictly hierarchical one. Any taxonomy is just one way of looking at things. Often the
first version of this is not even a any good. Yet once written and released, you cannot change it. Because others have
used your taxonomy and extended it. Now you are stuck.

We already have a better alternative, called composition. Instead of building on classes, you build on objects. (Yeah, I
know, those are bad too, but we can't get you over on our side in one big leap ) If you want to extend a class, use an
instance of that class as a DI (Dependencu Injection) parameter to the constructor of your 'extended' class. Pass
anything you don't change to this object and return the results. Use PHP's magic methods.

PHP actually has good support for OO programming, but this is not the OOP you think it is. Alan Kay, the inventor of the
term Object Oriented Programming and one of the main designers of SmallTalk, has this to say about what it is:

"I invented the term object-oriented, and I can tell you that C++ wasn't what I had in mind" - Alan Kay

"OOP to me means only messaging, local retention and protection and hiding of state-process, and extreme late binding of 
all things." - Alan Kay

Inheritance is not part of that. In fact inheritance breaks the 'late binding' part. DI does not. The messaging part is
also well supported by PHP through its magic methods. Any access to a property or call to a method of an object can be intercepted
and changed. You can in effect see these as 'messages' to an object. When you wrap and object and use PHP's magic methods,
you capture the message, open the envelope, read the contents, change it if needed, reseal the envelope and pass it on to
the wrapped object, without it knowing anything about it. Or without the calling object knowing anything about it. This
is a good thing, it allows you to create new functionality without either the calling object (or class) or the called object 
needing to be changed. This makes your code simpler and easy to change.

Rules of thumb
--------------

- treat 'extends' as a code smell
- inheritance trees deeper than two levels are just wrong
- final and private are your friend

