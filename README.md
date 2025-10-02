# workflow templates

This repo contains Github Action workflows to re-use on a central place for maintenance.

## content

### build.yaml

This builds from Go code multi-platform binaries. So, it expects a main.go file in the repository root and will be executed on Releases

### build-test.yaml

This build from Go code a `testapp` to see if build works. Go format is also executed and upload an artifact for test purpose

### container.yaml

This build a multi-platform container image with Docker, based on a Dockerfile which is also part of this repo. The container image will pushed on Github Container Registry and signed with Github OIDC within cosign. Tags are workflow execute and pushs on branch named dev.

### coverage.yaml

This test Go code and count the coverage to a badge in the README.md. This workflow runs only on main branch

###  helm.yaml

This build a Helm package with the content of /chart directory on the repo. Executor are changes in this directory. The package will pushed to the Github Registry.

###  ko.yaml

This build a container image from the Go code without Docker. Due the parallel execution of the container workflow, this workflow is manually to execute, but on each push.

### e2e-test.yaml

This build creates a Kind Cluster with different Kubernetes Versions and installs a Helm Chart from the directory /chart. The Helm Chart must install sucessful, otherwise the task will fail.

## usage

The workflows will be released but can be copied to the project repo on their needs. But there is no maintenance beside the dependbot activities. 

Workflows can be also included in the project repo. Example:

https://github.com/eumel8/helloworld/.github/workflows/container.yaml

```yaml
name: Build Docker Container (template)

on:
  push:

jobs:
  call-workflow:
    uses: eumel8/workflow-templates/.github/workflows/container.yaml@0.0.5
```
