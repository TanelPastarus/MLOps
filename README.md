# MLOps

The 3 (original) and 4 (added feature) feature models are on their respective branches (`classification_model` and `regression_model`).
Their performance output explanations and their model codes are in the README.md file on their respective branches.

The main branch contains only loading in the datafile, requirements.txt and cleaning the data, which is common for both models.

### 3-Feature Linear Regression Model

A Linear Regression model was trained to predict the total trip cost (`total_amount`) for NYC taxi trips, using three features: `trip_distance`, `fare_amount`, and `RatecodeID` (one-hot encoded).
The data was split 80/20 for training and testing.

The model achieved a strong R² score, meaning it explains most of the variance in total trip cost. `fare_amount` is by far the strongest predictor - it directly makes up most of the total amount. 
`trip_distance` adds a smaller independent signal, and the one-hot encoded `RatecodeID` dummies capture flat-rate and negotiated fare types that behave differently from the standard rate.

### 4-Feature Linear Regression Model

A fourth feature, `tip_amount`, was added to the original three (`trip_distance`, `fare_amount`, `RatecodeID`).
A clear improvement in model performance was observed across all three evaluation metrics.

### 3-Feature Logistic Regression Classification Model

A Logistic Regression model was trained to classify NYC taxi trips as either Credit Card or Cash payments, using three features: `trip_distance`, `fare_amount`, and `tip_amount`. 
The data was split 80/20 for training and testing, with features normalised using `StandardScaler`.

The model achieved 92% overall accuracy. Credit card prediction is near-perfect (F1: 0.95) because `tip_amount` is a very strong signal. 
Credit card trips almost always include a tip, cash trips almost never do. 
Cash prediction is slightly weaker (F1: 0.82) mainly due to class imbalance (there are more credit card trips).

The main reason for the gap in performance between the two classes is class imbalance. 
Adding more features or applying techniques like oversampling could help close this gap.

### 4-Feature Logistic Regression Classification Model

A fourth feature, `passenger_count`, was added to the original three (`trip_distance`, `fare_amount`, `tip_amount`).
A small improvement in overall accuracy was observed, increasing from 92% to 93%.

### _5. Add one more feature to initial selected features and then explain the following (question that is same for both branches)_

**a) How can you ensure the improvement is not due to randomness or data leakage?**
To rule out randomness, the model should be evaluated using cross-validation. If the improvement holds consistently across all folds, it is unlikely to be a random improvement.
To rule out data leakage, it is important to check whether the newly added feature is computed from other features already in the model.
For example in this dataset `passenger_count` (which is used for training the classification model) is independent, which means it is not derived from the other 3 features.

**b) What risks exist if this feature cannot be reliably generated in production?**
If the feature is not available at prediction time, for example, because the trip has not yet ended,
the model will either fail entirely or require a fallback.
