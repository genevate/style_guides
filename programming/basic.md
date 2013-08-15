# Basic Programming Styles

## The Law of Demeter (LoD)

0. Assume no knowledge of an object's internal structure.
0. A method can call other methods in its class directly.
0. A method can call methods on its own fields directly (but not on the fields' fields)
0. When a method takes parameters, the method can call methods on those parameters directly.
0. When a method creates local objects, that method can call methods on the local objects.
0. Chained messages can be sent to a target of similar types:
    0. Example: "example string".strip.upcase.reverse (i.e. string --> string --> string --> string)
0. Chained messages should not be sent to the target of different types:
    0. Bad: task.owner.full_name. (i.e. task --> owner --> string)
    0. Good: task.owner_full_name.

Resources:

  * [Demeter: It's not just a good idea. It's the law.](http://devblog.avdi.org/2011/07/05/demeter-its-not-just-a-good-idea-its-the-law)

## Single Responsibility Pattern (SRP)

0. Should do the smallest possible useful thing.
0. Should be explainable in a sentence (it is code smell if the word "and" is used in a sentence).
0. Everything should be highly related to a single purpose.
0. Does not allow extraneous responsibilities to leak in.
0. Isolation allows change without consequence and reuse without duplication.

Resources:

  * [Practical Object-Oriented Design in Ruby: An Agile Primer](http://www.amazon.com/Practical-Object-Oriented-Design-Ruby-Addison-Wesley/dp/0321721330/ref=sr_1_1?ie=UTF8&qid=1375637328&sr=8-1&keywords=Sandy+Metz+Object) by Sandi Metz

## Transparent, Reasonable, Usable, and Exemplary (TRUE)

0. Transparent - The consequences of change should be obvious in the code that is changing and in distant code that relies upon it.
0. Reasonable -The cost of any change should be proportional to the benefits the change achieves.
0. Usable - Existing code should be usable in new and unexpected contexts.
0. Exemplary - The code itself should encourage those who change it to perpetuate these qualities.

TRUE code not only meets today's needs but can also be changed to meet the needs of the future.

Resources:

  * [Practical Object-Oriented Design in Ruby: An Agile Primer](http://www.amazon.com/Practical-Object-Oriented-Design-Ruby-Addison-Wesley/dp/0321721330/ref=sr_1_1?ie=UTF8&qid=1375637328&sr=8-1&keywords=Sandy+Metz+Object) by Sandi Metz

## Recognizing Dependencies

An object has a dependency when it knows:

0. The name of another class.
    0. Solution: Dependency Injection. Inject an instance of the object via an argument rather than hard code the
        class/instance within the calling object.
0. The name of a message that it intends to send to someone other than self.
    0. Solution: Isolate external messages to a single method which can be messaged within the class. If anything
       changes with sending messages to the external object, only the one method needs to be refactored.
0. The arguments that a message requires.
    0. Solution: Use a hash as a single argument which can then set default values possibly making the argument list
       optional.
0. The order of those arguments.
    0. Solution: Use a hash as a single argument. Allows arguments to be passed in any order. If not a single hash then
       possibly use a required argument with a hash as the last argument for additional/optional arguments.

The goal is to keep as few dependencies as possible so that a class knows enough to do it's job and nothing else.

Resources:

  * [Practical Object-Oriented Design in Ruby: An Agile Primer](http://www.amazon.com/Practical-Object-Oriented-Design-Ruby-Addison-Wesley/dp/0321721330/ref=sr_1_1?ie=UTF8&qid=1375637328&sr=8-1&keywords=Sandy+Metz+Object) by Sandi Metz

