# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.148.1/containers/ubuntu/.devcontainer/base.Dockerfile

# [Choice] Ubuntu version: bionic, focal
ARG VARIANT="focal"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# https://learn.hashicorp.com/tutorials/terraform/install-cli
# hadolint ignore=DL3008
RUN apt-get update && apt-get install -y --no-install-recommends software-properties-common \
    && curl -fsSL https://apt.releases.hashicorp.com/gpg | apt-key add - \
    && apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main" \
    && apt-get update && apt-get install -y --no-install-recommends terraform \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# tflint
# https://github.com/terraform-linters/tflint
# hadolint ignore=DL3008
RUN apt-get update && apt-get install -y --no-install-recommends curl unzip \
    && curl -L "$(curl -Ls https://api.github.com/repos/terraform-linters/tflint/releases/latest | grep -o -E "https://.+?_linux_amd64.zip")" -o tflint.zip \
    && unzip tflint.zip \
    && rm tflint.zip \
    && mv tflint /usr/local/bin/ \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# tfsec
ENV BASHRC=/home/vscode/.bashrc
ENV GOPATH=/home/vscode/go
# hadolint ignore=DL3008
RUN touch $BASHRC \
    && mkdir -p $GOPATH \
    && echo 'export PATH='"$GOPATH/bin:$PATH" >> $BASHRC \
    && export PATH="$GOPATH/bin:$PATH" \
    && echo 'export TZ=Asia/Tokyo' >> $BASHRC \
    && export TZ=Asia/Tokyo \
    && echo Asia/Tokyo > /etc/timezone \
    && ln -snf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
    && apt-get install -y --no-install-recommends golang git \
    && go get -u github.com/tfsec/tfsec/cmd/tfsec \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
