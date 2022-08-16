# BiomedCurator

- [Overview](#overview)
- [BiomedCurator DEMO](#biomedcurator-demo)
- [BiomedCurator Data-Set](#biomedcurator-dataset)
- [BiomedCurator Description](#biomedcurator-description)
- [Evaluation](#evaluation)
- [Acknowledgement](#acknowledgement)
- [Contact](#contact)
- [Citation](#citation)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

# Overview

With the growth of data-driven science, the curation of public and community data sets has become a necessary task for ensuring the long-term usefulness of Biomedical domain. Scientific data typically comes in format with methodologies, experiment results, and the interpretation of those results and discussions in the form of statements. There are curation challenges in the form of scientific publications as to prevail most up-to-date structural data fields to create template. The task of biomedical data curation goes beyond fixing defects in data and annotate information based on related fields. Thus, curation must be done by human experts in the domain of the data, who are capable of interpreting the scientific literature, resolving conflicting interpretations, and reflecting the results in the data. In our BiomedCurator, several domain-specialist biologists are involved in the form of data curation from Pubmed and Clinical trial scientific articles as to create data template based on 61 fields of 11 categories ans sub-categories. We use this template as to train our model. 

# BiomedCurator DEMO
The BiomedCurator system provides a web interface to facilitate the process of creating, organining, and mainitaining data sets so they can be accessed and used by researchers, biologists, or physiologist looking for information. In our demo, users can input a PubMed/ClinicalTrial id, the system involves detecting, collectiong, linking, ralation mapping, indexing, and classifing of entittes over the entire given article. 

Users can access our demo via [http://underconstruction/biomedcurator/](http://underconstruction/biomedcurator/).

![Demo interface](images/BioMedCurator.png)

# BiomedCurator Data-Set

We conduct experiments on our curated data-sets based on Pubmed and ClinicalTrials to address the biomedical data curation extraction tasks. The Pubmed and ClinicalTrials data-sets  consist of 2,570 and 2,371 pubmed and clinical trials related scientific articles respectively. Biologists are assigned to annotate the entire PubMed and ClinicalTrial data-sets based on 61 fields. We use the annotated templete to train our BiomedCurator model.

# BiomedCurator Description

## Introduction

We present BiomedCurator, an interactive web application that extracts the structural data from scientific Pubmed and ClinicalTrial data sets. BiomedCurator uses state-of-the-art natural language processing techniques to extract the information of PubMed and Clinical trial articles and fill the 61 fields including 11 categories and subcategories created by biologists.  The BiomedCurator web application that address text generation based model for relation extraction, entity detection and recognition, text classification model for extracting several fields using BigBird, information retrieval from external knowledge base to retrieve IDs,  and a pattern-based extraction approach that can extract several fields using regular expressions over the Pubmed and Clinical trial data-sets. 

## Usage of BiomedCurator
Annotation tasks like entity mention detection, relation extraction; extraction task like pattern- and knowledge-based extraction, and text clasifcation, can be performed using BiomedCurator for PubMed and ClinicalTrial articles that fills the 61 biomedical fields. 

## BiomedCurator System
BiomedCurator system mainly comprises two platforms: BiomedCurator web interface and BiomedCurator back-end server. The overall workflow of the BiomedCurator system is illustrated as below.

![Work Flow](images/bio_data_extractor.png)

### BiomedCurator Web Interface
In [BiomedCurator web interface](#biomedcurator-demo), the user interface contains input panel, Enter a PubMed or ClinicalTrailas article ID here tab, Or select a sample ID below tab. For a given PubMed/ClinicalTrail ID from users or loading a sample text from a sample list, the output panel show the information of 61 fields based on pretrained BiomedCurator model. 

![BiomedCurator Description1](images/biomed_1.png)

In the result box,the users will able to download article from Download Article tab, or can extract information from the Download extracted information tab in plain text and JSON formats. The system will also provide the reference article URL for user reference. The BiomedCurator also shows the processing time from user input to result box through the backend models.

![BiomedCurator Description2](images/biomed_2.png)

The results are organized into sections. The user can click on the "+/-" button (the redbox) to expand/minimize its content.
For example, the Intervention Characteristics section shows relations between Drug and Dose extracted from the article.

![BiomedCurator Description3](images/biomed_3.png)

### BiomedCurator Back-end
The BiomedCurator back-end is for storing tools (e.g., NER, relatuion extraction based on generation model, classification model, pattern- and knowledge-based information extraction models) that transform into a pipeline. 

#### Neural Named Entity Recognition
Named entity recognition (NER) is a task of finding entities with specific semantic types such as Protein, Cell, and RNA in text. We build neural NER model, based on the [BERT](https://www.aclweb.org/anthology/N19-1423.pdf) model. The layer receives subword sequences and assigns contextual representations to the subwords via BERT. 

#### Generative Relation Extraction
In the geenrative-based relation extraction, currently we are formalizing binary relation extraction task as a template generation problem. For a given paragraph, we expect to train a model that can generate a sequence in our predefined structure so called templates. For the sequence-to-sequence model, we utilize the [Big Bird](https://arxiv.org/abs/2007.14062) model that can process up to 8x longer sequence than BERT. Therefore, for the sequence-to-sequence model, we utilize the Big Bird model to extract the relations from a given paragraph which is an input to the Big Bird model.

## Summary
We presented the **BiomedCurator** system for entity detection, relation extraction, information extraction based on pattern and knowledge base, hoping that we can bring insights for the biomedical studies on making scientific discoveries. The **BiomedCurator** system is continually evolving; we will continue to improve the system as well as to implement new functions such as n-ary relation extraction to further facilitate **BiomedCurator** research.

# Evaluation

## TODO

We evaluate our BiomedCurator system from several aspects: TODO 

# Acknowledgement
This work is based on results obtained from a project commissioned by the Public/Private R&D Investment Strategic Expansion PrograM ([PRISM](https://www.nibiohn.go.jp/prism/about/))

# Contact
* [Mohammad Golam Sohrab](https://orcid.org/0000-0001-5540-7834): sohrab.mohammad@aist.go.jp
* Khoa N. A. Duong
* Goran Topić
* Nogami-Itoh
* Masataka Kuroda
* Yayoi Natsume-Kitatani
* Masami Ikeda
* Hiroya Takamura

# Citation
If you find this work helpful, please use the following citation:

```
@inproceedings{biomed_curator_2022,
    title = "BioMedCurator: an Interactive Web Application for Template Generation from Biomedical Literature",
    author = "To be appeared",
    booktitle = "To be appeared",
    month = To be appeared,
    year = "To be appeared",
    address = "Online",
    publisher = "To be appeared",
    url = "To be appeared",
    pages = "To be appeared",
} 
```

Thanks!!!
