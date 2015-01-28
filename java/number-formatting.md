# NumberFormatting 

## Assignment
Format a number for a specific locale. For example, the number 12345.124 should be formatted as `12,345.12` in the USA locale, but `12.345,78` in the German locale.

## Solution
```java
DecimalFormat currencyFormatter = (DecimalFormat) NumberFormat.getInstance(Locale.getDefault());

currencyFormatter.setMaximumFractionDigits(2);
currencyFormatter.setMinimumFractionDigits(2);

System.out.println(currencyFormatter.format(123456.12));
```

Depending on your default Locale the currencyFormatter will format the number in the right way for you.

##### Will output:
```java
-123,456.78
```

##### Or if you have a locale like `Locale.GERMANY`:
```java
-123.456,78
```

### Executable Online Java Example:
Here is an in-browser example that you can try: [Coding Ground Example]
Steps to run: compile and execute.

[Coding Ground Example]:http://goo.gl/wq7aa5
