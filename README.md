# Market Basket Analysis on Bakery Dataset

## 1. Project Overview

### 1.1 Introduction
Data mining techniques have transformed industries by enabling businesses to gain actionable insights. In the retail industry, these approaches can lead to significant growth by optimizing product placement and marketing strategies.  

In environments such as cafes, restaurants, and bakeries, understanding customer purchasing behavior is crucial. Market Basket Analysis (MBA) is one of the most effective techniques to identify purchasing patterns. It helps businesses discover hidden associations between products, optimize promotions, and enhance store operations.  

This project applies MBA on a transactional bakery dataset to uncover meaningful relationships between items, ultimately increasing sales and customer satisfaction.  

### 1.2 Problem Statement
Large volumes of transactional data are generated daily in the food and beverage industry. Despite this, much of the data remains underutilized. Businesses often lack the tools or knowledge to extract meaningful insights, limiting their ability to make data-driven decisions.  

This project aims to apply **association rule mining** on a real-world bakery dataset to generate frequent item combinations and rules, revealing actionable insights for business improvement.

### 1.3 Rationale for Dataset Selection
A publicly available bakery dataset from Kaggle was selected because it contains detailed transactional data of items bought together. Its structured transactional format makes it ideal for market basket analysis with minimal preprocessing required.  

- **Dataset source:** Kaggle - [Bakery Sales Dataset](https://www.kaggle.com/datasets/akashdeepkuila/bakery)  
- **Features:** Transaction ID, Items, Date/Time, Period of Day, Weekday/Weekend  

### 1.4 Project Objectives
1. Perform Market Basket Analysis to understand customer purchasing behavior.  
2. Apply association rule mining to identify frequent and infrequent items and generate rules.  
3. Evaluate rule quality using metrics like support, confidence, and lift.  
4. Compare different rule mining techniques based on execution time and rule quality.  
5. Produce actionable insights for product placement, marketing, and promotions.  

## 2. Dataset Description
The dataset contains transactional sales data from a bakery:

- **Transaction:** Unique ID for each transaction  
- **Items:** Purchased items (categorical)  
- **Date/Time:** When the transaction occurred  
- **Period of Day:** Morning, Afternoon, Evening, Night  
- **Weekday/Weekend:** Indicates weekday or weekend  

**Dataset Size:** 20,507 rows with 9,465 unique transactions and 94 unique items.  

**Observations:**
- Most transactions occur during the day (morning and afternoon).  
- Weekends have higher transactions per day despite weekdays having more total transactions.  
- Popular items: Coffee, Bread, Tea, Cake  

## 3. Basic Data Exploration
- **Shape:** 20,507 entries, 5 features  
- **Unique Values:** 9,465 transactions, 94 items  
- **Transaction Patterns:**  
  - Most purchases in the afternoon and morning  
  - Coffee is the most purchased item  
  - Weekends see higher transactions per day  

## 4. Data Preprocessing

### 4.1 Data Cleaning
- No missing values  
- Outliers are not treated since the data is categorical  
- Rare items (sold once) are retained to maintain insights  

### 4.2 Grouping Items by Transaction
Grouped rows by transaction ID to represent each transaction as a list of items.  

### 4.3 Data Transformation
- Used a **Transaction Encoder** to convert grouped data into a Boolean array (rows = transactions, columns = unique items)  
- Prepared data for **association rule mining algorithms**  

## 5. Implementation of Apriori Algorithm
The **Apriori Algorithm** identifies frequent itemsets and generates association rules based on support, confidence, and lift.

### 5.1 Frequent Itemset Generation
- Minimum support = 0.01  
- Frequent itemsets occurring in at least 1% of transactions were considered  

### 5.2 Association Rule Extraction
- Lift ≥ 1 for positive associations  
- Support and confidence metrics used to evaluate rules  

### 5.3 Hyperparameter Tuning
| Min Support | Min Lift | Rules Generated |
|------------|----------|----------------|
| 0.01       | 1        | Many (strong + moderate) |
| 0.03       | 1        | 8 rules        |
| 0.05       | 1        | 2 rules        |
| 0.05       | 0.6/0.8  | None           |
| 0.1        | 1.2      | None           |

**Optimal parameters:** min support = 0.01, min lift = 1  

### 5.4 Visualizations
- Top 10 association rules and network graphs highlight most frequent item combinations  
- Separate analysis for weekdays/weekends and time of day  
- Coffee excluded for fairer analysis  

## 6. Implementation of Other Algorithms

### 6.1 FP-Growth
- Tree-based algorithm for frequent itemsets  
- Faster than Apriori for larger datasets  
- Top 10 rules by confidence visualized  

### 6.2 PrefixSpan
- Pattern-growth algorithm for sequential patterns  
- Identifies frequently occurring purchase sequences  
- Top 10 sequential purchase patterns visualized  

## 7. Evaluation and Analysis of Rules

### 7.1 Interpretation of Key Rules
- **Toast => Coffee:** Support = 0.0237, Confidence = 70.44%, Lift = 1.47  
- **Hot Chocolate => Cake:** Support = 0.0114, Confidence = 19.57%, Lift = 1.88  
- **Tea + Coffee => Cake:** Support = 0.01, Confidence = 20%, Lift = 1.93  

### 7.2 Actionable Insights
- Weekend promotions: Nomad + Coffee combo  
- Hot Chocolate and Cake often purchased together  
- Toast frequently paired with Coffee  
- Inventory planning based on popular combinations  

### 7.3 Business Strategy Implications
1. **Product Bundling:** Combo offers like “Buy Coffee, get 20% off on Toast”  
2. **Timed Promotions:** Morning/afternoon combos to boost sales  
3. **Targeted Marketing:** Personalized offers based on purchase history  
4. **Inventory Planning:** Stock popular combinations together  

## 8. Algorithm Comparison
- **Number of Rules:** Apriori ≈ FP-Growth < PrefixSpan  
- **Execution Time:** Apriori & PrefixSpan faster; FP-Growth slower for this dataset  

## 9. Conclusion

### 9.1 Key Insights
- Most transactions occur in mornings and afternoons  
- Weekends have higher transactions per day  
- Customer purchase patterns vary by time of day and type of day  
- Optimal parameters identified for Apriori  

### 9.2 Challenges Faced
- Dominant items like coffee overshadowed other associations  
- FP-Growth execution slower than expected  

### 9.3 Future Work
- Analyze time-based patterns for better marketing strategies  
- Combine MBA with customer segmentation  
- Apply advanced techniques like Neural Networks and LLMs  
- Integrate cost and profit margins for profitability analysis  

**Summary:**  
This project demonstrates the power of Market Basket Analysis using Apriori, FP-Growth, and PrefixSpan, producing actionable insights for marketing, inventory management, and strategic planning.
