# RSpec Styles

<!-- Tocer[start]: Auto-generated, don't remove. -->

## Table of Contents

  - [General](#general)
  - [Structure](#structure)
  - [Contexts](#contexts)
  - [Performance](#performance)

<!-- Tocer[finish]: Auto-generated, don't remove. -->

## General

- Use the following steps for writing a spec:
  - **Arrage**: This is where you define your subject and supporting depedencies to be tested.
  - **Execute**: This is where you execute the subject under test.
  - **Expect**: The last, and final, line of your spec then verifies what you tested matches your
    expectation.
- Use Coderay (i.e. `bundle install coderay`) to produce colorized output when running specs.
- Use `let` to define common objects used across multiple specs. Doing this provides the following
  benefits:
  - Provides a helpful error mesage if the object is not defined, missing, mispelled, etc. versus a
    lesser and non-intiutive error message if an instance variable was used.
  - Avoids having to create an instance variable in a `before` block which is inefficient as the it
    is contructed for *every* spec regardless if the spec needs it or not while a `let` only creates
    the object on demand.
- Run a single test or group of tests that match the substring: `example_spec.rb -e "example
  description"`
- Run line number of test (can be any line number of the test): `example_spec.rb -l 10`
- Alternatively, the SPEC_OPTS environment variable can be used: `SPEC_OPTS="-l 10" example_spec.rb`
- When using `raise_error`, test for both the error class and message:

        # Avoid
        raise_error(NameError)

        # Use
        raise_error(NameError, /bogus_method/)
- Use `pending` when wanting to skip a spec but also print out it's failed expectation without
  actually failing the spec. Should the implementation be completed without removing the pending
  status, the spec will fail to remind you you don't need the pending spec anymore.
- Use `skip` for skipping a spec entirely and avoiding any expectation output while still showing
  the spec has been skipped.
- Use [aggregate_failures](https://relishapp.com/rspec/rspec-expectations/docs/aggregating-failures)
  metadata to group expectation failures within a single spec together. By default, a spec will only
  print the first failure. Aggregations allows all failures to be displayed at once. While it is
  best to have one expectation per spec, sometimes you need to group expectations together for spec
  performance reasons (i.e. making an expensive database call while checking other aspects of the
  implementation).

## Structure

The files structure of your RSpec folder should look like the following:

    # With Ruby only
    /spec
      /support
        /cassettes (VCR, optional)
        /matchers
        /shared_contexts
        /shared_examples

      /spec_helper.rb
      /rails_helper.rb

    # With Rails (or some other framework)
    /spec
      /support
        /cassettes (VCR, optional)
        /matchers
        /rails
          /shared_contexts
          /shared_examples
        /ruby
          /shared_contexts
          /shared_examples
      /spec_helper.rb
      /rails_helper.rb

In the situation where you are using Rails, you'll want to break down your support files into `ruby`
and `rails` folders and then load those support files via the corresponding `spec_helper.rb` and
`rails_helper.rb` files since context matters.

## Contexts

- Use `context` when needing to make a slight alternation to the subject or provide addtional setup.
- Use `with` or `when` prefixes for your context definitions to help describe what makes the context
  unique.

## Performance

- Require `spec_helper.rb` or `rails_helper.rb` where appropriate. When not needing the Rails stack,
  definitely use `spec_helper.rb`.
- Reduce the number of gem dependencies to only what is needed. Use gem groups to help with this
  where the `:test` group and non-grouped gems would be the only dependencies loaded for improved
  test performance.
- Stub/mock API requests where appropriate. Tools like,
  [VCR](https://www.relishapp.com/vcr/vcr/docs) can help in this endeavor too.
