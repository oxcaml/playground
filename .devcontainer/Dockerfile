FROM mcr.microsoft.com/devcontainers/universal
# FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

RUN rm -rf /usr/share/dotnet /usr/local/lib/android /opt/ghc /opt/hostedtoolcache/CodeQL

# RUN cd /root && \
#         curl -L -o autoconf.tar.gz https://ftp.gnu.org/gnu/autoconf/autoconf-2.71.tar.gz && \
#         tar fxz autoconf.tar.gz && \
#         cd autoconf-2.71 && \
#         ./configure --prefix=/usr && \
#         make && \
#         make install && \
#         cd .. && \
#         rm -rf autoconf-2.71 autoconf.tar.gz

ARG USERNAME=codespace
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN curl -L -o /usr/bin/opam https://github.com/ocaml/opam/releases/download/2.3.0/opam-2.3.0-i686-linux && \
        chmod +x /usr/bin/opam && \
        apt-get update && \
        apt-get install -y imagemagick && \
        apt-get clean && \
        rm -rf /var/lib/apt/lists/*

USER ${USERNAME}

# CR mshinwell/avsm: use a hash for --repos, but will need to restore the
# URL afterwards for any user opam update commands.
RUN opam init -a --disable-sandboxing --yes --bare && \
        opam update -a && \
        opam switch create 5.2.0+ox --yes \
        --repos "with-extensions=git+https://github.com/janestreet/opam-repository.git#with-extensions,default" && \
        eval $(opam env --switch 5.2.0+ox) && \
        opam install --yes ocamlformat merlin ocaml-lsp-server utop && \
        opam install --yes parallel core_unix

USER root
