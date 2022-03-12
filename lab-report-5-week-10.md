vim# Lab Report Week 8

*Abhishek Govindarasu*

# Finding Variances In Test Cases

Using the script.sh file, running `sh script.sh >> results_{version_of_md_parse}`
for both my implementation and the implementation provided in the markdown-parse 
repository generates two files that print the test file name, and then the 
respective output.

Then using diff, we can see the respective output for both cases.

```
92c92
< []
---
> [/foo]
212c212
< []
---
> [url]
230c230
< []
---
> [baz]
270c270
< [/bar\* "ti\*tle"]
---
> []
492c492
< [/f&ouml;&ouml; "f&ouml;&ouml;"]
---
...
```


## 1. Test File 14
```
\*not emphasized*
\<br/> not a tag
\[not a link](/foo)
\`not code`
1\. not a list
\* not a list
\# not a heading
\[foo]: /url "not a reference"
\&ouml; not a character entity
```


In this file, my implementation returns `[]`
While the main implementation returns `[/foo]`


Looking at the markdown, since the square brackets are escaped, `/foo` is not a link.
In the main code, the checks for escaped characters are not in place (bug).
In my code, the section `(?<![!\\\\])` in the regular expression is a negative lookbehind that ensures the previous character befor the `[` is
not a backslash.



## 2. Test File 487
```
[link](/my uri)
```

In this file, my implementation returns `[/my url]`
While the main implementation returns `[]`

Links should not have spaces in them, so the main implementation is correct.
The bug in by code is that in the regex:
``(?<![!\\\\])\\[(?:[a-zA-Z_ ]+(?:\\\\[\\[\\]\\(\\)\\!`]+)*)+[a-zA-Z]*\\]\\((.*?|\\n.+?|.+?\\n|\\n.+?\\n)\\)``
It uses `.` to check for repeated characters in ``(.*?|\\n.+?|.+?\\n|\\n.+?\\n)``. This means that all characters including spaces is allowed and accepted in the link field. The fix is to replace every instance of `.` in that part of the regex to a more specific character class, maybe `[a-ZA-Z0-9_]` for example, which would then only allow those characters to be present in the link
