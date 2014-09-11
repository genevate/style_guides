# Capybara Styles

## Setup

* Add `Capybara.asset_host = "http://localhost:3000"` to the spec helper to view test pages using the development
  environment's asset pipeline (assumes that Rails is being served locally).

## Matchers

* Use [action methods](http://rubydoc.info/github/jnicklas/capybara/master/Capybara/Node/Actions) instead of [finder
  methods](http://rubydoc.info/github/jnicklas/capybara/master/Capybara/Node/Finders) to reliably interact with page
  elements.
* Use [RSpec matchers](http://rubydoc.info/github/jnicklas/capybara/master/Capybara/RSpecMatchers) instead of [node
  methods](http://rubydoc.info/github/jnicklas/capybara/master/Capybara/Driver/Node) to verify page elements.
* Avoid using `all` as it doesn't wait for the page to load and could cause race conditions.
* Avoid using `execute_script` as it can cause incompatibility conflicts with other Capybara drivers.
