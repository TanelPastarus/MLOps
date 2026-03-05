# MLOps

The 3 (original) and 4 (added feature) feature models are on their respective branches (`classification_model` and `regression_model`).
Their performance output explanations are in the README.md file on their respective branches.
The model code is in the `practice1.ipynb` file, regression branch has the regression model code and classification branch has the classification model code.

The main branch contains only loading in the datafile, requirements.txt and cleaning the data, which is common for both models.

### _5. Add one more feature to initial selected features and then explain the following (question that is same for both branches)_

**a) How can you ensure the improvement is not due to randomness or data leakage?**
To rule out randomness, the model should be evaluated using cross-validation. If the improvement holds consistently across all folds, it is unlikely to be a random improvement.
To rule out data leakage, it is important to check whether the newly added feature is computed from other features already in the model.
For example in this dataset `passenger_count` (which is used for training the classification model) is independent, which means it is not derived from the other 3 features.

**b) What risks exist if this feature cannot be reliably generated in production?**
If the feature is not available at prediction time, for example, because the trip has not yet ended,
the model will either fail entirely or require a fallback.