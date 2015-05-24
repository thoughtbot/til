# Custom page titles

Today I learned how you can make a custom title to be displayed for each page.
The extra part I have in this file's name is a part which is always displayed regardless of the title.
It is an easy one but I think it is an helpful TIL. Especially since the static part of the website allows 
users searching for your site to see what your site is about!


```haml
%title= (yield(:title) + ' :: ' unless yield(:title).blank?).to_s + 'Makichan - Anime pinboard'

```

This is snipped from my own template file. The ``` ' :: ' ``` part is the delimiter (I added spaces to the delimiter so you don't have to think about them when defining the title in the views), 
to be shown between the "dynamic" and "static" parts of the title. The second string is the static part of the title,
 which is always shown.

What the unless part is doing is to only show the "static" part of the title. In this case the static part is: "Makichan - Anime pinboard" If the title is blank (or not defined in the view) the delimiter is also hidden. 

In your view files you can do:

```haml
= content_for(:title, " Show #{@pin.title}")
```
