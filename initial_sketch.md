# design sketch

working document to design paradigmn, syntax, features, etc.

# words

- functional-bias but nowhere near pure

# language features

## types
- number
- string
  - heredocs
- list
- bool?

## control flow
### structures
- if / elif / else
- for _ in _
- case
- while until?
- |, >, <?
- continue
- break

---
obligatory hello world
- parens optional
```
# comment
.print "hello, world"
```

anything with `.` is builtin to something else
- ex: `.print` is builtin to prelude
- the following uses the `slice` function from the `str` lib
```
str.slice "hello" 4
```

types
```
808        # number
"yo"       # string
["ok", 90] # list
```
variables
- ANY alphanumeric with or without underscores that starts with a letter
- therefore everything that starts with a letter is owned by you
```
var = 5
my_favorite_word = "five"
list_of_5_things = ["list", "of", "five", "things", 5]

# no null, every type has a "false" val
nonull = 0
empty = ""
false = [] # follows the var name rules, so its valid

# immutable

```

functions
- declarative signature
- `:fn` is a keyword
```
# 1+ args, any type
# no return

:fn hello(name) { 
  .print "yo, {name}"
}
```

putting it together
```
:fn make_bio(first :str, last :str, ...) -> :str {
  bio = .fmt "name: {fn} {ln} \n and i like {fav_foods}"
  :if ... {
    for s in ... {
      bio = .fmt "{bio}\n{s}"
    }
  }
  bio
}
```