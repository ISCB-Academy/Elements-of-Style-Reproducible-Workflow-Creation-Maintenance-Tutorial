## Common Workflow Language and Nextflow Shared Elements

What are we in the end doing here?

We are trying to make our science as platform independent, workflow independent as possible while enabling open science.

I have made the case (I hope) that by practing a few "Elements of Style" the researcher can come a long way to help achieve the lofty goals of reproducibility.

Though seemingly ideal, they are within reach.

By using containers at the level of logical single purpose.  We can use the same containers across workflow languages.

This achieves a fan in engineering organizational structure that facilitates not only reproducible science, but also cleaner more testable components that lend themselves to assembly into other workflows and functions.

It readies the work for the next best component that can be stitched together in whatever workflow language supported by the platform that may be holding the data repository needed to be used to accomplish the specific scientific goal the researcher has in mind.

## Common Workflow Language

The Common Workflow language has the same structure as nextflow:

1. Inputs

2. Outputs

3. Scripts


## [Containers](https://www.commonwl.org/user_guide/07-containers/index.html)

