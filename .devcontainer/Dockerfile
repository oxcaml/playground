FROM mcr.microsoft.com/devcontainers/base:ubuntu-24.04

RUN apt-get update && apt-get -y install m4 build-essential autoconf opam libunwind-dev pkg-config

USER vscode

RUN opam init -a --disable-sandboxing --yes --bare && \
        opam update -a && \
        opam switch create 5.2.0+ox --yes \
        --repos "ox=git+https://github.com/oxcaml/opam-repository.git,default"

RUN opam install -y ocamlformat merlin ocaml-lsp-server odoc utop core parallel && opam clean -a
