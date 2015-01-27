# NumberFormatting 

## Assignment
How can someone format a number easily, without thinking too much about how the format would look like in a specific locale. Let's say we want to format: `12345.124` that it will look something like: `12,345.12` of course special characters according to the locale, but how can this be done?

## Solution
```java
DecimalFormat currencyFormatter = (DecimalFormat) NumberFormat.getInstance(Locale.getDefault());

currencyFormatter.setMaximumFractionDigits(2);
currencyFormatter.setMinimumFractionDigits(2);

System.out.println(currencyFormatter.format(123456.12));
```

Depending on your default Locale the currencyFormatter will format the number in the right way for you.

##### Will output:
```
-123,456.78
```

##### Or if you have a locale like `Locale.GERMANY`:
```java
-123.456,78
```

### Executable Online Java Example:
I prepared an online java testing for you here: [Coding Ground Example] All you have to do is press: compile and execute. Hope you like it.

[Coding Ground Example]:http://goo.gl/wq7aa5