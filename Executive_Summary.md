# Executive Summary
---
## Predicting Coronavirus Infections

Aziz Maredia, Katharine King, Max Bosse, Manuel Sainz de la Peña

---
## Problem Statement

What attributes of colleges contribute to an increased probability that the campus will see greater than 5% of the student population infected with the Coronavirus?

---

## Datasets and sources

* [`nyt_college.csv`](./datasets/nyt_college.csv): Colleges and counts of Coronavirus case counts, [NYT Repository](https://github.com/nytimes/covid-19-data/tree/master/colleges)
* [`admissions1.csv`](./datasets/admissions1.csv): Data pulled from IPED's database, part 1, [IPED Database](https://nces.ed.gov/ipeds/)
* [`admissions2.csv`](./datasets/admissions2.csv): Data pulled from IPED's database, part 2, [IPED Database](https://nces.ed.gov/ipeds/)
* [`sports.csv`](./datasets/sports.csv): Data pulled from IPED's database, part 3, [IPED Database](https://nces.ed.gov/ipeds/)
* [`regions.csv`](./datasets/regions.csv): State region and sports division
* [`state_policies.csv`](./datasets/state_policies.csv): State Social Distancing and other Coronavirus policies as of August 11th, [Kaiser Family Foundation](https://github.com/KFFData/COVID-19-Data/tree/kff_master/State%20Policy%20Actions/State%20Social%20Distancing%20Actions)
* [`classplan.csv`]('./datasets/classplan.csv'): Dataset of colleges and their intended plan for the Fall of 2020 [The Chronicle of Higher Education](https://www.chronicle.com/article/heres-a-list-of-colleges-plans-for-reopening-in-the-fall/)
* [`combined_df.csv`]('./datasets/combined_df.csv): Merged Dataframe created in [intro_data_merging_cleaning]('./code/intro_data_merging_cleaning.ipnyb')

Target Column: Predict a University's classification into **greater_than_5**, which indicates whether a college has case counts that exceed 5% of the total enrolled population


---

During exploratory analysis of the dataset we found several notable features that had strong correlations to case counts and our target column 'greater_than_five.' The most strongly correlated column contained data about the number of freshman students submitting ACT scores as part of their admissions process . The ACT tends to be used more often in the middle section of the United States, this regionalization may be influencing the correlation ([source](https://www.collegeraptor.com/getting-in/articles/act-sat/preference-act-sat-state-infographic/)).

Total enrollment correlated strongly with the overall case count, but not as strongly with the engineered columns were used to control for overall school size. That said, freshman enrollment did have a small but relatively strong relationship with the target column 'greater_than_five' suggesting that where schools enrolled a large freshman class, case counts may see increases overall.

Other notable features include engineered features created with the categorical features included in the initial dataset. The second most correlated feature after processing the categorical features was engineered using a class plan column indicating colleges would primarily have courses in person and a column indicating state had reopened bars, we labeled this feature 'packed_bars.' This indicates that colleges that were planning to have in-person classes in a state where bars were reopened in mid-August saw higher infection rates overall. The two heatmaps included below show the top positive and negative correlations between the features and the target variable 'greater_than_five,' indicting a college has had cases exceeding 5% of the total enrollment.

Most Positive Correlations             |  Most Negative Correlations
:-------------------------:|:-------------------------:
![Postive Correlations](.././Images/correlation_top.png)  |  ![Negative Correlations](.././Images/correlation_bottom.png)


---
## Modeling

To model and predict which colleges would have outbreaks, we explored several classification models, including Decision Trees, Logistic Regression models, and Neural nets. Ultimately we found that the Logistic Regression model performed the best on our data. The final model produced a training score of 0.8, as well as a 0.8 testing score. While this was not incredibly far from our baseline of 0.76, we felt this illustrates part of the challenge of working with Public Health Data, especially in a time where the world faces an unprecedented global disaster.

To begin, we ran several models at once with default parameters to help decide which models to focus on refining. The scores for the initial models are below:

|Model|Best Score|
|---|---|
|LogisticRegression() |0.7485714285714286|
|KNeighborsClassifier()|0.6228571428571429|
|DecisionTreeClassifier()|0.7142857142857143|
|BaggingClassifier()|0.7771428571428571|
|RandomForestClassifier()|0.7771428571428571|
|AdaBoostClassifier()|0.8057142857142857|
|SVC()|0.7485714285714286|

---
## Conclusions and Recommendations
That said, our data does indicate that much of the ability for colleges to avoid widespread infection, depends on the State's policies and actions to limit the spread of Coronavirus.
