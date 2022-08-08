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

We conduct experiments on our curated data-sets based on Pubmed and ClinicalTrials to address the biomedical data curation extraction tasks. The Pubmed and ClinicalTrials data-sets  consist of 2,570 and 2,371 pubmed and clinical trials related scientific articles respectively. Biologists are assigned to annotate the entire PubMed and ClinicalTrial data-sets based on 61 fields. We use the annotated templete to train our BioMedCurator model.

## Sample Data Format of BioMedCurator 
Examples of annotation for an entity (**T**), a relation (**R**) are shown in the following. Text-bound annotation identifies a specific span of text and assigns it a type. In text-bound annotation (**T1**) of a span “**Angiotensin-converting enzyme 2**”,  **0** denotes start-offset and **31** denotes end-offset of the annotation span, where type is **GENE_OR_GENOME**. The normalization annotation (**N1**) is attached to the text-bound annotation (**T1**) which is associated with the unified medical language system ([UMLS](https://www.nlm.nih.gov/research/umls/licensedcontent/umlsknowledgesources.html)) entry with the [UMLS](https://www.nlm.nih.gov/research/umls/licensedcontent/umlsknowledgesources.html) concept unique identifier (CUI) as **C0960880**. Entites are detected based on the reference annotated templete created by biologists.  
```
    T1	drug/therapy	Cilengitide
    T2	dose	600 mg/m2   
    R1  T1  T2
    T3	drug/therapy	Docetaxel
    T4	dose	75 mg/m2  
    R2  T3  T4
    T5	drug/therapy	Docetaxel
    T6	dose	75 mg/m2 
    R3  T5  T6
    T7	drug/therapy	Cilengitide
    T8	dose	240 mg/m2 
    R4  T7  T8
    T9	drug/therapy	Cilengitide
    T10	dose	400 mg/m2 
    R5  T11  T10
    T11	drug/therapy	Cilengitide
    T12	dose	600 mg/m2
    R6  T11  T12
    T13	drug/therapy	Docetaxel
    T14	dose	75 mg/m2 
    R7  T13  T14
    T15	drug/therapy	Cilengitide
    T16	dose	240 mg/m2 
    R8  T15  T16
    T17	drug/therapy	Cilengitide
    T18	dose	400 mg/m2 
    R9  T17  T18
    T19	drug/therapy	Cilengitide
    T20	dose	600 mg/m2
    R10  T19  T20
    T21	drug/therapy	Docetaxel
    T22	dose	75 mg/m2 
    R11  T21  T22
    T23	drug/therapy	Cilengitide|Docetaxel
    T24	dose	240 or 400 or 600 mg/m2 (Cilengitide)|75 mg/m2 (Docetaxel) 
    R12  T23  T24
    T25	drug/therapy	Cilengitide|Docetaxel
    T26	dose	240 or 400 or 600 mg/m2 (Cilengitide)|75 mg/m2 (Docetaxel) 
    R13  T25  T26
    T27	drug/therapy	Cilengitide|Docetaxel
    T28	dose	240 or 400 or 600 mg/m2 (Cilengitide)|75 mg/m2 (Docetaxel)
    R14  T27  T28
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
