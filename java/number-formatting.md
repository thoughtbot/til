# NumberFormatting 

## Assignment
Format a number for a specific locale. For example, the number 12345.123 should be formatted as `12,345.12` in the USA locale, but `12.345,12` in the German locale.

## Solution
```java
DecimalFormat currencyFormatter = (DecimalFormat) NumberFormat.getInstance(Locale.getDefault());

currencyFormatter.setMaximumFractionDigits(2);
currencyFormatter.setMinimumFractionDigits(2);

System.out.println(currencyFormatter.format(12345.12));
```

Depending on your default Locale the currencyFormatter will format the number the right way.

##### If you have a locale like `Locale.US` it will output:
```java
12,345.12
```

##### Or if you have a locale like `Locale.GERMANY`:
```java
12.345,12
```

### What about the Locale
Using `Locale.getDefault()` allows you to get the System default, so it depends on your settings. You can test it for other Locale's by using fixed locale values like: `Locale.GERMAN`or `Locale.US` for USA. You also can find the Local according to the `language`/`country` by using `Locale(String language)` or `Locale(String language, String country)`. More details can be found here: [Documentation for Locale].

### Executable Online Java Example:
Here is an in-browser example that you can try: [Coding Ground Example]
Steps to run: compile and execute.

[Coding Ground Example]:http://www.tutorialspoint.com/compile_java_online.php?PID=0Bw_CjBb95KQMbHZ0NWc1OVRONkE
[Documentation for Locale]:http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html
