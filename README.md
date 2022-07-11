Jan 2020 - Oct 2021
# Numerai Submission

![Numerai Logo](images/numerai_logo.png)

Numerai is a quant hedge fund that is built on thousands of crowdsourced ML models. It gathers insights through the Numerai Tournament (https://numer.ai/tournament), where participants around the world build ML models on abstract financial data to predict the stock market. Models can be staked with the NMR cryptocurrency to earn rewards based on performance. An open-source dataset is available (download from the tournament link) for developing the model, while live data is posted weekly for participants to submit predictions. Predictions are scored on their correlation with the ground-truth.

In this project, a Stacked Ensemble of Gradient Boosted Trees and Regression Models was developed to tackle this challenge. 10 different tree-based or linear models were trained on the 310 original features + engineered features, and they fed their predictions to a Meta-Estimator, which then produced a final prediction. The general architecture is as shown below:

![Ensemble Architecture](images/ensemble_architecture.png)

The Stacked Ensemble was then used to compete from Nov 2020 to Oct 2021 for a total of 46 weeks. All models are ranked based on a 20-week moving average of their scores, and this model attained the following achievements:
```
Highest Ranking: 100 out of 3000+ staked models worldwide (Sept 2021)
Highest Correlation Score: 0.0732 (30 Jun 2021)
Cumulative Returns on NMR Stake: 238.7%
```
Refer to this README for a quick summary of the implementation, or view the notebooks for an in-depth description.

## Data Exploration

![Dataset Example](images/dataset_example.png)

Each entry (id) in the obfuscated dataset represents a stock at a specific week (era), and the 310 features represent various quantitative attributes of the stock, while the target depicts its performance. The features and targets were only one of 5 discrete, normalized values: 0, 0.25, 0.5, 0.75 or 1.

The dataset was split into train (120 eras, 500K entries) and and validation (22 eras, 100K entries). To evaluate the performance of the trained model, correlation scores will be generated on each of the 22 eras in the validation set, before calculating the mean and standard deviation to determine the accuracy and consistency of the model.

## Baseline Model

Refer to the notebook "baseline_models.ipynb" for more details.

A simple XGBoost Model (max_depth=5, learning_rate=0.1, n_estimators=200, colsample_bytree=0.1) was created to act as a benchmark to evaluate subsequent models and feature engineering techniques. On the validation set, the model had the following performance across 22 eras:
```
Mean Correlation Score: 0.0260
Standard Deviation across Eras: 0.0307
```
These scores were decent, and as of Nov 2021, a validation correlation of 0. 0260 is in the 76.3 percentile of all results, while a correlation of 0.0300 is in the 98.3 percentile.

## Feature Engineering

Refer to the notebook "feature_engineering.ipynb" for more details.








This repo has 4 notebooks:
1. baseline_models.ipynb - initial default models suggested by Numerai to serve as a benchmark and as a model for iterating through different parameters
2. feature_engineering.ipynb - creating additional features to add to the existing 310 features to improve inference
3. hyperparameter_tuning.ipynb - tuning the hyperparameters of different models being used in the final model ensemble
4. stacked_model_ensemble.ipynb - pipeline to stack multiple models together and train a final meta-model to improve the predictions as compared to just a single model.

We managed to achieve a validation score (by era) of 0.0302 with standard deviation 0.0307, as compared to that of the baseline model (Slow XGB Model, which is the baseline suggested in Numerai docs) with score of 0.0284 and standard deviation of 0.0306
