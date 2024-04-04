---
layout: post
title:  "AutoGluon for FPL Prediction"
date:   2024-03-21 16:01:51 +0000       
categories: jekyll update
---
Another approach to the FPL predictor project that I am currently working on has been to use the Autogluon package. The table below shows the test scores
for various models tried by AutoGluon, with the best overall performance coming from the weighted ensemble.

| Model               |   Validation Score |
|:--------------------|------------:|
| NeuralNetFastAI     |    -2.61968 |
| LightGBM            |    -2.60456 |
| LightGBMLarge       |    -2.58797 |
| XGBoost             |    -2.61013 |
| **WeightedEnsemble_L2** |    **-2.56407** |
| LightGBMXT          |    -2.58705 |
| ExtraTreesMSE       |    -2.59106 |
| RandomForestMSE     |    -2.63888 |
| NeuralNetTorch      |    -2.73893 |
| KNeighborsUnif      |    -3.02923 |
| KNeighborsDist      |    -3.06765 |
The image below shows the models that make up this particular weighted ensemble. It uses a combination of just the three best scoring models to produce a slightly better one. 

![AutoGluon_Ensemble](/assets/ensemble_model.png)

When testing the other models that I have built thus far, the AutoGluon model does not perform particuarly well, although better than the simple random forest, as expected. 
The results are displayed in the table below.

|               |  Mean Fraction of Top Score |   Mean Fraction of Average Score |
|:--------------|-----------------:|-----------------:|
| Neural Network           |          58.7308 |          147.288 |
| Random Forest Split      |          57.6625 |          144.364 |
| **AutoGluon** |          **57.1401** |          **143.019** |
| Random Forest            |          55.7754 |          140.253 |

My next aim is to use a custom ensemble of models to achieve the best possible results. I am curious to see if a combination of the above models will result in a better overall performance.
This will reqiure further work, retraining the models on smaller datasets, in order to keep the current test set (the 2023/24 season) as such.