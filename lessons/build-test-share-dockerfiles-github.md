# Combining dependency management with conda and Docker

We can combine an environment.yml file with a Dockerfile, build and test on our laptops or within `shell.cloud.google`.  Create a repository separately for each or combine into a file that can be used for the entire workflow in the repository.

@@ Overview

The [`nf-core`](https://github.com/nf-core) community has established a highly practical convention for creating  docker containers by re-using an **environment.yml** file that can be also used for installing dependencies in an interactive session.

There are 2 main ingredients to this Dockerfile formula:

1. The **environment.yml** file

2. The template **Dockerfile**.

## environment.yml and [`nf-core/scrnaseq`](https://github.com/nf-core/scrnaseq).

This file has no difference when used within a Dockerfile installation or when used natively for installing dependencies via conda.

This file can be used to create a concise Dockerfile, as has been done with the [`nf-core/scrnaseq`](https://github.com/nf-core/scrnaseq).

Here is the environment.yml

```bash
# You can use this file to create a conda environment for this pipeline:
#   conda env create -f environment.yml
name: nf-core-scrnaseq-1.1.0
channels:
  - conda-forge
  - bioconda
  - defaults
dependencies:
  - conda-forge::python=3.7.3
  - conda-forge::markdown=3.1.1
  - conda-forge::pymdown-extensions=6.0
  - conda-forge::pygments=2.5.2
  - bioconda::multiqc=1.8
  - bioconda::salmon=1.4.0
  - bioconda::r-seurat=3.0.2
  - bioconda::bioconductor-isee=1.6.0
  - bioconda::bioconductor-tximeta=1.4.0
  - bioconda::bioawk=1.0
  - bioconda::bioconductor-alevinqc=1.2.0
  - bioconda::bioconductor-tximport=1.14.0
  - bioconda::star=2.7.2c #2.7.3a is broken!
  - samtools=1.10
  - gffread=0.11.7
  - bioconda::kallisto=0.46.2
  - bioconda::bustools=0.40.0
  - font-ttf-source-code-pro=2.030 #Required for fonts in alevinQC
```

## Dockerfile

Now with this file, the docker container may be built that supports the entire workflow:

The Dockerfile is the most integral file in the process, it constitutes the main installation blueprint in which the auxillary files **`environment.yml`** will be included.

Here is the `Dockerfile` for the [`nf-core`](https://github.com/nf-core)

```bash
FROM nfcore/base:1.13.3
LABEL authors="Peter J Bailey, Alexander Peltzer, Olga Botvinnik" \
      description="Docker image containing all software requirements for the nf-core/scrnaseq pipeline"

# Install the conda environment
COPY environment.yml /
RUN conda env create --quiet -f /environment.yml && conda clean -a

# The conda bug with tbb - salmon: error while loading shared libraries: libtbb.so.2
# pandoc via conda was not working
RUN apt-get update && apt-get install -y libtbb2 pandoc-citeproc

# Add conda installation dir to PATH (instead of doing 'conda activate')
ENV PATH /opt/conda/envs/nf-core-scrnaseq-1.1.0/bin:$PATH

# Dump the details of the installed packages to a file for posterity
RUN conda env export --name nf-core-scrnaseq-1.1.0 > nf-core-scrnaseq-1.1.0.yml
```

Note the name in the file `nf-core-scrnaseq-1.1.0` is the same as the name in the `environment.yml` file `name: nf-core-scrnaseq-1.1.0`.

## Combining to build the docker image**🐳 Where your files go 

To build the docker container and create the docker image we will need the auxillary files to be in the same directory or a subdirectory of the root repo of the Dockerfile."It is typical that all files reside in the same directory. An also common practice is to create a helper folder named `bin` to hold all of the scripts and executables. To proceed withh the installation commands, make sure that your files in your directory look similar to this if you want to use the template without updating any paths:

```bash
├── Dockerfile
├── environment.yml
``


## Building smaller containers 

Rather than us building the entire single cell RNA-seq workflow that is already beautifully built and maintained.  We are going to break apart the dockerfile and we will show you two different ways of building.  We will set up automatic testing with GitHub actions and then test our container's functionality from the command line.

This gets at the philosophy we are teaching today, of single purpose containers for modular workflow programming and maintenance.

## STAR - a minimal Dockerfile

Let's have a look at the minimal Dockerfile for STAR that was built without a environment.yml

```bash
# Dockerfile for STAR
# https://github.com/alexdobin/STAR
FROM continuumio/miniconda3:4.8.2

RUN conda install -c bioconda star=2.7.2c
```

This is built and is running with GitHub actions to build and push the images to the GitHub container registry.

To test this docker image, you need to authenticate.

## Authenticating on the GitHub container registry

To authenticate, you need to use your GitHub personal token.   In this case, you are going to put it into an environment variable and pipe it to the docker login.

```bash
export CR_PAT=**`your personal GitHub token`**
echo $CR_PAT | docker login ghcr.io -u adeslatt --password-stdin
```

Once authenticated - you can test your container.

```bash
docker run --rm -v $PWD:$PWD -it ghcr.io/adeslatt/star-docker:main STAR -h
```

I didn't quite tell you how I pushed it to the container registry - but I will - in the coming lesson

## Multiqc

The multiqc is a little more complicated because there are some more environment problems we need to worry about.

Dockerfile here looks more like the full one from the nf-core/scrnaseq workflow

```bash
# Dockerfile for multiqc
# https://multiqc.info/
FROM continuumio/miniconda3

# Install the conda environment
COPY environment.yml /
RUN conda env create --quiet -f /environment.yml && conda clean -a

# The conda bug with tbb - salmon: error while loading shared libraries: libtbb.so.2
# pandoc via conda was not working
RUN apt-get update && apt-get install -y libtbb2 pandoc-citeproc

# Add conda installation dir to PATH (instead of doing 'conda activate')
ENV PATH /opt/conda/envs/multiqc-1.8/bin:$PATH

# Dump the details of the installed packages to a file for posterity
RUN conda env export --name multiqc-1.8> multiqc-1.8.yml
```

And the `environment.yml` as well - leaner but with a few extra items.

```bash
# You can use this file to create a conda environment for this pipeline:
#   conda env create -f environment.yml
name: multiqc-1.8
channels:
  - conda-forge
  - bioconda
  - defaults
dependencies:
  - conda-forge::python=3.7.3
  - conda-forge::markdown=3.1.1
  - conda-forge::pymdown-extensions=6.0
  - conda-forge::pygments=2.5.2
  - bioconda::multiqc=1.8
  - font-ttf-source-code-pro=2.030 #Required for fonts in alevinQC
```

Finally we have the third broken out component, a part of Salmon release

## Alevin

The Dockerfile here like the multiqc 

```
# Dockerfile for (salmon's) alevin 
# https://salmon.readthedocs.io/en/latest/alevin.html/
FROM continuumio/miniconda3

# Install the conda environment
COPY environment.yml /
RUN conda env create --quiet -f /environment.yml && conda clean -a

# The conda bug with tbb - salmon: error while loading shared libraries: libtbb.so.2
# pandoc via conda was not working
RUN apt-get update && apt-get install -y libtbb2 pandoc-citeproc

# Add conda installation dir to PATH (instead of doing 'conda activate')
ENV PATH /opt/conda/envs/multiqc-1.8/bin:$PATH

# Dump the details of the installed packages to a file for posterity
RUN conda env export --name salmon-1.4.0> salmon-1.4.0.yml
```

and the accompanying environment.yml file is here:

```bash
# You can use this file to create a conda environment for this pipeline:
#   conda env create -f environment.yml
name: salmon-1.4.0
channels:
  - conda-forge
  - bioconda
  - defaults
dependencies:
  - conda-forge::python=3.7.3
  - conda-forge::markdown=3.1.1
  - conda-forge::pymdown-extensions=6.0
  - conda-forge::pygments=2.5.2
  - bioconda::salmon=1.4.0
  - font-ttf-source-code-pro=2.030 #Required for fonts in alevinQC
```

Now we have built these from subdirectories I named to be the names of the repositories where they will be deposited.

## making your own Dockerfiles

So you each could do the same with these as well.

In a terminal window, make a directory for Alevin and change into that directory.

```bash
mkdir alevin-docker
cd alevin-docker
``

Make a README.md, a markdown file that will display at the root of your GitHub repository.

The README.md I have with my Dockerfile is:

```bash
# Salmon's Alevin Docker

A minimal container holding Salmon
```

## Build and tag

Before we deposit into GitHub, lets build and test our Dockerfile (assumes docker daemon is running in your terminal).

```bash
docker build -t alevin .
```

## Now upon success we make a repository

Since we are at the command line, lets just go ahead and make our repository from here:

The following commands 
1. create an initial branch `-b main`
2. adds all the files (Dockerfile, environment.yml and README.md) to the (local version) of your repository.

```bash
git init -b main
git add . && git commit -m "initial commit"
```

Next we use the GitHub command line tool to create this new repository, after we tell git how to set the upstream rounting.


```bash
git push --set-upstream origin main
gh repo create
```

Finally, we need to add a tag, so we can have a release.  When we get to GitHub actions you will see why.
To tag, let's find out the unique identifier for this push to GitHub

```bash
git log --pretty=oneline
```

Now let's add a tag with the first 6 characters of the latest GitHub push hash
```bash
git tag -a v1.4.0 86a45f
```

Now we need to push this tag to the repository
```bash
git push origin v1.4.0
```

## Testing or running the docker image

You can test my images, but not yours yet, we have to get to the GitHub actions lessons and then we can.

To use the created docker image, a simple yet very practical way is to mount as a volume the current working directory. This will ensure access to the files available in the folder but also allow the generated results of the analysis to be retained after exiting the docker container. 

To run the docker container with the current working directory mounted, type the following command: 

```bash
docker run --rm -v $PWD:$PWD -w $PWD -it ghcr.io/adeslatt/multiqc-docker:main multiqc --help
```
