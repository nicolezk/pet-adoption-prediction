# pet-adoption-prediction
This repository contains the code for the project of the Machine Learning course given at Universitat Politécnica de Cataluña (UPC).

## Data
The data was obtained from [Kaggle's "PetFinder.my Adoption Prediction"](https://www.kaggle.com/c/petfinder-adoption-prediction/data) competition.

## How to execute and reproduce results
Execute the notebooks in the following order:
1. data_wrangling.ipynb
2. EDA.ipynb
3. feature_engineering.ipynb
4. model_tunning.ipynb
5. model_tunning_split_dogs_and_cats.ipynb

---
## Project description
Millions of stray animals suffer on the streets in countries all over the world. Based on a [Kaggle competition](https://www.kaggle.com/c/petfinder-adoption-prediction/data) hosted by Malaysia’s leading animal welfare platform, PetFinder.my, we decided to create a machine learning pipeline to predict how fast an animal will be adopted after arriving in a shelter. The data comes from the animals’ profiles in petfinder.my and contains features such as animals characteristics (breed, age, color, fur length, etc), health conditions (vaccinated, sterilized, etc), type (dog or cat), location (state, shelter identification) and other descriptive information. By predicting the adoption speed of an animal we expect to help the shelters to improve the pets profiles so that they can find a caring home faster and there won’t be so many animals suffering on the streets or being euthanized in shelters.

## Data analysis
The data exploration part was divided into three different sections: 
data wrangling, 
exploratory and descriptive analysis (EDA) and 
feature engineering. 
In the data wrangling step, a series of checks were performed to ensure that the data would be consistent and in a concise format. For the EDA step the variables were analyzed individually (univariate analysis) and paired together (multivariate analysis) to check their distributions and relationships amongst them. At last, in the feature engineering part, we generated new variables from the original ones using the insights we found in the exploratory analysis.

## Main conclusions from EDA
- There are more female pets (57%) than male ones (43%) among the ones in singular pet posts.
- 77% of the pet posts are of only one pet. The quantity of pets ranges from 1 to 20.
- At least 75% of the animals are 1-year-old or less.
- 1 rescuer was responsible for more than 400 profiles. The second most recurrent is around 300 profiles.
- Dogs are more vaccinated than cats.
- Unhealthy pets seem less likely to be adopted right away.
- Cats seem to be adopted faster than dogs.
- Vaccinated animals seem to be slightly more likely to not be adopted after 100 days after being listed.

## Balancing classes
Predicting the adoption speed is a classification problem because the target variable is a category of speed that goes from 0 up to 4, zero being the fastest and 4 the slowest. First, the classes were balanced to make sure the models wouldn’t be biased by unbalanced classes. When comparing the results of models trained in unbalanced versus balanced data, we achieved a decrease of 0.11 in the error (RMSE) by balancing the classes.

## Model tuning
Several algorithms were selected to validate which one would perform better in the data. We trained models for Linear, Ridge and Lasso Regression, Softmax Regression, XGBoost, Random Forest (not considering the order of the categories) and Ordinal Random Forest (which considers the order of the categories).  We also created 2 additional models, one just for cats and the other just for dogs, where we use the best model obtained to check if  an individual model for each type of animal would be better than 1 single model for all types.

#### Pipeline
1. Split the data into a train set and a test set.
2. Select the hyperparameters grid for each algorithm
3. Use cross validation to find the best parameters for each model
4. Compare RMSE and choose the best model 
5. Retrain that model with whole data
6. Evaluate the model’s generalization power in the test set

## Evaluation and results
Even though this is a classification problem, given that the target variable is ordinal (predicting 5 instead of 1 is worse than predicting 2 instead of 1), we decided to use the  root mean square error to evaluate the models’ performances. We have compared the cross validation (CV) RMSE for each model and found the best model to be Random Forest Classifier, with an RMSE of 1.26. After choosing such model and using cats-only and dogs-only datasets to train separate models, we found a slight change in perf, but for the sake of simplicity decided to keep the whole dataset and one single model as the final choice. When tested against the test dataset, the model presented an RMSE of 1.21 (better than the CV results) which shows that the model generalizes well.

## Conclusions
We could validate that the classification algorithms performed better than the adapted regression models. The Random Forest algorithm presented the overall lowest cross validation RMSE, and even though intuitively the Ordinal Random Forest Classifier seemed a better choice, its results were slightly worse than the normal Random Forest Classifier, so we chose the latter as the best model found.

## Possible extensions
Further experiments could be done trying neural networks and deep learning for ordinal classification to evaluate performance. Furthermore the usage of natural language processing and sentiment analysis could be done in the “Description” field to attempt to obtain more meaningful features for the model.

---
## Project contributors
[Luiz Fonseca](https://www.linkedin.com/in/luiz-fonseca-data-scientist/)

[Nicole Kovacs](https://www.linkedin.com/in/nicolezk/)






