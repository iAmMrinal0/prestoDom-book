# Example

We will take an example of a counter which increment or decrements based on the button click.

```haskell
module UI.Template where

import Prelude
import PrestoDOM

import Control.Monad.Eff (Eff)
import Data.Either (Either(..))
import FRP (FRP)

data Action = Increment | Decrement

type State = {counter :: Int}

screen :: forall i eff. Screen Action State eff Action
screen =
  { initialState
  , view
  , eval
  }

initialState :: State
initialState = {counter: 0}

view :: forall i w eff. (Action -> Eff (frp :: FRP | eff) Unit) -> State -> PrestoDOM Action w
view push state =
  linearLayout
    [ height $ V 600
    , width $ V 400
    , orientation "vertical"
    , gravity "center"
    ]
    [ textView
      [ width $ V 80
      , height $ V 25
      , text $ show state.counter
      , textSize 16
      ]
    , linearLayout
      [ height $ V 50
      , width Match_Parent
      , background "#969696"
      , gravity "center"
      , visibility "visible"
      , onClick push $ const Increment
      ]
      [ textView
        [ width $ V 80
        , height $ V 25
        , text "Increment"
        , textSize 16
        ]
      ]
     , linearLayout
      [ height $ V 50
      , width Match_Parent
      , background "#969696"
      , gravity "center"
      , visibility "visible"
      , onClick push $ const Decrement
      ]
      [ textView
        [ width $ V 80
        , height $ V 25
        , text "Decrement"
        , textSize 16
        ]
      ]
    ]

eval :: Action -> State -> Either Action State
eval action state =
  case action of
    Increment -> Right state {counter = state.counter + 1}
    Decrement -> Right state {counter = state.counter - 1}
```



