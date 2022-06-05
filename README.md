# backspace
a simple scripting language that transpiles to bash

## motivation

i was creating a bash script for my dotfiles and had a few thoughts:
- bash is awesome!
- really quick to just "get things done"
- ultra-portable, not even python required

...but it's also quite a pain to write and debug
- the syntax / variable gotchas are rly terrible
- tbh spent more time on stackoverflow debugging than in the editor

after taking some time to read and really learn the bash (big s/o to
[TLDP.org's guide](https://tldp.org/LDP/abs/html/)), one thing really stood
out to me:

> i love the minimal type system (number, string, or list)

- do we reaaalllyy need much more than that to just get things done?

these days, "general-purpose" languages can do pretty much everything under
the sun. still, i believe there's something to be said about languages that
instead do one thing and do it well ("unix philosophy"?).

a great example of a language that embraced this ideas is elm, a functional
language for building web ui's. it took away the need to write complex
javascript to manage state and made building ui's genuinely more enjoyable.[^1]

i'd argue that javascript is so widely ~~loved~~ adopted for the same reason
that we still write bash today. it's just **everywhere**... and it gets the
job done!

although javascript, like bash, can be a real pita to write, its shortcomings
didn't stop it from becoming the most popular programming language in the
world... the community just _made it better_.
- it got faster (v8 / nodejs)
- writing became easier (coffeeScript, typescript, elm, ...)
- websites got stacked (ember, angular, react, vue, ...)
- and they improved the language! (ES6)

so what if something similar could be done for bash?

tl;dr bash is awesome but can suck to write. let's fix that.

[^1]: recommended reading: ["On General-Purpose Languages"](https://github.com/elm/projects/blob/master/notes/on-general-purpose.md) by the elm creator.