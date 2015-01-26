# Sorting in reverse order

`Data.Ord` contains a newtype, `Down`, which can wrap any type that has an
`Ord` instance, in order to provide a reversed `Ord` instance for that type.

For example:

```hs
Prelude> import Data.Ord (Down(..))
Prelude Data.Ord> :info Down
newtype Down a = Down a         -- Defined in ‘Data.Ord’
instance Ord a => Ord (Down a)  -- Defined in ‘Data.Ord’
Prelude Data.Ord> Down 3 > Down 4
True
```

This can be very convenient for reversing sort order:

```hs
Prelude> import Data.Ord (Down(..), comparing)
Prelude Data.Ord> import Data.List (sortBy)
Prelude Data.Ord Data.List> sortBy (comparing Down) [1..10]
[10,9,8,7,6,5,4,3,2,1]
```
