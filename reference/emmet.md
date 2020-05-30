# Emmet

> [返回参考](/reference/)

## Base

Operation      | Transction
---------------|-----------------------------
Child: >       | div>ul>li
Sibling: +     | div+div>p>span+em
Climb-up: ^    | div+div>p>span+em^bq
Multi: *       | ul>li*5
Grouping: ()   | div>(div>ul>li*2>a)+div>p
               | (div>dl>(dt+dd)*3)+footer>p
ID and CLASS   | div#header+div.page.class2
Custom attr    | td[title="Hi!" colspan=3]
Numbering: $   | ul>li.item$*5 (item1..item5)
               | ul>li.item$$$*5 (item0001..)
Reverse Num    | ul>li.item$@-*5
From 3         | ul>li.item$@3*5
Reverse From 3 | ul>li.item$@-3*5
Text: {}       | a{Click me}
               | p>{Click}+a{here}+{to jump}

## Implicit tag names

Short        | Full
-------------|------------------
.cls1>.cls2  | div.cls1>div.cls2
em>.info     | em>span.info
ul>.item*3   | ul>li.item*3
table>#rw$*4 | table>tr#rw$*4

## Html

* **Shortcuts**

0                    | 1                              | 2
---------------------|--------------------------------|------------------------------------
script               | style                          | link
form                 | input                          | label
hr                   | br                             | form:get
script:src           | link:css                       | a:link
input:text, input:t  | input:password, input:p        | input:checkbox, input:c
input:radio, input:r | input:file, input:f            | input:submit, input:s ; input:reset
input:image, input:i | input:button, input:b          | select:disabled, select:d
option, opt          | button:submit, button:s, btn:s | button:disabled, button:d, btn:d

* **Shortened**

Short      | Tranaction & Full    | Short   | Tranaction & Full
-----------|----------------------|---------|----------------------------
! / html:5 | html page code       | btn     | `<button></button>`
hdr        | `<header></header>`  | ftr     | `<footer></footer>`
str        | `<strong></strong>`  | bq      | `<blockquote></blockquote>`
inp        | input with name & id | ifr     | iframe
table+     | table>tr>td          | select+ | select>option
dl+        | dl>dt+dd             | ul+/ol+ | ul>li/ol>li