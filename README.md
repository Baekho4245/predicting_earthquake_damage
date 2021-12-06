![Header_Image](images/title.png)

# ABSTRACT

Earthquakes happen unexpectedly and sometimes, violently. We normally don't think about it in our daily lives, but we always do after the destruction. There are laws to help mitigate the damage of earthquakes, especially in areas with many titonic plates, but now we can take action to mitigate those damages before hand, through the power of data

# Business Problem

The Nepalese government wants to find out how to minimalize destruction. Using data collected from the Nepal Earthquake in 2015, build a predictive model to correctly classify how much damage a building will have based on its characteristics.

Because we are building a predictor for potentially remodeling some buildings, having false positives will be extremely expensive, and we definately do not want to miss false negatives as that could potentionally put lives at risk. Accuracy is a metric that is a combination of recall and precision.

We also found some class imbalance in our target variable, at about a 67 / 33 split. While it is not the perfect 50 / 50 split we would like, there should be enough data at this split to build a sufficient model.

# Data Understanding

This is our preprocessed dataset:
![full_df_values](/images/full_df_values.png)

Because we are looking into the predicting total damage grade caused by the features of the house, house information such as building uses, secondard building uses, and ownership should have no effect in the overall damage caused by an earthquake. Thus, we dropped those columns, reducing our dataset about 33%.

![df_values](/images/df_values.png)

Next, for the df_labels. Because we are interested in modeling for the major damage category, we relabeled 'light damage' and 'some damage' into one, '0', and 'major damage' as '1', turning our model into binary classifier. This introduced the potential 33/67 class imbalance split. But again, because the class imbalance is not too extreme, creating a model with this data should not be too big of an issue.

# Data Preparation

For the remaining object types, we converted them into a categorical so we can pass the dataset into a StandardScaler to find the most important features, turning our dataset into this:

![major_damage](/images/major_damage.png)

# Modeling

## KNN

For our baseline model, we created a KNN with parameters (here) for an accuracy rate of (x%). The KNN model took an exceptionally long time because of the sheer size of our dataset and number of features. Coupled with the low explainability, the KNN model is best left to the side while we explore potentionally better models.

![KNN_validation](/images/KNN_validation.png)

## Logistic Regression

The Logistic Regression model scored an accuracy rate of (x%), which is higher than the previous KNN model. With much faster runtime, and easier interpretibility, the Logistic Regression model outclasses the KNN in pretty much every way.

![Logistic_Regression_validation](/images/Log_reg_val.png)

Because our model does not seem to be overfitting / underfitting, we did not feel a need to add in regularization.

## Random Forest 

The Random Forest Classifier ended up being our best model. With these parameters (here), the model scored an accuracy rate of (x%). While the Random Forest Classifier took longer than the Logistic Regression in training time, they share around the same level of explainability. And because we had enough resources and time to model using Random Forests, we chose to make it our final model.

![Random_Forest_validation](/images/random_forest_val.png)


# Results

Our business problem has no bias against false negatives / false positives, the F1 score metric determined that the Random Forest Classifier is the best model with an F1 score of 68%.

The benefits of the Random Forest Classifier is the explainability of the model, meaning we can determine the most important features necessary for prediction. For more information on how we determined the most important features, check out our data_viz notebook!

# Data Limitations

The data was collected in Nepal, 2015, the application for the model may be difficult to find. In order to use this model for prediction, the features of the buildings in the new estimating area has to be somewhat similar to that of buildings in Nepal. With the data being 6 years old, it is also possible many potential dangers have been fixed.

# Conclusion

Because earthquakes can be sudden and violent, it is imperative that areas in risk of an earthquake, prepare before it is too late. With the help of our model, with an  68.2% accuracy, we can determine help point regulators to buildings that could be buildings that is in risk of destruction come a major earthquake.