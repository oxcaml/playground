# A playground for OxCaml

To make a playground, press the green "Code" button, then select "+" next to
"Codespaces".  A new Codespace will open.  It currently takes maybe 20 or 30
minutes to initialize; please be patient.  We'll work on improving this startup
time shortly.  You can click the link in the status popup in the bottom-right
of the window to see current progress (although there are no spinners).

Once initialized you should have a full opam environment with the OxCaml
compiler and dune on the path.  VSCode will have the OCaml Platform plugin
together with the LSP server and merlin, the editor assistant.

## Building your first OxCaml project

```shell
$ cd parallel-example/filter
$ dune build filter.exe
$ ../_build/default/filter/filter.exe
$ mogrify -format jpg filtered-ox.pgm
```

Then you can open `filtered-ox.pgm` directly from the sidebar on the left (expand the `parallel-example` directory in the tree view).  Behold the *filtered ox*.
