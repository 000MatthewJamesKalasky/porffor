# rhemyn
a basic experimental wip regex engine/aot wasm compiler in js. regex engine for porffor. uses own regex parser, no dependencies (excluding porffor internals). <br>
age: ~1 day

made for use with porffor but could possibly be adapted, implementation/library notes:
- exposes functions for each regex "operation" (eg test, match)
- given a regex pattern string (eg `a+`), it returns a "function" object
- wasm function returned expects an i32 pointer to a utf-16 string (can add utf-8 option later if someone else actually wants to use this)

## syntax
🟢 supported 🟡 partial 🟠 parsed only 🔴 unsupported

- 🟢 literal characters (eg `a`)
- 🟢 escaping (eg `\.\n\cJ\x0a\u000a`)
  - 🟢 character itself (eg `\.`)
  - 🟢 escape sequences (eg `\n`)
  - 🟢 control character (eg `\cJ`)
  - 🟢 unicode code points (eg `\x00`, `\u0000`)
- 🟢 sets (eg `[ab]`)
  - 🟢 ranges (eg `[a-z]`)
  - 🟢 negated sets (eg `[^ab]`)
- 🟢 metacharacters
  - 🟢 dot (eg `a.b`)
  - 🟢 digit, not digit (eg `\d\D`)
  - 🟢 word, not word (eg `\w\W`)
  - 🟢 whitespace, not whitespace (eg `\s\S`)
- 🟠 quantifiers
  - 🟠 star (eg `a*`)
  - 🟠 plus (eg `a+`)
  - 🟠 optional (eg `a?`)
  - 🟠 lazy modifier (eg `a*?`)
  - 🔴 n repetitions (eg `a{4}`)
  - 🔴 n-m repetitions (eg `a{2,4}`)
- 🔴 assertions
  - 🔴 beginning (eg `^a`)
  - 🔴 end (eg `a$`)
  - 🔴 word boundary assertion (eg `\b\B`)