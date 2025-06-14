FROM mcr.microsoft.com/devcontainers/universal
# FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

RUN df -h

RUN rm -rf /usr/share/dotnet /usr/local/lib/android /opt/ghc /opt/hostedtoolcache/CodeQL

RUN du -sh /usr/*
RUN du -sh /usr/local/*
RUN du -sh /opt/*
RUN ls -l /

RUN df -h

RUN cd /root && \
        curl -L -o autoconf.tar.gz https://ftp.gnu.org/gnu/autoconf/autoconf-2.71.tar.gz && \
        tar fxz autoconf.tar.gz && \
        cd autoconf-2.71 && \
        ./configure --prefix=/usr && \
        make && \
        make install && \
        cd .. && \
        rm -rf autoconf-2.71 autoconf.tar.gz

ARG USERNAME=codespace
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN curl -L -o /usr/bin/opam https://github.com/ocaml/opam/releases/download/2.3.0/opam-2.3.0-i686-linux && \
        chmod +x /usr/bin/opam && \
        apt-get update && \
        apt-get remove -y swig3.0 unixodbc-dev libpq-dev \
        default-libmysqlclient-dev libgdiplus jq python3-pip sqlite3 \
        libsqlite3-dev tk-dev uuid-dev clang lldb llvm gdb vim-doc xtail \
        libsecret-1-dev && \
        apt-get install -y imagemagick && \
        apt-get clean && \
        rm -rf /var/lib/apt/lists/*

RUN df -h

USER ${USERNAME}

# CR mshinwell/avsm: use a hash for --repos, but will need to restore the
# URL afterwards for any user opam update commands.
RUN opam init -a --disable-sandboxing --yes --bare && \
        opam update -a && \
        opam switch create 5.2.0+ox --yes \
        --repos "with-extensions=git+https://github.com/janestreet/opam-repository.git#with-extensions,default" && \
        eval $(opam env --switch 5.2.0+ox) && \
        opam install --yes ocamlformat && \
        opam install --yes merlin && \
        opam install --yes ocaml-lsp-server && \
        opam install --yes utop && \
        opam install --yes parallel && \
        opam install --yes core_unix

RUN df -h

USER root
