Nov 2020 - Oct 2021
# Numerai Submission

![Numerai Logo](images/numerai_logo.png)

Numerai is a quant hedge fund that is built on thousands of crowdsourced ML models. It gathers insights through the Numerai Tournament (https://numer.ai/tournament), where participants around the world build ML models on abstract financial data to predict the stock market. Models can be staked with the NMR cryptocurrency to earn rewards based on performance. 

An open-source dataset is available for developing the model, while live data will be posted weekly for participants to submit their predictions. The dataset is split into train (500K entries) and validation (100K entries), with each entry having 310 features and a single label, all being discrete numbers [0, 0.25, 0.5, 0.75, 1].

In this project, a Stacked Ensemble of Gradient Boosted Trees and Regression Models was developed to tackle this tournament. 




The dataset is split into train and validation, with each entry having 310 features and a single label, all being discrete numbers [0, 0.25, 0.5, 0.75, 1]. The train dataset has more than 500,000 entries, while that of the validation set is above 100,000. Each week, a new test set will be released for users to submit their predictions for it, and a score will be available at the end of the week.

This repo has 4 notebooks:
1. baseline_models.ipynb - initial default models suggested by Numerai to serve as a benchmark and as a model for iterating through different parameters
2. feature_engineering.ipynb - creating additional features to add to the existing 310 features to improve inference
3. hyperparameter_tuning.ipynb - tuning the hyperparameters of different models being used in the final model ensemble
4. stacked_model_ensemble.ipynb - pipeline to stack multiple models together and train a final meta-model to improve the predictions as compared to just a single model.

We managed to achieve a validation score (by era) of 0.0302 with standard deviation 0.0307, as compared to that of the baseline model (Slow XGB Model, which is the baseline suggested in Numerai docs) with score of 0.0284 and standard deviation of 0.0306
