# Numerai Tournament

This project is an attempt at the Numerai Tournament (https://numer.ai/tournament), an international machine learning tournament with cash rewards every week in NMR cryptocurrency coins. Participants attempt to predict the stock market thorugh obfuscated data provided by Numerai. Predictions will be used to contribute to the meta-model that Numerai uses. 

The dataset is split into train and validation, with each entry having 310 features and a single label, all being discrete numbers [0, 0.25, 0.5, 0.75, 1]. The train dataset has more than 500,000 entries, while that of the validation set is above 100,000. Each week, a new test set will be released for users to submit their predictions for it, and a score will be available at the end of the week.

This repo has 4 notebooks:
1. baseline_models.ipynb - initial default models suggested by Numerai to serve as a benchmark and as a model for iterating through different parameters
2. feature_engineering.ipynb - creating additional features to add to the existing 310 features to improve inference
3. hyperparameter_tuning.ipynb - tuning the hyperparameters of different models being used in the final model ensemble
4. stacked_model_ensemble.ipynb - pipeline to stack multiple models together and train a final meta-model to improve the predictions as compared to just a single model.

We managed to achieve a validation score (by era) of [X] with standard deviation [Y], as compared to that of the baseline model with score of [X] and standard deviation of [Y]
