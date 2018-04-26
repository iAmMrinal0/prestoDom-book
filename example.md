# Example

We will take an example of a counter which increments or decrements based on a button click.

### 

We will use a `linearLayout` and to show the text we will use a `textView`

Our actions are basically `Increment` or `Decrement`

And our state is an `Int(Integer)` with the count value. We start our state with the counter set to `0` and our `eval` function will handle the state updation based on our actions.

```haskell
module Counter where

import Prelude
import PrestoDOM

import Control.Monad.Eff (Eff)
import Data.Either (Either(..))
import FRP (FRP)

data Action = Increment | Decrement

type State = Int

screen :: forall i eff. Screen Action State eff Action
screen =
  { initialState
  , view
  , eval
  }

initialState :: State
initialState = 0

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
      , text $ show state
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
    Increment -> Right $ state + 1
    Decrement -> Right $ state - 1
```



