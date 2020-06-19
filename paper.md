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

Gene expression data have been archived in public repositories, the NCBI Gene Expression Omnibus (GEO; https://www.ncbi.nlm.nih.gov/geo/) and the EBI ArrayExpress (AE; https://www.ebi.ac.uk/arrayexpress/). Unlike the International Nucleotide Sequence Database (https://www.insdc.org/), these two databases have not been exchanging data with each other. Furthermore, the DNA DataBank of Japan (DDBJ) in the National Institute of Genetics started a similar repository called the Genomic Expression Archive (GEA; https://www.ddbj.nig.ac.jp/gea/) in 2018. Hence there is a need for integration of these public gene expression databases. Thus, we have maintained an index of these public gene expression databases, called All Of gene Expression (AOE; https://aoe.dbcls.jp/en) to integrate gene expression data and make them all searchable together.

During the DBCLS/NDBC 2019 BioHackathon, we worked on the refinement of Reference Expression Dataset (RefEx; https://refex.dbcls.jp/?lang=en) for gene expression analysis in order to make gene expression data reusable. The gene expression data to integrate in the hackathon were mainly project-based, and those included those of FANTOM5[@Kawaji:2017], GTEx v8, fly and rice.

We felt that users wanted to reuse data from FANTOM6 project which was just published with bioRxiv preprint (https://doi.org/10.1101/700864; http://fantom.gsc.riken.jp/6/). The data consists of the large-scale expression profiles after the knockdown of long non-coding RNAs (lncRNAs) using several technologies including antisense oligo (ASO) and siRNA.

The original purpose of the knock-down experiments in the FANTOM6 project was identifying what genes are affected by the perturbation of a specific lncRNAs, andthen predicting the functions of the lncRNAs. However, other researchers can reuse the data for annotating their lists of genes with speific phenotypes (for example, up-/down-regulated in specific experimental conditions/tissues). They can compare their list with the gene sets affected by the knock-down of a lncRNA, and can find potential key regulators related to the phenotype.

There are several hurdles to establish an interface for the above analysis. The first issue is about the metadata of the FANTOM6 datasets. The current FANTOM6 metadata is designed only for understanding the dataset by readers of the FANTOM6 preprints and papers, and is not enogh for resuing them. For example, the sample information is not annotated based on well-known ontologies (e.g. cell ontology, cell line ontology, and tissue ontology). Another issue is related to a social aspect of the data management. Human resources for this type of studies are always lacking especially in the field of the biological data engineers and curators, it is not easy to perform the integration of large-scale gene expression data.

We tackled the problems in the reuse of the FANTOM6 data at the ELIXIR BioHackathon-Europe 2019 by pointing out what are existing issues with their possible solutions, and we decided plans and schedules for the implementation of the search interface.

# Results

During the ELIXIR BioHackathon-Europe 2019, we discussed the following points about the reuse of gene expression data.

1. Requirements in gene expression data production.
2. Reusing Cap Analysis of Gene Expression (CAGE) data for lncRNA knockdown from FANTOM6 in other research projects.

## Requirements in gene expression data production.

We clarified what is needed for the data production of gene expression data, especially in the large scale projects including FANTOM, GTEx and Human Cell Atlas. For making large-scale experssion data to be reusable in other projects, one of the important resources is a rich metadata explaining each dataset. During the data production in the large-scale projects, the production of datasets takes longer time, and the data is gradually expanding. The data production process includes sample collection, sequencing, and bioinformatics analysis, which starts in various timings and sometimes requires starting over due to experimental failures.

Metadata must be collected in the same timing along with the data production processes, and should not do after the completion of all data production. The source of metadata could only be found as handwritten texts in lab notes or unused storages. Technicians and research scientists who did experiments might be left from laboratories. However, the simultaneous metadata collection is not straightforward. If experiment protocols are changed, the format of metadata should be adjusted to new protocols. If nomenclature of terms in the metadata is not fixed, the metadata collected from experimentalists cannot be unified. Thus, the metadata collection is a long-term and laborous work.

To be able to produce high-quality metadata, we need good data engineers and data curators. The data engineers can implement systems to collect necessary information from wet researchers and technicians. The data curators can decide and adjust rules for the data and metadata format and correct them both manually and computationally if there are mistakes and errors in the data. However, especially in Japan, we are not easy to hire such skilled people. Possible reasons might be: we have not provided good career paths for such talents; and we have no courses for learning required skills for data engineers and curators. This is a social problem, and we need much efforts and long time to solve them.


## Reusing Cap Analysis of Gene Expression (CAGE) data for lncRNA knockdown from FANTOM6 in other research projects.

The FANTOM6 consortium performed knock-down experiments with lncRNA antisense oligos, followed by the expression profiling using the CAGE protocol (KD-CAGE). The CAGE protocol can identify active transcription start sites in the genome with their expression levels. The original purpose of the lncRNA KD-CAGE is for predicting the function of each lncRNA by observing the changes of expression levels after its knocking down. In the pilot phase of the FANTOM6 project, they performed ~300 KD-CAGE assays with the human dermal fibroblast cells. The result both raw and analysis data is available in the public repository and their web site (https://fantom.gsc.riken.jp/6/).

Although the original aims of the lncRNA KD-CAGE is to predict the function of lncRNAs, the expression profiles can potentially be reused for other analysis. For example, if the genes changed by the knock-down of specific lncRNAs are matched with the list of differentially expressed genes in another biological phenotype/stimulus, we can infer the relationship between the phenotype or stimulus and the lncRNA.

To achieve such type of the analysis, we discussed the actual analysis method. Through the discussion, we concluded that an enrichment analysis may be suitable for this purpose. A user input is a list of interesting genes. The list is compared with the lists of lncRNA-related genes obtained by the analysis of the FANTOM6 lncRNA KD-CAGE expression profiles, and (adjusted) P-values of enrichments are calculated with Fisher's exact test or similar method. To achieve the method, we need to do the followings as a first step. First, we retrieve the list of lncRNA-related genes from the FANTOM6 lncRNA KD-CAGE expression profiles. Next, we implement a web-based system for performing the analysis, which is useful for wet researches who do not have enough computation skills.

In addition to the above functions, the system should also support or consider the following extensions. The first one is extensibility of the FANTOM6 KD data. The FANTOM6 project is ongoing, and more data will be released later using different lncRNAs and cell types. Along with the continuous releases of the datasets, the system should be able to easily process and load the new additional datasets. The second one is expansion to public KD datasets over the FANTOM6 data. The analysis is not limited to the FANTOM6 KD-CAGE data. Thus, if we can collect more KD data from public repositories, we can make the system to be able to provide more rich results. These are future plans after the prototype system implementation.

We estimate the development of the method and the prototype system can be achieved in 2020. We will keep discussion and evaluation of the method.

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

