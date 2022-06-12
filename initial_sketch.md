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
- pass
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

# immutable types
changeme = "s3cr3tp4ssw0rd"
changeme = 10 # ERR, won't be implicitly converted to :str either

shadowme = 10
shadowme = 11 # OK
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
    :for s :in ... {
      bio = .fmt "{bio}\n{s}"
    }
  }
  bio
}

# no need to anotate type :any of input variable
:fn echo_machine(anything) -> :any {
  anything
}
```

concurrency
- bash supports subshells with `wait` and `( dostuff )`
- syntax pending, syntax is being worked
- `.fork` or `.spawn` with `.wait` ?
```
#! /bin/bash
sleep 3 & sleep 5 ; wait < <(jobs -p)
# also wait -n / wait -f

#! backspace
:fn do_smth() -> :str {
  .print "doing smth..."
  core.sleep 3
  "done"
}

pid = .fork do_smth()
.wait pid

pid = .fork () => {
  .print "anon func"
}
```

ok turns out bash 4 has associative arrays so
- not sure if this feature is worth, but noting it
- maybe just forget this and defer to jq / library
- bash 4 apparently not on darwin due to licensing so...

`:case`, `:match` or both?
```
result = 3
place = :match result {
  1 => "1st"
  2 => "2nd"
  r :if r <= 3 && r >= 5 =>
    "not bad"
  _ => "nt"
}
```

list comprehensions
```
[x :for x :in 1..10 :if num.even]
```

custom types? or just validate?
- do the :num things need to be a different kind of object in a lang?
  - so types and keywords all share the same `:` prefix?
```
# custom type
# declare conditions
#   list of 2, both number
:typedef coord {
  .type   == :list # typechecking needs discussion re: types
  .length == 2
  list.map .type == [:num, :num]
}

my_coordinate ::coord = ["five", 5] # ERR
my_coordinate ::coord = [5, 5]      # OK
list.map .type my_coordinate == [:num, :num]

# or pipe to get expression (parser must look ahead)
coord_types = my_coordinate
  | list.map .type
coord_types == [:num, :num] # OK

# (uglier) alternative
:fn is_valid_coord(input :list) {
  :pass :if .type input == :list :else .return 1
  :if .length input == 2 ?                   :pass : .return 1
  :if list.map .type input == [:num, :num] ? :pass : .return 1
}
```

## further questions
how will return work? exit code + value?
null type? no enum wrapper...

# :words list

todo: move this to a new doc

## types
```
# value types
:num
:str
:list
:function

# special types
:any
:type # val types are of this type

# custom types
:typedef
::mytype
```

## control flow
```
:if
:elif
:else

:while
:for
:in

:match

:pass
:pass
:break
```
