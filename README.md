# dousu-vscode-dev-containers

![Docker Image CI](https://github.com/dousu/dousu-vscode-dev-containers/workflows/Docker%20Image%20CI/badge.svg)

Images and configurations for VScode Remote-Container

## How to Use

```
git submodule add <URL> dev-containers-repo
// For Mac or Linux
ln -s dev-containers-repo/containers/<image name>/.devcontainer .devcontainer
// For Windows
mklink /D .devcontainer dev-containers-repo\containers\kubernetes-helm\.devcontainer
code .
```

## Linting

```
docker run --rm -i hadolint/hadolint < containers/python-docker-gcloud/.devcontainer/Dockerfile
```
