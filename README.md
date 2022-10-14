# st-histology-ml

## Project Description
The goal of this project is to develop a machine learning model to predict spatially localized gene expression from histology images.

The field of barcode-based spatially resolved transcriptomics (SRT) uses spatially barcoded mRNA and next-generation sequencing technology to recover gene expression level data that corresponds to a specific locus (gene expression spot) within a tissue sample. In addition, haematoxylin-and-eosin (H&E) stained images provide a visual representation of these tissue sections and can be leveraged as additional information for the analyses of these data.

Now that spatially localized gene expression data and associated histology images are available, one goal is to predict gene expression levels of specific tissue loci directly from a histology image of the tissue sample itself, instead of utilizing sequencing technology to determine expression levels. This is desirable so that predicted expression can be obtained on future H&E images that did not have corresponding gene expression measured, thereby obtaining spatial gene expression without the cost of directly measuring it. This project is concerned with developing a machine learning model to perform this prediction by extracting features of the H&E image as inputs, and outputting the predicted expression levels of a specific gene at each image location. 

## Data
Data for this project was retrieved from the SpatialLIBD R/Bioconductor package (http://spatial.libd.org/spatialLIBD/). This package includes 12 lowres (600x600 pixels) LIBD human dorsolateral pre-frontal cortex (DLPFC) spatial transcriptomics samples generated with the 10x Genomics Visium platform. Each sample has an associated histology image and bulk-RNAseq logcounts matrix.

## Feature Extraction
The most basic features used as inputs for the model were the RGB/Grayscale color space and the HSL (Hue, Saturation, Lightness) color space. To develop more advanced features, a 13x13 pixel image patch centered around each barcoded spot was inputted into an autoencoder. Then, the features within the latent space were used as inputs for classification.

## Classification
The baseline model performed binary classification for a select number of genes strongly correlated to the input features. Target classes were 0 (no gene expression at spot x) and 1 (positive gene expression at spot x). To perform binary classification, features were standardized and a logistic regression model performed prediction. 

## File Structure
| <br />
| _ Preprocessing.Rmd <br />
|    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; R Markdown notebook containing quality control operations to remove uninformative genes and spots. <br />
| <br />
| _ EDA.Rmd <br />
|     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; R Markdown notebook containing exploratory data analysis, including spot plots, feature extraction methods, and correlation analysis <br />
| <br />
| _ Models.Rmd <br />
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; R Markdown notebook performing binary classification of select genes found to be highly correlated with the input features. <br />
