# Project report

All code for tasks described in this report is avaliable in our <a href="https://github.com/d-kozhevnikova/Ageing-transcriptome-meta-analysis/blob/main/AgeingTranscriptionMetaRegression.ipynb">Jupyter Notebook</a>.

## Introduction

In this project, we reproduce the results of a gene expression meta-analysis performed by <a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7906136/#SD2">Daniel Palmer and colleagues in 2021</a>. In this study transcriptomic signatures associate with ageing were identified for brain, heart and muscle tissues based on the analysis of 127 publicly-available microarray and RNA-Seq datasets from mice, rats, and humans.<br>
Overall, changes in gene expression with age followed the following patterns:
<ul>
  <li>overexpression of immune and stress response genes with age</li>
  <li>underexpression of metabolic and developmental genes</li>
</ul>
In muscle and heart tissues genes involved in cell response processes were found to be activated. It was also found that genes differentially expressed with age were mainly central for protein-protein interaction networks. Previously in the <a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2732303/">paper from 2009</a> by the same authors similar common ageing gene signatures were identified such as:
<ul>
  <li>overexpression of inflammation, immune response and lysosomes related genes</li>
  <li>underexpression of collagen, energy metabolism (especiallu mitochondrial) genes</li>
  <li>changes in expression of apoptosis genes and cell cycle regulation genes</li>
</ul>
Finally, it was found that genes differentially expressed with age are rarely tissue-specific but rather are commonly expressed in multiple tissues.<br>
The outline of analysis pipeline from the original study is the following:
<ol>
<li>Linear regression performed for each gene inside each dataset. The slope of the regression corresponds to the direction in change of gene expression with age (if positive - gene is upregulated with age and vice versa)</li>
<li>Genes for which regression slope is statistically significant are selected</li>
<li>Meta regression analysis was performed with <i>Cumulative Binomial test</i></li>
<li>False discovery rate correction was performed by permutating gene IDs in the original dataset and repeating the meta-regression analysis. Based on this an average percentage of statistically significantly differentially expressed genes was identified - this allowed calculating critical p-value at which FDR was less than 0.05</li>
<li>Tissue specificity analysis was run with <i>tau</i> index used as a measure of tissue specificity</li>
<li>Differentially expressed genes (DEGs) that had evidence of association with age across multiple datasets were selected for further analysis</li>
<li>Enrichment analysis with David and topGO R tool was performed</li>
</ol>
As additional steps authors also performed:
<ul>
<li>dN/dS analysis - ratio of non-synonymous to synonymous substitutions in the sequences of main DEGs in different species. These calculations showed that those genes are predominantly evolutionary conserved across species</li>
<li>Random Forest ML model on GO terms was built to identify the GO terms that can best predict whether a particular gene will be over- or underexpressed with age</li>
</ul>
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

