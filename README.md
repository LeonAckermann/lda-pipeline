# text-lda

This repository contains the code of an Experiment pipeline for Topic Modeling using LDA (Latent Dirichlet Allocation) written in R.

## Table of Contents
1. [Overview](#overview)
2. [Installation](#installation)
3. [Usage](#usage)

## Overview
The pipeline is composed of the following steps:

**1. Data Preprocessing**<br>
The data preprocessing converts the data into a document term matrix (DTM) and removes stopwords, punctuation, etc. which is the data format needed for the LDA model.

**2. Model Training**<br>
The model training step trains the LDA model on the DTM with a number of iterations and predefined amount of topics.

**3. Model Inference**<br>
The model inference step uses the trained LDA model to infer the topic term distribution of the documents.

**4. Statistical Analysis**<br>
The analysis includes the methods like linear regression, binary regression, ridge regression or correlation to analyze the relationship between the topics and the prediction variable. It is possible to control for a number of variables and to adjust the p-value for multiple comparisons.

**5. Visualization**<br>
The visualization step creates wordclouds of the significant topics found by the statistical analysis.

## Installation
To install the required packages, run the following command:
```bash
bash requirements.sh
```


## Usage
In an example where the topics are used to predict the PHQ-9 score, the pipeline can be run as follows:

**0. Setup**<br>
Before running the pipeline, make sure to have the following command in your R script:
```R
source("./src/main.R")
```


**1. Data Preprocessing**<br>
To preprocess the data, run the following command:
```R
data <- read.csv("data.csv")
dtm <- ldaDtm(data=data,
              id_col="id",
              data_col="text")
```

**2. Model Training**<br>
To train the LDA model, run the following command:
```R
model <- ldaModel(dtm=dtm,
                  num_topics=20,
                  num_iterations=1000)
```

**3. Model Inference**<br>
To infer the topic term distribution of the documents, run the following command:
```R
preds <- ldaPreds(model=model,
                  dtm=dtm)
```

**4. Statistical Analysis**<br>
To analyze the relationship between the topics and the prediction variable, run the following command:
```R
test <- ldaTest(model=model,
                preds=preds,
                dtm=dtm,
                pred_var="phq9",
                control_vars=c("age",..),
                test_method="linear_regression")
```

**5. Visualization**<br>
To visualize the significant topics as wordclouds, run the following command:
```R
ldaWordclouds(model=model,
              test=test)
```









