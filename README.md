# DeepChrome

Go to Vizualization Website: [DeepChrome visualization website](http://qdataw.cs.virginia.edu/)

Reference Paper: [DeepChrome: Deep-learning for predicting gene expression from histone modifications](http://bioinformatics.oxfordjournals.org/content/32/17/i639.abstract)

BibTex Citation:
```
@article{singh2016deepchrome,
  title={DeepChrome: deep-learning for predicting gene expression from histone modifications},
  author={Singh, Ritambhara and Lanchantin, Jack and Robins, Gabriel and Qi, Yanjun},
  journal={Bioinformatics},
  volume={32},
  number={17},
  pages={i639--i648},
  year={2016},
  publisher={Oxford Univ Press}
}
```

DeepChrome is a unified CNN framework that automatically learns combinatorial interactions among histone modification marks to predict the gene expression. It is able to handle all the bins together, capturing both neighboring range and long range interactions among input features, as well as automatically extract important features. In order to interpret what is learned, and understand the interactions among histone marks for prediction, we also implement an optimizationbased technique for visualizing combinatorial relationships from the
learnt deep models. Through the CNN model, DeepChrome incorporates representations of both local neighboring bins as well as the whole gene.

**Feature Generation for DeepChrome model:** 

We used the five core histone modification (listed in the paper) read counts from REMC database as input matrix. We downloaded the files from [REMC dabase](http://egg2.wustl.edu/roadmap/web_portal/processed_data.html#ChipSeq_DNaseSeq) and used "bedtools multicov" to get the read counts. 

Bins of length 100 base-pairs (bp) are selected from regions (+/- 5000 bp) flanking the transcription start site (TSS) of each gene. The signal value of all five selected histone modifications from REMC in bins forms input matrix X, while discretized gene expression (label +1/-1) is the output y.

For gene expression, we used the RPKM read count files available in REMC database. We took the median of the RPKM read counts as threshold for assigning binary labels (-1: gene low, +1: gene high). 

We divided the genes into 3 separate sets for training, validation and testing. It was a simple file split resulting into 6601, 6601 and 6600 genes respectively. 

We performed training and validation on the first 2 sets and then reported AUC scores of best performing epoch model for the third test data set. 

Toy dataset has been provided inside "code/data" folder.

After downloading "code/" folder:

To perform training : 
```
th doall.lua
```
To perform testing/Get visualization output: 
```
the doall_eval.lua
```
