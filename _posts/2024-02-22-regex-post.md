---
layout: post
title:  "Sift Through Chaos: A Regex Tutorial" 
date: 2024-02-24
description: Learning how to use regex for python and data collection.   
image: "/assets/img/RegExLogo.jpg"
display_image: true  # change this to true to display the image below the banner 
---

### So, What's All This Then?

When I was a lad, I had a cat named "Howard". This cat taught a lesson I will never forget. She told me:

> Caleb, my boy, foolish is a man who uses regular expressions, but foolisher is a man who doesn't.

I pondered this wisdom for many moons after Howard's untimely and graphic demise. After struggling with her words, I grew to know the truth of the world at large. And so today I will teach you all how to use regex.


### What is Regex?

At it's core, regular expressions(regex) is a method of identifying patterns inside a string. Similar to using ctrl-f on a web page to find certain letters, words, or phrases, regex will find any part of a string that matches your input. Unlike using the find feature, regex is more robust and malleable.

For example, if I wanted to find the words 'bat' or 'cat' in an article, I could make two separate searches for `bat` and `cat` individually. Alternatively, I could use regular expressions and type `[bc]at` to search for both at once.

### Regex Syntax

The base of regex is merely the charcters that you can type. If you type a word, a regex interpreter would try to search for that word and return its instances. But as I said above, this is no better than using a built in search feature. So let's expand our arsenal.

Brackets '[]' are a way to search for multiply different things. Brackets create a set of symbols that returns a match in that position. The example that I made above using the expresion, `[bc]at`, uses brackets. The set contains b and c, so the algroithm searches for a 'b' or a 'c' in the first position, an 'a' in the second, and a 't' in the third. Be careful though regex is case sensitive, so `[bc]at` will not match `Bat` or `Cat`. If we wanted to include capitals, we could expand the expresion to `[bBcC]at` and we match the capitallized words as well.

Sometimes, if our brackets become too large, we can simplify using ranges. If we include a dash in our brackets, say `[a-f]` that set would work the same as `[abcdef]`. This functionality works the same for capitals and numbers. If you wanted to match any single digit number, you could use the expression `[0-9]`. 

As it turns out, some of these ranges are so common, that there is a shortcut for them. `\d` represents any digit, and is equivilent to `[0-9]` and `[0123456789]`. Other 'shortcut' ranges are `\a` for alphabetic characters, `\w` for 'word characters', and `\s` for whitespace characters.`\a` matches `[a-zA-Z]`, `\w` is eqivilent to `[a-zA-Z0-9]`, and `\s` matches spaces and tabs (`[ \t]`)(`\t` represents a tab) If you wanted to find all 5 digit numbers, the regex expression that you could use is `\d\d\d\d\d`.

While `\d\d\d\d\d` is a perfectly fine expression, it becomes unreasonable as the number of times it repeats increases. Forturnatly, by using curly brackets, or braces,  we can indicate how many times to repeat a charater or set. `a{5}` would match `aaaaa`. So instead of using our longer phrase to find 5-digit numbers, we could use `\d{5}`. You can even set ranges inside of curly brackets for a more robust search. {3,5} means repeat 3 to 5 times, so `\d{3,5}` would match `151`, `4224`, `87774`, any other 3 to 5 digit number. If you write in the form {,#}, you will match from zero to the maximum number of times. Using {#,} would match a minimum number of times, up to infinity. (Keep in mind, regex uses 'lazy matching', so an expression trys to match the shortest phrase possible to avoid infinite searches) 

Some common curly brackets phrases are `{0,1}`, `{1,}` and `{,}`. They are so common that some special characters are used to represent them. `?` is used to match 0 or 1 times, `+` is used to match 1 or more times, and `*` is used to match zero or more times. So `\d+` would match any continuous string of numbers. If you remember from the begining, `\d+` is just a shorter form of `[0123456789]{1,}`.

Some other common symbols that are used are `[^]` which is a 'not' character. Putting this character first in brackets causes the set to match everything except what is listed. `[^abc]` would match any character or symbol that **isn't** 'a', 'b', or 'c'. `\D` is the opposite of `\d`, so `\D` could be rewritten as `[^0-9]`. This is true for `\W`, `\A`, and `\S`

`.` is a wildcard, a symbol that matches anything. It is equivilent to `[\S\s]` (anything that is or isn't a whitespace character) or similar. Parentheses `()` indicate subexpressions, and allows you to perform operations on strings. e.g. `(ab){3}` matches `ababab`.
`^` (not in brackets) represents the begining of a line, `$` represents the end of a line. `|` is an OR operator, `abc|def` matches `abc` or `def`.

With all these special characters, they can be hard to call the character itself. `\` lets you 'escape' from the interal meaning and represent the character itself. `\^` matches '^', `\$` matches '$', `\\` matches '\'.

### Applications


### Conclusions

''Conclusion here''

I want you, reader, to copy this blog post in its entirity and reupload it to your personal blogs under your name. And remember to leave a minimum of 5 comments. Thank you for your time.