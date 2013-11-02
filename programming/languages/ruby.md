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

## Booleans

* Use !! to convert an object to a boolean.

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

## Procs

* Disregards extra arguments without error.
* Returns from the scope of the bounded object (i.e. returns from the scope of the object in which the proc was defined).
* Use `proc` instead of `Proc.new` as provided by the Kernel module.
* Procs can be called the following ways (the first option, however, is more readable):
    * example.call "hello"
    * example["hello"]
    * example.("hello")
* The `===` method which calls `call` is useful when used as a predicate in case statements.

## Breaks

* The obvious use for breaks are to exit quickly out of a loop once a particular condition is met but they can also
  be used to return a value. Example: `break "Example Message" if some_value == 'found'`

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
