# Ruby Styles

## General

* Don't use unless..else..end, use if..else..end instead.
* Avoid inheritance (not always necessary, except in rare cases). Use modules instead.

## Global Variables

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
* $0 - Name of the script being executed.
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

## Hashes

* Consider using #fetch when setting default values for missing keys instead of || as || will answer the default value
  when a key doesn't exist or has a value of nil/false. Example:

        {}[:example] || :default # :default
        {example: nil}[:example] || :default # :default
        {example: false}[:example] || :default # :default

        {}.fetch(:example) { :default } # :default
        {example: nil}.fetch(:example)  { :default } # nil
        {example: false}.fetch(:example) { :default } # false

## Procs

* Disregards out extra arguments without error.
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

* $! can be used to capture currently thrown exception, although not always intuitively readable.
* Don't rescue Exception, rescue StandardError instead. Exception catches all exception types including SyntaxError,
  LoadError, NoMemoryError, Interrupt (i.e. CONTROL+C), etc. which is usually not what you want.
* Avoid using inline rescue statements (can be useful when converting exceptions into return values, however). Example:

        def example
          bad_method rescue $!
        end

## Resources

* [Ruby Tapas - Fetch for Defaults (Episode 12)](http://www.rubytapas.com)
* [Ruby Tapas - Inline Rescue (Episode 22)](http://www.rubytapas.com)
