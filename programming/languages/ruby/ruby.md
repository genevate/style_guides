# Ruby Styles

## General

- Use spaces around operators:

        # No
        a=1+2
        a,b=1,2
        a>b ? true : false

        # Yes
        a = 1 + 2
        a, b = 1, 2
        a > b ? true : false
- Avoid inheritance (not always necessary, except in rare cases). Use modules instead.

## Variables

- Use `snake_case` for variable names.
- Avoid the following global variables since it makes code harder to read and maintain (NOTE: if globals are used,
  ensure the longer aliases are used instead of the crpytic shortcuts):
    - $/ - Input record separator. Alias: $INPUT_RECORD_SEPARATOR. Default: newline.
    - $. - Current input line number of the last file read. Alias: $INPUT_LINE_NUMBER.
    - $\ - Output record separator. Alias: $OUTPUT_RECORD_SEPARATOR. Default: nil.
    - $; - String#split default field separator. Alias: $FIELD_SEPARATOR.
    - $, - Output field separator. Alias: $OUTPUT_FIELD_SEPARATOR.
    - _$ - Input variable for each object within an IO loop.
    - $! - Last exception thrown. Alias: $ERROR_INFO.
    - $@ - Backtrace array of last exception thrown. Alias: $ERROR_POSITION.
    - $& - String match of last successful pattern match for current scope. Alias: $MATCH.
    - $` - String to the left of last successful match. Alias: $PREMATCH.
    - $' - String to the right of last successful match. Alias: $POSTMATCH.
    - $+ - Last bracket matched by the last successful match. Alias: $LAST_PAREN_MATCH.
    - $<n> - nth group of last successful regexp match.
    - $~ - Last match info for current scope. Alias: $LAST_MATCH_INFO.
    - $< - Object access to the concatenation of all file contents given as command-line arguments. Alias: $DEFAULT_INPUT.
    - $> - Output destination of Kernel.print and Kernel.printf. Alias: $DEFAULT_OUTPUT. Default: $stdout.
    - $_ - Last input line of string by gets or readline. Alias: $LAST_READ_LINE.
    - $0 - Name of the script being executed. Alias: $PROGRAM_NAME.
    - $- - Command line arguments given for script. Alias: $ARGV.
    - $$ - Ruby process number of current script. Alias: $PROCESS_ID or $PID.
    - $? - Status of the last executed child process. Alias: $CHILD_STATUS.
    - $: - Load path for scripts and binary modules via load or require. Alias: $LOAD_PATH.
    - $" - Array of module names as loaded by require. Alias: $LOADED_FEATURES.
    - $-d - Status of the -d switch. Alias: $DEBUG.
    - $-K - Source code character encoding being used. Alias: $KCODE.
    - $-v - Verbose flag (as set by the -v switch). Alias: $VERBOSE.
    - $-a - True if option -a ("autosplit" mode) is set.
    - $-i - In-place-edit mode. Holds the extension if true, otherwise nil.
    - $-l - True if option -l is set ("line-ending processing" is on).
    - $-p - True if option -p is set ("loop" mode is on).
    - $-w - True if option -w is set (Ruby warnings).
    - $stdin - Current standard input.
    - $stdout - Current standard output.
    - $stderr - Current standard error output.

## Constants

- Use `SCREAMING_SNAKE_CASE` for constant names.
- Use the following global constants:
    - \_\_FILE__ - Current file.
    - \_\_LINE__ - Current line.
    - \_\_dir__ - Current directory.
    - ARGF - IO stream for processing files, given as command-line arguments, via a script.

## Shortcuts

- Use the following global shortcuts:
    - %() - Yields an interpolated, quoted string.
        `%(Example Says: #{message}) # => "Example Says: Hello!"`
    - %Q() - Same behavior as %().
    - %q() - Yields a non-interpolated, quoted string.
        `%q(One Two Three) # => "One Two Three"`
    - %W() - Yields an interpolated string array.
        `%W(one two, #{three}) # => ["one", "two", "three"]`
    - %w() - Yields a non-interpolated string array.
        `%w(one two, three) # => ["one", "two", "three"]`
    - %r() - Yields an interpolated regular expression.
        `%r(one|#{two}) # => /one|two/`
    - %s() - Yields a non-interpolated symbol.
        `%s(test) # => :test`
    - %I() - Yields an interpolated symbol array.
        `%I(one two #{three}) # => [:one, :two, :three]`
    - %i() - Yields a non-interpolated symbol array.
        `%i(one two three) # => [:one, :two, :three]`
    - %x() - Executes an interpolated system command (does not echo to STDOUT or return the running command's result).
        `%x(echo #{message}) # => "Huzzah!"`

## Splats

- Commonly used in method and/or block arguments.
- Can be used to slurp collections into a variable on the left side of an assigment (a.k.a. *multiple assignment*):

        a = %i(one two three four five)

        *b, c, d = *a # => b == [:one, :two, :three], c == :four, d == :five
        b, *c, d = *a # => b == :one, c == [:two, :three, :four], d == :five
        b, c, *d = *a # => b == :one, c == :two, d == [:three, :four, :five]
- Multiple assignment should generally be avoided as it makes code harder to read, maintain, and modify.
    - In rare cases, multiple assignment is acceptable in the following situations:
        - Variable swaping. Example: `a, b = b, a`
        - Related variables assignment. Example: `lat, long = x, y`
- Can be used to expand collections on the right side of an assignment (a.k.a. *destructuring*):

        a1 = %i(one two three)
        a2 = %w(red black white)

        a, b, c = *a1 # => a == :one, b == :two, c == :three
        a, b, c = :insert, *a1 # => a == :insert, b == :one, c == :two
        [*a1, *a2] = # => [:one, :two, :three, "red", "black", "white"]
- Use explicit over implicit splatting as implicit splatting assumes an object behaves like an Array. Example:

        a = :one, :two, :three # => a == [:one, :two, :three]
- Any object that responds to the #to_ary method can be used in an implicit splat.
- Splats can be grouped (handy in block arguments) which allows for values of an array to be auto-assigned to variables
  without having to use an intermediate variable to do the same thing. Example:

        vehicles = {"Volkswagen" => "New Beetle"}
        vehicles.each {|(make, model)| puts "Make: #{make}, Model: #{model}"} # => "Make: Volkswagen, Model: New Beetle"
- Use a naked splat (*) when defining arguments to be ignored (useful in subclass contructors as well). Example:

        def example required, *
          puts "Required argument is: #{required}."
        end

        example 1, 2, 3, 4, 5 # => "Required argument is: 1"
- Use a double naked splat (**) with keyword arguments to assign additional options to a named hash (WARNING: Should
  be avoided in most cases but can be useful in supporting legacy code backwards compatibility). Example:

        def example string, keyword_1: 1, keyword_2: 2, **options
          puts "Additional Options are: #{options.inspect}."
        end

        example "test", extra_1: "one", extra_2: "two" # => Additional Options are: {:extra_1=>"one", :extra_2=>"two"}.
- Use a double naked underscore splat (**_) with keyword arguments to ignore additional options to a named hash (WARNING: Should
  be avoided in most cases but can be useful in supporting legacy code backwards compatibility and/or testing). Example:

        def example keyword_1: 1, keyword_2: 2, **_
        end

        example extra_1: "one", extra_2: "two" # => Both of the "extra_*" arguments are completely ignored in this case.

## Assigments

- Use inline assigment, with parentheses, in loop conditions to keep code concise. Example:

        lines = 0
        while(chunk = file.read(1024))
          lines += chunk.count "\n"
        end
  The use of parentheses indicates that the *chunk- assigment is intentional and avoids the confusion of thinking that
  the assigment (=) was not meant to be an equals (==).

## Arguments

- Use _ to ignore an argument or multiple arguments. Example:

        a = [%w(Mr. Billy Bob Simpson), %w(Mrs. Sally Jane Ruffy)]
        a.map { |_, first, _, last| [first, last] } # =>  [["Billy", "Simpson"], ["Sally", "Ruffy"]]
- When using ambiguous arguments, that don't clearly express their intent, define a local variable instead. Example:

        include_super = false
        String.instance_methods include_super

- Use `key:,` to enforce a keyword argument:

        def example first_name:, last_name: "Grant"
          puts [first_name, last_name].compact - ' '
        end

        example last_name: "Smith" # => ArgumentError: missing keyword: first_name
- Use keyword arguments instead of option hashes so that an ArgumentError is thrown for unknown keywords:

        def say name, prefix: "Hello"
          puts "#{prefix} #{name}"
        end

        example "Bob", bogus: "Foo" # => ArgumentError: unknown keyword: bogus

## Booleans

- Avoid using `!!` to convert an object to a boolean.
- Remove spaces after !:

        !example

## Characters

- Use double quotes for a single characters: `"a"`.

## Numbers

- In most situations, it is important to use `Integer(value)` instead of `value.to_i` when converting a possible
  non-integer value into an integer. The former will throw an exception, the latter will not (yields zero instead).
  Example:

        value = "example"
        Integer(value) # => ArgumentError: invalid value for Integer(): "example"
        value.to_i # => 0
  This pattern applies to Floats as well.
- Use `#to_i` for explicit conversion of an object to an integer. Useful when forcing an object to convert to an
  integer. Example: "1234".to_i.
- Use `#to_int` for implicit conversion of an object to an integer. Useful when building an object that might need to
  behave like an integer. Ruby calls `#to_int` when processing objects that behave like integers.
- Literals can be used for shorthand representations of different numbers:
    - `0x22 = 34` (Integer, hexadecimal, 0-16 format)
    - `0o22 = 18` (Integer, octal, 0-8 format)
    - `0b11 = 3` (Integer, binary, 0-1 format)
    - `1e11 = 100000000000.0` (Float, exponential notation)
    - `11i = (0+11i)` (Complex)
    - `3/6r = (1/2)` (Rational)
    - `2_2 = 22` (any, the "_" is used to visual separate/delimit numbers)

## Strings

- Use double quotes for strings: `"example"`
- Use [] to parse substrings. Example:

        song = "05 - Misty Mountain Hop"
        song[5, song.length] # => "Misty Mountain Hop"
- Use [0,0] to prepend to a string. Example:

        song = "Misty Mountain Hop"
        song[0,0] = "05 - "
        song # => "05 - Misty Mountain Hop"
- Use [] with a regular expression to parse a substring. Example:

        song = "05 - Misty Mountain Hop"
        song[/M.+n/] # => "Misty Mountain"
- Use [] with a regular expression and a second argument to parse substring group. Example:

        song = "05 - Misty Mountain Hop"
        song[/^\d{2} - (.+)/, 1] # => "Misty Mountain Hop"
- Use [] with a regular expression and named groups to parse a substring group. Example:

        song = "05 - Misty Mountain Hop"
        song[/^(?<track>\d{2})(?<delimiter> - )(?<title>.+)/, :title] # => "Misty Mountain Hop"

## Enumerables

- Use `.with_index` instead of `.(each|map|select|etc)_with_index` as the `.with_index` syntax can easily be chained
  to existing enumerable objects. Example: `example.each.with_index { |target, index| puts "#{index}: #{target}" }`.

- Use `.with_object` instead of `.(each|map|select|etc)_with_object` as the `.with_object` syntax can easily be chained
  to existing enumerable objects. Example: `example.each.with_object("Test") { |target, object| puts "#{object}: #{target}" }`.

## Arrays

- Avoid spaces around brackets []:

        # No
        example = [ 1, 2, 3 ]

        # Yes
        example = [1, 2, 3]
- Use `%w(one two three)` instead of `[“one”, “two”, “three"]` when building an array of strings.
- Use `Array` when dealing with a collection that might be nil:

        # No
        params[:ids] = nil
        if params[:ids]
          params[:ids].each { |id| # Process. }
        end

        # Yes
        Array(params[:ids]).each { |id| # Process. } # If :ids is nil, then it will be converted to an empty array.
- Use `Set` instead of `Array` when managing unique elements. `Set` is a hybrid of Array's inter-operation
  capabilities and Hash's fast lookup.
- Use Array#concat when concatenating arrays. It is faster than using `<<` and `.flatten!` or using `+=`. It also
  updates the target array in place whereas `+=` will create a new array object of the concatenated source arrays.
- Use Array#reduce with an initial value so that empty arrays don't evaluate to nil (especially with numbers):

        # No
        [].reduce(:+) # => Evaluates to nil.

        # Yes
        [].reduce(0, :+) # => Evaluates to 0.
- Use `#to_a` for explicit conversion of an object to an array. Useful when forcing an object to convert to an
  array. Example: `(1..10).to_a`.
- Use `#to_ary` for implicit conversion of an object to an array. Useful when building an object that might need to
  behave like an array. Ruby calls `#to_ary` when processing objects that behave like arrays.

## Hashes

- Use symbols for keys: `{a: “one”, b: “two”, c: “three"}`.
- Avoid spaces when defining a hash:

        # No
        example = { key: "value" }

        # Yes
        example = {key: "value"}
- Indent and list one key per line when too long to define in a single line:

        {
          make: "BMW",
          model: "R1200GST",
          year: 2014,
          color: "Black/Black",
          mileage: 30_000
        }
- Use blocks when setting default values:

        # Will use the same array object for each new key.
        Hash.new []

        # Will initialize a new array object for each new key.
        Hash.new {|hash, key| hash[key] = []}
- Use `#fetch` when setting default values for missing keys instead of `||` as `||` will answer the default value when a
  key doesn't exist or has a value of nil/false. Example:

        {}[:example] || :default # :default
        {example: nil}[:example] || :default # :default
        {example: false}[:example] || :default # :default

        {}.fetch(:example) { :default } # :default
        {example: nil}.fetch(:example)  { :default } # nil
        {example: false}.fetch(:example) { :default } # false
- Use a block instead of a value for the default (second) argument of `#fetch`. This provides the following benefits:
    0. Blocks can be defined once for easy reference in multiple defaults (DRY).
    0. Blocks are lazy evaluated which improves application performance.
- Use symbols as default values for Hash#fetch. This will make it easier to debug when a value is expected but not
  supplied. Example: `example.fetch(:logger) { :unknown_logger }`.

## Loops

- Use `begin..end while <condition>` in lieu of a do while loop (it is the equivalent in Ruby).
- Use `<number>.times.map` instead of `(0...<number>).map` as it reads better and requires less setup.
- Use `each do..end` instead of `for in do..end` since `for` doesn't introduce a new scope and uses `each` under
  the covers. Additionally, `each` is more concise.
- Use `loop do...end` instead of `while true do...end` for infinite loops as it expresses intent and is idiomatic.

## Breaks

- The obvious use for breaks are to exit quickly out of a loop once a particular condition is met but they can also
  be used to return a value:

        break "Example Message" if some_value == "found"

## Control Flow

- Use `and` and `or` sparingly and for control flow only since they have lesser precidence than their `&&` and `||`
  counterparts. Additionally, `and` and `or` do not evaluate to a return value like `&&` and `||` (hence their
  significance for control flow).
- Use the ternary operator for one-liners:

        a > b ? "Yep" : "Nope"

- Use the ternary operator with a single expression per branch only:

        # No
        a > b ? (a - 2 + 1000) : message_y(message_x(b))

        # Yes
        a > b ? "Yep" : "Nope"
- Use if..else..end (not the ternary operator) for complex multi-line expressions:

        if condition
          ...
        else
          ...
        end
- Never use `unless..else..end`, use `if..else..end` instead.
- Avoid using parentheses around conditions:

        # No
        if (n > 5)
        end

        # Yes
        if n > 10
        end

## Cases

- Indent `when` statements:

        case status_code
          when 100..199 then "informational"
          when 200..299 then "success"
          when 300..399 then "redirection"
          when 400..499 then "client error"
          when 500..599 then "server error"
          else
            "unknown"
        end
- Use lambda's in `when` statements when needing to evaluate code since lambda's alias the `===` method to the `call`
  method.

## Blocks

- Use braces, with spaces between each brace, for one-liners:

        (1..5).detect { |item| item == 2 }
- Use `do..end` for multi-liners:

        %w(one two three).map do |word|
          ...
          ...
        end

*NOTE: `do…end` blocks have a higher precedence over `{…}` blocks*

## Procs

- Disregards extra arguments without error.
- Returns from the scope of the bounded object (i.e. returns from the scope of the object in which the proc was defined).
- Use `proc` instead of `Proc.new` as provided by the Kernel module.
- Procs can be called the following ways (the first option, however, is more readable):
    - example.call "hello"
    - example["hello"]
    - example.("hello")
- The `===` method which calls `call` is useful when used as a predicate in case statements.

## Lambdas

- Respects defined arguments and throws errors if extra arguments are not defined.
- Returns from the scope of the lambda, not the bounded object in which it was defined.
- Use lambdas, by default, over procs.
- Lambda can be defined via `lambda` or `->`. The latter is preferred.

## Exceptions

- Use `fail` to throw new exceptions and `raise` to re-throw an exception within another exception. NOTE: Both `fail`
  and `raise` are synonyms but using them in context can help give special meaning/readability to the code. This was
  a pattern introduced by [Jim Weirich](https://en.wikipedia.org/wiki/Jim_Weirich).
- Don't rescue Exception, rescue StandardError instead. Exception catches all exception types including SyntaxError,
  LoadError, NoMemoryError, Interrupt (i.e. CONTROL+C), etc. which is usually not what you want.
- Avoid using inline rescue statements (can be useful when converting exceptions into return values, however). Example:

        def example
          bad_method rescue $!
        end
- Avoid using exceptions for control flow. Use catch and throw instead. Example:

        # No
        begin
          22 / 0
        rescue ZeroDivisionError
          puts "Wait, what? You divided by zero!?!"
        end

        # Yes
        def thrower
          ...
          throw :complete
        end

        def catcher
          ...
          # Exit early if :complete is caught while attempting to perform work.
          catch(:complete) do
            thrower
          end
        end
- Use top-level rescue clauses when dealing with exceptions:

        # No
        def example
          # Do work.
          begin
            # Do suspicious work.
          rescue StandardError
            # Do exception.
          end
        end

        # Yes
        def example
          # Do positive work.
        rescue StandardError
          # Do negative work.
        end

## Debugging

- Use `p` instead of `puts` when debugging. Reasons:
    - Returns the value given - makes printing of inline values possible while not obstructing control flow.
    - Inspects by default (i.e. which is the same as `puts some_object.inspect`).
- Use `pp` to pretty print objects when debugging. Is part of the standard library, so make sure to `require "pp"`.
  Additionally, the #pretty_print method allows objects to generate a pretty printed version of themselves for storage
  within a local variable for later inspection if necessary.

## Objects

### General

- Use `Object#tap` to communicate that the method subject is also the object being returned. It also serves as a concise
  way to modify and return and object within a single step.

        # No
        def update_params params
          params[:example] = "Example"
          params
        end

        # Yes
        def update_params params
          params.tap { |param| param[:example ] = "Example" }
        end

### Comparing Objects

- When defining the `<=>` method for an object, make sure to check for type:

        def <=>(other)
          return nil unless other.is_a?(self.class)
          some_method <=> other.some_method
        end

### Value Objects

- Follows value semantics rather than reference semantics.
- Must be immutable.
- Defines `#==` (value equality) to be equivalent to itself and other instances of same values.
  - It must check that the class (type) of the other object is identical before checking it's values.
  - It must not be equivalent to other instances of different values or classes (types).
- Defines `#===` (case equality) to behave identically to `#==` (make it an alias of `#==`).
- Defines `#eql?` (hash equality) to behave identically to `#==` (make it an alias of `#==`). This is important when
  using an instance as a hash key.
- Defines `#equal?` (identity equality) as equal only to itself.
- Defines `#hash` to use value equality (state of all values) plus class to produce a unique hash.
- Consider using the [Adamantium](https://github.com/dkubb/adamantium) gem when building value objects.

## Modules

- Modules allow code to be namespaced.
- When defining modules, use nesting instead of shorthand:

          # No
          module ParentModule::ChildModule
            Module.nesting # => [ParentModule::ChildModule]
          end

          # Yes
          module ParentModule
            module ChildModule
              Module.nesting # => [ParentModule::ChildModule, ParentModule]
            end
          end
    - When nested, you maintain hierarchy and constant/method lookup within the hierarchy. Using the shorthand
      would cause constants, for example, defined in the *ParentModule- to not be found and makes debugging any related
      errors much harder.
- Use `module_function` to mark methods in a module that will be private instance methods when included in a class.
  These methods can also be accessed as class level methods via the module. This allows classes to include module
  methods when all or many of the methods are needed by the class but also allows classes to simply reference the module
  directly when only a few of the methods are required.
- Submodles can include containing modules. Example:

        module Outer
          module Inner
            include Outer
          end
        end

## Structs

- Avoid using `Struct.new(...).new(...)` for creating a new instance of an anonymous class as it suffers a serious
  [performance penalty](https://pragtob.wordpress.com/2016/04/12/dont-you-struct-new-new). Use a `class` instead
  to contantize and properly name an object like this.

## Classes

- Use `CamelCase` for class names.
- Never use `@@` class variables since the inheritance hierarchy uses the same variable. Example: `@@variable`.
- When implementing an abstract class, throw a NotImplementedError (inherits from RuntimeError) for methods that
  need to be implimented by a subclass. This will, in turn, clearly explain to future developers what needs to be fixed
  with clear documentation and a stack trace back to the abstract class. Example:

        class AbstractExample
          def overwrittable_method
            fail NotImplementedError, "The method, #overwrittable_method, is not implemented yet."
          end
        end

## Methods

- Use `snake_case` for method names.
- Use `?` for boolean methods. Example: `example.admin?`
- Use `!` for cautionary methods. Example: `example.destroy!` Good uses of bang:
  - Use when throwing an error instead of returning nil.
  - Use when bypassing a cache to force fetch.
  - Use when implementation has performance implictions.
  - Use when it may cause unexpected side effects.
- Define methods in the following order (from top to bottom within class definition):
    - Class methods
    - Public methods
    - Protected methods
    - Private methods
- Use the same indentation for all protected/private method sections of a class:

        # No
        class Example
          protected

            def protected_method_1
            end

          private

            def private_1
            end
        end

        # Yes
        class Example
          def public_method_1
          end

          protected

          def protected_method_1
          end

          private

          def private_1
          end
        end

- Class methods should be defined as `def self.method_name..end`.
    - Do not use `self << class..end` as it is confusing to read when there are multiple methods defined within.
    - Do not use `def ClassName.method_name..end` as it is redundant and can complicate refactoring.
- Avoid parentheses for method definitions:

        # No
        def example(one, two)
        end

        # Yes
        def example one, two
        end
- When using parentheses, do not put spaces around the parentheses:

        # No
        example( "param" )

        # Yes
        example("param")
- When using parentheses, do not put a space between the name and parameters:

        # No
        example ("param")

        # Yes
        example("param")
- Use spaces around `=` for default parameters:

        # No
        def vehicle make="BMW", model="R1200GS"
        end

        # Yes
        def vehicle make = "BMW", model = "R1200GS"
        end

- Avoid explicit use of `return` statements when unnecessary:

        # No
        def example
          return "Hi"
        end

        # Yes
        def example
          "Hi"
        end
- Explicit Conversions (i.e. #to_s): Represent object conversions from classes that are vaguely or absolutely unrelated
  to the target class. These messages are issued by a non-core Ruby object, never a core Ruby object. These are lenient
  methods.
- Implicit Conversions (i.e. #to_str): Represent object conversions from classes that are strongly related to the target
  class. These messages can be issued by a core Ruby object. These are strict methods and will issue exceptions when not
  found.
- Conversion Functions (i.e. Integer(), String(), Array(), etc.): For times when objects needs to be converted to a core
  type, sensibly, with the most leniency.
- With Ruby 2.1+, methods return a symbolized version of their name instead of nil when there is nothing to return. This
  can be combined with `private` statements or any statment that takes a symbol. *NOTE: This technique should only be
  used in situations when a single method is defined but not for multiple methods as it is redundant.*

        # No
        def example
        end
        private :example

        # Yes (single method)
        private def example
        end

        # Yes (multiple methods)
        private

        def example1
        end

        def example2
        end

## Monkey Patches

- Avoid monkey patching code you don't own because each patch adds additional maintenance and debugging effort to a
  project as core/third-party libraries are updated. Use any of the following alternatives to better localize custom
  changes for easier debugging and maintainability:
    - Use aliases. Example: `alias SCE Some::Custom::Example`.
    - Use a helper module that defines methods to make the dependant code more concise. Include the module in objects
      that need the additional functionality.
    - Extend instance objects with helper module functionality. Example:

            example = Example.new
            example.extend(ExampleHelpers)

## Macros

- Macros are methods which dynamically generated methods, classes, and/or modules at class/module load time. Examples:
    - attr_reader
    - attr_accessor

## Deprecations

- Use `Kernal.warn` when deprecating a method. Example:

            # **DEPRECATED:** Use `example_two` instead.
            def example
              warn "[DEPRECATION] `example` is deprecated. Use `example_two` instead."
              example_two
            end

## Threads

- Use .handle_interrupt over #raise or #kill to safely handle asynchronise interrupts. NOTE: These are hard to
  use correctly so read method documentation for more info.
- Use `MonitorMixin` (via `require "monitor"` and `include MonitorMixin`) to enhance an existing class so that all
  methods are executed with mutual exclusion (including recursive exclusion). NOTE: This might be overkill in some cases
  where using a Mutex would be simpler. Read the documentation for further details.
- Use the [Concurrent Ruby](https://github.com/ruby-concurrency/concurrent-ruby) gem as an alternative to making
  mutually exclusive operations Additionally, it is also more performant and supports MRI, Rubinius, and JRuby.

## Files

- Use IO::SEEK_SET to set position in file from which to read. Example: `file.seek 0, IO::SEEK_SET`.
- Use IO::SEEK_CUR to read from current position in file. Example: `file.seek 10, IO::SEEK_CUR`.
- Use IO::SEEK_END to read from end of a file. Example: `file.seek -10, IO::SEEK_END`.

## Load versus Require

- Prefer `require` over `load`.
- Use `load` when you need to read and load files every time you parse it.
- Use `require` when you need to read and load files when referenced the first time only.

## Tests

### MiniTest

- Run a single test: `example_test.rb --name=test_me`
- Run tests that match a regular expresion: `example_test.rb --name=/test_me/`
- Alternatively, the TESTOPTS environment variable can be used: `TESTOPTS="--name=test_me" example_test.rb`

## Resources

- [Confident Ruby](http://www.confidentruby.com) by Avdi Grimm
- [Ruby Tapas - Fetch for Defaults (Episode 12)](http://www.rubytapas.com)
- [Ruby Tapas - Inline Rescue (Episode 22)](http://www.rubytapas.com)
- [Ruby Tapas - Hash Default Values (Episode 45)](http://www.rubytapas.com)
- [Ruby Tapas - Utility Function (Episode 49)](http://www.rubytapas.com)
- [Ruby Tapas - Include Namespace (Episode 50)](http://www.rubytapas.com)
- [Ruby Tapas - Selectively Run Tests (Episode 53)](http://www.rubytapas.com)
- [Ruby Tapas - ARGF (Episode 58)](http://www.rubytapas.com)
- [Ruby Tapas - Break with Value (Episode 71)](http://www.rubytapas.com)
- [Ruby Tapas - Tail 1 - Random Access (Episode 72)](http://www.rubytapas.com)
- [Ruby Tapas - Tail 2 - Do While (Episode 73)](http://www.rubytapas.com)
- [Ruby Tapas - Concat (Episode 79)](http://www.rubytapas.com)
- [Ruby Tapas - Splat Basics (Episode 80)](http://www.rubytapas.com)
- [Ruby Tapas - Implicit Splat (Episode 81)](http://www.rubytapas.com)
- [Ruby Tapas - Inline Assigments (Episode 82)](http://www.rubytapas.com)
- [Ruby Tapas - Splat Group (Episode 84)](http://www.rubytapas.com)
- [Ruby Tapas - Ignore Arguments (Episode 85)](http://www.rubytapas.com)
- [Ruby Tapas - Naked Splat (Episode 86)](http://www.rubytapas.com)
- [Ruby Tapas - String Subscript Regex (Episode 99)](http://www.rubytapas.com)
- [Ruby Tapas - String Subscript Assignment (Episode 107)](http://www.rubytapas.com)
- [Ruby Tapas - Catch and Throw (Episode 110)](http://www.rubytapas.com)
- [Ruby Tapas - p (Episode 113)](http://www.rubytapas.com)
- [Ruby Tapas - pp (Episode 115)](http://www.rubytapas.com)
- [Ruby Tapas - Intent Revealing Argument (Episode 119)](http://www.rubytapas.com)
- [Ruby Tapas - and-or (Episode 125)](http://www.rubytapas.com)
- [Ruby Tapas - Thread Interruptions (Episode 143)](http://www.rubytapas.com)
- [Ruby Tapas - Bulk Generation (Episode 144)](http://www.rubytapas.com)
- [Ruby Tapas - Monitor (Episode 146)](http://www.rubytapas.com)
- [Ruby Tapas - Atomic (Episode 147)](http://www.rubytapas.com)
- [Ruby Tapas - Constant Lookup Scope (Episode 158)](http://www.rubytapas.com)
- [Ruby Tapas - Reduce Reduce (Episode 160)](http://www.rubytapas.com)
- [Ruby Tapas - Not Implemented (Episode 166)](http://www.rubytapas.com)
- [Ruby Tapas - Multiple Assignment (Episode 174)](http://www.rubytapas.com)
- [Ruby Tapas - Fail and Raise (Episode 188)](http://www.rubytapas.com)
- [Ruby Tapas - Hash Equality (Episode 204)](http://www.rubytapas.com)
- [Ruby Tapas - Conversion Function (Episode 207)](http://www.rubytapas.com)
- [Ruby Tapas - Implicit Conversion (Episode 210)](http://www.rubytapas.com)
- [Ruby Tapas - Spaceship Revisited (Episode 218)](http://www.rubytapas.com)
- [Ruby Tapas - Adamantium (Episode 219)](http://www.rubytapas.com)
- [Ruby Tapas - Evil Monkeys (Episode 226)](http://www.rubytapas.com)
- [Ruby Tapas - Loop (Episode 277)](http://www.rubytapas.com)
