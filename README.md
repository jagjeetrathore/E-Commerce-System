## Objectives
 **Primary objective** is to segment customers based on their RFM (Recency, Frequency, Monetary value) metrics . RFM is a marketing analysis tool used to identify a firm's best clients, based on the nature of their spending habits.
 **Secondary  objective** is to build a machine learning model to predict the customer Lifetime Value (LTV), a metric that indicates the total revenue a business can reasonably expect from a single customer account. LTV is often considered the “Golden Metric” for online retailers, as it helps predict future revenue and measures long-term business success. We hypothesize that there is a positive correlation between RFM score and LTV.

## Data Preparation
The chosen dataset is a transactional data set from an online e-commerce system obtained from UCI’s machine learning repository [1]. It was of excellent quality with only a few challenges to overcome. As this is Point of Sale (POS) data, it required additional thought for manipulation and normalization of the dataset. Some identifiers or behaviors were difficult to interpret as we have zero knowledge of the POS system, eg. stock codes, or behaviours of cancellations, refunds, discounts, etc.
## Data Preprocessing
We wanted to avoid removing any records that would be considered a net positive profit or income. Beyond the scope of standard normalization or data-cleaning process, such as renaming columns or converting to correct types, removal of NaN’s or nulls etc. we discovered some discrepancies. 
First we examined any duplicate records to remove and we found approximately 5225. Next, we discovered records with negative quantities. After inspection, we concluded many of these to be cancellations. Out of 22,190 records, we could clearly identify 3,654 as cancelled. 
Prior to the removal of these records, we had to also identify and flag other cancelled records by incorporating additional logic. These records did not have the original InvoiceNo. approximately 5192 records were identified and dropped by finding records with negative quantities and matching them against their mirror records where the InvoiceNo’s were not the same (equivalence of absolute value of quantities).
After removing mismatched cancelled orders, the remaining cancelled orders and their originals we opted to only capture totals or Invoice totals (cart price) greater than 0. This removed any remaining discounts or negative values that did not represent bought products or customer behavior. Finally the cleaned data contains only model-contributing records

## Customer Segmenation based on Recency, Frequency and Revenue by K-means

#### k = 4 as suggested by Elbow and Silhouetee Methods 

![FrequencyCluster](https://github.com/jagjeetrathore/E-Commerce-System/blob/master/images/Frequency_Cluster.png)
![RecencyCluster](https://github.com/jagjeetrathore/E-Commerce-System/blob/master/images/Recency_Cluster.png)
![RevenueCluster](https://github.com/jagjeetrathore/E-Commerce-System/blob/master/images/Revenue_Cluster.png)
### Machine Learning Model for LTV Prediction 
Prediction of Life Time Value
* Define a time frame for customers' lifetime value calculation. This depends upon business goals, for this we choose 6 months.
* Define the predictors that we will use to predict Future and create them.     	
* Calculate LTV for ML Model, use RFM scores as predictors for each customerID, utilize 3 months of data for calculating RFM, to predict next 6 months.
* Lifetime Value calculation: Calculate 6 month LTV for each customer which we will use for training our model. The revenue will become our LTV. Now we need to merge the 2 dataframe to see correlation with LTV and our predictors.
#### Model Evaluation: Comparision of  Classifiers with and without Hyperparamter tunning
![Classifiers_Comparison](https://github.com/jagjeetrathore/E-Commerce-System/blob/master/images/model_comparison.png)
![ROC_Curve_Analysis](https://github.com/jagjeetrathore/E-Commerce-System/blob/master/images/ROC_Curve_Analysis.png)
### Conclusion:
LTV segments describe specific customer purchasing patterns and behaviour which is very useful for differentiated target marketing. We also predicted each segment with a 0.84 F1 score using the Extra Trees Classifier. This prediction model may be used to classify new customers to receive the appropriate marketing offers. 

Through analysis and model building we discovered that ~40% of the customers within this dataset had only one transaction. These may be consumers performing a guest checkout. (or First time buyers) These customers are important to identify and target for customer retention strategies, requiring further investigation and business intelligence.

The dataset was limited to only 13 months of transactional data, however, we prefer it to be a larger time frame as this may have shed light on undiscovered areas for analysis such as seasonality, annually or bi-annual analysis, or customer loyalty. Insights into how the e-commerce system handles the data manipulation of transactions such as bonuses, coupons, discounts, cancellations and refunds would be helpful in creating a cleaner data file.
There were also significant challenges encountered while cleaning the data as we often found transactions with non-zero quantity and a unit price of zero, or product descriptions with value ‘Manual’ etc.




