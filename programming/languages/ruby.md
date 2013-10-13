# Ruby Styles

## General

* Don't use unless..else..end, use if..else..end instead.
* Avoid inheritance (not always necessary, except in rare cases). Use modules instead.

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

## Exceptions

* $! can be used to capture currently thrown exception, although not always intuitively readable.
* Don't rescue Exception, rescue StandardError instead. Exception catches all exception types including SyntaxError,
  LoadError, and Interrupt which is usually not what you want.
* Avoid using inline rescue statements (can be useful when converting exceptions into return values, however). Example:

        def example
          bad_method rescue $!
        end

## Resources

* [Ruby Tapas - Fetch for Defaults (Episode 12)](http://www.rubytapas.com)
* [Ruby Tapas - Inline Rescue (Episode 22)](http://www.rubytapas.com)
