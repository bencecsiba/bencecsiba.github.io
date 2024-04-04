---
layout: post
title:  "AutoGluon for FPL Prediction"
date:   2024-03-21 16:01:51 +0000       
categories: jekyll update
---
Another approach to the FPL predictor project that I am currently working on has been to use the Autogluon package. The table below shows the test scores
for various models tried by AutoGluon, with the best overall performance coming from the weighted ensemble.

| Model               |   RMSE |
|:--------------------|-----------------:|
| NeuralNetFastAI     |        0.141883  |
| LightGBM            |        0.042974  |
| LightGBMLarge       |        0.042861  |
| XGBoost             |        0.0358369 |
| **WeightedEnsemble_L2** |        **1.17335**   |
| LightGBMXT          |        0.955469  |
| ExtraTreesMSE       |        0.170214  |
| RandomForestMSE     |        0.195836  |
| NeuralNetTorch      |        0.0555069 |
| KNeighborsUnif      |        0.846408  |
| KNeighborsDist      |        0.977883  | 

The image below shows the models that make up this particular weighted ensemble. Interestingly, it uses three models that weren't the best performing models individually. 

![AutoGluon_Ensemble](../assets/ensemble_model.png)

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