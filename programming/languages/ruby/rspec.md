# RSpec Styles

* Run a single test or group of tests that match the substring: `example_spec.rb -e "example description"`
* Run line number of test (can be any line number of the test): `example_spec.rb -l 10`
* Alternatively, the SPEC_OPTS environment variable can be used: `SPEC_OPTS="-l 10" example_spec.rb`
* When using `raise_error`, test for both the error class and message:

        # No
        raise_error(NameError)

        # Yes
        raise_error(NameError, /bogus_method/)
