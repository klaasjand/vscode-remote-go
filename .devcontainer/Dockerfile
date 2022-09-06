FROM golang:1.19.0-bullseye
LABEL maintainer="Klaas Jan Dijksterhuis"

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create a user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        curl \
        git

# Remove or comment out to use root user
USER $USERNAME

# goimports updates your Go import lines, adding missing ones and removing unreferenced ones.
RUN go install golang.org/x/tools/cmd/goimports@latest
# Simple utility for extracting a JSON representation of the declarations in a Go source file.
RUN go install github.com/ramya-rao-a/go-outline@latest
# gopls provides IDE features, such as as intelligent autocompletion, signature help, refactoring, and workspace symbol search.
RUN go install golang.org/x/tools/gopls@latest

# Tools below are needed for the basic features of the Go extension.
RUN go install github.com/uudashr/gopkgs/v2/cmd/gopkgs@latest
RUN go install github.com/go-delve/delve/cmd/dlv@latest
RUN go install honnef.co/go/tools/cmd/staticcheck@latest
