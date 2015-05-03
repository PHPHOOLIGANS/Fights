
# php hooligan manifesto

1. Program in the spirit of PHP.

  PHP is not Java, Ruby or Python. PHP just gets things done without looking pretty.
  PS. Looking pretty is not a bad thing as such.

2. Keep things simple. Don't be clever.

  Complexity is the real enemy of any programmer. So keep your code short and to the point, don't add things you don't need now (YAGNI - You Ain't Gonna Need It ). Seperate different concerns in different namespaces or classes.

3. Use basic types if you can, imitate them if you can't.

  Objects aren't bad by themselves, but they bring a lot of extra complexity. A string is just a string, not much extra to know about it. But what does a ParsedXML object do? If you need objects, e.g. to avoid parsing xml strings again and again, imitate the xml string by adding a __toString() method. Also try to code your public methods in such a way that they also accept xml as a simple string. This means that someone reading your code understands what is going on without having to understand the ParsedXML class.

  But remember that objects are always shared. When passing a string to a function, the string is passed by value. If you pass an object instead, it is passed by reference. This means that it is possible for any part of your application to sneakily change information in the passed objects. Therefore encapsulation isn't perfect and the complexity of your application will increase.

4. PHP is vaguely typed, embrace it.

  PHP is not a compiled language with compile-time type checking. So a lot of things that work in other languages don't make much sense in PHP. Instead of shoe-horning some kind of type-checking in PHP and getting only the drawbacks of both vague typing and runtime fatal errors for your effor, it is much better to embrace dynamic typing.

  Accept that your method may not get the type you need and you will only find it out at runtime. Convert anything that can logically be converted to what you need. Use duck-typing where possible.

  There is a nice convergence if you combine duck-typing with composition and dependency injection. Code becomes smaller, you will need less classes and there is no need for deep class hierarchies.

5. Don't try to make PHP do stuff its not designed for.

  You can write a daemon in PHP, but it's not the right tool for it. PHP is meant for the web, with a stateless request-response cycle. So memory usage and garbage collection is not an important issue, fast parse/compile times are.

  PHP is designed as a templating language with direct writes to the response. So while a Request object makes some sense, a Response object not so much. There's no way to force someone to use the Response object only and there are numerous libraries and built-in parts that aren't designed for it.

  Reflection shouldn't be used in production environments. It is a sign you are trying to do stuff PHP doesn't really want you to do. Don't try to be clever.

6. PHP scales almost forever, but it isn't fast.

  If you need performance, use a different language. If you need scalability, use PHP. Don't do micro optimization. You can use __call() and the other magic methods. Yes they will make your script slower, but so will any PHP statement you use. The important thing is scalability and maintainability, not performance. (Ok so performance has some role to play, just don't use it as a reason to add complexity.)

7. Design Patterns are a code smell.

    Most design patterns in use in PHP today have been copied more or less verbatim from Java design patterns. PHP isn't Java, Java design problems have java solutions. They fairly often don't match. Whenever I see a design pattern name in an identifier there is a good chance the design pattern has been used as a replacement for careful design not as a consequence of it.

8. Avoid deep class hierarchies.

  PHP isn't object oriented, but it does allow you to do object oriented design. Any programming language does, even C. PHP does provides some handy syntactic tools to help you implement an OO design. But PHP isn't particular, it also has parts that have a functional programming ancestry. It has even stuff that can be traced back to Javascript and to scheme and lisp before that. I think some parts might have even been influenced by Smalltalk.

  But the point is, if you want to do Object Oriented Programming, you start with objects, not classes. Classes aren't needed for OO, what you need are Encapsulation and Message Passing. Both these things can be achieved perfectly without any need for any kind of class hierarchy. In fact class inheritance makes your code more brittle, resistant to change, things break somewhere else when you change something here.

  So use dependency injection - composition over inheritance - which gives you runtime binding where class inheritance is 'compile'-time binding.
    Use private and - judiciously - final. Make your components into black boxes, keep the public API surface as small as possible. Prevent third-party inheritance where you can use composition and dependency injection instead.
    Use __call(), __get(), __exists(), etc. This is a real strength of PHP which I've only seen in Smalltalk before. Method calling is implemented as real message passing. An object can intercept any call made to it and respond. The environment (PHP) allows you to do this and this one thing allows you to implement many powerful ideas. You can proxy any other object perfectly, which again allows you to use Encapsulation to full effect and ties in with dependency injection for a powerful alliance.

9. Be inconsistent instead of incorrect or incompatible.

  PHP is inconsistent and this is good. PHP steals API's like no other language. Someone made a C api for X? PHP implements it almost verbatim. While PHP isn't C, the thing to remember is that the original developers of the C API probably knew their problem domain pretty well. They very probably made a fairly optimal API for C. While a PHP centered API would be nice, it's much less useful when it is implemented by someone less versed in the original problem domain. So stealing API's is good.

  PHP is inconsistent and it is good. The main project I work on started somewhere in 1998. I can find code in it that hasn't changed since 2000. PHP still runs it without a problem. PHP is backwards compatible to a fault. This means that over the years while it grew from a simple web templating language to its current role as most mainstream web application environment it has become inconsistent. But upgrading from PHP3 to 4 and then to 5 was very painless. Seeing the humble roots of PHP and the many people working on it over the years it is an unbelievable achievement that is often overlooked.

  As for the needle/haystack problem - string functions use haystack/needle, array functions use needle/haystack, remember it or learn to use an IDE.

10. As I said: steal, so here goes:

http://stackoverflow.com/questions/694246/how-is-php-done-the-right-way/694309#694309
http://thinkrelevance.com/blog/2007/05/17/design-patterns-are-code-smells
    http://michaelkimsal.com/blog/php-is-not-object-oriented/
http://stackoverflow.com/questions/49002/prefer-composition-over-inheritance/53354#53354
http://www.codinghorror.com/blog/2007/05/the-best-code-is-no-code-at-all.html

11. Keep up to date

    ( yes - PHP Hooligans go to 11 )
    PHP is ever changing and improving (mostly). So read the blogs and announcements, go join a community and have strong opinions loosely held, learn and keep learning.
    http://www.planet-php.org/
    http://www.php-developer.org/
    http://www.php.net/ ( see the upcoming events and the news )
