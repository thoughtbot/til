# Sectioning

You can partially apply an infix function by wrapping one argument and the
function name in parentheses. When the returned function is called with an
argument, Haskell will apply that argument to whichever side was left blank.
This is known as [sectioning]. Sectioning is often used when converting to
[point-free style]

```hs
-- Infix function +
f x = 3 + x

-- Point-free style
-- Haskell will apply the argument to the right side of +
f = (3+)

-- Point-free style
-- Haskell will apply the argument to the left side of +
-- Since addition is commutative, this is equivalent to the definition above
f = (+3)
```

[sectioning]: https://www.haskell.org/haskellwiki/Section_of_an_infix_operator
[point-free style]: https://www.haskell.org/haskellwiki/Pointfree
