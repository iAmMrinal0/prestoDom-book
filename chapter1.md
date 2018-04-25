# Architecture

PrestoDOM follows the Elm architecture which is basically a combination of having 3 specific parts:

* Initial State: the initial state
* Eval: a way to update our state
* View: a way to view our state as HTML

You can read more about the Elm architecture over [here.](https://guide.elm-lang.org/architecture/)

A simple example looks like the following:

```haskell
type State = {title :: String}

initialState :: State
initialState = {title: "Hello World"}

data Action = UpdateTitle | NextScreen

eval :: Action -> State -> Either Action State
eval UpdateTitle state = Right $ state {title = "Title Updated"}
eval NextScreen state = Left NextScreen

view :: forall i w eff. (Action -> Eff (frp :: FRP | eff) Unit) -> State -> PrestoDOM Action w
view push state = linearLayout
  
```



