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
We want to <b>minimize the possibility of late shipment </b> so that the late shipment rate could drop to at least 20%.

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
For the modeling we compare the performance between 3 algorithms: Logistic Regression, Random Forest, XGBoost. The modelings are done using the preprocessed dataset and using hyperparameter tuning.<br>
Models are evaluated using AUC score and Recall. The models performances are shown below.<br>

| Model | AUC Score | Recall |
| --- | --- | --- |
| **Logistic Regression** | **71%** | **75%** |
| **Random Forest** | **74%** |  **67%** |
| **XGBoost** | **73%** | **70%** |

From the performances above, we recommend <b>XGBoost </b>for the machine learning algorithm for shipping prediction model.

## Potential Impact
For the potential impact, here the scenario that we created:<br>
* The model is implemented for the internal environment of the company
* Every products arrival are predicted before they are shipped
* Assume that with the prediction result, the company already knows which products are expected to be late. Therefore, they should be able to make countermeasure for those products and hopefully, they will arrive on time instead.

Now if we take a look at the confusion matrix<br>
![alt text](https://github.com/ramafhgit/E-Commerce-Shipping-Prediction/blob/main/conf.png "conf matrix")<br>

If we assume that all the products that are predicted to be late can be handled by the company so that they won't, then the only products that <b>will</b> be late is the one in the false negative domain. These products are predicted to arrive on time, so there is no way the company would know that they would be late.<br>

Which means, if our assumptions are correct, then the <b> late shipment rate</b> would only be around <b>17.9%</b>.

| Metrics | Before | After |
| --- | --- | --- |
| **Late Shipment Rate** | **59.6%** | **17.9%** |
| **Potential Loss** | **$412,772** |  **$123,806** |


Notes:<br>
* Potential loss are calculated by assuming that the customer whose products arrived late would churn.
* Customer value are calculated by averaging total cost of products per unique customer.
* The 'After' potential loss are calculated by multiplying the customer value to 17.9% of the original dataset size.
* Our initial goal of minimizing the late shipment rate to 20% <b>is fulfilled</b>
* All these potential impacts are based on the assumption that all the products that are predicted to arrive late could be anticipated so that they arrive on time instead.

## Business Recommendation
* <b>Implement the machine learning model to internal environment of the company</b>, so that the company can make a countermeasure toward the products that are expected to be late.
* <b>Keep the customer up to date</b>, so that they know whether their products will arrive on time.
* <b>Keep an eye on the sale days</b>, since it might be causing the late shipment based regarding the discount. Possible solution:<b> Hire temporary workers, collaborate with 3rd party shipping companies to increase the shipping fleet, etc.</b>
* <b>Create a hierarchical shipment system </b> according to product importance so that the products with higher importance receive special treatments.

# Our Team
This project is part of a learning path for Data Science Bootcamp in [Rakamin_Academy](https://rakamin.com/), and is done by our team : <i>Smells Like Team Spirit</i>.<br>
<br>
**Members**<br>
| Member | Email | LinkedIn |
| --- | --- | --- |
| **Our Mentor: Gerry Chandra** | - | https://www.linkedin.com/in/gerrychandra |
| **Rama Hakiim (me)** | ramafhakiim@gmail.com | https://www.linkedin.com/in/ramafhakiim |
| **Fajri Ardiansyah** | ardiansyahfajri@gmail.com | - |
| **Alya Atiqoh** | alyaaatiqoh123@gmail.com | - |
| **Teguh Tri Handoyo** | teguhtrihandoyo1@gmail.com | www.linkedin.com/in/teguh-tri-handoyo-51437312b/ |
| **Saniyyah Larissa** | SaniyyahLarissa@gmail.com | www.linkedin.com/in/saniyyah-larissa-3943271b4/ |
