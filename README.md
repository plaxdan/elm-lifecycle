A symmetrical simplified Elm lifecycle diagram.

![Elm Lifecycle](https://rawgithub.com/plaxdan/elm-lifecycle/master/elm-lifecycle.svg)

Below is a simplified description of events just to help follow along the above diagram. For more detailed descriptions of Elm workflow please see one of the following resources:

- http://guide.elm-lang.org
- http://www.elm-tutorial.org/en/

#### `init`

An [`HTML.App.program`](http://package.elm-lang.org/packages/elm-lang/html/1.0.0/Html-App#program) is created within athe `main` function of an Elm program. The `Html.App.program` initiates the Elm application by calling the `init` function. This creates a `(Model, Cmd Msg)` tuple which is handed off to the Elm runtime.

1. `main` is called
1. `Html.App.program` is called within `main`
1. `Html.App.program` calls your `init` function
1. The `init` function returns a `(Model, Cmd Msg)` tuple which is handed off to the Elm runtime
1. The Elm runtime runs the `Cmd` and then calls your `update` function with the resultant `Msg` and `Model` (thus closing the "update loop")
1. `update` then returns a new `(Model, Cmd Msg)` tuple
1. the update loop may continue until no more `Cmd`s are run

Once the Elm program has been initialized and a view is rendered to the screen then further updates come from either:

- subscription to external events such as time, or a web socket
- or, from user interaction with the view

#### `subscriptions`

1. an external event occurs to which your application is subscribed
1. the `subscriptions` function passes a `Sub Msg` to the Elm runtime The `Msg` will most likely [contain a payload](http://www.elm-tutorial.org/en/02-elm-arch/05-msg-payload.html) from the event.
1. the Elm runtime passes the `Msg` (with its payload) and the current `Model` to your `update` function (thus beginning the update loop)
 
#### `view`

1. the user interacts with the view (clicks a button, mouseover a div etc)
1. if an [`Html.Events`](http://package.elm-lang.org/packages/elm-lang/html/1.0.0/Html-Events) event has been configured for the user behavior, then an `Html Msg` is passed to the Elm runtime.
1. the Elm runtime passes the `Msg` (with its payload) and the current `Model` to your `update` function (thus beginning the update loop)
