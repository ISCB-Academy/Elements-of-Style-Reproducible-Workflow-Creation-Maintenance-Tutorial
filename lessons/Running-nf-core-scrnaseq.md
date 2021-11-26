## Running [nf-core/scrnaseq](https://github.com/nf-core/scrnaseq)

We acknowledge Lifebit and the use of their platform Lifebit's CloudOS key in development of the open source software Nextflow workflow used in this work.  
<p align="center"><img src="https://github.com/lifebit-ai/dry-bench-skills-for-researchers/blob/main/assets/lifebitCloudOS.png"  width="250" align="right" ></p>

## Beginning inside Jupyterlab

First you select a terminal window upon starting.

Inside the terminal you type:

```bash
conda init bash
exec -l bash
```

As a best practice, begin with creating a conda environment.   We will discuss more about this later.  For now, think of this as a way of keeping your room clean.   Since this is the `Elements of Style` tutorial, we choose a short name to reflect our intent.

```
conda create -n eos -y
```

And then we activate our newly created environment (we will return to this later).
```
conda activate eos
```

## A small detour

Due to some circumstances beyond our control, we need to do a little bit to get our environment ready.
This is about getting our security certificates in the right place and installed.


```
curl --verbose https://live.cardeasexml.com/ultradns.php
```

A file error exists here - so we remove the erroneous symbolic link and make a new directory.

```
sudo rm /etc/ssl/certs
sudo mkdir /etc/ssl/certs
```

Now we can update our certificates
```
sudo update-ca-certificates
```

## Installing GitHub Command-line

It will be easiest for our work if we have GitHub command line installed.  Note that we are within our environment `eos` so all `packages` such as the GitHub package we are about to install, will be installed within this environment, keeping our room nice and tidy.

```
conda install gh
```

## Authenticating with GitHub Token

Within GitHub, you have the ability to generate a personal token.  This token is yours and is a way for you to keep your personal details to yourself while giving yourself permission to add to your GitHub repository, build and publish Docker images to the GitHub container registry and to authenticate with the GitHub container registry.   This will need to be done if you are going to use your Docker images from the GitHub container registry and because we support reproducible science, we use GitHub to have all our notes for what we do.

### Generating a GitHub Token

<img src=https://github.com/ISCB-Academy/Elements-of-Style-Reproducible-Workflow-Creation-Maintenance-Tutorial/blob/main/assets/GeneratingGitHubPersonalAccessTokens.gif width="550" align="left">

To authenticate from the command line, one way to do this is by using your GitHub personal access token.
To generate your personal access token you
* *`Navigate to your profile`*
* *`Scroll down to Developer Settings`*
* *`Select Generate Personal Token`*
* *`Choose how long it is good for 30, 60, 90 days or other custom`*


### Now we authenticate

```bash
gh auth login
```

## Cloning our repository for the day

Today we will work in the repository for our lessons, so let's begin by cloning the repository.

```bash
git clone https://github.com/ISCB-Academy/Elements-of-Style-Reproducible-Workflow-Creation-Maintenance-Tutorial.git
```

Navigate into that directory

```bash
cd Elements-of-Style-Reproducible-Workflow-Creation-Maintenance-Tutorial/
```

## Getting data for the day

Make a data directory and change into that directory

```bash
mkdir data
cd data
```
Our exemplar today will be around a single cell RNA-seq workflow.   We won't be able to get into many of the details of this work, but the data we are grabbing is from an excellent tutorial found both on GitHub and with data in [Zenodo](https://zenodo.org/record/3457880/) which we will use.

Lets go ahead and get our files for executing.

```bash
wget https://zenodo.org/record/3457880/files/subset_pbmc_1k_v3_S1_L001_R1_001.fastq.gz
wget https://zenodo.org/record/3457880/files/subset_pbmc_1k_v3_S1_L001_R2_001.fastq.gz
wget https://zenodo.org/record/3457880/files/subset_pbmc_1k_v3_S1_L002_R1_001.fastq.gz
wget https://zenodo.org/record/3457880/files/subset_pbmc_1k_v3_S1_L002_R2_001.fastq.gz
```

Additionally, lets get our reference files.

```bash
wget https://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_35/gencode.v35.transcripts.fa.gz
wget https://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_35/gencode.v35.annotation.gtf.gz
wget https://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_35/GRCh38.primary_assembly.genome.fa.gz
```

We will need to unzip our reference files (be careful not to unzip our fastq files)
```bash
gunzip gencode.v35.transcripts.fa.gz
gunzip gencode.v35.annotation.gtf.gz
gunzip GRCh38.primary_assembly.genome.fa.gz
```

## Installing Nextflow

We also need to install Nextflow.  Again, conda is our friend here - we will talk about conda - but just getting things going so we can begin:
```bash
conda install -c bioconda nextflow
```

## Now running our single cell RNA-seq workflow

We have all the pieces and we can now run.

Move up a directory and let's begin and execute our nextflow workflow here is the command (*`this will take about 10 minutes - so we will keep going and return to inspect the output - by default we are only running the Alevin alignment`*):

```bash
nextflow run nf-core/scrnaseq --input "data/*_R{1,2}_001.fastq.gz" --transcript_fasta "data/gencode.v35.transcripts.fa" --gtf "data/gencode.v35.annotation.gtf" --fasta "data/GRCh38.primary_assembly.genome.fa" -profile docker
```

## Citations

The basic benchmarks that were used as motivation for incorporating the three available modular workflows can be found in [this publication](https://www.biorxiv.org/content/10.1101/673285v2).

We offer all three paths for the processing of scRNAseq data so it remains up to the user to decide which pipeline workflow is chosen for a particular analysis question.

You can cite the `nf-core` publication as follows:

> **The nf-core framework for community-curated bioinformatics pipelines.**
>
> Philip Ewels, Alexander Peltzer, Sven Fillinger, Harshil Patel, Johannes Alneberg, Andreas Wilm, Maxime Ulysse Garcia, Paolo Di Tommaso & Sven Nahnsen.
>
> _Nat Biotechnol._ 2020 Feb 13. doi: [10.1038/s41587-020-0439-x](https://dx.doi.org/10.1038/s41587-020-0439-x).

