# Ruby on Rails Styles

## Objects

- Avoid Globals. Example: `Current.user`. This introduces issues with concurrency and reduces the
  explicitness of your code. Read more on why [globals are harmful](http://bit.ly/2FbNM4R).
- Avoid `Object#try` as it leads to brittle and hard to debug code. Use the null object pattern or
  refactor your code in a manner that doesn't result in a `nil`.
- Avoid using concerns as they introduce multiple inheritance which is hard to maintain and test. An
  object should have only one responsibility. By using concerns, you introduce side effects and
  multiple behaviors that are hard to reason about. Extract distinct behavior to multiple objects.
  Use object composition instead.
- Avoid `#class_attribute`. While better than class variables (`@@`), it makes code more Rails-
  specific. Use object composition and/or class methods instead in order to keep your objects simple
  and testable.

## Database

- [Apply indexes](http://robots.thoughtbot.com/post/163627511/a-grand-piano-for-your-violin) where
  appropriate.
- PostgreSQL prepared statements are enabled by default (ActiveRecord creates up to 1000 prepared
  statements per connection). These can be disabled (set `statement_limit: false`) or you can limit
  them via database.yml settings:

        production:
          adapter: postgresql
          statement_limit: 200
- Use the `_at` suffix to represent represent date/time columns. Example: `published_at`.

## Models

- Use associations to represent relationships between other models (i.e. `belongs_to`, `has_many`,
  etc).
- Use `enum` to represent model statuses, kinds, etc.
- Use scopes:
  - Scopes are helpful in extracting and naming `where` clauses (or other complex queries). Scopes
    provide a way to self-describe behavior that can be reused multiple places throughout the
    system. Scopes are easier to test too.

        # No
        Post.where status: :published

        # Yes
        scope(:published, -> { where status: :published })
        Post.published
  - Avoid scopes that only use `#order` or `#limit`. Unless this is a common pattern, it's better to
    chain onto an existing scope for specific situations.
- Avoid adding business logic of any kind to models. Your models should only surface data and
  related associations. Use business objects that are composed of a model for specialized behavior.
- Avoid callbacks. Callbacks add side effects that is hard to maintain and test. Isolate and extract
  behavior to dedicated business objects instead.
- Avoid validations. Validations add side effects that is hard to maintain and test in all
  situations. Use database constraints (especially uniqueness contraints) when possible. Otherwise,
  extract behavior to business objects.
- Attachments
  - Avoid `ActiveStorage` as it introduces polymorphic and single table inheritance to your
    application that makes one table a junk pile of attachment associations. Use gems like
    [CarrierWave](https://github.com/carrierwaveuploader/carrierwave) that allow for attachments to
    be added to individual tables as needed.
  - Avoid allowing users to upload executable files.
  - Always validate attachment content type.
- SQL Injection
  - Don't substitute params directly into dynamic SQL statements. Use the following
    instead: ["name like ?", "%params[:names]%"]

## Views

- Use [Slim](https://github.com/slim-template/slim) to render views. It uses a concise, low ceremony
  syntax, that is also more performant than ERB.
- User renderer extensions to all files. Example:
  - SLIM: `*.html.slim`
  - SASS: `*.css.sass`
- Fragment cache when possible for anything that doesn't change much. Examples:
  - Site headers
  - Site navigation menus
- Forms
  - Use blanks for select statements. Example: include_blank: "-select-".
- HTML Injection
  - Use the 'h' method to render form values in your views so that SQL or other code is not
    executed.

## Controllers

- Use `filter_parameter_logging :password` to filter sensitive information from the logs.
- Use `protect_from_forgery` to prevent CRSF attacks.
- Use `before_action` and `after_action` macros sparingly. There are cases where assigning the
  current, blocking certain actions, etc. can be helpful but don't over do it.
- Authorize user access before rendering content.

## Caching

  - Use `#stale?` when calculating responses in order to properly detect if there are changes or
    not. This will speed up response time by avoiding the template later if there are no changes
    with a 304 (not modified) response. Otherwise, if there is an update, a standard 200 response
    will be given. [Tutorial](https://www.sitepoint.com/how-to-increase-performance-in-rails).
  - Add caches_page when appropriate. Example: `caches_page :index, :show`.
  - Add expires_page when appropriate. Example: `action: :show, id: @post`.

## Logging

- Use blocks when logging as [blocks are more performant](http://bit.ly/2FaEcit):

        # No
        logger.debug "Example"

        # Yes
        logger.debug { "Example" }
