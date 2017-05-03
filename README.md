# boot-nodejs #
[![Clojars Project](https://img.shields.io/clojars/v/degree9/boot-nodejs.svg)](https://clojars.org/degree9/boot-nodejs)

Node.js wrapper task for [boot-clj][1].

* Provides `nodejs` task for generating node.js entrypoint.
* Provides `serve` task for executing node.js server.

> The following outlines basic usage of the task, extensive testing has not been done.
> Please submit issues and pull requests!

## Usage ##

Add `boot-nodejs` to your `build.boot` dependencies and `require` the namespace:

```clj
(set-env! :dependencies '[[degree9/boot-nodejs "X.Y.Z"]])
(require '[degree9.boot-nodejs :refer :all])
```

Generate a node.js cljs edn file.

```bash
boot nodejs -i app.server/init -e nodejs
```

Start a node.js server script.

```bash
boot serve -s nodejs
```

Use in a wrapper task:

```clojure
(boot/deftask start-server
  "Start app server."
  [...]
  (let [...]
    (comp
      (nodejs :init-fn 'app.server/init)
      (serve))))
```

## Task Options ##

The `nodejs` task exposes options for generating a node.js compatible .cljs.edn file.

```clojure
e edn       VAL str  "Node.js main edn name. (nodejs)"
i init-fn   VAL sym  "Node.js init function."
d develop       bool "Sets nodejs-cljs dev flag."
```

By default the `nodejs` task will produce a `nodejs.cljs.edn` file.

The `serve` task exposes options for starting a Node.js instance.

```clojure
s script VAL str  "Node.js main script file. (nodejs)"
```

If you use a custom `:edn` name for `nodejs` task, that name can be used for the `:script` option of the `serve` task.

***

[1]: https://github.com/boot-clj/boot
