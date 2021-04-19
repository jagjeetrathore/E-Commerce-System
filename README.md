## Objectives
 **Primary objective** is to segment customers based on their RFM (Recency, Frequency, Monetary value) metrics . RFM is a marketing analysis tool used to identify a firm's best clients, based on the nature of their spending habits.
 **Secondary  objective** is to build a machine learning model to predict the customer Lifetime Value (LTV), a metric that indicates the total revenue a business can reasonably expect from a single customer account. LTV is often considered the “Golden Metric” for online retailers, as it helps predict future revenue and measures long-term business success. I find that there is a positive correlation between RFM score and LTV.
## Data Preparation
The chosen dataset is a transactional data set from an online e-commerce system obtained from UCI’s machine learning repository [1]. It was of excellent quality with only a few challenges to overcome. As this is Point of Sale (POS) data, it required additional thought for manipulation and normalization of the dataset. Some identifiers or behaviors were difficult to interpret as we have zero knowledge of the POS system, eg. stock codes, or behaviours of cancellations, refunds, discounts, etc.
## Data Preprocessing
I wanted to avoid removing any records that would be considered a net positive profit or income. Beyond the scope of standard normalization or data-cleaning process, such as renaming columns or converting to correct types, removal of NaN’s or nulls etc. I discovered some discrepancies. 
I opted to only capture totals or Invoice totals (cart price) greater than 0. This removed any remaining discounts or negative values that did not represent bought products or customer behavior. Finally the cleaned data contains only model-contributing records
## Customer Segmenation based on Recency, Frequency and Revenue by K-means
#### k = 4 as suggested by Elbow and Silhouetee Methods 

![FrequencyCluster](https://github.com/jagjeetrathore/E-Commerce-System/blob/master/images/Frequency_Cluster.png)
![RecencyCluster](https://github.com/jagjeetrathore/E-Commerce-System/blob/master/images/Recency_Cluster.png)
![RevenueCluster](https://github.com/jagjeetrathore/E-Commerce-System/blob/master/images/Revenue_Cluster.png)
### Machine Learning Model for LTV Prediction 
Prediction of Life Time Value
* Define a time frame for customers' lifetime value calculation. This depends upon business goals, for this I choose 6 months.
* Lifetime Value calculation: Calculate 6 month LTV for each customer which I will use for training the model. 
![Correlation between RFM and LTV](https://github.com/jagjeetrathore/E-Commerce-System/blob/master/images/RFM_LTV.png)
#### Model Evaluation: 
**Comparision of  Classifiers with and without Hyperparamter tunning**
![Classifiers_Comparison](https://github.com/jagjeetrathore/E-Commerce-System/blob/master/images/model_comparison.png)
![ROC_Curve_Analysis](https://github.com/jagjeetrathore/E-Commerce-System/blob/master/images/ROC_Curve_Analysis.png)
### Conclusion:
we invest in customers (like discounts and promotions) to generate revenue.These actions make some customers more valuable in terms of lifetime value but there are some customers who pull down this profitability. So we need to segment customers and act accordingly. I also predicted each segment with a 0.84 F1 score using the Extra Trees Classifier. This prediction model may be used to classify new customers to receive the appropriate marketing offers. 

Through analysis and model building we discovered that ~40% of the customers within this dataset had only one transaction. These may be consumers performing a guest checkout. (or First time buyers) These customers are important to identify and target for customer retention strategies, requiring further investigation and business intelligence.

The dataset was limited to only 13 months of transactional data, however,I prefer it to be a larger time frame as this may have shed light on undiscovered areas for analysis such as seasonality, annually or bi-annual analysis, or customer loyalty. Insights into how the e-commerce system handles the data manipulation of transactions such as bonuses, coupons, discounts, cancellations and refunds would be helpful in creating a cleaner data file.
There were also significant challenges encountered while cleaning the data as we often found transactions with non-zero quantity and a unit price of zero, or product descriptions with value ‘Manual’ etc.
