Predicting Song Popularity Using Spotify Dataframe Metrics

Overview

Everyone knows a popular song—whether it's your favorite that you can't stop listening to or a tune that you can't escape no matter where you go. But have you ever wondered what makes a song so popular? In this project, we explore specific metrics from Spotify's API dataframe to uncover what drives the popularity of the songs you love.

Our Database

We start with two dataframes sourced from Kaggle. After loading both datasets, we notice they contain the same columns, so we concatenate them. To ensure data quality, we check for duplicate track IDs and drop any duplicates from the combined dataframe. Additionally, we remove unnecessary object types (like naming info), leaving us with a clean dataset ready for modeling.

Initial Model

For our first modeling attempt, we utilize a Random Forest Regressor. This choice is informed by its ability to handle larger sample sizes (our dataset contains approximately 130,000 rows) and its effectiveness in addressing multicollinearity, which we anticipate may be an issue.

We run the model with default parameters and calculate several performance metrics, but the initial results are disappointing, yielding an R-squared score of just 0.16.


Addressing Data Imbalance

Noticing a skewed sample size—where the majority of our target variable values fall on the lower end—we recognize that the dataset would benefit from a more balanced representation of popular songs. To achieve this, we apply the RandomUnderSampler to artificially create a more even distribution.

After re-running the Random Forest model with the balanced dataset, we achieve a significant improvement, raising the R-squared score to 0.45.


Hyperparameter Tuning

To further enhance our model's performance, we incorporate hyperparameter tuning using GridSearchCV. We define a parameter grid and execute a grid search, obtaining the best hyperparameter values for our Random Forest model.

After applying these optimized parameters to the RandomUnderSampled dataset, we see another boost in performance, with the R-squared score climbing to approximately 0.49.


Cross-Validation and Pipeline Creation

To evaluate the consistency of our model, we conduct cross-validation, which reveals variable scores across the folds, indicating some instability in our model's predictions.

We then create a robust pipeline that integrates several features: first, the RandomUnderSampler for balancing the dataset, followed by StandardScaler for scaling features, and finally the RandomForestRegressor. We expand our parameter grid to include more values for searching, given the smaller scale of the data.

After running cross-validation with the new pipeline setup, we perform feature selection once more. However, we create another similar model using the pipeline parameters, only to find a decline in performance compared to previous results.


Final Attempts and Conclusion

In an effort to improve our score, I attempted another model using the highest-performing parameters but removed the three lowest-performing features. This adjustment resulted in a marginal decline in performance, with no significant improvement observed.

Despite exploring various models, most yielded exceptionally poor scores, leading to their exclusion from further consideration.


Conclusion

In conclusion, while I believe that with more time, knowledge, and resources, a stronger predictive score could be attainable, the complexity of "song popularity" poses significant challenges. Conclusively proving the factors influencing song popularity may be elusive, especially with the models we employed. However, I have read that more advanced neural networks could better address multicollinearity issues, which might be an interesting direction for future exploration.
