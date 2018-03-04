# RSpec Styles

<!-- Tocer[start]: Auto-generated, don't remove. -->

## Table of Contents

  - [General](#general)
  - [Performance](#performance)

<!-- Tocer[finish]: Auto-generated, don't remove. -->

## General

- Run a single test or group of tests that match the substring: `example_spec.rb -e "example
  description"`
- Run line number of test (can be any line number of the test): `example_spec.rb -l 10`
- Alternatively, the SPEC_OPTS environment variable can be used: `SPEC_OPTS="-l 10" example_spec.rb`
- When using `raise_error`, test for both the error class and message:

        # No
        raise_error(NameError)

        # Yes
        raise_error(NameError, /bogus_method/)

## Performance

- Require `spec_helper.rb` or `rails_helper.rb` where appropriate. When not needing the Rails stack,
  definitely use `spec_helper.rb`.
- Reduce the number of gem dependencies to only what is needed. Use gem groups to help with this
  where the `:test` group and non-grouped gems would be the only dependencies loaded for improved
  test performance.
- Stub/mock API requests where appropriate. Tools like,
  [VCR](https://www.relishapp.com/vcr/vcr/docs) can help in this endeavor too.
