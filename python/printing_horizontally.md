# Printing Horizontally

The print() function can't be used to print horizontally (simulate a user 
typing) because print() inserts a new line at the end of the string. Instead, 
sys.stdout.write() has to be used.


## Example

    import sys
    import time
    
    def slow_type(string):
        for letter in string:
            sys.stdout.write(letter)
            sys.stdout.flush()
            time.sleep(0.07) # Randon can be used to vary the speed of scroll.

    slow_type("This string will be typed horizontally on the console\n")
