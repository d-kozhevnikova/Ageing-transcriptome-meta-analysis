# Project report

All code for tasks described in this report is avaliable in the [Jupiter Notebook]().

## Introduction

In this project, we reproduce the results of a meta-analysis of gene expression in mice reported by Palmer, Daniel et al. in 2021  [palmer2021ageing](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7906136/#SD2). In this study transcriptome signatures of ageing in brain, heart and muscle were derived from 127 public microarray and RNA-Seq datasets from mice, rats, and humans. Gene expression patterns revealed overexpression of immune and stress response genes with age, as well as underexpression of metabolic and developmental genes. In muscle and heart cell response processes were found to be activated. It was indicated that gene ageing signatures are associated with key genes in protein interaction networks. Previously in thr paper [de2009meta](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2732303/) several common signatures of aging were highlighted including overexpression of inflammation, immune response and lysosomes related genes, underexpression of collagen, energy metabolism and MT genes, as well as alterations in expression of apoptosis genes. The reasoning that genes that display differential expression with age are mainly common for different tissues was confirmed.  

The outline of the original study is the following: 
1. Linear regression was performed for each gene inside each dataset. The slope of the regression corresponds to the level of change in gene expression.
2. Genes statistically significantly associated with age were selected.
3. Meta regression was performed with Binomial test.
4. False discovery rate correction by permutation, the genes by critical P value sorted.
5. Differentially expressed genes (DEGs) were identified in each set of datasets.
6. DEGs were identified in all datasets combined.
7. Enrichment analysis with David and topGO R tool was performed.
8. dN/dS analysis - the authors calculated the ratio of no synonymus to synonymous substitutions in the main DEGs with age in different species. The result of their calculation showed that those genes are predominantly evolutionary conserved across species.
9. Random Forest ML models was build to identify the most important GO terms in the age-related DEGs.
10. Tissue specificity analysis was run with tau index used as a measure of tissue specificity. From the results of this analysis the authors found that the majority of age-associated DEGs are evenly expressed among tissues.

### Machine learning approach used in the paper `palmer2021ageing`

...

### Weak points of the paper

For the analysis of the significantly different expressions across the datasets, the authors used the binomial test. In cases where the dataset number is small, such meta-regression tests are not statistically significant because they don't reflect the effect size. Additionally, two different data types are explored, RNA-seq and microarray DNA, which require correction for the type of the data when they are combined. 

### Suggestions for approach improvements

Another approach for meta-regression can be used, in our project we applied meta-regression using the PyMare package for a higher specificity analysis.

## Results

### Preprocessing of the gene expression data

From the data avaliable on the [github repository](https://github.com/maglab/AgeingSignatures2020_supplementary) we selected 20 mice microarray datasets originated from brain, heart and muscle. (12 (14) samples from brain, 5 from heart and 8 (12) from muscle) Each dataset contains expression levels of around 20000 genes from several samples.

#### Quality control

To explore a similarity of the samples we applied the Principal Component Analysis (PCA) method of data clustering. The samples belonging to different ages showed to be intermingled in the samples, so no samples were removed. 

#### Statistical testing

To estimate differencially expressed genes (DEGs) we conducted **linear regression** analysis for all the datasets. The regression equation:

$$Y_{ij} = \beta_{0j} + \beta_{1j}Age{i} + \epsilon_{ij}$$

The slope of this regression identifies the coefficient of differencial expression. **F test** with 0.05 cutoff was then used to identify the significance of the coefficients and the coefficients variances were calculated. 

...???

### Meta-analysis of the datasets

...???

subsetting_stats_genes - takes in the results of dataset builder and retorns tables with all significantl expressed genes

Firstly the global metaanalysis was conducted to identify DEGs across all tissues. 

Next, the same analysis was conducted separately for each tissue. ???

To identify genes differentially expressed in tissue across all datasets we applied **meta regression** with the corresponding function from the **PyMare** package. This function takes as input the estimated regression coefficients for individual datasets and the variance of these coefficients. It produces weighted assessments of gene expression effects, taking into account the level of uncertainty. In our meta regression function, we passed the coefficient values, variances of coefficients, and tissue parameters and obtained..... ???

### GO enrichment analysis

Gene Onthology enrichment analysis was done with **gseapy** python package to identify functional categories for the obtained DEGs. In the genes overexpressed with age across multiple datasets in the brain, the enrichment terms are the following:

<img
  src="/figs/Enrich_terms_over_brain.jpg"
  alt="Enrichment terms in the brain overexpressed genes"
  title="Enrichment terms in the brain overexpressed genes"
  style="display: inline-block; margin: 0 auto; max-width: 300px">
  
In the muscle overexpressed genes with age, the picture is the following:

<img
  src="/figs/Enrich_terms_over_muscle.jpg"
  alt="Enrichment terms in the muscle overexpressed genes"
  title="Enrichment terms in the muscle overexpressed genes"
  style="display: inline-block; margin: 0 auto; max-width: 300px">
  
For heart overexpressed genes:

<img
  src="/figs/Enrich_terms_over_heart.jpg"
  alt="Enrichment terms in the heart overexpressed genes"
  title="Enrichment terms in the heart overexpressed genes"
  style="display: inline-block; margin: 0 auto; max-width: 300px">
  
For heart underexpressed:

<img
  src="/figs/Enrich_terms_under_heart.jpg"
  alt="Enrichment terms in the heart underexpressed genes"
  title="Enrichment terms in the heart underexpressed genes"
  style="display: inline-block; margin: 0 auto; max-width: 300px">
  
Enriched terms in the genes differentially overexpressed with age across multiple datasets in all three tissues are:

<img
  src="/figs/Enrich_terms_over_allthetissues.jpg"
  alt="Enrichment terms overexpressed genes in all tissues "
  title="Enrichment terms overexpressed genes in all tissues"
  style="display: inline-block; margin: 0 auto; max-width: 300px">
  
While for underexpressed:

<img
  src="/figs/Enrich_terms_under_allthetissues.jpg"
  alt="Enrichment terms underexpressed genes in all tissues "
  title="Enrichment terms underexpressed genes in all tissues"
  style="display: inline-block; margin: 0 auto; max-width: 300px">
  
  

### Search in GenAge database

## Gene expression comparison in Brain, Heart and Muscle

### Upregulated and Downregulated genes common between Brain, Heart and Muscle:
We carried out intersection analysis of Upregulated and Downregulated genes that are common between all three tissues. Five genes (**ACER2, RHPN2, CD2AP, RRAGC, SKAP2**) were overexpressed whereas four genes (**CRB3, HOXD12, UBN1, SLC6A3**) were underexpressed in Brain, Heart and Muscle.

### Upregulated genes: 
Description of common upregulated genes in Brain, Heart and Muscle tissues
  **1. ACER2**: may lead to changes in the metabolism of ceramide and other lipid molecules
  
  **2. RHPN2**: may affect cell adhesion, migration, and signaling, which could impact various physiological and pathological processes
  
  **3. CD2AP**: may disrupt the structure and function of the glomerular filtration barrier in the kidney, leading to proteinuria, inflammation, and progressive kidney damage.
  
  **4. RRAGC**: may affect the activity of the mTORC1 signaling pathway, which plays a key role in regulating cell growth, autophagy, and metabolism
  
  **5. SKAP2**: Differential expression of SKAP2 may influence T-cell activation and migration, which are essential for immune surveillance and defense against infections and cancer

<img
  src="/figs/uregulated genes intersection.png"
  alt="Upregulated genes intersection in all tissues "
  title="Upregulated genes intersection genes in all tissues"
  style="display: inline-block; margin: 0 auto; max-width: 300px">


### Downregulated genes:
Description of common upregulated genes in Brain, Heart and Muscle tissues
  
  **1. CRB3**: encodes a protein that is important for maintaining the structure and function of epithelial cells
  
  **2. HOXD12**: member of the homeobox gene family that is involved in regulating embryonic development and differentiation
  
  **3. UBN1**: involved in chromatin remodeling, which is important for regulating gene expression. 
  
  **4. SLC6A3**: encodes a dopamine transporter protein that is involved in the regulation of dopamine signaling in the brain

<img
  src="/figs/downregulated gebes ibtersection.png"
  alt="Downregulated genes intersection in all tissues "
  title="Downregulated genes intersection genes in all tissues"
  style="display: inline-block; margin: 0 auto; max-width: 300px">

## GenAge intersection analysis

From GenAge repository we downloaded about mouse genes and removed duplicates. The set of genes were intersected with Upregulated and Downregulated genes ideitnfied in our study. 

### Upregulated genes intersection with GenAge:
In the upregulated set of genes seven genes were reported in GenAge. 

  **1. EFEMP1**: encodes a protein that is involved in cell adhesion and signaling
  
  **2. TRP53BP1**: This gene is involved in the DNA damage response and plays a role in maintaining genomic stability
  
  **3. PAWR**: involved in the regulation of apoptosis (programmed cell death) and has been implicated in various physiological and pathological processes, including cancer and neurodegeneration 
  
  **4. CDKN1A**: This gene encodes a protein called p21, which is a key regulator of cell cycle progression and DNA damage response 
  
  **5. GRN**: encodes a protein called progranulin, which is involved in various physiological processes, including inflammation, wound healing, and neuronal development 
  
  **6. GPX4**: encodes an enzyme called glutathione peroxidase 4, which plays a critical role in protecting cells from oxidative stress 
  
  **7. HNRNPD**: This gene encodes a protein called heterogeneous nuclear ribonucleoprotein D, which is involved in RNA processing and gene expression regulation

<img
  src="/figs/Genage iontersection with upregulated genes.png"
  alt="Genage iontersection with upregulated genes in all tissues "
  title="Genage iontersection with upregulated genes in all tissues"
  style="display: inline-block; margin: 0 auto; max-width: 300px">

### Downregulated genes intersectio with GenAge:
Incase of downregulated genes only three genes were reported in GenAge database.

  **1. POU1F1 (Pit-1)**: a transcription factor that plays a critical role in the development and function of the pituitary gland

  **2. FOXM1**: a transcription factor that regulates the expression of genes involved in cell cycle progression, DNA replication, and repair

  **3. NUDT1 (nucleoside diphosphate-linked moiety X motif 1)**: an enzyme involved in nucleotide metabolism and DNA damage response

<img
  src="/figs/Genage intersection with downregulated genes.png"
  alt="Genage intersection with downregulated genes in all tissues "
  title="Genage iontersection with downregulated genes in all tissues"
  style="display: inline-block; margin: 0 auto; max-width: 300px">

## Discussion

### The list of differentially expressed genes across aging

According to the results of `palmer2021ageing` study all tissues and every tissue studied consistently overexpressed the following genes:

<img
  src="/figs/Palmer_table_overexpressed.jpg"
  alt="Table of the top-5 genes most consistently overexpressed with age across datasets for all tissues and for each tissue studied. `palmer2021ageing`"
  title="Overexpressed genes"
  style="display: inline-block; margin: 0 auto; max-width: 300px">
  
And the picture of underexpressed genes is the following:

<img
  src="/figs/Palmer_table_underexpressed.jpg"
  alt="Table of the top-5 genes most consistently underexpressed with age across datasets for all tissues and for each tissue studied. `palmer2021ageing`"
  title="Underexpressed genes"
  style="display: inline-block; margin: 0 auto; max-width: 300px">
  
We obtained a list of differentially expressed genes across aging and intersected them with GenAge database. Describtion of some of these genes ... .

...

We further conducted enrichment analyses for genes differentially expressed in each tissue and for all three tissues together. According to its findings, immune system activation genes were overexpressed in the brain. Differentiation-related genes were overexpressed in muscles, resulting in a decrease in regeneration activity and muscle deterioration. An increase in GABA signaling and ion transport was observed in the heart. All tissues collectively exhibit an increase in the activity of immune and proteilitic genes, while metabolic genes decrease. The described results are in line with the conclusions made in the paper `palmer2021ageing`. 


## Credits

THis repository was created by Andrey Stapran (MSc 2nd year LS), Shahzeb Khan (MSc 2nd year LS) and Daria Kozhevnikova (MSc 1st year LS) as part of a final project for **Computational Biology of Aging** course taught by **Professor Ekaterina Khrameeva** at Skolkovo Institute of Science and Technology, Moscow

## References

```{bibliography}
Palmer, Daniel et al. “Ageing transcriptome meta-analysis reveals similarities and differences between key mammalian tissues.” Aging vol. 13,3 (2021): 3313-3341. doi:10.18632/aging.202648

de Magalhães, João Pedro et al. “Meta-analysis of age-related gene expression profiles identifies common signatures of aging.” Bioinformatics (Oxford, England) vol. 25,7 (2009): 875-81. doi:10.1093/bioinformatics/btp073
```

Footer
© 2023 GitHub, Inc.
Footer navigation
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About

lalala
