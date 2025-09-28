# Kaggle - Puffy Lost Sleep Challenge

This repository consists of different models that were used to predict the order refunds based on the historical order data, customer events on the e-commerce website like click, changes in the cart, checkout clicks, number of edits, etc.
About 20+ features were engineered out of this dataset, for example- order hour, avg price per item, time from first event, time from last event, num product added to cart, num products removed from cart etc.

The Kaggle challenge link is here - https://www.kaggle.com/competitions/the-puffy-lost-sleepchallenge/leaderboard?tab=public

### Steps
1. EDA
2. A diverse set of features was engineered using both the order-level and event-level datasets.
- Behavioral Features
    - has_checkout_completed, has_checkout_started, has_add_to_cart: Indicate different levels of purchase intent.
    - num_events_total, num_clicks, num_page_views, num_add_to_cart: Quantify overall engagement on the platform.

- Temporal Features
    - order_month, order_hour, is_weekend: Capture shopping behavior patterns across time (e.g., late-night impulse purchases, weekend activity).

- Derived Metrics
    - avg_price_per_item, total_items, time_from_first_event, time_from_last_event: Provide insight into purchasing patterns and timing.

 3. Logistic Regression

    The final dataset of features was scaled using Standard Scaler and a LR model was developed with max_iter=1000, class_weight='balanced'.
    With the threshold tuning, the final results from Logistic regression were -

    With recall = 94% we are prediciting most refunded orders but with precision 32% we have a lot of misclassifications as refunded. This will predict orders that are not refunded as also refunded.

5. LightGBM

   Next a LigtGBM model was developed and tuned using cross validation to further improve predictions. LightGBM Captures complex non-linear relationships, Handles large feature sets and sparsity, and has Better precision–recall tradeoff.
   To determine the optimal classification threshold for converting predicted probabilities into binary refund predictions, I used F1-score maximization based on the validation set. This is especially important in imbalanced classification settings where the default threshold of 0.5 may not be optimal.

   I selected the threshold that maximizes the harmonic mean of precision and recall (F1-score). Final threshold - 0.91

   Finally, Proportion of predicted refunded (1): 0.04918032786885246 ~ 4.9% refunds
            Proportion of predicted non-refunded (0): 0.9508196721311475 ~ 95.08% non-refunds
   
    
    
