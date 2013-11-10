# Ruby Styles

## General

* Don't use unless..else..end, use if..else..end instead.
* Avoid inheritance (not always necessary, except in rare cases). Use modules instead.

## Global Variables

The following are worth knowing but should be avoided since it makes code harder to read and maintain:

* $/ - Input record separator. Alias: $INPUT_RECORD_SEPARATOR. Default: newline.
* $. - Current input line number of the last file read. Alias: $INPUT_LINE_NUMBER.
* $\ - Output record separator. Alias: $OUTPUT_RECORD_SEPARATOR. Default: nil.
* $; - String#split default field separator. Alias: $FIELD_SEPARATOR.
* $, - Output field separator. Alias: $OUTPUT_FIELD_SEPARATOR.
* _$ - Input variable for each object within an IO loop.
* $! - Last exception thrown. Alias: $ERROR_INFO.
* $@ - Backtrace array of last exception thrown. Alias: $ERROR_POSITION.
* $& - String match of last successful pattern match for current scope. Alias: $MATCH.
* $` - String to the left of last successful match. Alias: $PREMATCH.
* $' - String to the right of last successful match. Alias: $POSTMATCH.
* $+ - Last bracket matched by the last successful match. Alias: $LAST_PAREN_MATCH.
* $<n> - nth group of last successful regexp match.
* $~ - Last match info for current scope. Alias: $LAST_MATCH_INFO.
* $< - Object access to the concatenation of all file contents given as command-line arguments. Alias: $DEFAULT_INPUT.
* $> - Output destination of Kernel.print and Kernel.printf. Alias: $DEFAULT_OUTPUT. Default: $stdout.
* $_ - Last input line of string by gets or readline. Alias: $LAST_READ_LINE.
* $0 - Name of the script being executed. Alias: $PROGRAM_NAME.
* $* - Command line arguments given for script. Alias: ARGV.
* $$ - Ruby process number of current script. Alias: $PID.
* $? - Status of the last executed child process. Alias: $CHILD_STATUS.
* $: - Load path for scripts and binary modules via load or require. Alias: $LOAD_PATH.
* $" - Array of module names as loaded by require. Alias: $LOADED_FEATURES.
* $-d - Status of the -d switch. Alias: $DEBUG.
* $-K - Source code character encoding being used. Alias: $KCODE.
* $-v - Verbose flag (as set by the -v switch). Alias: $VERBOSE.
* $-a - True if option -a ("autosplit" mode) is set.
* $-i - In-place-edit mode. Holds the extension if true, otherwise nil.
* $-l - True if option -l is set ("line-ending processing" is on).
* $-p - True if option -p is set ("loop" mode is on).
* $-w - True if option -w is set (Ruby warnings).
* $stdin - Current standard input.
* $stdout - Current standard output.
* $stderr - Current standard error output.

## Global Constants

* \_\_FILE__ - Current file.
* \_\_LINE__ - Current line.
* \_\_dir__ - Current directory.
* ARGF - IO stream for processing files, given as command-line arguments, via a script.

## % Shortcuts

* %() - Yields an interpolated, quoted string.
    `%(Example Says: #{message}) # => "Example Says: Hello!"`
* %Q() - Same behavior as %().
* %q() - Yields a non-interpolated, quoted string.
    `%q(One Two Three) # => "One Two Three"`
* %W() - Yields an interpolated string array.
    `%W(one two, #{three}) # => ["one", "two", "three"]`
* %w() - Yields a non-interpolated string array.
    `%w(one two, three) # => ["one", "two", "three"]`
* %r() - Yields an interpolated regular expression.
    `%r(one|#{two}) # => /one|two/`
* %s() - Yields a non-interpolated symbol.
    `%s(test) # => :test`
* %I() - Yields an interpolated symbol array.
    `%I(one two #{three}) # => [:one, :two, :three]`
* %i() - Yields a non-interpolated symbol array.
    `%i(one two three) # => [:one, :two, :three]`
* %x() - Executes an interpolated system command (does not echo to STDOUT or return the running command's result).
    `%x(echo #{message}) # => "Huzzah!"`

## Splats

* Also known as *Destructuring*. Examples:

        a1 = %i(one two three)
        a2 = %w(red black white)

        a, b, c = *a1 # => a == :one, b == :two, c == :three
        a, b, c = :insert, *a1 # => a == :insert, b == :one, c == :two
        [*a1, *a2] = # => [:one, :two, :three, "red", "black", "white"]
* Can be used to expand collections on the right side of an assignment (as shown above).
* Can be used to suck up multiple values into a single variable on the left side of an assigment:

        a = %i(one two three four five)

        *b, c, d = *a # => b == [:one, :two, :three], c == :four, d == :five
        b, *c, d = *a # => b == :one, c == [:two, :three, :four], d == :five
        b, c, *d = *a # => b == :one, c == :two, d == [:three, :four, :five]
* Commonly used in method and/or block arguments.
* Use explicit over implicit splatting as implicit splatting assumes an object behaves like an Array. Example:

        a = :one, :two, :three # => a == [:one, :two, :three]
* Any object that responds to the #to_ary method can be used in an implicit splat.
* Splats can be grouped (handy in block arguments) which allows for values of an array to be auto-assigned to variables
  without having to use an intermediate variable to do the same thing. Example:

        vehicles = {"Volkswagen" => "New Beetle"}
        vehicles.each {|(make, model)| puts "Make: #{make}, Model: #{model}"} # => "Make: Volkswagen, Model: New Beetle"
* Use a naked splat (*) when defining arguments to be ignored (useful in subclass contructors as well). Example:

        def example(required, *)
          puts "Required argument is: #{required}."
        end

        example 1, 2, 3, 4, 5 # => "Required argument is: 1"

## Assigments

* Use inline assigment, with parentheses, in loop conditions to keep code concise. Example:

        lines = 0
        while(chunk = file.read(1024))
          lines += chunk.count "\n"
        end
  The use of parentheses indicates that the *chunk* assigment is intentional and avoids the confusion of thinking that
  the assigment (=) was not meant to be an equals (==).

## Arguments

* Use _ to ignore an argument or multiple arguments. Example:

        a = [%w(Mr. Billy Bob Simpson), %w(Mrs. Sally Jane Ruffy)]
        a.map { |_, first, _, last| [first, last] } # =>  [["Billy", "Simpson"], ["Sally", "Ruffy"]]

## Booleans

* Use !! to convert an object to a boolean.

## Strings

* Use [] to parse substrings. Example:

        song = "05 - Misty Mountain Hop"
        song[5, song.length] # => "Misty Mountain Hop"
* Use [0,0] to prepend to a string. Example:

        song = "Misty Mountain Hop"
        song[0,0] = "05 - "
        song # => "05 - Misty Mountain Hop"
* Use [] with a regular expression to parse a substring. Example:

        song = "05 - Misty Mountain Hop"
        song[/M.+n/] # => "Misty Mountain"
* Use [] with a regular expression and a second argument to parse substring group. Example:

        song = "05 - Misty Mountain Hop"
        song[/^\d{2} - (.+)/, 1] # => "Misty Mountain Hop"
* Use [] with a regular expression and named groups to parse a substring group. Example:

        song = "05 - Misty Mountain Hop"
        song[/^(?<track>\d{2})(?<delimiter> - )(?<title>.+)/, :title] # => "Misty Mountain Hop"

## Arrays

* Use Array#concat when concatenating arrays. It is faster than using `<<` and `.flatten!` or using `+=`. It also
  updates the target array in place whereas `+=` will create a new array object of the concatenated source arrays.

## Hashes

* Use blocks when setting default values.
    * Example: Hash.new []. Will use the same array object for each new key.
    * Example: Hash.new {|hash, key| hash[key] = []}. Will initialize a new array object for each new key.
* Consider using #fetch when setting default values for missing keys instead of || as || will answer the default value
  when a key doesn't exist or has a value of nil/false. Example:

        {}[:example] || :default # :default
        {example: nil}[:example] || :default # :default
        {example: false}[:example] || :default # :default

        {}.fetch(:example) { :default } # :default
        {example: nil}.fetch(:example)  { :default } # nil
        {example: false}.fetch(:example) { :default } # false

## Loops

* `begin..end while <condition>` is the equivalent of a do while loop.

## Breaks

* The obvious use for breaks are to exit quickly out of a loop once a particular condition is met but they can also
  be used to return a value. Example: `break "Example Message" if some_value == 'found'`

## Procs

* Disregards extra arguments without error.
* Returns from the scope of the bounded object (i.e. returns from the scope of the object in which the proc was defined).
* Use `proc` instead of `Proc.new` as provided by the Kernel module.
* Procs can be called the following ways (the first option, however, is more readable):
    * example.call "hello"
    * example["hello"]
    * example.("hello")
* The `===` method which calls `call` is useful when used as a predicate in case statements.

## Lambdas

* Respects defined arguments and throws errors if extra arguments are not defined.
* Returns from the scope of the lambda, not the bounded object in which it was defined.
* Use lambdas, by default, over procs.
* Lambda can be defined via `lambda` or `->`. The latter is preferred.

## Exceptions

* Don't rescue Exception, rescue StandardError instead. Exception catches all exception types including SyntaxError,
  LoadError, NoMemoryError, Interrupt (i.e. CONTROL+C), etc. which is usually not what you want.
* Avoid using inline rescue statements (can be useful when converting exceptions into return values, however). Example:

        def example
          bad_method rescue $!
        end

## Modules

* Modules allow code to be namespaced.
* Use `module_function` to mark methods in a module that will be private instance methods when included in a class.
  These methods can also be accessed as class level methods via the module. This allows classes to include module
  methods when all or many of the methods are needed by the class but also allows classes to simply reference the module
  directly when only a few of the methods are required.
* Submodles can include containing modules. Example:

        module Outer
          module Inner
            include Outer
          end
        end

## Methods

* Always define methods in the following order (from top to bottom within class definition):
    * Class methods
    * Public methods
    * Protected methods
    * Private methods
* Class methods should be defined as `def self.method_name..end`.
    * Do not use `self << class..end` as it is confusing to read when there are multiple methods defined within.
    * Do not use `def ClassName.method_name..end` as it is redundant and can complicate refactoring.

## Files

* Use IO::SEEK_SET to set position in file from which to read. Example: `file.seek 0, IO::SEEK_SET`.
* Use IO::SEEK_CUR to read from current position in file. Example: `file.seek 10, IO::SEEK_CUR`.
* Use IO::SEEK_END to read from end of a file. Example: `file.seek -10, IO::SEEK_END`.

## Tests

### MiniTest

* Run a single test: `example_test.rb --name=test_me`
* Run tests that match a regular expresion: `example_test.rb --name=/test_me/`
* Alternatively, the TESTOPTS environment variable can be used: `TESTOPTS="--name=test_me" example_test.rb`

### RSpec

* Run a single test or group of tests that match the substring: `example_spec.rb -e "example description"`
* Run line number of test (can be any line number of the test): `example_spec.rb -l 10`
* Alternatively, the SPEC_OPTS environment variable can be used: `SPEC_OPTS="-l 10" example_spec.rb`

## Resources

* [Ruby Tapas - Fetch for Defaults (Episode 12)](http://www.rubytapas.com)
* [Ruby Tapas - Inline Rescue (Episode 22)](http://www.rubytapas.com)
* [Ruby Tapas - Hash Default Values (Episode 45)](http://www.rubytapas.com)
* [Ruby Tapas - Utility Function (Episode 49)](http://www.rubytapas.com)
* [Ruby Tapas - Include Namespace (Episode 50)](http://www.rubytapas.com)
* [Ruby Tapas - Selectively Run Tests (Episode 53)](http://www.rubytapas.com)
* [Ruby Tapas - ARGF (Episode 58)](http://www.rubytapas.com)
* [Ruby Tapas - Break with Value (Episode 71)](http://www.rubytapas.com)
* [Ruby Tapas - Tail 1 - Random Access (Episode 72)](http://www.rubytapas.com)
* [Ruby Tapas - Tail 2 - Do While (Episode 73)](http://www.rubytapas.com)
* [Ruby Tapas - Concat (Episode 79)](http://www.rubytapas.com)
* [Ruby Tapas - Splat Basics (Episode 80)](http://www.rubytapas.com)
* [Ruby Tapas - Implicit Splat (Episode 81)](http://www.rubytapas.com)
* [Ruby Tapas - Inline Assigments (Episode 82)](http://www.rubytapas.com)
* [Ruby Tapas - Splat Group (Episode 84)](http://www.rubytapas.com)
* [Ruby Tapas - Ignore Arguments (Episode 85)](http://www.rubytapas.com)
* [Ruby Tapas - Naked Splat (Episode 86)](http://www.rubytapas.com)
* [Ruby Tapas - String Subscript Regex (Episode 99)](http://www.rubytapas.com)
* [Ruby Tapas - String Subscript Assignment (Episode 107)](http://www.rubytapas.com)
