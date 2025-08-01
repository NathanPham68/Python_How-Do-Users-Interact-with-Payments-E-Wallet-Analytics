# 📊 [Python] How Do Users Interact with Payments? | E-Wallet Analytics

<img width="745" height="498" alt="image" src="https://github.com/user-attachments/assets/df5f5775-3425-467c-b17a-f8c5b24aa884" />

## 📑 Table of Contents

1. [📖 Overview](#overview)

2. [📚 Import libraries & data](#import-libraries-&-data)

3. [🧪 Part I: Exploratory Data Analysis (EDA)](#part-i:-exploratory-data-analysis-(eda))

4. [🧹 Part II: Data Wrangling & Analysis](#part-ii:-data-wrangling-&-analysis)

5. [🤝 Contributing](#Contributing)

## 📖 **Overview**

This project simulates the responsibilities of a Data Analyst (DA) working at an e-wallet company. The objective is to analyze and understand the current state of payments and transactions in the context of an e-wallet ecosystem using real-world-like datasets.

### 🔍 **Goal**

To uncover insights about payment behaviors and transaction patterns that can inform business decisions, identify anomalies, and highlight performance trends across products and teams.

### 👤 **Who is this project for?**

- Data analysts & business analysts

- Decision-makers & stakeholders in the fintech industry

- Product teams optimizing e-wallet services

### 📁 **Datasets**

[**Link to Datasets**](https://drive.google.com/drive/folders/1Mv9Mk9DgKKVlJX_aVvYDTZnck3cHIJuV?usp=sharing)

The project uses the following CSV files:

<details>
  <summary><strong>Table 1: Products</strong></summary>

* product.csv (493 rows × 3 columns) – Product details including product ID, team ownership, category, etc.

| Column Name  | Data Type | Description |
|-------------|----------|-------------|
| product_id  | INT      | Unique identifier for each product |
| category    | TEXT     | Product category |
| team_own    | TEXT     | Team responsible for the product |

</details>

<details>
  <summary><strong>Table 2: Payment Report</strong></summary>

* payment_report.csv (920 rows × 5 columns) – Monthly payment volumes for various products.

| Column Name    | Data Type | Description |
|---------------|----------|-------------|
| report_month  | DATE     | Month of the payment report |
| payment_group | TEXT     | Type of payment (e.g., refund, purchase) |
| product_id    | INT      | Associated product ID |
| source_id     | INT      | Source of the transaction |
| volume        | FLOAT    | Total payment volume |

</details>

<details>
  <summary><strong>Table 3: Transactions</strong></summary>

* transactions.csv (1,324,002 rows × 9 columns) – Transaction-level data, including transaction types and merchant information.

| Column Name    | Data Type | Description |
|---------------|----------|-------------|
| transaction_id | INT      | Unique transaction identifier |
| merchant_id    | INT      | Merchant involved in the transaction |
| volume         | FLOAT    | Transaction amount |
| transType      | INT      | Type of transaction |
| transStatus    | TEXT     | Status of the transaction (e.g., completed, failed) |
| sender_id      | INT      | Sender of the transaction |
| receiver_id    | INT      | Receiver of the transaction |
| extra_info     | TEXT     | Additional details about the transaction |
| timeStamp      | TIMESTAMP | Time when the transaction occurred |

</details>

### 🧠 **Problem-Solving Mindset (Step-by-Step Guide)**

Each exercise follows a logical approach that you can use when solving any Python problem:

1. Read & Understand the Problem
→ Identify the goal, keywords, and the expected input/output

2. Clarify Input and Output
→ Know the required data type and format clearly

3. Sketch a Quick Plan
→ Outline your solution idea briefly

4. Link Back to What You've Learned
→ Map your plan to Python knowledge: loops, conditions, etc.

5. Break Down the Problem
→ Think in smaller steps:

    - Looping through data

    - Checking conditions

    - Updating variables or collections

6. Write a Function Skeleton
→ Example: def function_name(params): ...

7. Implement Step-by-Step Logic
→ Code exactly what you planned using loop → condition → update flow

8. Test with Sample Inputs
→ Compare actual output with the expected one

9. Refactor if Needed
→ Improve readability, fix bugs, or optimize performance

### 🛠️ **Tools Used**

- Python

- Pandas for data analysis

- Matplotlib / Seaborn (optional for visualization)

- Google Colab

## 📚 **Import libraries & data**

```ruby
!pip install pandas==2.1.4 ydata-profiling==4.6.4
```

```ruby
import numpy as np
import pandas as pd
import os
import warnings
import seaborn as sns
import matplotlib.pyplot as plt

warnings.filterwarnings('ignore')
```

```ruby
path = '/content/drive/MyDrive/DAC 1 on 1 /Python/Project_2_payment_report/Dataset'

payment_report = pd.read_csv(path+"/payment_report.csv", encoding = 'utf-8')
product = pd.read_csv(path+"/product.csv", encoding = 'utf-8')
transactions = pd.read_csv(path+"/transactions.csv", encoding = 'utf-8')
```

<img width="1283" height="561" alt="image" src="https://github.com/user-attachments/assets/51c5227d-5e7c-47e4-9f2d-126f0a32c841" />

<img width="1283" height="572" alt="image" src="https://github.com/user-attachments/assets/c2394f28-c813-4c1a-a8ab-f4ef079ab70e" />

<img width="1283" height="585" alt="image" src="https://github.com/user-attachments/assets/9a93cb13-1503-4fcd-910d-3c4641a1e0b0" />

## 🧪 Part I: Exploratory Data Analysis (EDA)

Tasks:

1. Inspect data quality:

    - Check for missing values, duplicate rows, and incorrect data types.

    - Evaluate numerical columns for anomalies (e.g., negative payment volume).

2. Data Preparation:

    - Create a new DataFrame payment_enriched by merging payment_report.csv with product.csv.

3. Initial Data Observations:

Identify columns with potential issues:

- Missing data: How many rows affected? Which columns?

- Incorrect data types: Should a column be numeric instead of string?

- Duplicates: Are there repeated rows or duplicate primary keys?

- Invalid values: E.g., volume = 0 for an active product.

### ✔️ EDA payment_report.csv & product.csv

<img width="1283" height="647" alt="image" src="https://github.com/user-attachments/assets/757b5c19-3613-4660-8024-cbbe46cbf40a" />

<img width="1283" height="331" alt="image" src="https://github.com/user-attachments/assets/5103c43a-bf37-4ee5-8384-94fec50517b3" />

<img width="1283" height="662" alt="image" src="https://github.com/user-attachments/assets/536df279-c25c-4580-8d13-da698fbe432e" />

<img width="1283" height="684" alt="image" src="https://github.com/user-attachments/assets/9d249c72-714c-48fb-bfd2-012bca9382cf" />

```ruby
from ydata_profiling import ProfileReport

p_report = ProfileReport(payment_report_enriched, title="Payment Report", explorative=True)
p_report.to_notebook_iframe()
```

[**Link to code**](https://colab.research.google.com/drive/1dmWHuvxJYoPvjKu-u157WK0bBxq1Hol7?usp=sharing)

<img width="1283" height="637" alt="image" src="https://github.com/user-attachments/assets/f4c960f9-7e11-4a09-90c2-dd307a8c32f4" />

- Missing data: 2% (22 rows) of `category, team_own` because some Product IDs in `payment_report` df don't exist in `product` df -> Next step: No action

- Duplicates: 0 row -> Next step: No action

- Incorrect data types: 0 row -> Next step: No action

- Incorrect values: 0 row -> Next step: No action

### ✔️ EDA transactions.csv

<img width="1283" height="432" alt="image" src="https://github.com/user-attachments/assets/dc1b308a-e86e-49e6-b1c8-a7b1ad19ce54" />

<img width="1283" height="430" alt="image" src="https://github.com/user-attachments/assets/e924fb1a-aab6-4235-9a0c-05185ea19963" />

<img width="1283" height="107" alt="image" src="https://github.com/user-attachments/assets/1dc0abb1-a616-48f8-87b3-5e1f1f0a7580" />

```ruby
from ydata_profiling import ProfileReport

t_report = ProfileReport(transactions, title="Transactions Report", explorative=True)
t_report.to_notebook_iframe()
```

[**Link to code**](https://colab.research.google.com/drive/1dmWHuvxJYoPvjKu-u157WK0bBxq1Hol7?usp=sharing)

<img width="1283" height="638" alt="image" src="https://github.com/user-attachments/assets/a31e270a-3a45-4b25-bd03-79531a5d3cd6" />

<img width="1283" height="602" alt="image" src="https://github.com/user-attachments/assets/786c4fad-96a5-4fe1-894d-c9dee27dfbb0" />

- Missing data: `sender_id, receiver_id, extra_info` -> Next step: No action

- Duplicates: 28 rows -> Next step: Delete rows

- Incorrect data types: 0 row -> Next step: No action

- Incorrect values: 0 row -> Next step: No action

## 🧹 Part II: Data Wrangling & Analysis

### ✔️ Q1. Top 3 product_ids with the highest volume

Find the top 3 products with the highest revenue to identify which products are generating the most income. This helps in focusing on the highest-performing products for sales and marketing strategies.

```ruby
payment_enriched_cleaned1 = payment_report_enriched
payment_enriched_cleaned1[['product_id','source_id']]=payment_enriched_cleaned1[['product_id','source_id']].astype(str)

product_group_by_volumns =  payment_enriched_cleaned1.groupby('product_id')['volume'].sum()
Top_3_product_ids = product_group_by_volumns.sort_values(ascending=False).head(3)
Top_3_product_ids
```

<img width="1283" height="256" alt="image" src="https://github.com/user-attachments/assets/44d50b74-230c-4bd7-a88a-d5af8f2d0093" />

```ruby
top3_product = payment_report_enriched.groupby(by = 'product_id', as_index = False)['volume'].sum().sort_values(by = 'volume', ascending = False).head(3)
top3_product
```

<img width="1283" height="191" alt="image" src="https://github.com/user-attachments/assets/19203bb8-8bea-4367-be50-37217b4be9b2" />

### ✔️ Q2. Given that 1 product_id is only owed by 1 team, are there any abnormal products against this rule?

Check whether each product is managed by a single team to ensure clear ownership and avoid potential conflicts in responsibility.

<img width="1283" height="294" alt="image" src="https://github.com/user-attachments/assets/2267bf9a-ec8e-49f2-a6e9-3b44aaac04a6" />

### ✔️ Q3. Find the team has had the lowest performance (lowest volume) since Q2.2023. Find the category that contributes the least to that team.

Identify the team with the lowest performance in terms of total transaction volume since Q2 2023. Once the lowest-performing team is found, determine the product category that contributes the least to that team's total volume. This analysis helps pinpoint underperforming teams and categories, providing insights for potential improvements or strategic decisions.

<img width="1283" height="617" alt="image" src="https://github.com/user-attachments/assets/7afc4fe6-6aad-4259-83f2-7be08fd6d28b" />

<img width="1283" height="628" alt="image" src="https://github.com/user-attachments/assets/d5a077e2-d99a-4f8e-9108-3880e077ac2d" />

### ✔️ Q4. Find the contribution of source_ids of refund transactions (payment_group = ‘refund’), what is the source_id with the highest contribution?

The goal is to analyze the distribution of refund transactions across different source_ids and identify which source_id has the highest contribution. This helps in understanding refund patterns and potential areas for improvement.

<img width="1283" height="307" alt="image" src="https://github.com/user-attachments/assets/f5402804-ba76-4268-9dfd-d145cbe8b08f" />

### ✔️ Q5. Define type of transactions (‘transaction_type’) for each row, given:

- transType = 2 & merchant_id = 1205: Bank Transfer Transaction

- transType = 2 & merchant_id = 2260: Withdraw Money Transaction

- transType = 2 & merchant_id = 2270: Top Up Money Transaction

- transType = 2 & others merchant_id: Payment Transaction

- transType = 8, merchant_id = 2250: Transfer Money Transaction

- transType = 8 & others merchant_id: Split Bill Transaction

- Remained cases are invalid transactions

The purpose of this task is to categorize each transaction into a specific transaction type based on the given conditions. By doing so, we can clearly identify the type of each transaction in the dataset, which helps in analyzing and understanding transaction patterns, processing specific transactions, and detecting any anomalies or invalid transactions.

```ruby
def define_transaction_type(row):
    transType = row['transType']
    merchant_id = row['merchant_id']

    if transType == 2:
        if merchant_id == 1205:
            return "Bank Transfer Transaction"
        elif merchant_id == 2260:
            return "Withdraw Money Transaction"
        elif merchant_id == 2270:
            return "Top Up Money Transaction"
        else:
            return "Payment Transaction"
    elif transType == 8:
        if merchant_id == 2250:
            return "Transfer Money Transaction"
        else:
            return "Split Bill Transaction"
    else:
        return "Invalid Transaction"

# Apply the custom function to create a new column 'transaction_type'
transactions['transaction_type'] = transactions.apply(define_transaction_type, axis=1)
```

<img width="1283" height="535" alt="image" src="https://github.com/user-attachments/assets/0464071d-da38-4ad0-9b2e-60780553ac71" />

📝 **Another method**

```ruby
conditions = [
    (transactions['transType'] == 2) & (transactions['merchant_id'] == 1205),
    (transactions['transType'] == 2) & (transactions['merchant_id'] == 2260),
    (transactions['transType'] == 2) & (transactions['merchant_id'] == 2270),
    (transactions['transType'] == 2) & (~transactions['merchant_id'].isin([1205, 2260, 2270])),
    (transactions['transType'] == 8) & (transactions['merchant_id'] == 2250),
    (transactions['transType'] == 8) & (~transactions['merchant_id'].isin([2250])),
]

transaction_types = [
    'Bank Transfer Transaction',
    'Withdraw Money Transaction',
    'Top Up Money Transaction',
    'Payment Transaction',
    'Transfer Money Transaction',
    'Split Bill Transaction'
]

transactions['transaction_type'] = np.select(conditions,
                                             transaction_types,
                                             default= 'Invalid Transactions')
transactions
```

<img width="1283" height="491" alt="image" src="https://github.com/user-attachments/assets/c15e3061-ab66-4e73-bae0-fb5059dd96ca" />

### ✔️ Q6. Of each transaction type (excluding invalid transactions): find the number of transactions, volume, senders and receivers

This helps in understanding the distribution of transactions across different types, as well as the engagement of unique senders and receivers for each type of transaction.

<img width="1283" height="567" alt="image" src="https://github.com/user-attachments/assets/5696eb8a-43c1-4bdf-9a33-b6d14e968c6d" />

<img width="1283" height="581" alt="image" src="https://github.com/user-attachments/assets/5e6aeb73-2e3c-4d04-87c6-c3fa44ec9c89" />

## 🤝 **Contributing**

Feel free to fork this repo and add more beginner-friendly exercises or suggest improvements to existing ones. 

Collaboration is welcome!


