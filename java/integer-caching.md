Number Caching
--------------

The following code creates 2 integer objects and compares them:

```
public static void main(String[] args) {
  Integer a = 1000, b = 1000;
  System.out.println(a == b);
  Integer c = 100, d = 100;
  System.out.println(c == d);
}
```

When ran, this block of code will print out:

Expected output
---------------
```
false
false
```

Actual output
-------------
```
false
true
```

Reason
------
JVM caches objects for int values from -128 to 127 for some optimisation purposes. In this way, references of "c" and "d" is the same.
