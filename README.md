# Store Sales Forecasting 

![enter image description here](https://github.com/amar-chakka/ISB_Sales_Forecasting/blob/b228d3f906ca50046363a655c731df7e5cdeae5b/SalesForecasting.png?raw=true)


### The HR department has hired me as data science consultants. They want to supplement their exit interviews with a more proactive approach.

Estimating and predicting sales is an important and key challenge in retail analytics. Analysis in this area is plagued by issues related to sparseness of the sales data and multiple SKUs and categories.

**The objective of this project is to:**

-   Predict weekly store sales for each product in a given store (80% weightage)
-   Identify categories and stores that move together (20% weightage)

This will help the planning and merchandizing team for buying and placement of product in store to maximize sales and reduce lost sales opportunities.

The Business Intelligence Analysts of the Company provided  three datasets that contain information about store_cities, Sales, Product Hierarchy.

## Product_hierachy

**Observations on product hierarchy dataset:**

-   No. of Variables: 10    
-   Numeric values: 3    
-   Categorical values: 7    
-   No. of entries: 699    
-   50 fields in cluster_id have null values which we will fill with a new cluster as 'cluster_11'.    
-   product_length, product_depth and product_width have null values. Since this are redundant fields for the purpose of forecasting, we will drop this fields.    
-   We will also drop hierachy id columns except for hierarchy1_id. This is kept in view of identifying product bundling opportunities

# stores_cities data
**Observations in store_cities dataset:**
-   No. of entries: 144    
-   Numeric variables: 1    
-   Categorical variable: 3    
-   Null values: Nil    
-   No null values in the dataframe    
-   dtypes respectively are found to be correct    
-   No action required.

# Sales
**Observations in Sales dataset:**
-   No. of entries:19454838    
-   No. of Variables: 13    
-   Numeric values:5    
-   Categorical values:8    
-   Null values found in sales, revenue, stock, price and promo_discount_2 which we will be filling through cross referencing.    
-   We will drop promo_bin_1, promo_bin_2, promo_type_1, promo_type_2 and promo_discount_type_2 categorical fields as these are irrelevant for the purpose of forecasting model

## Target variable

### sales – Daily product sales.

## EDA 

1.  We can infer that STO1 are bigger format stores followed by ST02, ST03 and ST04 respectively. Though there could be few exceptions.
2.  It can be inferred that ST01 are in metro cities followed by ST02, ST03 and ST04 in T-1, T-2 and T-3 cities respectively.
3.   Date dtype is object that needs to be converted to datetime
4.  Missing values in sales, revenue, stock, price and promo_discount_type2 which we identified can be imputed through cross referencing
5.  Fields like promo_bin_1, promo_bin_2 and promo_discount_2 were having maximum null values and were found to be unwanted columns. We have decided to drop the same.

Top stores in terms of revenue
![enter image description here](https://github.com/amar-chakka/ISB_Sales_Forecasting/blob/9d5bb7fcdbb9fde510ffc09b5af761951f6a4cd4/TopStores_Revenue.png?raw=true)


Top stores by volume of sales
![enter image description here](https://github.com/amar-chakka/ISB_Sales_Forecasting/blob/0f5b773019052fe9bf7a7dee8436d6578a2e62e5/TopStores_Volume.png?raw=true)

**Observations:**

1.  We found that 80:20 rule applies to this retail business.
2.  Top 20% of the products are generating 80% revenue for the business.
3.  135 out of 649 products are generating 80% revenue.
4.  The business should focus in maximizing sales from this top 135-140 products.
5.  Product bundling strategies of the slow moving products should be around this fast moving products.
6.  Cross selling opportunities within the same category of the slow moving products and Fast moving products should be looked into.
7.  The Data set provided doesn't contain invoice level transaction information. This will be required for proper BASKET ANALYSIS and subsequent bundling opportunities across related and unrelated categories of products.
Using scikit-learn's train_test_split function to split the dataset into train and test sets. 80% of the data will be in the train set and 20% in the test set, as specified by test_size=0.2
Tried with different classifiers with all one hot encoded columns & selective features  over sampled data.

Final Model is XGBoostRegressor

### Actionable Insights 
1.  Bundle products within the same cluster id and hierarchy1 id level for cross selling opportunities.
2.  Within the same cluster level, we should look at add-on selling opportunities. A fast moving product within a cluster need to be bundled with a slow moving product to improve Basket size and Ticket size.
3.  The client need to provide invoice level daily sales data for proper consumer BASKET ANALYSIS. It will give clear picture of products and the store that move together.
4.  Invoice level daily sales data will help to design store specific promotions, bundling opportunities.
5.  The sell-thru of the products is very very low at 2.75% cumulative. We can infer safely that complete data set of all the products is not provided to us for evaluation and only products with poor sell-thru is being provided. If this is not true, then we can say that the retail business is not performing at the current stage and need serious revival. Otherwise it will be prudent to close the stores and wind up the business.
6.  From the sell-thru analysis we found most items overstocked and are slow moving vis a vis the stock levels. This gives an opportunity to reduce the stocking plan of the 699 products and free up shelves and warehouse to introduce newer products or to allocate space to categories which are growing and doing better.
7.  The current stocks need to be liquidated with better discounting. This will free up space and capital.
8.  From the SPF (Sell per Sq.Ft) analysis, though not conclusive as unit of store size is missing, we can still infer that the business is loss making given it sell only the given products (condition).
9.  More data points like footfall, selling area, invoice, product price, margins, opex, organization structure etc. required to arrive at performance matrices like conversions, basket size, Ticket size, realization, profit, GMROI etc. to take strategic decisions like store restructuring in terms of format, size, products, promotions, stocking plan, cost,  etc.



To check out my notebook, please click [here](https://github.com/amar-chakka/ISB_Sales_Forecasting/blob/0f5b773019052fe9bf7a7dee8436d6578a2e62e5/Testing%20Utility.ipynb).
