---
title: "TogoEx: the integration of gene expression data"
tags:
  - gene expression
authors:
  - name: Hidemasa Bono
    orcid: 0000-0003-4413-0651
    affiliation: 1
  - name: Takeya Kasukawa
    orcid: 0000-0001-5085-0802
    affiliation: 2
affiliations:
  - name: DBCLS, Japan
    index: 1
  - name: RIKEN, Japan
    index: 2
date: 08 January 2020
bibliography: paper.bib
---

# Abstract

Gene expression data have potential to obtain many new biomedical findings by reusing and integrating publicly available datasets since most of the datasets were usually analyzed only focusing on what their data producers have interests to (like genes of interests). However, we have the serveral issues to enable the efficient reuse of the public expression data: current available metadata for gene expression data is not sufficient enough to re-use; and human resources are lacking to tackle the integration of gene expression data. In the ELIXIR Biohackathon-Europe 2019, we discussed what is necessary to achieve a new analysis interface to utilze the FANTOM6 CAGE data after the knockdown of long ncRNAs (lncRNAs), considered possible solutions against the issues, and decided implmentation plans and scheduled to implement it.


# Introduction

Gene expression data have been archived in public repositories, the NCBI Gene Expression Omnibus (GEO; https://www.ncbi.nlm.nih.gov/geo/) and the EBI ArrayExpress (AE; https://www.ebi.ac.uk/arrayexpress/). Unlike the International Nucleotide Sequence Database (https://www.insdc.org/), these two databases have not been exchanging data with each other. Furthermore, the DNA DataBank of Japan (DDBJ) in the National Institute of Genetics started a similar repository called the Genomic Expression Archive (GEA; https://www.ddbj.nig.ac.jp/gea/) in 2018. Hence there is a need for integration of these public gene expression databases.
Thus, we have maintained an index of these public gene expression databases, called All Of gene Expression (AOE; https://aoe.dbcls.jp/en) to integrate gene expression data and make them all searchable together.

During the DBCLS/NDBC 2019 BioHackathon, we worked on the refinement of Reference Expression Dataset (RefEx; https://refex.dbcls.jp/?lang=en) for gene expression analysis in order to make gene expression data reusable. The gene expression data to integrate in the hackathon were mainly project-based, and those included those of FANTOM5[@Kawaji:2017], GTEx v8, fly and rice.

We felt that users wanted to reuse data from FANTOM6 project which was just published with bioRxiv preprint (https://doi.org/10.1101/700864; http://fantom.gsc.riken.jp/6/). The data consists of the large-scale expression profiles after the knockdown of long non-coding RNAs (lncRNAs) using several technologies including antisense oligo (ASO) and siRNA.

The original purpose to perform the knock-down experiment in the FANTOM6 project was what genes are affected by the perturbation of a specific lncRNAs to elucidate the functions of the lncRNAs. However, other researchers can reuse the data by comparing their list of genes with speific phenotypes (for example, up-/down-regulated in specific experimental conditions/tissues). They can compare the list of genes with affected ones by the knock-down of a lncRNA and find potential key regulators related to the phenotype.

There are several hurdles to provide an interface for the analysis.  The first issue is about the metadata of the FANTOM6 datasets. The current FANTOM6 metadata is designed only for understanding the dataset by readers of the FANTOM6 preprints and papers, and not for resuing them. For example, the sample information is not annotated based on well-known ontologies (e.g. cell ontology, cell line ontology, and tissue ontology). Another issue is related to a social aspect of the data management. Human resources are generally lacking to tackle the integration of gene expression data, especially in the field of the data engineers and curators. 

We tackled the problems to achieve the reuse of the FANTOM6 data in the ELIXIR BioHackathon-Europe 2019 by making it clears what are issues and their possible solutions, and we decided implementation plans and schedules to implement a system for the search interface.

# Results

During the ELIXIR BioHackathon-Europe 2019, we discussed the following points about the reuse of gene expression data.

1. Requirements in gene expression data production.
2. Reusing Cap Analysis of Gene Expression (CAGE) data for lncRNA knockdown from FANTOM6 in other research projects.

## Requirements in gene expression data production.

We clarified what is needed in the data production for gene expression data collection including FANTOM, GTEx and Human Cell Atlas. For making large-scale data to be reusable in other projects, one of the important resources is a rich metadata explaining each dataset. During the data production in the large-scale projects, pieces of whole datasets are gradually stored. This is because data production processes, for example, sample collection, sequencing, and bioinformatics analysis, takes longer time until their finishing and sometimes need to be redone due to experimental failures.

Metadata must be simultaneously collected during this data production processes, and its collection would be long-term work. If ones try to gather metadata after the finishing of the data production project, metadata collection is always tough or impossible. The source of metadata could be found as handwritten texts in lab notes. Technicians and research scientists who did experiments might be left from laboratories.

However, the simultaneous metadata collection is not straightforward. If experiment protocols are changed, the format of metadata should be adjusted to new protocols. If nomenclature of terms in the metadata is not fixed, the metadata collected from experimentalists cannot be unified.

To be able to produce high-quality metadata, we need good data engineers and data curators. The data engineers can implement systems to collect necessary information. The data curators can decide and adjust the rules for the data collection and correct them if there are mistakes and errors. However, we, especially in Japan, usually don’t have such skilled people. Possible reasons are that we have not been able to provide career paths for such talents, and we have no courses for learning required skills for data engineers and curators. This is a social problem, and we need long time to solve them.


## Reusing Cap Analysis of Gene Expression (CAGE) data for lncRNA knockdown from FANTOM6 in other research projects.

**Need to write texts here**


# Conclusion

After a stimulus discussion in the ELIXIR BioHackathon-Europe 2019, we could make clear the current issues in the transcriptome data production, and we also could successfully make a plan to reuse the CAGE data for lncRNA knockdown in FANTOM6 project.
While the Reference Expression dataset in DBCLS (RefEx) currently includes transcriptome data for normal tissues and cell lines, we discussed how to reuse transcriptome data for knockdown.
This is only a starting point to reuse public knockdown data, but these 'reuse-ready' data can be useful for molecular biology in the near future.

# Future work

We will continue current effort to integrate gene expression data to increase the usability of these data in life science.

By gathering and then curating gene expresion datasets, those data not in NCBI GEO, EBI AE and DDBJ GEA can be included in AOE. We will also work for it.

# Jupyter notebooks created

We tried to code with Jupyter Notebook in bash kernel, but it seems that CWL is suitable for our purpose. We are willing to use BioHackrXiv to publish our activity in the ELIXIR BioHackathon-Europe 2019.

# Acknowledgement

This work was funded by ELIXIR, the research infrastructure for life-science data, as part of the ELIXIR BioHackathon-Europe 2019.

# References

- Functional Annotation of Human Long Non-Coding RNAs via Molecular Phenotyping. doi: https://doi.org/10.1101/700864
- All of gene expression (AOE): an integrated index for public gene expression databases. doi: https://doi.org/10.1101/626754
- RefEx, a reference gene expression dataset as a web tool for the functional analysis of genes. doi: https://doi.org/10.1038/sdata.2017.105
- The FANTOM5 project (collection). https://www.nature.com/collections/fantom5

