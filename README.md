### Final Report and Analysis: Maternity Health Risk

#### Executive Summary
This analysis of maternal health risk data factors revealed blood pressure and blood sugar as key factors in evaluating pregnancy-related health risks.  Data exploration, cleansing, and  modeling is performed in order to develop a set of signals for healthcare providers to potentially when monitoring patients to optimize deployment of care personnel and resoures.  We evaluated 3 different models: logistic regression, random forest, and XGBoost and compared their performance. Each of the models achieved around 80% accuracy in classifying patients as low, mid or high-risk, with the XGBoost model performing slightly better at identifying the risk categories.  Recommendations for further study include improvements to the data collection process as well as developing more advanced learning models and increasing the number of unique observations and feature types in order to improve the prediction accuracy and precision.

#### Rationale
The rationale for this machine learning project is to provide healthcare providers with a means to identify high-risk pregnancies so they can add these signals to clinical workflows and triage care and resources accordingly, leading to improved health outcomes for the population.

#### Research Question
Can we build a model that can accurately predict maternal health risk in order to provide healtcare poroviders with a set of signals they can use in operations when monitoring patients in order to optimize the deploymenyt of care personnel, attention, and equipment?

#### Data Sources
The data comes from the UCI machine learning library and is title "Maternal Health Risk". https://archive.ics.uci.edu/dataset/863/maternal+health+risk

#### Methodology
Exploratory Data Analysis is performed for this submission, including data cleansing, outlier analysis, checking for missingness, checking for class imbalances, and standardization of data features as necessary.  We then fit and evaluate three types of classification models to the data: logistic regression, random forest, and xgboost.  We compare how each perform based on accuracy as well as ROC_AUC to measure the model's usefulness in making predictions.

#### Results
In summary, we explored the raw dataset to determine what data features may influence pregnancy risk.  Ultimately we built, scored, and compared three types of classification models to predict risk level based on age, blood pressure, heart rate, and blood sugar

1.  Initial Data Analysis and Cleanup Recommendations
    - the dataset had three risk categories:  low, mid, and high.  we converted these to numeric values for modeling purposes.
    - there was an abundance of duplicate values.  these have the potential to skew or bias the model results.  we remove these records from the analysis, but note the cause of the duplicates warrants further investigation and analysis
    - the risk levels as a target variable for the predictions was not balanced, this could be a purposeful data collection strategy or have some other legitimate business reason.  However, for purposes of modeling, we recommend balancing strategies be deployed in either sampling or in the modeling stages.
  
2.  Key Features/Influencers
    - Blood Sugar appears to show a strong correlation with risk level
    - Blood Pressure (both systolic and diastolic) have significant correlation with maternal risk categorization
    - Body Temperature was slightly less interesting in terms of correlation and heart rate did not seem to be too significant in terms of influence

3.  Logistic Regression Model and Performance
    - After standardizing the numeric features, the basic logistic regression performed decently for low-risk classification (79% precision, 66% recall) and high-risk classification (67% precision, 43% recall), but struggled to predict mid-risk classification (29% precision, 43% recall).
    - The ROC-AUC score, which measures how well the model differentiates between risk levels showed relatively decent predictive ability at about 80%.
  
4.  Random Forest Model and Performance
    -For the random forest model used grid search cross validation to find the best fit.  The ROC-AUC score for this model was 79%, so it was very slightly less effecting in distinguishing between the risk levels when compared to the logistic regression.
    -But in terms of sheer accuracy (% of correct predictions), it came out at about 73% accurate, quite an improvement over logistic regression (59%), but had noticeably lower success at recall at the mid-risk level (37% precision, 19% recall).

5.  XGBoost Model and Performance
    -XGBoost was also used to model the training data using grid search cross validation to find the best model.  The ROC-AUC score came in slightly better than random forest, at 80%, roughly on par with the logistic regression.
    -In terms of the accuracy score, this model came in at 74% accuracy as well, but once again struggled at the mid-risk level (44% precision, only 19% recall).  So slightly better than Random Forest in the mid-level.

7.  Model Comparison and Takeaways
    -In terms of model selection and deployment, this is really where the business/clinical use is going to come into play.  If the business use/systm is essentially bifurcated to focus on classifying low risk patients and treat the other classes the same, then XGBoost is your model of choice, it performed the best with respect to predicting low risk.
    -If there was a business case or even a quantifiable business cost assigned to properly identifying all three risk levels, then the logistic regression may be your best bet to err on the side of caution with respect to your mid-level risk patients. If the goal of the model is to really focus on getting the high risk level patients right because of their outsized impact on care resources, then the Random Forest would be useful given it has the highest precision (78%) and recall (91%) at this critically importantly risk level.


#### Business Impact and Takeaways
Ideally, we'd like to improve the performance of predicting mid-risk and high-risk cases, as having misdiagnoses in those instances could theoretically lead to treatment delay or misallocation of personnel and resources.

As an overall takeaway, the analysis underscores the importance of monitoring and prioritizing resources for intervention particularly based on blood sugar and blood pressure readings as well as age.

This analysis and modeling could also be useful for targeting individuals for wellness checks or programming, identifying low and mid risk patients and then pre-emptively providing them with information or programming to help keep things like blood sugar in check in low risk level ranges.

From a data perspective, there were challenges to this dataset including duplicate records, some extreme outliers in heart rate and age, and class balance issues in the dataset with fewer 'high risk' observations and more 'low risk' observations.  These issues could be addressed through improvements to the systems and processes that collect the data.  A higher volume of data collected would be useful too, as the data became a bit thinned out once the duplicates were removed and given the stratification of the risl levels across the data.  It may also prove useful to have timestamp data associated with multiple readings from individuals to evaluate how the data changes over the timeframe of the pregnancy as an additional risk signal.
