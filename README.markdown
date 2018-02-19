# :smile: Cl-Emoji [![Quicklisp](http://quickdocs.org/badge/cl-emoji.svg)](http://quickdocs.org/cl-emoji/)
cl-emoji provides the Unicode emoji characters

:smile: :heart_eyes: :scream: :alien: :fire: :zzz: :hand:

cl-emoji is able to treat Emoji 5.0 defined in Unicode 10.0! (ex. UFO; https://emojipedia.org/flying-saucer/)

## :boom: Usage

```lisp
(ql:quickload :cl-emoji)
(emoji:codepoint '("U+1F600"))
=> "😀"
(emoji:name "grinning face")
=> "😀"
(emoji:annotation "face")
=> (("😀" "U+1F600" "grinning face" ("face" "grin" "person")) ...)

;; We can also get emoji with slack-like string
(emoji:alpha-code ":grin:")
=> "😁"
```

```lisp
(format t "Hello~a!~%" (emoji:name "grinning face"))
=> Hello😀!
```
According to PR #3, we can use following APIs.

If you tell emoji version to cl-emoji API, do like this (and I checked if path generated at API calling):

```lisp
CL-USRE> (trace format)
CL-USER> (cl-emoji:annotation "grin")
  0: (FORMAT NIL "file ~A"
             "/home/foo/cl-emoji/data/emoji_4.0_release-30.lisp")
  0: FORMAT returned
       "file /home/foo/cl-emoji/data/emoji_4.0_release-30.lisp"
(("😀" ("U+1F600") "grinning face" ("face" "grin") "Smileys & People"
  "face-positive")
 ...)
CL-USER> (let ((cl-emoji:*current-version* (second cl-emoji:+versions+)))
           (cl-emoji:annotation "grin"))
  0: (FORMAT NIL "file ~A"
             "/home/foo/cl-emoji/data/emoji_5.0_release-31.lisp")
  0: FORMAT returned
       "file /home/foo/cl-emoji/data/emoji_5.0_release-31.lisp"
(("😀" ("U+1F600") "grinning face" ("face" "grin") "Smileys & People"
  "face-positive")
 ...)
```

### :smile: Groups and Subgroups

Those are appears in [Full Emoji Data](http://www.unicode.org/emoji/charts-beta/full-emoji-list.html), for instance `Smileys & People` is a group and `face-positive` is a subgroup.

You can get emoji by group name and subgroup name with API `cl-emoji:group` and `cl-emoji:subgroup`.
see also [Full Emoji Data](http://unicode.org/emoji/charts/full-emoji-list.html)

### :smile: Search
If you want to search available annotations/groups/subgroups, then.

```
CL-USER> (emoji:group-apropos "foo")

CL-USER> (emoji:subgroup-apropos "bar")

CL-USER> (emoji:annotation-apropos "bazz")

```

## :laughing: Author

* asciian (asciian@outlook.jp)

## :ok_hand: Copyright

Copyright (c) 2015 asciian (asciian@outlook.jp)

* src/cl-emoji.lisp is licensed under the MIT License
* data/emoji-list.lisp is licensed under the Unicoded License
