# Architecture

PrestoDOM follows the Elm architecture which is basically a combination of having 3 specific parts:

* Initial State: the initial state
* Eval: a way to update our state
* View: a way to view our state as HTML

You can read more about the Elm architecture over [here.](https://guide.elm-lang.org/architecture/)

A simple pattern looks like the following:

```haskell
type State = {...}

initialState :: State
initialState = {...}

data Action = A | B

eval :: Action -> State -> Either Action State
eval A state = Right state
eval B state = Left B

view :: forall i w eff. (Action -> Eff (frp :: FRP | eff) Unit) -> State -> PrestoDOM Action w
view push state =
  linearLayout
  [] []

screen =
  { initialState
  , view
  , eval
  }
```



