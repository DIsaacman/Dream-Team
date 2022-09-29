# Draft

It becomes clear that when trying to produce a model that will be used in a real world situation, the dataset needs to be reliable, consistent, and real. This is difficult when dealing with a financial use case as acquiring such sensitive data is quite difficult.

Initially there was a desire to take feature columns from various dataframes and concat them into one datatframe that we would then use. This raises the issue of inconsistencies between dataframe features and resulting in a final dataframe that has feature values that do not align. In other words, a row that has features that did not actually exist in the real world (no user presented with those particular combination of feature values) and therefore skewed and unrealistic data.

To then run a machine learning model on this dataframe and expect this model to predict a real world case is naive.

Ultimately, as has become clear through this course, quality of data is paramount.


### First Model: Linear Regression

The first model run ont he dataset did not produce outstanding results.

The balanced accuracy score was 0.6767254220456802 , which is very low.

The classification report also showed some disappointing numbers. Presicion for predicting quality loans was 36%, which is much too low to be of any use.

![](Images/regression_model_report.JPG)
