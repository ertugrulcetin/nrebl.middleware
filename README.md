# nrebl.middleware

*VERY ALPHA*

The start of an nREPL middleware that will spy on an nREPL connection
and capture the results of evaluation for browsing in
[REBL](https://github.com/cognitect-labs/REBL-distro).

## Installation

Multiple setups should be possible.  Here we describe one way using
tools.deps.

1. Install [clojure](https://clojure.org/)
2. Install REBL to a known path
3. Setup your `deps.edn`

```clojure
{:aliases {:nrepl {:extra-deps {nrepl/nrepl {:mvn/version "0.4.5"}}}
           :rebl {:extra-deps {
	                  org.clojure/clojure {:mvn/version "1.10.0-RC2"}
                      org.clojure/core.async {:mvn/version "0.4.490"}
     	              com.cognitect/rebl {:local/root "<PATH-TO-REBL-JAR>/REBL-0.9.108/REBL-0.9.108.jar"}}}
           :cider {,,,} ;; configure cider/nrepl deps here
           }}}}
```

## Usage

```
clj -A:nrepl:cider:rebl -m nrepl.cmdline --middleware '[nrebl.middleware/wrap-nrebl cider.nrepl/cider-middleware]'
```

## Help Wanted

There's lots that can be done to improve this.  Help & suggestions welcome.

## License

Copyright © 2018 FIXME

Distributed under the Eclipse Public License either version 1.0 or (at
your option) any later version.