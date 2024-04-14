# Introduction
## Exploring Automobile Sales Data📊🔍

👋 Welcome to the documentation of my analysis on **car sales data**. In this repository, I delve into the intricacies of car sales transactions💰 to gain insights into various aspects of the business operations. My analysis aims to answer several key questions that are crucial for understanding the performance of our sales, identifying areas for improvement, and making informed business decisions📈. A dashborad was created for the data as well.

I performed an EDA on the data and created a tableau dashboard for easy and fast communication of findings.

---
🔍Jubyter notebook? Check them here: [Jubyter Notebook.](car_sales_analysis.ipynb)

🔍Tableau Dashboard? Check them here: [Tableau Dashboard.](car_sales_analysis.ipynb) 

# Background

In the competitive automotive industry, understanding sales dynamics is crucial for staying ahead.🚗 My study dives into sales data to extract insights that can drive growth and enhance customer satisfaction.💡 By analyzing factors such as sales volumes, pricing strategies, and customer demographics, we aim to uncover actionable insights that inform strategic decision-making. 📊 Through this study, we empower stakeholders to adapt strategies, streamline processes, and capitalize on emerging opportunities in the dynamic automotive market.🌟


Data hails from [Kaggle @ Dee](https://www.kaggle.com/datasets/ddosad/auto-sales-data/data).

Information on the data? [Click here.](#information-of-the-data)

 
## The questions I wanted to answer were:

1. What are the overall sales trends over time? Are there any seasonal patterns or fluctuations in sales volumes?
2. Which product lines or models are the best-selling? 
3. How do pricing strategies, as indicated by variables like "PRICEEACH" and "MSRP," impact sales volumes?
4. What is the distribution of customers across different regions or countries? Are there any geographical trends in sales performance?

5. Are there any anomalies or outliers in the data that may require further investigation?


# Tools I used 
I used the following tools:
- **Python:** Leveraged python libraries such as numpy, pandas, matplotlib and seaborn  to extract insights from the dataset and create visualization for the data. 
- **VSCode:** Employed Visual Studio Code as the integrated development environment (IDE) for writing SQL scripts and managing project files, enhancing productivity and code readability.
  
- **Git:** Utilized Git for version control, allowing for collaborative development and tracking changes made to project files over time, ensuring project integrity and facilitating seamless collaboration.

# The analysis 
Breakdown of the approach used 👇

### 1. What are the overall sales trends over time? Are there any seasonal patterns or fluctuations in sales volumes?
```py
# Extract the Year, Quarters, Months and Weeks from the date data.
df['Year'] = df['ORDERDATE'].dt.year
df['Month'] = df['ORDERDATE'].dt.month
df['Quaters'] = df['ORDERDATE'].dt.quarter
df['Week'] = df['ORDERDATE'].dt.isocalendar().week
```
- Plot the various charts to display the trends
```py
# Yearly Sales
plt.figure(figsize=(20,5))
sns.set_theme(style='whitegrid')
col = ['#2E27B7','#F80D0F','#26F801']

sns.lineplot(data = df, x = 'ORDERDATE', y = 'SALES', hue = 'Year', ci = None,palette=col)
plt.title('Yearly Sales', loc = 'left')
```
![Sales_By_Year](https://github.com/DataNerdss/Automobile_Sales_Analysis_Project/assets/116424752/f1d4d31c-9dcb-44eb-8e41-69db658f46f7)

``` py
# Monthly Sales

plt.figure(figsize=(20,5))
sns.set_theme(style='whitegrid')
col = ['#2E27B7','#F80D0F','#26F801']

sns.lineplot(data = df, x = 'Month', y = 'SALES', hue = 'Year', ci = None,palette=col)
plt.title('Monthly Sales', loc = 'left')
```
![Monthly_Sales](https://github.com/DataNerdss/Automobile_Sales_Analysis_Project/assets/116424752/67125a43-b056-438f-bd38-4038566161e3)

``` py
# Weekly Sales
plt.figure(figsize=(20,5))
sns.set_theme(style='whitegrid')
col = ['#2E27B7','#F80D0F','#26F801']

sns.lineplot(data = df, x = 'Week', y = 'SALES', hue = 'Year', ci = None,palette=col)
plt.title('Weekly Sales', loc = 'left')
```
![Weekly_Sales](https://github.com/DataNerdss/Automobile_Sales_Analysis_Project/assets/116424752/ae891796-2769-4290-a020-01314b1831af)

## Summary of the result

Seasonality: There appears to be a pattern of fluctuation in sales over time. This could suggest seasonality in the data, with certain times of the year experiencing higher or lower sales volumes.

Overall Trend: While there are fluctuations, there seems to be a general increasing trend in sales over the observed period.

Outliers: There are a few notable spikes in sales, particularly around March, 2019 and April,2020 and late 2019. These spikes could represent exceptional events or promotions that significantly boosted sales during those periods.

Periods of Stability: Between some of the spikes, there are periods of relatively stable sales, suggesting consistent performance during those times.

### 2. Which product lines are the best-selling? 
```py
# Sales vs Productline
df_1 = pd.DataFrame(df.groupby('PRODUCTLINE')['SALES'].sum().sort_values(ascending = False))
df_1['SALES_K'] = df_1["SALES"]/1000

plt.figure(figsize=(10,5))

sns.barplot(data = df_1, x = 'PRODUCTLINE', y = 'SALES_K', palette='magma', ci = None)
for p in plt.gca().patches:
    plt.gca().annotate(f'{p.get_height():.1f}k', (p.get_x() + p.get_width() / 2., p.get_height()),
                       ha='center', va='bottom', fontsize=8)

plt.title('Sales by ProductLine', loc = 'left')
```
![Productline_Sales](https://github.com/DataNerdss/Automobile_Sales_Analysis_Project/assets/116424752/545bcd27-1312-4e69-8f1f-6bf890458443)

### Summary of the result

1. **Classic Cars** have the highest sales among all product lines, totaling approximately $3.8 million with **Vintage Cars** coming next, with sales reaching around $1.8 million.

3. **Trucks and Buses** and **Motorcycles** both have significant sales, each exceeding \$1.1 million.

4. **Planes** and **Ships** follow with sales around \$970,000 and \$700,000, respectively. and **Trains** have the lowest sales among the product lines, totaling approximately \$226,000.

### Note
Avearge price of the items was not compared because there exists some outliner in the sales column.

🔍Jubyter notebook? Check them here: [Jubyter Notebook.](car_sales_analysis.ipynb)

🔍Tableau Dashboard? Check them here: [Tableau Dashboard.](car_sales_analysis.ipynb) 


### 3. How do pricing strategies, as indicated by variables like "PRICEEACH" and "MSRP," impact sales volumes?


Correlation betweem the three variables.
|           | PRICEEACH |    MSRP   |   SALES   |
|-----------|-----------|-----------|-----------|
| PRICEEACH |  1.000000 |  0.778393 |  0.808287 |
| MSRP      |  0.778393 |  1.000000 |  0.634849 |
| SALES     |  0.808287 |  0.634849 |  1.000000 |

![Correlation_sales_by_price](https://github.com/DataNerdss/Automobile_Sales_Analysis_Project/assets/116424752/30063d6e-adc1-4ba1-add4-ac8da9e628e4)

### Summary on the result

1. **Price Each (PRICEEACH) and Sales (SALES)**: There is a strong positive correlation of approximately 0.808 between the price of each item and the total sales amount. This indicates that as the price of each item increases, the total sales also tend to increase. 

2. **MSRP and Sales (SALES)**: There is a moderate positive correlation of approximately 0.635 between the Manufacturer's Suggested Retail Price (MSRP) and the total sales amount. This indicates that items with higher MSRP values tend to generate higher total sales.

Overall, these correlations suggest that there are positive relationships between the price of each item, MSRP, and total sales amount. However, it's important to remember that correlation does not imply causation, and other factors may also influence these relationships.


### 4. What is the distribution of customers across different cities or countries? Are there any geographical trends in sales performance?

These are the top 10 countries the customers are buying from.
![top_10_countries](https://github.com/DataNerdss/Automobile_Sales_Analysis_Project/assets/116424752/64e9abfe-ff21-4dea-99c6-bc3abf56bc09)

Top 10 cities as well.
![top_10_cities](https://github.com/DataNerdss/Automobile_Sales_Analysis_Project/assets/116424752/ddb49555-2a63-42ee-941f-0aef22793b8f)

Amount of items bought by the top 10 customers.
![Sales_by_customer](https://github.com/DataNerdss/Automobile_Sales_Analysis_Project/assets/116424752/417a1c26-c38c-4f2b-bbff-f5b2757c3dfc)



### Summary of the results

- **Euro Shopping Channel**: Leads in sales with a total of \$912,294.11, making it the top customer in terms of sales. **Mini Gifts Distributors Ltd.**, follows closely behind Euro Shopping Channel with total sales of \$654,858.06.
- **Australian Collectors, Co.**: Holds the third position with total sales amounting to \$200,995.41. **Muscle Machine Inc** stays close to Australian Collectors, Co. with total sales of \$197,736.94.
- **La Rochelle Gifts, Dragon Souveniers, Ltd., Land of Toys Inc., The Sharp Gifts Warehouse, AV Stores, Co., Anna's Decorations, Ltd**: These customers also contribute significantly to sales, each with total sales ranging from approximately \$153,996 to \$180,124.

In summary, Euro Shopping Channel and Mini Gifts Distributors Ltd. are the top two customers in terms of total sales.

### 5. Are there any anomalies or outliers in the data that may require further investigation?

Yes, there are outliners present in the data.
Lets explore the numerical columns for the outliners


![QuantityOrdered_dist](https://github.com/DataNerdss/Automobile_Sales_Analysis_Project/assets/116424752/192337d9-e42d-4036-ae07-bec15891b00c)

![price_per_item_dist](https://github.com/DataNerdss/Automobile_Sales_Analysis_Project/assets/116424752/c174c7f4-7563-4d49-9044-7f861a94caae)

![Sales_dist](https://github.com/DataNerdss/Automobile_Sales_Analysis_Project/assets/116424752/7f3ee590-06a2-4f38-a302-3072c1742a6c)



# Information of the data



