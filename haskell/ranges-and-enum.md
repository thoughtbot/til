# Ranges and Enum

Ranges can be constructed from any instance of Haskell's `Enum` typeclass,
including custom types that derive from `Enum`. For example, the custom `Day`
type below:

```hs
data Day = Sunday | Monday | Tuesday | Wednesday | Thursday | Friday | Saturday deriving (Show, Enum)
[Monday .. Friday]

-- returns
[Monday,Tuesday,Wednesday,Thursday,Friday]
```
