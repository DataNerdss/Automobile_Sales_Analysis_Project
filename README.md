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

5. Are there any notable relationships between sales quantities and other variables, such as "QUANTITYORDERED" or "ORDERLINENUMBER"?
6. Can we identify any patterns or trends in customer behavior based on variables like "DAYS_SINCE_LASTORDER" or "DATE_SINCE_LASTORDER"?

7. Are there any anomalies or outliers in the data that may require further investigation?


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
- Plot the various plot to display the trends
```py
# Yearly Sales
plt.figure(figsize=(20,5))
sns.set_theme(style='whitegrid')
col = ['#2E27B7','#F80D0F','#26F801']

sns.lineplot(data = df, x = 'ORDERDATE', y = 'SALES', hue = 'Year', ci = None,palette=col)
plt.title('Yearly Sales', loc = 'left')
```
![#](Images\Sales_By_Year.png)
``` py
# Monthly Sales

plt.figure(figsize=(20,5))
sns.set_theme(style='whitegrid')
col = ['#2E27B7','#F80D0F','#26F801']

sns.lineplot(data = df, x = 'Month', y = 'SALES', hue = 'Year', ci = None,palette=col)
plt.title('Monthly Sales', loc = 'left')
```
![](Images\Monthly_Sales.png)
``` py
# Weekly Sales
plt.figure(figsize=(20,5))
sns.set_theme(style='whitegrid')
col = ['#2E27B7','#F80D0F','#26F801']

sns.lineplot(data = df, x = 'Week', y = 'SALES', hue = 'Year', ci = None,palette=col)
plt.title('Weekly Sales', loc = 'left')
```
![](Images\Weekly_Sales.png)

## Summary of the result

Seasonality: There appears to be a pattern of fluctuation in sales over time. This could suggest seasonality in the data, with certain times of the year experiencing higher or lower sales volumes.

Overall Trend: While there are fluctuations, there seems to be a general increasing trend in sales over the observed period.

Outliers: There are a few notable spikes in sales, particularly around March, 2019 and April,2020 and late 2019. These spikes could represent exceptional events or promotions that significantly boosted sales during those periods.

Periods of Stability: Between some of the spikes, there are periods of relatively stable sales, suggesting consistent performance during those times.

### Note
By understanding these trends, businesses can make informed decisions regarding inventory management, marketing strategies, and resource allocation to capitalize on peak sales periods and mitigate slower periods.

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
![](Images\Productline_Sales.png)

### Findings

1. **Classic Cars** have the highest sales among all product lines, totaling approximately $3.8 million.
  
2. **Vintage Cars** come next, with sales reaching around \$1.8 million.

3. **Trucks and Buses** and **Motorcycles** both have significant sales, each exceeding \$1.1 million.

4. **Planes** and **Ships** follow with sales around \$970,000 and \$700,000, respectively.

5. **Trains** have the lowest sales among the product lines, totaling approximately \$226,000.





# Information of the data



