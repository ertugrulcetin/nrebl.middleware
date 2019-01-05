# nrebl.middleware

*VERY ALPHA*

The start of an nREPL middleware that will spy on an nREPL connection
and capture the results of evaluation for browsing in
[REBL](https://github.com/cognitect-labs/REBL-distro).

**NOTE: REBL requires a commercial license if it's to be used for commercial work**

## Installation (leiningen)

Assuming you're running a recent leiningen (2.8.3) follow the steps:

1. Install REBL to a known path.
2. Add the following to your `~/.lein/profiles.clj` `:user` profile:

```clojure
 :user  {:repl-options {:nrepl-middleware [nrebl.middleware/wrap-nrebl]}
         :dependencies [[rickmoynihan/nrebl.middleware "0.1.0-SNAPSHOT"] ;; set this to the latest nrebl version
                        [org.clojure/core.async "0.4.490"]]
         :resource-paths ["/Users/rick/Software/rebl/REBL-0.9.109.jar"] ;; set this to where your REBL jar is installed
         :injections [(require '[cognitect.rebl :as rebl])] 
         }
```

3. Ensure `:resource-paths` in the snippet you inserted above is set to the fully qualified location for where your REBL `.jar` file can be found.

Whilst the above is the simplest layout, it can be preferable to instead put the above profile configuration into an `:nrebl` profile, and then merge that into `:user`.  This can help to organise your profiles more cleanly and aide in debugging profile issues.  This setup would then look something like this:

```clojure
 :nrebl  {:repl-options {:nrepl-middleware [nrebl.middleware/wrap-nrebl]}
         :dependencies [[rickmoynihan/nrebl.middleware "0.1.0-SNAPSHOT"] ;; set this to the latest nrebl version
                        [org.clojure/core.async "0.4.490"]]
         :resource-paths ["/Users/rick/Software/rebl/REBL-0.9.109.jar"] ;; set this to where your REBL jar is installed
         :injections [(require '[cognitect.rebl :as rebl])] 
         }

 :user [:nrebl
        ;;:other-tool-profiles...]	
```

## Usage (lein)

1. Run `lein repl` and/or connect to  nREPL with your Editor.
2. Evaluate `(rebl/ui)` (the :injections should make this available in every namespace)
3. The REBL UI should appear
4. Evaluate more forms in the REPL, they should each then appear in REBL.

## Installation (tools.deps)

1. Install [clojure](https://clojure.org/)
2. Install REBL to a known path
3. Setup your `deps.edn`

```clojure
{:aliases {:nrepl {:extra-deps {nrepl/nrepl {:mvn/version "0.4.5"}}}
           :rebl {:extra-deps {
	                  org.clojure/clojure {:mvn/version "1.10.0-RC3"}
                      rickmoynihan/rebl.middleware {:git/url "git@github.com:RickMoynihan/nrebl.middleware.git", :sha "6f37f09fef0df14b855b443838f7dcc0ff6fd1d1"}
                      org.clojure/core.async {:mvn/version "0.4.490"}
     	              com.cognitect/rebl {:local/root "<PATH-TO-REBL-JAR>/REBL-0.9.108/REBL-0.9.108.jar"}}}
           :cider {,,,} ;; configure cider/nrepl deps here
           }}}}
```

## Usage (tools.deps)

```
clj -A:nrepl:cider:rebl -m nrepl.cmdline --middleware '[nrebl.middleware/wrap-nrebl cider.nrepl/cider-middleware]'
```

Then connect to your REPL, and run

```
(cognitect.rebl/ui)
```

You should now be able to evaluate forms and have REBL capture them.

## Help Wanted

There's lots that can be done to improve this.  Help & suggestions welcome.

## License

Copyright © 2018 Rick Moynihan

Distributed under the Eclipse Public License either version 1.0 or (at
your option) any later version.
