# Diwali_Sales_Analysis

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv('Diwali Sales Data.csv', encoding='unicode_escape')
# To Avoid Encoding Error so we have used Unicode_escape

df.shape
df.head()
df.info()

#Drop Unwanted / Blanks Columns
df.drop(['Status', 'unnamed1'], axis=1, inplace=True)

# Checking Null values
pd.isnull(df).sum()

df.dropna(inplace=True)

#Change Data type
df["Amount"] = df['Amount'].astype('int')

#ReName Column
df.rename(columns = {'Marital_Status' : 'Shadhi'})

#Describe specific columns

df[['Age','Orders','Amount']].describe()

# EDA (Exploratory Data Analysis)

# Gender

ax=sns.countplot(x='Gender', data=df)

for bars in ax.containers:
    ax.bar_label(bars)

sales_gen = df.groupby(['Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending = False)

sns.barplot(x='Gender', y='Amount', data = sales_gen)

ax=sns.countplot(data=df, x = 'Age Group', hue= 'Gender')

# Age

for bars in ax.containers:
    ax.bar_label(bars)

#Total Amount VS Age Group
sales_age = df.groupby(['Age Group'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
sns.barplot(x='Age Group', y= 'Amount', data=sales_age)

# State    
 #Total Amount VS Age Group
sales_state = df.groupby(['State'], as_index=False)['Orders'].sum().sort_values(by='Orders', ascending=False).head(10)
sns.set(rc={'figure.figsize':(15,8)})
sns.barplot(x='State', y= 'Orders', data=sales_state)

# Marital Status

ax = sns.countplot(data=df, x='Marital_Status')

sns.set(rc={'figure.figsize':(6,4)})
for bars in ax.containers:
    ax.bar_label(bars)

 #Total Amount VS Age Group
sales_state = df.groupby(['Marital_Status', 'Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
sns.set(rc={'figure.figsize':(7,5)})
sns.barplot(x='Marital_Status', y= 'Amount', hue='Gender', data=sales_state)

# Occupation

ax = sns.countplot(data=df, x='Occupation')

sns.set(rc={'figure.figsize':(25,5)})
for bars in ax.containers:
    ax.bar_label(bars)

 #Total Occupation VS Amount Group
sales_state = df.groupby(['Occupation'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
sns.set(rc={'figure.figsize':(25,8)})
sns.barplot(x='Occupation', y= 'Amount', data=sales_state)

# Product_Category
ax = sns.countplot(data=df, x='Product_Category')

sns.set(rc={'figure.figsize':(6,4)})
for bars in ax.containers:
    ax.bar_label(bars)

 #Product_Category VS Amount Group
sales_state = df.groupby(['Product_Category'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10)
sns.set(rc={'figure.figsize':(30,7)})
sns.barplot(x='Product_Category', y= 'Amount', data=sales_state)

 #Product_Category VS Amount Group
sales_state = df.groupby(['Product_ID'], as_index=False)['Orders'].sum().sort_values(by='Orders', ascending=False).head(10)
sns.set(rc={'figure.figsize':(30,7)})
sns.barplot(x='Product_ID', y= 'Orders', data=sales_state)

# Conclusion:
Married Women age group 26 to 35 yrs from UP, Maharashtra and Karnataka working in IT, Healthcare and Aviation are mostly likely to buy products from food, clothing and electronic category 
