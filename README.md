<p>
</p>
<br/><br/>


# Elements-of-Style-Reproducible-Workflow-Creation-Maintenance-Tutorial
<br/><br/>
<img src="https://github.com/ISCB-Academy/Elements-of-Style-Reproducible-Workflow-Creation-Maintenance-Tutorial/blob/main/assets/ISCBAcademyLogo.png"  width="100" align="right" >
<br/><br/>
## Agenda for the day:
| Time (UTC)    | Programme       |
| ------------- | --------------------------------------------------------------------------- |
| 11.00 - 11.10 | *Welcome Address and Presentation of Tutorial Agenda* |
| 11.10 - 11.20 | 1. [A few simple rules for easier workflow maintenance and reuse]()<img src="https://github.com/ISCB-Academy/Elements-of-Style-Reproducible-Workflow-Creation-Maintenance-Tutorial/blob/main/assets/The_Elements_of_Programming_Style.jpg" width="50" align="right">|
| 11.20 - 11.30 | 2. [An overview of a short RNA-seq workflow]()|
| 11.30 - 11.40 | 3. [Begin with environment setup - Conda]() <img src="https://upload.wikimedia.org/wikipedia/commons/e/ea/Conda_logo.svg" width="50" align="right">|
| 11:40 - 12.00 | 4. [Dockerfile for each process - Docker]() <img src="https://www.docker.com/sites/default/files/d8/2019-07/Moby-logo.png" width="50" align="right">|
| 12:00 - 12:20 | 5. [GitHub Actions to build, test and deposit container images]() <img src="https://github.com/ISCB-Academy/Elements-of-Style-Reproducible-Workflow-Creation-Maintenance-Tutorial/blob/main/assets/Octocat.png" width="50" align="right"> |
| 12.20 - 12.30 | 6. [Zenodo for DOIs and Genomic Summary and other Data]() <img src="https://github.com/ISCB-Academy/Elements-of-Style-Reproducible-Workflow-Creation-Maintenance-Tutorial/blob/main/assets/Zenodo_logo.jpg" width="50" align="right">|
| 12.30 - 12.45 | :coffee:      *Short break - Stretch your legs! (15 minutes)*            :coffee:|
| 12.45 - 13.00 | 7. [Stitching processes with a standard workflow - Nextflow]() <img src="https://github.com/nextflow-io/trademark/blob/master/nextflow2014_no-bg.png" width="50" align="right"> |
| 13.00 - 13.20 | 8. [Stitching processes with another standard workflow - Common Workflow Language]() <img src="https://github.com/common-workflow-language/logo/blob/main/CWL-Logo-HD.png" width="50" align="right">|
| 13.50 - 14.00 | *Closing remarks and future directions*|
<br/><br/>


## Background Information and other Topics of Interest
|   |   |   | <p align="center"><img src="https://github.com/lifebit-ai/dry-bench-skills-for-researchers/blob/main/assets/lifebitCloudOS.png"  width="250" align="right" ></p> |
|---|---|---|---|
|[Command Line Skills](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/blob/main/classes/1-using-the-command-line/1-using-the-command-line.ipynb)  | [Reading and Plotting Data in R](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/blob/main/classes/1-using-the-command-line/2-reading-data-and-plotting-in-R.ipynb) |  [Why Git and GitHub](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/blob/main/classes/2-intro-to-git-github/1-why-git-and-setup.md) | [Forking in GitHub](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/blob/main/classes/2-intro-to-git-github/2-the-fork-git-routine.ipynb)|
| [Git Add Git Commit](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/blob/main/classes/2-intro-to-git-github/3-the-add-push-git-routine.ipynb)| [Nextflow](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/tree/main/classes/4-intro-to-nextflow) | [Nextflow patterns](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/blob/main/classes/5-running-a-nextflow-analysis/2-nextflow-resources.md) | [Finding Data](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/blob/main/classes/4-intro-to-nextflow/BONUS-Finding-Data.md)  |
|  [Conda for managing dependencies](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/blob/main/classes/3-intro-to-conda-docker/1-conda-for-managing-dependencies.ipynb) | [Docker Build Test Share Reuse](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/blob/main/classes/3-intro-to-conda-docker/2-build-test-share-reuse-docker.ipynb) | [Getting End-to-End Example Data](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/blob/main/classes/5-running-a-nextflow-analysis/Getting-todays-data.md) | [GitHub Hello World Fun](https://guides.github.com/activities/hello-world/)|
| [SRA and RNAseq](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/tree/main/mini-courses/2_sra_and_rnaseq) |[Variant Calling Sarek](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/tree/main/mini-courses/1_variant_calling)  | [End-to-End Example](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/tree/main/classes/5-running-a-nextflow-analysis) | [Dry Bench Skills Recap](https://github.com/lifebit-ai/dry-bench-skills-for-researchers/blob/main/classes/5-running-a-nextflow-analysis/Dry-Bench-Skills-Recap.md)|
|[Using GitHub Actions]() | [Using Zenodo](https://github.com/sheynkman-lab/Long-Read-Proteogenomics/blob/main/AWStoZenodo.md) |[Long Read Proteogenomics](https://github.com/sheynkman-lab/Long-Read-Proteogenomics#readme) |[The Impact of Sex on Algernative Splicing (rMATS, Papermill, JupyterLab notebooks)](https://github.com/TheJacksonLaboratory/sbas#readme) |

## Tutorials Given:

[2021 November 19 - ISCB Academy Sponsored - 3 hour Tutorial **Agenda**](https://github.com/ISCB-Academy/Elements-of-Style-Reproducible-Workflow-Creation-Maintenance-Tutorial/blob/main/Elements-of-Style-Reproducible-Tutorial-Agenda.md)


## About

In a short 3 hour course, the learner learned elements of style in the construction and containerization of small single-function processes that facilitate reproducible workflow creation and execution.  This hands-on-tutorial was given through a webinar with the ISCB Academy.  This repository was used in the course and contains self-learnings to facilitate work.  In this repository, contains how these processes may be kept up-to-date and alert the creator to the functional state of these processes (working or failing) by using a feature found within GitHub called GitHub Actions.  This hands-on-course will use a small example to provide the structure, philosophy and approach to achieving this desirable outcome.  This course seeks to help to demystify and make accessible powerful methods one can use to achieve platform independence and platform interoperability.  Using a simple RNASeq pre-baked analysis example to demonstrate these techniques, we will break down and walk the learner through each of the construction steps.  The learners will be introduced to Conda, Docker, GitHub and the standard workflow language, Nextflow.  If time permits, we will also show how these containerized processes can also be represented in a second standard workflow language implementation (e.g. Common Workflow Language or WDL). By the end of the course, the learner will understand these Elements of Style and will know how Conda, Docker, GitHub, Zenodo, and Nextflow enable reproducible research.  Moreover, these steps will be on GitHub for the Learner to return to and reproduce themselves after the end of the course.  In taking this course, the Learner will also be shown the power of JupyterLab notebooks to facilitate literate programming.  Through their participation in the class, learners will learn and understand FAIR (findability, accessibility, interoperability and reusability) best practices. We ask all participants to get a GitHub, Zenodo and ORCID accounts prior to the course.  We ask for minimal background knowledge of the command line, simple commands in the shell environment, we enable a bit of self-learning from the repository to facilitate the acquisition of this knowledge.
