## GitHub Actions

GitHub has built-in capability to execute workflows upon pushes to the repository, exposing these advanced capabilities to the everyday GitHub users.

Examples for GitHub Actions include minimal execution of your end-to-end workflow.

As an example, have a look at this [Long-read-proteogenomics](https://github.com/sheynkman-lab/Long-Read-Proteogenomics) repository and the badges for workflows that it contains.

## End-to-End Workflow testing

There are two workflows executed here within the limits GitHub offers, basically 8GB of memory and small amount of diskspace.

```bash
name: Testing for Long Reads Proteogenomics with Sqanti
# This workflow runs the pipeline with the minimal test dataset to check that it completes without any syntax errors
on:
  push:
    branches:
      - dev
  pull_request:
  release:
    types: [published]

jobs:
  test:
    name: Run workflow tests
    runs-on: ubuntu-latest
    env:
      NXF_VER: ${{ matrix.nxf_ver }}
      NXF_ANSI_LOG: false
    strategy:
      matrix:
        # Nextflow versions: check pipeline minimum and current latest
        nxf_ver: ['20.01.0', '']
    steps:
      - name: Check out pipeline code
        uses: actions/checkout@v2
      - name: Install Nextflow
        run: |
          wget -qO- get.nextflow.io | bash
          sudo mv nextflow /usr/local/bin/
      - name: Run pipeline with test data
        run: |
          nextflow run ${GITHUB_WORKSPACE} --config conf/test_with_sqanti.config
```

This vignette walks the user through the automatic testing workflow from [Long Read Proteogenomics](https://github.com/sheynkman-lab/Long-Read-Proteogenomics/wiki/Vignette-Long-Read-Proteogenomics-Workflow-with-Test-Data) - help the researcher in understanding the details of inputs, outputs and scripts that are very straightforward shell scripts helps one understand what is happening here, and better yet, how the researcher can do this with their own work. 
There are a lot of details here, but one doesn't need to know much to get started with GitHub actions


## Automatic deployment of actions

In the case of the three Dockerfiles reviewed in the previous lesson, each were released once successfully built and then we used GitHub actions to automatically build and publish the images, making them accessible with a degree of confidence that they have been built and therefore there are no syntactical reasons why it should not run.

This means that we are in a way, using GitHub actions as a complier for our images.

## Example of Creating GitHub actions for star-docker container.

The STAR docker is the simplest of containers.  Why we would do so is that one can imagine scaling to 100s to 1000s of files that need to be aligned with STAR.  The smaller the image, the smaller the machine that could be used to execute that image.   Food for thought as we continue to scale.

<img src=https://github.com/ISCB-Academy/Elements-of-Style-Reproducible-Workflow-Creation-Maintenance-Tutorial/blob/main/assets/MakingGitHubActionsWithStar-Docker.gif width=650 align="left">
