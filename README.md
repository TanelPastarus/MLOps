# MLOps

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

**a) How can you ensure the improvement is not due to randomness or data leakage?**
To rule out randomness, the model should be evaluated using cross-validation. If the improvement holds consistently across all folds, it is unlikely to be a random improvement.
To rule out data leakage, it is important to check whether the newly added feature is computed from other features already in the model.
In this dataset `passenger_count` is independent, which means it is not derived from the original 3 features.

**b) What risks exist if this feature cannot be reliably generated in production?**
If `passenger_count` is not available at prediction time, for example, because the trip has not yet ended,
the model will either fail entirely or require a fallback.