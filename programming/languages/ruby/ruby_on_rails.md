# Ruby on Rails Styles

## Objects

- Avoid using `Object#try` as it leads to brittle and hard to debug code. Use the null object
  pattern or refactor your code in a manner that doesn't use a `nil` object.

## Database

- [Apply indexes](http://robots.thoughtbot.com/post/163627511/a-grand-piano-for-your-violin) where
  appropriate.
- PostgreSQL prepared statements are enabled by default (ActiveRecord creates up to 1000 prepared
  statements per connection). These can be disabled (set `statement_limit: false`) or you can limit
  them via database.yml settings:

        production:
          adapter: postgresql
          statement_limit: 200
- Use the `_at` suffix to represent represent date/time columns. Example: `<example>_at`.

## Model

- Attachments
  - Do not allow users to upload executable files (via Paperclip, for example).
  - Always validate attachment content type.
- SQL Injection
  - Don't substitute params directly into dynamic SQL statements. Use the following
    instead: ["name like ?", "%params[:names]%"]

## View

- Apply renderer extensions to all files. Example:
  - SLIM: *.html.slim
  - SASS: *.css.sass
- Fragment cache when possible for anything that doesn't change much. Examples:
  - Site headers
  - Site navigation menus
- Forms
  - Select statements should include blanks. Example: include_blank: "-select-"
- HTML Injection
  - Use the 'h' method to render form values in your views so that SQL or other code is not
    rendered.

## Controller

- Use filter_parameter_logging(:password) to filter sensitive information from the logs.
- Use protect_from_forgery to prevent CRSF attacks.
- Authorize user access before rendering content.
- Caching
  - Use `#stale?` when calculating responses in order to properly detect if there are changes or
    not. This will speed up response time by avoiding the template later if there are no changes
    with a 304 (not modified) response. Otherwise, if there is an update, a standard 200 response
    will be given. [Tutorial](https://www.sitepoint.com/how-to-increase-performance-in-rails).
  - Add caches_page when appropriate. Example: caches_page :index, :show
  - Add expires_page when appropriate. Example: action: :show, id: @post

## Logging

- Use blocks when logging as [blocks are more
  performant](http://guides.rubyonrails.org/debugging_rails_applications.html#impact-of-logs-on-performance):

        # No
        logger.debug "Example"

        # Yes
        logger.debug { "Example" }
