![](Images/digital-loan.jpg)
# Digital Lender



## Purpose

There are two complimentary goals in our project : first, to create a currency converter, and second, a money lending service. We utilize machine learning in order to determine the credit worthiness of the user. These services are delivered using Amazon Lex.


## The Data

The data used in our machine learning model comes from https://www.kaggle.com/datasets/laotse/credit-risk-dataset?resource=download . It essentially simulates credit risk data, such as a bank might collect.

### Manipulating The Data

For the purposes of this project we wanted to keep the data features to a minimum. Given the user will be asked to provide information that will then fill in each column, we did not want this question and answer process to be too long or invasive as the service would then be less attractive.

As such, the dataset was reduced from 12 columns to just 8. Given one column - "person_home_ownership" - was a categorical variable, this was expanded to 4 columns using OneHotEncoder().

The dataset also proved to contain a sampling bias, as is to be expected from a realistic credit risk dataset. Safe loans (25473) far outweighed risky loans (7108). This was corrected using RandomOversampler() resulting in equal 0 and 1 values in the target column.

The dataset values were also scaled using StandardScaler().

## Data Considerations

It becomes clear that when trying to produce a model that will be used in a real world situation, the dataset needs to be reliable, consistent, and real. This is difficult when dealing with a financial use case as acquiring such sensitive data is quite difficult.

Initially there was a desire to take feature columns from various dataframes and concatenate them into one datatframe that we would then use. This raises the issue of inconsistencies between dataframe features resulting in a final dataframe that has feature values that do not align. In other words, a row that has features that did not actually exist in the real world (no user presented with those particular combination of feature values) and therefore skewed and unrealistic data.

To then run a machine learning model on this dataframe and expect this model to predict a real world case is naive.

Ultimately, as has become clear through this course, quality of data is paramount.

## Applicability Considerations

For many reasons this project, at least the money lending aspect, is unlikely to be used in a real world situation. For one, a user can simply lie when answering the questions and thereby get a better interest rate. The project was intended as more of a "proof of concept". It allowed us to explore the combination of a machine learning backend with an Amazon Lex frontend. The concept of lending money was a convenient way to incorporate supervised machine learning with a clearly defined target - low risk or high risk.

While we do not see this service being useful as a money lender as it stands, we do see possibilities for something similar with the rise of online banking as well as decentralised loan services. The main weakness of our product is the unreliability of the data provided by the user. Solving this could be as simple as drawing from centralised services to provide rigorous credentials coupled with KYC (Know Your Customer). Allowing for collateralization would also make this service more realistic, however with modifications. There is also the medium to long term potential for digital identities that are tied to a user that could create a scenario where a user could verify themselves and provide credentials in a way that could be trusted https://vitalik.eth.limo/general/2022/01/26/soulbound.html.

## Finding The Best Model

### First Model: Linear Regression

The first model run on the dataset did not produce outstanding results.

The balanced accuracy score was 0.6767254220456802 , which is very low.

The classification report also showed some disappointing numbers. Presicion for predicting quality loans was 36%, which is much too low to be of any use.

![](Images/regression_model_report.JPG)


### Second Model: Balanced Random Forest

The second model ran prduced better results than the first.

The balanced accuracy score was 0.7595678653679563. This is still not great, but is an improvement.

The classification report showed an imporvement in precision for both 0 and 1 targets. Recall was also improved.

![](Images/balanced_random_forest_report.JPG)


### Third Model: K-Nearest Neighbors (KNN)

The third model, although better than the first, showed a slight loss of precision from the second model.

The third model resulted in an accuracy report similar to the second model at 0.7560599383987882.

The classification report showed a slight reduction in precision and recall scores from the second model.

![](Images/knn_model_report.JPG)


### Fourth Model: Support Vector Machines (SVM)

The fourth model outperformed previous models in terms of precision.

The fourth model resulted in an accuracy report of 0.7807512889761846.

However, the classification report showed 0.0 precision and 0.0 recall for value '1'.


![](Images/svm_report.JPG)


### Fifth Model: Adaboost Model (Base Estimator = DecisionTreeClassifier)

The fifth model was the best performing model.

This model resulted in an accuracy report of 0.8397170494891675.

The classification report shows 84% precision for both 0 and 1 values. Recall for 0 values was high at 98%, but quite low at 35% for 1.

![](Images/adaboost_report.JPG)

## Saving the Machine Learning Model

After running tests on multiple machine learning models it was clear that Adaboost had the best results.

In order to make this model available to new data we needed to save the model for later loading. We achieved this using the 'pickle' library. We used pickle to serialize our model and then later to deserialize the model to make new predictions on user generated data. 