# MLOps

### 3-Feature Linear Regression Model

A Linear Regression model was trained to predict the total trip cost (`total_amount`) for NYC taxi trips, using three features: `trip_distance`, `fare_amount`, and `RatecodeID` (one-hot encoded).
The data was split 80/20 for training and testing.

The model achieved a strong R² score, meaning it explains most of the variance in total trip cost. `fare_amount` is by far the strongest predictor - it directly makes up most of the total amount. 
`trip_distance` adds a smaller independent signal, and the one-hot encoded `RatecodeID` dummies capture flat-rate and negotiated fare types that behave differently from the standard rate.


### 4-Feature Linear Regression Model

A fourth feature, `tip_amount`, was added to the original three (`trip_distance`, `fare_amount`, `RatecodeID`).
A clear improvement in model performance was observed across all three evaluation metrics.