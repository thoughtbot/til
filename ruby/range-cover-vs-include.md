# Range cover? vs include? method

The `cover?` method yields better performance than `include?`,
however there are subtle differences to when one should be used over other.

## Range#include?

This method checks that the argument is actually present as an element in the
range.

## Range#cover?

This method checks if an argument is covered by the range.
It checks that the argument fits somewhere between the beginning and the end of
the range.

Prefer `Range#cover?` its efficiency,
since it handles most of the real-world situations.
