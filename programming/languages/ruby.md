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
