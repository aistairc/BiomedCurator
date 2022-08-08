# BioMedCurator

- [Overview](#overview)
- [BioMedCurator DEMO](#biomedcurator-demo)
- [BioMedCurator Data Set](#cord-nerd-dataset)
- [BioMedCurator Description](#bennerd-description)
- [Evaluation](#evaluation)
- [Acknowledgement](#acknowledgement)
- [Contact](#contact)
- [Citation](#citation)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

# Overview

We present BioMedCurator, an interactive web application that extracts the structural data from scientific Pubmed and ClinicalTrial data sets. BioMedCurator uses state-of-the-art natural language processing techniques to extract the information of PubMed and Clinical trial articles and fill the 61 fields including 11 categories and subcategories created by biologists.  The BioMedCurator web application that address text generation based model for relation extraction, entity detection and recognition, text classification model for extracting several fields using BigBird, information retrieval from external knowledge base to retrieve IDs,  and a pattern-based extraction approach that can extract several fields using regular expressions over the Pubmed and Clinical trial data-sets. 

# BioMedCurator DEMO
The BioMedCurator system provides a web interface to facilitate the process of text annotation and its disambiguation without any training for end users like researchers or biologists. In our demo, users can input a plain text of any biomedical document to extract entities with their corresponding types and UMLS CUI(s) in BRAT format. It also provides a feature to filter out some of the specific entities by their types via a simple checkbox list (the setting button on the top right of page).

Users can access our demo via [http://underconstruction/biomedcurator/](http://underconstruction/biomedcurator/).

![Demo interface](images/BioMedCurator.png)

# BioMedCurator Data Set

We are the first to perform entity linking (EL) task on [CORD-19](https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge) data set. [CORD-NER](https://uofi.app.box.com/s/k8pw7d5kozzpoum2jwfaqdaey1oij93x) dataset comprises only NER  task.  To solve the EL task, we expand this dataset by leveraging a CUI for each mention in the [CORD-NER](https://uofi.app.box.com/s/k8pw7d5kozzpoum2jwfaqdaey1oij93x) dataset, we call this covid-19 open research dataset for named entity recognition and disambiguation [CORD-NERD](https://drive.google.com/file/d/1uJgtqqggkVXv7uGLuG3wYWstIaa7bqRO/view?usp=sharing) dataset that includes UMLS-based training, development, and test sets. Available at, 

## Manually Annotated Training Set

In addition with the [UMLS-based test set](#umls-based-test-set), we assigned a biologist to annotate 1,000 random sentences based on chemical, disease, and gene types along with its corresponding CUI to create a [manually annotated test set](https://github.com/aistairc/BENNERD/blob/master/data/Manually_Annotated_Test_Set.zip). 

## Sample Data Format of BioMedCurator 
Examples of annotation for an entity (**T**), a normalization (**N**) are shown in the following. Text-bound annotation identifies a specific span of text and assigns it a type. In text-bound annotation (**T1**) of a span “**Angiotensin-converting enzyme 2**”,  **0** denotes start-offset and **31** denotes end-offset of the annotation span, where type is **GENE_OR_GENOME**. The normalization annotation (**N1**) is attached to the text-bound annotation (**T1**) which is associated with the unified medical language system ([UMLS](https://www.nlm.nih.gov/research/umls/licensedcontent/umlsknowledgesources.html)) entry with the [UMLS](https://www.nlm.nih.gov/research/umls/licensedcontent/umlsknowledgesources.html) concept unique identifier (CUI) as **C0960880**. 
```
    T1	GENE_OR_GENOME 0 31	Angiotensin-converting enzyme 2
    N1	Reference T1	UMLS:C0960880
    T2	GENE_OR_GENOME 33 37	ACE2
    N2	Reference T2	UMLS:C1422064
    T3	CORONAVIRUS 44 54	SARS-CoV-2
    N3	Reference T3	UMLS:C5203676
    T4	CHEMICAL 55 63	receptor
    N4	Reference T4	UMLS:C0597357
    T5	CORONAVIRUS 120 130	SARS-CoV-2
    N5	Reference T3	UMLS:C5203676
    T6	EVOLUTION 158 170	phylogenetic
    N6	Reference T6	UMLS:cui_less
    T7	WILDLIFE 195 198	bat
    N7	Reference T7	UMLS:C1412726
    T8	CORONAVIRUS 214 224	SARS-CoV-2
    N8	Reference T3	UMLS:C5203676
    T9	NORP 259 277	intermediate hosts
    N9	Reference T9	UMLS:cui_less
    T10	CORONAVIRUS 282 292	SARS-CoV-2
    N10	Reference T3	UMLS:C5203676
```

# BioMedCurator Description


## Introduction

In this work, we present a BERT-based Exhaustive Neural Named Entity Recognition and Disambiguation (BENNERD) system by addressing [CORD-NER](https://uofi.app.box.com/s/k8pw7d5kozzpoum2jwfaqdaey1oij93x) data set. The entity disambiguation (ED) or entity normalization (EN) is a.k.a entity linking (EL) task. The objective of this work is to facilitate recent pandemic of corona virus disease 2019 (COVID-19) research that mainly covers **biomedical domain**, especially new entity types (e.g., coronavirus, viral proteins, and immune responses) by addressing [CORD-NER](https://uofi.app.box.com/s/k8pw7d5kozzpoum2jwfaqdaey1oij93x) dataset. In contrast to biomedical domain, it also gives a shed on **general domain** entity types (e.g., person, organization, location, date, group etc.). Moreover, along with **flat** or non-overlapping, the BENNERD system also solves **nested** or overlapping entities. The BENNERD system is composed of four models: **NER** that enumerates [exhaustively](https://www.aclweb.org/anthology/D18-1309.pdf) all possible spans as potential entity mentions and classifies them into entity types, masked language model as **BERT**, **candidate generation model** to find a list of candidate entities, and **candidate ranking model** to disambiguate the entity for concept indexing. 

## Usage of BioMedCurator
Annotation tasks like entity mention detection and entity normalization based on [CORD-NER](https://uofi.app.box.com/s/k8pw7d5kozzpoum2jwfaqdaey1oij93x) can be performed in BioMedCurator for COVID-19 research. The [CORD-NER](https://uofi.app.box.com/s/k8pw7d5kozzpoum2jwfaqdaey1oij93x) contains 63 biomedical and general entity types therefore BioMedCurator can be applied on other biomedical corpora like GENIA, BC5CDR etc. In contrast to biomedical domain, BioMedCurator can be applied on general domain for mention detection and normalization in some extent as the unified medical language system ([UMLS](https://www.nlm.nih.gov/research/umls/licensedcontent/umlsknowledgesources.html)) is used as only knowledge base. BioMedCurator can be used to visualize annotation output for manual analysis and evaluation performances. 

## BioMedCurator System
BioMedCurator system mainly comprises two platforms: BioMedCurator web interface and BioMedCurator back-end server. The overall workflow of the BioMedCurator system is illustrated as below.

![Work Flow](images/BENNERD_WORK_FLOW-1.png)

### BioMedCurator Web Interface
In [BioMedCurator web interface](#bennerd-demo), the user interface contains input panel, load a sample tab, annotation tab, gear box tab, and .TXT and .ANN tabs. For a given text from users or loading a sample text from a sample list, the annotation tab will show the annotations with the text based on best NER- and EL-based training model. Different colors represent different entity types and, when the cursor floats over a coloured box representing an entity above text, the corresponding concept unique identifier (CUI) on the UMLS is shown. Users can save the machine readable text and annotation files as .txt and .ann where the .ann annotation file provides standoff annotation output in [brat](https://brat.nlplab.org) format.

### BioMedCurator Back-end
The BENNERD back-end is for storing tools (e.g., NER, EL) that transform into a pipeline. It is composed of BERT-based exhaustive neural named entity recognition (NER) model and the prediction of NER model then fed to entity linking (EL) model that disambiguate the predicted entities by addressing candidate generation model (to find a list of candidate entities) and candidate ranking model.

#### Neural Named Entity Recognition
Named entity recognition (NER) is a task of finding entities with specific semantic types such as Protein, Cell, and RNA in text. We build neural NER model, based on the [BERT](https://www.aclweb.org/anthology/N19-1423.pdf) model. The layer receives subword sequences and assigns contextual representations to the subwords via BERT. We generate mention candidates based on the same idea as the [span-based model](https://www.aclweb.org/anthology/D18-1309.pdf).

#### Entity Linking
The [CORD-NER](https://uofi.app.box.com/s/k8pw7d5kozzpoum2jwfaqdaey1oij93x) dataset gives a shed on entity recognition system, but it does not address entity linking (EL) task which is important to address COVID-19 research.  For example, the mention SARS-CoV-2 needs to be disambiguated. Since the term SARS-CoV-2 in this sentence refers to a virus, it should be linked to an entry of a virus in the knowledge base (KB), not to an entry of ‘SARS-CoV-2 vaccination’, which corresponds to therapeutic or preventive procedure to prevent a disease. To address EL, we implement **candidate generation model** to find a list of candidate entities in the [UMLS](https://www.nlm.nih.gov/research/umls/licensedcontent/umlsknowledgesources.html) KB for linking and **candidate ranking model** to disambiguate the entity for concept indexing.

## Summary
We presented the **BioMedCurator** system for entity linking, hoping that we can bring insights for the biomedical studies on making scientific discoveries. The **BioMedCurator** system is continually evolving; we will continue to improve the system as well as to implement new functions such as n-ary relation extraction to further facilitate **BioMedCurator** research.

# Evaluation

## TODO

We evaluate our BioMedCurator system from several aspects: comparison with existing state-of-the-art models, different pre-trained bert models, categorical performance, and evaluation on manually annotated test sets.

# Acknowledgement
This work is based on results obtained from a project commissioned by the Public/Private R&D Investment Strategic Expansion PrograM (PRISM)

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
    author = "Sohrab, Mohammad Golam and Duong, Khoa and Topić, Goran and Masami, Ikeda and Takamura, Hiroya",
    booktitle = "To be appear",
    month = To be appear,
    year = "To be appear",
    address = "Online",
    publisher = "To be appear",
    url = "To be appear",
    pages = "To be appear",
} 
```

Thanks!!!
