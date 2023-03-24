# Ageing transcriptome meta-analysis
In this repository, you will find 
final project for Skoltech course "Computational Biology of Aging" performed by:
<ul>
<li>Andrey Stapran</li>
<li>Daria Kozhevnikova</li>
<li>Shah Zeb Khan</li>
</ul>
This project tries to reproduce the results of the original paper by Palmer D. et al., 2021 <a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7906136/"><b>Ageing transcriptome meta-analysis reveals similarities and differences between key mammalian tissue</b></a><br><br>The following files are available in this repository:
<ol>
<li><b>datasets_used</b> - list of datasets in tsv format used in the current analysis - available as normalized gene counts (RPKM, log2) for studied genes for each sample</li>
<li><b>figs</b> - folder with figures describing the results of our project and original study</li>
<li><b>results</b> - folder with results of our project. Contains three subfolders (each has meta-regression results for datasets used in the analysis + union of all genes studied in these datasets - to be used as background for GO enrichment analysis)</li>
<ul>
<li><b>allthree</b> - folder with results of meta-regression analysis for heart, brain, and muscle tissue combined</li>
<li><b>heart</b> - folder with results of meta-regression analysis for heart</li>
<li><b>brain</b> - folder with results of meta-regression analysis for brain</li>
<li><b>muscle</b> - folder with results of meta-regression analysis for muscle</li>
</ul>
<li><i>AgeingTranscriptionMetaRegression.ipynb</i> - commented jupyter notebook with the code used for the analysis in the current project</li>
<li><i>Presentation.pdf</i> - slides with the results of our project</li>
<li><a href="https://github.com/d-kozhevnikova/Ageing-transcriptome-meta-analysis/blob/main/Project%20report.md"><i>Project report.md</i></a> - <b>main part with the description of experimental procedure and results obtained in this project</b></li>
<li><i>References.bib</i> - file with references</li>
<li><i>metadata.xlsx</i> - <i>xlsx</i> file with description of the datasets used in the analysis</li>
</ol>
<br>
For the GitHub repository of the original paper please refer to <a href="https://github.com/maglab/AgeingSignatures2020_supplementary">this link</a><br>
