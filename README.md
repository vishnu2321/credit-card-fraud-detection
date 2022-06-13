# Credit-Card-Fraud-Detection

Used modules -> Pyspark, sklearn, pyspark ml library \
Language -> **Python** \
The data is taken from Kaggle, Dataset URL -> "https://www.kaggle.com/datasets/dhanushnarayananr/credit-card-fraud" \
Format of data -> CSV

The dataset contains 10,00,000 records with 7 attribute columns and 1 label column.

#### Columns

    - distance_from_home 
    - distance_from_last_transaction 
    - ratio_to_median_purchase_price 
    - repeat_retailer 
    - used_chip 
    - used_pin_number 
    - online_order 
    - fraud(label)
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Data Preprocessing

The data from kaggle is loaded into spark dataframe. \
The dataframe is repartitioned into 4 partitions for parallel processiong of smaller chucks of dataframe on multiple executors.
The data is imbalanced. (Fradulent count - 87403, Non-fradulent count - 912597) 

The dataframe is balanced using dataframe sample method which takes attributes as follows - with replacement of record (True/False), percentage of records for sample(%), seed(Random Integer) \
The dataframe columns are casted to float type for evaluation. 

The corelation coefficients of all columns are calculated and the values of columns greater than 0.8 and less than -0.8 are dropped. \
The dataframe is split for training and testing. \
The values are aggregated to form one new column using assembler feature from pyspark ml lib.

The numerical columns contain values of different ranges so to optimize they are scaled using **MinMaxScaler**.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Training the Model

The dataframe is trained and model is built using **Linear SVC**.

The model is later tested.

#### Accuracy

The accuracy is **0.8928114393812941**. \
The confusion matrix is calculated for True Positive Rate(TPR) and True Negative Rate(TNR).

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
