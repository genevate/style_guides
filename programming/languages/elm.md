# Elm Styles

## General

- Use two-space indentation.
- Use commas (in arrays, list, records, etc) after each item not before.
- Use `Message` instead of `Msg`.

## App Module/Structure

Use the following module structure when designing your application:

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
- Main.elm - The entry-point to your SPA which loads the app and `Router` module.

## Imports

- Prefer qualified over unqualified imports.
- Use unqualified imports sparingly (i.e. `import Html exposing (..)`) in order to avoid naming
  conflicts and reduce code readability.

## Modules

- Avoid defining modules with all functions exposed as top-level functions (i.e. `module Example
  exposing (..)`). Limit what you expose to only those methods which are needed, everything else
  should be kept private.

The following illustrates the various types of module templates you might use within you app.

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

    module API.Country exposing (..)

    import Http
    import App.Models as Models
    import App.Types exposing (ID, Token)
    import App.Decoders as Decoders
    import API.Kit as APIKit

    -- REQUESTS

    show : ID -> Token -> Cmd Message
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
        Http.send Response request

    -- MESSAGES

    type Message
      = Response (Result Http.Error Models.CountryBody)

    -- UPDATES

    update : Message -> Models.CountryBody
    update message =
      case message of
        Response (Ok body) ->
          {data = body.data, error = Nothing}

        Response (Err error) ->
          {data = Nothing, error = APIKit.parseError error}

## Records

- Use the `-- RECORDS` section of your module to define all initial records needed for the module.
- Define the `initialRecord` function (where the `Record` suffix is replaced with the actual name of
  the record you providing default values for) within the `-- RECORDS` section of your module (this
  should be defined directly after your `-- MODELS` section).
- Avoid passing parameters to your `initialRecord` functions. These functions should remain simple
  and provide safe defaults. If needing to modify the default values of one of these functions, use
  a record update (i.e. `updatedRecord = {initialRecord | key = value}`) instead.
