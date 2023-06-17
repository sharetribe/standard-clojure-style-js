# clojurefmt-js

A library to format Clojure code written in ~1000 lines of JavaScript.

## TODO

- [ ] need to add additional cases for namespace maps (what is allowed?)
- [ ] PR upstream to Clojure-Sublimed the option map for Repeat (can remove Repeat1)
- [ ] chat with Nikita about what he wants to do about emoji length inside of Strings
- [ ] add a test case for every rule

## Formatting Rules

- trim trailing whitespace (ie: `rtrim` every line)
- ensure a single newline character (`\n`) at the end of the file
- convert all tab characters to spaces (except tab characters inside of Strings)
- [cljfmt option] `:remove-surrounding-whitespace?` = true
- [cljfmt option] `:remove-trailing-whitespace?` = true
- [cljfmt option] `:insert-missing-whitespace?` = true
- [cljfmt option] `:remove-consecutive-blank-lines?` = true
- format and sort `ns` forms according to Stuart Sierra's [how to ns]
- indentation follows the guide from Niki Tonsky's [Better clojure formatting]
- comments that contain the String `clojurefmt:ignore` cause the next form to be ignored by the formatter

[how to ns]:https://stuartsierra.com/2016/clojure-how-to-ns.html
[cljfmt option]:https://github.com/weavejester/cljfmt#formatting-options
[Better clojure formatting]:https://tonsky.me/blog/clojurefmt/

## Things that clojurefmt-js does NOT do

- no config options
  - all projects using clojurefmt-js follow the same rules
- From cljfmt:
  > "It is not the goal of the project to provide a one-to-one mapping between a Clojure syntax tree and formatted text; rather the intent is to correct formatting errors with minimal changes to the existing structure of the text.
  > If you want format completely unstructured Clojure code, the [zprint project](https://github.com/kkinnear/zprint) may be more suitable.
- no enforced max line length
  - text editors have the ability to wrap lines if you desire
- vertical alignment of `let` forms and map literals are allowed
  - the choice is up to the author
  - [cljfmt option] `:remove-multiple-non-indenting-spaces?` = false
  - I have seen too many code examples where vertical alignment adds clarity
- no configuration or special rules for indentation
  - the rules from [Better clojure formatting] are simple, easy to learn, and produce consistent-looking code
  - 100% compatible with [Parinfer] users
  - avoids the complexity of the [cljfmt `:indents` option]
  - avoids the complexity of different rules for different forms (ie: no [semantic indentation])

[Parinfer]:https://shaunlebron.github.io/parinfer/
[cljfmt `:indents` option]:https://github.com/weavejester/cljfmt/blob/master/docs/INDENTS.md
[semantic indentation]:https://guide.clojure.style/#body-indentation

## References

- https://clojureverse.org/t/clj-commons-building-a-formatter-like-gofmt-for-clojure/3240/95
- https://github.com/clj-commons/formatter/issues/9
- https://tonsky.me/blog/clojurefmt/
- https://github.com/parinfer/parindent
- [emoji length article](https://hsivonen.fi/string-length/)

## Development

```sh
## run unit tests
bun test

## test a single file
bun run jest format.test.js

## lint JS
bun run lint
```

## License

[ISC License](LICENSE.md)
