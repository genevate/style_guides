# Elm Styles

<!-- Tocer[start]: Auto-generated, don't remove. -->

## Table of Contents

  - [General](#general)
  - [Imports](#imports)
  - [Modules](#modules)
  - [Flags](#flags)
  - [Functions](#functions)
  - [Lets](#lets)
  - [Ports](#ports)
  - [Maybes](#maybes)
  - [Records](#records)
  - [Case Expressions](#case-expressions)
  - [Structure](#structure)
  - [Templates](#templates)
    - [Main](#main)
    - [HTML](#html)
    - [API](#api)

<!-- Tocer[finish]: Auto-generated, don't remove. -->

## General

- Use two-space indentation.
- Use commas (in arrays, list, records, etc) after each item not before.
- Use `Message` instead of `Msg`.

## Imports

- Prefer qualified over unqualified imports.
- Use unqualified imports sparingly (i.e. `import Html exposing (..)`) in order to avoid naming
  conflicts and reduce code readability.
- Avoid lots of imports (there should be more lines of code than import lines).
- Avoid recursive imports. Refactor to reduce the circular imports to a single import.

## Modules

- Avoid defining modules with all functions exposed as top-level functions (i.e. `module Example
  exposing (..)`). Limit what you expose to only those methods which are needed, everything else
  should be kept private.

## Flags

- Use JSON encoded/decoded values for program flags to improve error handling between JavaScript and
  Elm. Example:

      main : Program Flags Model Message
      main =
        Navigation.programWithFlags LocationChange
          {
            init = init,
            view = view,
            update = update,
            subscriptions = subscriptions
          }

## Functions

- Avoid anonymous functions (i.e. `(\ -> )`). Use a named function instead as it'll have a type
  signature and name which makes it readable, understandable, and easier to maintain. The caveat to
  this is if the annonymous function is small, it can be helpful within one-off situations in a
  `let` statement. Again, use sparingly.

## Lets

- Use `let...in` statements when needing to define a variable that is used multiple times within the
  same function. For anything else, extract to a function.

## Ports

- Use a single module for all ports. Example: `Ports.elm`.
- Use JSON encoded/decoded values when sending data between JavaScript and Elm to improve error
  handling. Example:

      port module App.Ports exposing (..)

      import Json.Encode as JSONE
      import Json.Decode as JSOND

      port localStorageSet : (String, JSONE.Value) -> Cmd message
      port localStorageGet : String -> Cmd message
      port localStorageResponse : (JSOND.Value -> message) -> Sub message

## Maybes

- Design data structures that avoid optional values to begin with.
- Avoid code that combines checking for optionals with code that calculates values.
- When extracting a functions to calculate values, they should never accept a `Maybe` (this includes
  all arguments) but can answer a `Maybe`.
- Avoid using `Maybe List a`. Any function, like `List`, which has an inherent empty state (i.e.
  `[]`) does not need to classifed as a `Maybe`.
- Use `a` or `an` prefixes for function arguments that are maybes. This clarifies the type when used
  in a `case` statment to avoid ambiguity and use of unwanted shadow variables. Example:

      toLabel : Maybe String -> String
      toLabel aLabel =
        case aLabel of
          Just label ->
            label

          Nothing ->
            "Unknown"

## Records

- Use the `-- RECORDS` section of your module to define all initial records needed for the module.
- Define the `initialRecord` function (where the `Record` suffix is replaced with the actual name of
  the record you providing default values for) within the `-- RECORDS` section of your module (this
  should be defined directly after your `-- MODELS` section).
- Avoid passing parameters to your `initialRecord` functions. These functions should remain simple
  and provide safe defaults. If needing to modify the default values of one of these functions, use
  a record update (i.e. `updatedRecord = {initialRecord | key = value}`) instead.
- Use a flat record structure initially and wait to use a more complex nested structure until you
  refactor and see a need arise as this lead to few complications with unpacking and updating the
  nested record. Example:

      # No
      type alias Model = {label: String, point: Point}
      type alias Point = {x: Int, y: Int}

      # Yes
      type alias Model = {label: String, x: Int, y: Int}
- Use records to extract complex function signatures. When the argument list of a function exceeds
  more than three arguments, this is a good time to extract the details to a record. Example:

      # No
      example : String -> String -> String -> String -> String
      example label slug notes bio =
        "add implementation here"

      # Yes
      type alias Person = {label: String, slug: String, notes: String, bio: String}

      example : Person -> String
      example person =
        "add implementation here"

## Case Expressions

- Avoid large case expressions. Try to extract common functionality.
- Avoid recursive calls to `update` (degrades performance).

## Structure

Use the following structure when designing your application:

- API - Contains the client modules for processing request/responses to internal/external APIs. Use
  singular naming for single resource requests and plural naming for a collections of resources
  (example: `Country.elm` and `Countries.elm`).
- App
  - Decoders.elm - Defines app-wide JSON decoders.
  - Encoders.elm - Defines app-wide JSON encoders.
  - Models.elm - Defines app-wide type aliases for your models.
  - Ports.elm - Defines app-wide ports to JavaScript.
  - Router.elm - Defines app-wide routing, authorization, and navigation.
  - Types.elm - Defines app-wide types.
- Pages - Contains the various pages of your Single Page App (SPA). This are loaded and managed by
  the `Router` module. The directory structure can be broken down further by namespace within
  your app.
- Main (`Main.elm`) - The entry-point to your SPA which loads the app and `Router` module.

## Templates

The following illustrates the various templates you might use within you app.

### Main

    module Application exposing (..)

    import Html exposing (Html, text)

    -- MODEL

    type alias Model =
      {
      }

    -- INIT

    init : (Model, Cmd Message)
    init =
      (Model, Cmd.none)

    -- VIEW

    view : Model -> Html Message
    view model =
      text ""

    -- MESSAGE

    type Message
      = None

    -- UPDATE

    update : Message -> Model -> (Model, Cmd Message)
    update message model =
      (model, Cmd.none)

    -- SUBSCRIPTIONS

    subscriptions : Model -> Sub Message
    subscriptions model =
      Sub.none

    -- MAIN

    main : Program Never Model Message
    main =
      Html.program
        {
          init = init,
          view = view,
          update = update,
          subscriptions = subscriptions
        }

### HTML

    module Example exposing (..)

    import Html exposing (Html, text)

    -- MODEL

    type alias Model =
      {
      }

    -- INIT

    init : (Model, Cmd Message)
    init =
      (Model, Cmd.none)

    -- VIEW

    view : Model -> Html Message
    view model =
      text ""

    -- MESSAGE

    type Message
      = None

    -- UPDATE

    update : Message -> Model -> (Model, Cmd Message)
    update message model =
      (model, Cmd.none)

### API

    module API.Countries exposing (..)

    import Http
    import App.Types exposing (ID, Token, WebData)
    import App.Models as Models
    import App.Decoders as Decoders
    import API.Kit as APIKit

    -- REQUESTS

    index : Token -> Cmd (WebData Models.CountriesBody)
    index token =
      let
        request = Http.request {
          method = "GET",
          headers = APIKit.readHeaders token,
          url = "/api/countries",
          body = Http.emptyBody,
          expect = Http.expectJson Decoders.countriesBody,
          timeout = Nothing,
          withCredentials = False
        }
      in
        APIKit.send request

    show : ID -> Token -> Cmd (WebData Models.CountryBody)
    show id token =
      let
        request = Http.request {
          method = "GET",
          headers = APIKit.readHeaders token,
          url = "/api/countries/" ++ id,
          body = Http.emptyBody,
          expect = Http.expectJson Decoders.countryBody,
          timeout = Nothing,
          withCredentials = False
        }
      in
        APIKit.send request
