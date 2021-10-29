# E-Commerce-Shipping-Prediction : Overview
* Shipment punctuality prediction. Dataset acquired from  [E-Commerce Shipping Data | Kaggle](https://www.kaggle.com/prachi13/customer-analytics)
* Use Log Transform to transform features with outliers
* No Sampling on target column (pretty balanced)
* Trained model with 3 different algorithms
* Use Hyperparameter tuning on each algorithm
* etc

## Problem
Anterin Dong is an Indonesian e-commerce company that has its own shipment service. There are 3 shipment mode available: Flight, Ship, and Road. The company's motto is "Your order is our happiness, and your happiness is our pride”. <br>
Now as things stand, Anterin Dong has a 59.6% late shipment rate which means the majority of the shipment is arriving late. This is obviously a problem.

## Goals
We want to <b>minimize the possibility of late shipment </b> so that the late shipment rate could drop at least by 20%.

## Objective
Create a model to predict the shipment arrival; so that the company knows which products is going to arrive late.

## Insights
1. Target column distribution is imbalanced, but still acceptable.<br>
![alt text](https://github.com/ramafhgit/E-Commerce-Shipping-Prediction/blob/main/target.png "target")<br>
0 = On time; 1 = Late. As we can see the target distribution is slightly imbalanced, with 1 or Late being the majority.

2. Some interesting correlation from the 'Discount_offered' column and 'Product_weight' towards the target column.<br>
![alt text](https://github.com/ramafhgit/E-Commerce-Shipping-Prediction/blob/main/disc.png "discount")<br>
![alt text](https://github.com/ramafhgit/E-Commerce-Shipping-Prediction/blob/main/weight.png "weight")<br>
![alt text](https://github.com/ramafhgit/E-Commerce-Shipping-Prediction/blob/main/multi.png "multi")<br>
We can see from the first graph that the higher the discount, the shipment is always late.<br>
From the second graph however, the heavier the product, the shipment tend to be on time. <br>
From the third graph we can look at them more clearly:

* Products that arrived on time has the discount value in range of 0%-10%. Other than that, the shipments are always late.
* The weights of the products that arrived on time are in range of 1-2 kg or 4-6 kg. Other than those, the shipments are late.
Now this begs us the question:<br>
a. Why would product weight matter in a shipment punctuality?<br>
b. Is there a different handling in products with a higher discount and the ones that have lower discount?<br>
c. Was there any specific events related to the discounts? For example: sale day, black friday, etc so that the demand actually became out of hand hence the late shipment?<br>

3. Product Importance. <br>
![alt text](https://github.com/ramafhgit/E-Commerce-Shipping-Prediction/blob/main/prod%20imp.png "prod imp")<br>
As we can see, there are 3 product importance category : low, medium, and high. <br>
But then it's curious how all of them has a similar late shipment rate. Products with higher product importance should be prioritized; meaning their late shipment rate has to be lower to the other category -- if possible close to zero.<br>
This shows that the management regarding the product importance is not as good as it should be.

## Modeling
For the modeling we compare the performance between 3 algorithms: Logistic Regression, Random Forest, XGBoost.
