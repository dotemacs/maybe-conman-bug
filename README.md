# myapp

A Clojure library designed to demo a potential bug in [conman](https://github.com/luminus-framework/conman)

## Usage

```
git clone https://github.com/dotemacs/maybe-conman-bug
cd maybe-conman-bug
lein deps
lein repl
```
then in the REPL

```clojure
(require 'myapp.db :verbose)
(in-ns 'myapp.db)
(mount/start)
```
and the following error pops up:

```
IllegalArgumentException Invalid configuration options: (:adapter)
sun.reflect.NativeConstructorAccessorImpl.newInstance0
(NativeConstructorAccessorImpl.java:-2)
```

Then if I comment out **:adapter** in **pool-spec** so that it looks like:

```clojure
(def pool-spec
  {;;:adapter    :postgresql
   :init-size  1
   :min-idle   1
   :max-idle   4
   :max-active 32
   :jdbc-url "jdbc:postgresql://localhost/myapp"})
```

eval **pool-spec** and back in the repl:

```clojure
(mount/start)

```
the connection is established just fine:

```
{:started ["#'myapp.db/*db*"]}
```
