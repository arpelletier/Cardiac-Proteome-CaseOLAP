# Cardiac Proteome CaseOLAP:

This repository contains the code associated with the paper, "Defining relationships among functional cardiac subproteomes and heart disease". The goal of this project is to understand protein-disease relationships between cardiac proteins and subcategories of CVD from experimental protein datasets as reported in the biomedical literature. The code is separated into three notebooks: 1) curation of the cardiac proteome, 2) text mining association, and 3) analysis of text mining results.

### Publication: 
1. [Defining relationships among functional cardiac subproteomes and heart disease](in preparation)

***1. Curation of the Cardiac Proteome*** : 

The first step details the curation of the cardiac proteome used for the text mining association. Input used for this analysis can be found in './data/protein_lists', with a sub-folder for each species among human, mouse, rat, and pig. Within each sub-folder are text files containing a list of proteins found within each ProteomeXchange experiment. In total there are 37 ProtomeXchange identifiers with 34 associated publications across four species. This notebook details parsing of these files, retaining a unique list of proteins found within the UniProt reference proteome of each species. Only human genes with at least one ortholog among mouse, rat, and pig are considered for downstream analysis. Proteins from these genes were grouped based on sequence similarity using UniRef90 protein groups. The resulting cardiac proteome and proteome for each species are output in './output/protein_lists'. Synonyms for each UniRef90 protein group are extracted using ProtExam (https://github.com/pinglab-utils/protexam). in preparation for text mining association. All associated figures as a result of these analysis can be found at './figures'.

```
jupyter Cardiac_Proteome_Curation.ipynb
```
---------------------------
***2. CaseOLAP text mining analysis*** : 

CaseOLAP is a cloud computing platform for phrase-mining, for user-defined entity-category association. The original CaseOLAP can be found at (https://github.com/CaseOLAP/caseolap). In this study, CaseOLAP is used to quantify the strength of association between protein groups as defined in the previous section and eight cardiovascular diseases. This pipeline describes the major steps for PubMed abstracts as text data, the cardiac protein groups as entity list, and MeSH descriptors attached to abstracts as categories. The entities and categories used in this analysis can be accessed at './caseolap/input/entities.txt' and './caseolap/input/categories.txt', respectively. Major changes to the original pipeline consist of 1) case-sensitive entity matching within text documents and 2) a list of unreliable synonyms to exclude from text mining analysis. The list of synonyms not considered for text mining analysis can we viewed and modified at './caseolap/data/remove_these_synonyms.txt'.

```
jupyter ./caseolap/runner.ipynb
```
-------------------------------

***3. Analysis of Text Mining Results *** : 

Following text mining analysis, the CaseOLAP scores quantifying the strength of association between protein groups and eight cardiovascular disease categories are analyzed. Redundant protein groups which obtained matching scores based on overlapping synonyms are merged. Sub proteomes are identified as protein groups with strong association to a specific disease category. Protein groups are further categorized based on their obtained scores. These categories consist of description here. A detailed summary of this analysis can be found at './output/summary_table.tsv'. Pathway analysis was performed on Category I to determine biological pathways found in common between all cardiovascular disease. Pathway analysis was performed on all available Category II protein groups to determine biological pathways distinct to a CVD. Pathway analysis results can be found at './output/reactome_results'. All associated figures as a result of these analysis can be found at './figures'.


```
jupyter Analysis_Text_Mining_Results.ipynb
```
