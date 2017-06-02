# Using map function instead of for loop in Python command line option

In this sceanrio, we will write a for loop for iterating over range using 
Python command prompt

$ python -c "import sys; for r in range(10): print r"

But, this will fail with syntax error.

For loop does not work in command line option with import statement instead
you have to use map function with annoymous function

$ python -c "import sys; map(lambda x: sys.stdout.write('%d' %x), xrange(10))"

This will give you appropriate output.
