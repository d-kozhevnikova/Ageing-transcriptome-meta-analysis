# Project report

All code for tasks described in this report is avaliable in the [Jupiter Notebook]().

style blocks from [jupyter_book](https://jupyterbook.org/en/stable/intro.html) API for making the report more beautiful.

Use the following directive to refer to a particular picture in the text {numref}`hallmarks_taxonomy`


## Introduction

In this project, we reproduce the results of a meta-analysis of gene expression in mice reported by Palmer, Daniel et al. in 2021  [palmer2021ageing](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7906136/#SD2). In this study transcriptome signatures of ageing in brain, heart and muscle were derived from 127 public microarray and RNA-Seq datasets from mice, rats, and humans. Gene expression patterns revealed overexpression of immune and stress response genes with age, as well as underexpression of metabolic and developmental genes. It was indicated that gene ageing signatures are associated with key genes in protein interaction networks. Previously in thr paper [de2009meta](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2732303/) several common signatures of aging were highlighted including overexpression of inflammation, immune response and lysosomes related genes, underexpression of collagen, energy metabolism and MT genes, as well as alterations in expression of apoptosis genes. The reasoning that genes that display differential expression with age are mainly common for different tissues was confirmed.  

## Results

#### Preprocessing of the gene expression data

From the data avaliable on the [github repository](https://github.com/maglab/AgeingSignatures2020_supplementary) we selected 20 mice microarray datasets originated from brain, heart and muscle. Each dataset contains expression levels of around 20000 genes from several samples.

To estimate differencially expressed genes (DEGs) we conducted linear regression analysis for all the datasets. The regression equation:

$$Y_{ij} = \beta_{0j} + \beta_{1j}Age{i} + \epsilon_{ij}$$

The slope of this regression identifies the coefficient of differencial expression. F test with 0.05 cutoff was then used to identify the significance of the coefficients. 

To further identify the genes with significant changes in expression across the datasets cumulative binomial test was applied. 

meta-regression???

#### Meta-analysis of the datasets

Firstly the global metaanalysis was conducted to identify DEGs across all tissues. For that the datasets with genes regression data were processed with the **PyMare** package.

Next, the same analysis was conducted separately for each tissue. 


Put figures in your report. If some of the pictures were produced with python code, save them in a separate folder within the folder of your project. Use the following directive to put a figure inside the text:

```{figure} figs/hallmarks_taxonomy.png
:name: hallmarks_taxonomy
Hallmarks taxonomy.
```

#### GO enrichment analysis


## Discussion

Discuss your results here and answer additional questions from questions/tasks section of **project proposal**. 

**!!!!!!!!!!!Our Project tasks/questions:**
1) Reproduce the results of the paper. Try to use a maximum of python for conducting meta-analysis. PyMare package can help you.
2) Describe some weak points of the paper (if any).
3) Could you suggest improvements to the approach?
4) Obtain a list of differentially expressed genes across aging. Intersect them with GenAge database. Describe some of these genes.
5) Conduct enrichment analysis.
6) Explain the ML approach used in the paper.

#### The genes differentially expressed with age

#### Machine learning approach used in the paper `palmer2021ageing`
ML: list of GO terms that are enriched   build decision tree plot to understand wheather - enrichment term on each node of the tree (does the gene belong 
des tree for each gene based on the functional categories - decides if the gene are dif expressed
selected funct categories that predict best if the gene is diff expressed.


## Credits
This text prepared by [Daria Kozhevnikova](https://linktoyourprofile/scholar/or/linkedin.com) 

The Jupiter Notebook for the data analysis prepared by Andrey Stapran

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
