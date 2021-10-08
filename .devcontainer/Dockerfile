# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.192.0/containers/ubuntu/.devcontainer/base.Dockerfile

# [Choice] Ubuntu version: bionic, focal
ARG VARIANT="focal"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

RUN \
  curl -fsSLo /usr/share/keyrings/yourbase.asc https://apt.yourbase.io/signing-key.asc && \
  echo "deb [arch=amd64 signed-by=/usr/share/keyrings/yourbase.asc] https://apt.yourbase.io stable main" > /etc/apt/sources.list.d/yourbase.list && \
  apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
      build-essential \
      libreadline-dev \
      libssl-dev \
      yb \
      zlib1g-dev


