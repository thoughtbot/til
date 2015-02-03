# Varying Length String
The standard [ISO/IEC 1539](http://www.iso.org/iso/catalogue_detail.htm?csnumber=6129) has introduced the concept of *iso varying string* in Fortran. The modern Fortran 2003+ has standardized the concept of *varying length string*: a string of arbitrary and dynamical variable length.

### Define a varying length string
In Fortran 2003 a varying length string can be defined a deferred length, allocatable character variable
```fortran
character(len=:), allocatable:: string
```

### Use a varying length string
There are essentially two ways to use a varying string:

1. Explicitly allocate it;
2. exploit the LHS automatic allocation of Fortran 2003+.

#### Explicit allocation
To allocate an empty string of `60` characters type
```fortran
allocate(character(len=60) :: string)
```
or to allocate a string containing a default value type
```fortran
allocate(string, source='my default value')
```
#### Exploit LHS automatic allocation
Modern Fortran standards (2003+) allow the automatic (re)allocation of the Left Hand Side (LHS) of an expression if it has the attribute `allocatable`. This feature can be exploited to automatically vary the string length to fit the actual value
```fortran
string = 'my default value'
```
By default, many compilers does not allow the LHS (re)allocation, thus it must be explicitly enable at compile time. The following is an incomplete list of switches to enable LHS (re)allocation with the most used compiler:

+ *GNU gfortran* `-frealloc-lhs`
+ *Intel Fortran Compiler* `-assume realloc_lhs`
+ *IBM XL Fortran Compiler* `-qxlf2003=autorealloc`

### Note
A varying length string can be used as any other character variables except for the `read` built-in function: in order to use a varying length string into a `read` expression, the string must be previously allocated.
