# Basic Programming Styles

## Bare Words

0. Bare words are lowercase words with no special modifier in front of them. Example:
    * example = This is a bare word which is also a method.
0. The following are NOT bare words but introduce scope limitations (using Ruby syntax but applicable to
   other languages):
    * $example = Global variable
    * @@example = Class variable
    * @example = Instance variable
    * EXAMPLE = Constant variable
0. It is good design to use bare words as they allow for greater flexibility when enhancing/refactoring
   future code due to fewer scope limitations/complexities.

## Messages and Methods

0. Message - A name for a responsibility an object may have. In other words, you send a message to a collaborator
   (i.e. object) not a method.
0. Method - A named, concrete, implementation for which a responsibility may be fullfilled. There can be many methods
   for a single responsibility.

## Command-Query Separation (CQS)

* Specifies that methods should be categorized as follows:
    * **Queries**: Answer a result without changing the observable system state (i.e. no side side effects). Also means
      that queries can be chained (in any order) without consequences.
    * **Commands** (a.k.a. modifiers/mutators): Change the system state but do not answer a result.
* Caveats:
    * Adhering strictly to this principal makes popping values off a collection, for example, cumbersome because
      two steps are involved to answer the value to be removed AND changing the state of the collection. Being able
      simply *pop* a value off a collection (which answers the value and changes state) in one step is very convenient.

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

## Single Responsibility Pattern (SRP)

0. Should do the smallest possible useful thing.
0. Should be explainable in a sentence (it is code smell if the word "and" is used in a sentence).
0. Everything should be highly related to a single purpose.
0. Does not allow extraneous responsibilities to leak in.
0. Isolation allows change without consequence and reuse without duplication.

## Transparent, Reasonable, Usable, and Exemplary (TRUE)

0. Transparent - The consequences of change should be obvious in the code that is changing and in distant code that relies upon it.
0. Reasonable -The cost of any change should be proportional to the benefits the change achieves.
0. Usable - Existing code should be usable in new and unexpected contexts.
0. Exemplary - The code itself should encourage those who change it to perpetuate these qualities.

TRUE code not only meets today's needs but can also be changed to meet the needs of the future.

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

## Inheritance

0. Defines a parent/child relationship where behavior defined in the superclass is inherited/overwritable by the subclass.
0. Also known as automatic message delegation whereby messages received by the subclass automaticall bubble up to the
   superclass when not found in the subclass.

### Template Method Pattern

0. Basic object structure is defined by the superclass but overwritable by the subclass.
0. Methods defined in the subclass provide customized behavior which the superclass will message.
0. Useful for initializing similar objects with different default behavior.
0. Imposes sublcass requirements that is not obvious but can be illeviated by defining default methods in the
   superclass that raise NotImplementedError exceptions. NOTE: These exceptions should explain themselves by indicating
   why the exception was thrown via a useful error message. Example:

        raise NotImplementedError, "This #{self.class} cannot respond to:"

### Hook Method Pattern

0. Allows customized subclass method behavior without needing to know the abstract algorithm used by the superclass.
0. Each hook method is defined by the superclass but overwrittable by the subclass.
0. Most importantly, hook methods remove the need for subclasses to call the super method and reduces tight coupling
   between the subclass and superclass. Example:

        class Vehicle
          def initialize options = {}
            after_initialize options
          end

          def after_initialize options = {}
          end
        end

        class Truck < Vehicle
          def after_initialize options = {}
            options.reverse_merge! wheel_size: 10
          end
        end

## Resources

* [Ruby Tapas - Barewords (Episode 4)](http://www.rubytapas.com)
* [Ruby Tapas - Message and Method (Episode 11)](http://www.rubytapas.com)
* [Command-Query Separation](http://martinfowler.com/bliki/CommandQuerySeparation.html)
* [Practical Object-Oriented Design in Ruby: An Agile Primer](http://www.amazon.com/Practical-Object-Oriented-Design-Ruby-Addison-Wesley/dp/0321721330/ref=sr_1_1?ie=UTF8&qid=1375637328&sr=8-1&keywords=Sandy+Metz+Object) by Sandi Metz
