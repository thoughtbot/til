# Yanking text to register

Yanking and deleting text will save the text to the same unnamed register. Every time you delete a word, your 
yanked word will be overwritten. This caused me endless amounts of frustration when I accidentally deleted a word and had to
remember what I yanked earlier.

I learned that you can specify a register to save your yanked word to by prepending your yank command with `"a`. Where `a`
is a register. There are a number of different registers which do different things. If you want to learn more read VIM's [register
documentation](http://vimdoc.sourceforge.net/htmldoc/change.html#registers).

An example usage is:

`"ayw`

This will save the yanked word to the register `a`. After deleting various things in your file you can always paste your yanked
word by:

`"ap`

Even after deleting various words in your file. Your yanked word will always be in register `a`.
The VIM wiki has more details on [Replacing a word with yanked text](http://vim.wikia.com/wiki/Replace_a_word_with_yanked_text).

# More on Registers

[Zamith](https://github.com/zamith) mentioned using the null register which is the black hole register. Whatever goes in there is gone forever. This is his example:

```
yw       # Save a word to the unnamed register
"_dw     # Delete a word and "save" to the _ register
```
  
If you then try to `"_p`, nothing will happen, because the `_` register never saves anything. The unnamed register (which is mentioned above) can also be set to the clipboard. Which is useful for copying content outside of VIM.

`set clipboard=unnamed`
  
Another tip is to use the `:registers` command in VIM. This command will show you what is in each register. Thanks [iwz](https://github.com/iwz) for the tip!

