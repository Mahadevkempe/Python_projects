# Exploratory Data Analysis (EDA)

# Business Problem Statement:
The objective is to analyze customer data to identify the key factors contributing to customer churn for a telecom company. By understanding the patterns and reasons behind customer attrition, the company can implement targeted retention strategies to reduce churn and improve customer satisfaction. The analysis will involve exploring demographics, service usage, contract types, and payment methods to derive actionable insights

# Objective:
 The analysis explores customer churn patterns, focusing on various factors such as payment methods, contract types, tenure, and demographic attributes. The goal is to identify which factors are most strongly associated with higher churn rates to guide customer retention strategies.
 
# Customer Churn Analysis.  

# 1. Find the number of customers who churned and those who didn't.
    ab =sns.countplot(x= "Churn", data=df)
    ab.bar_label(ab.containers[0])
    plt.show()

# 2.Calculate the percentage of customers who churned and those who didn't.
    group_by = df.groupby("Churn").agg({'Churn':"count"})
    plt.pie(group_by["Churn"],labels=group_by.index ,autopct= "%1.2f%%")
    plt.show()
    
# 3.Show the relationship between gender and churn using a count plot with labeled bars.
    plt.figure(figsize=(4,4))
    ab = sns.countplot(x="Gender", data=df, hue = "Churn")
    plt.title("Churn by Gender")
    ab.bar_label(ab.containers[0])
    ab.bar_label(ab.containers[1])
    plt.show() 

 # 4. Find the number of senior citizen customers and non-senior citizen customers.
    plt.figure(figsize=(4,4))
    ab = sns.countplot(x="SeniorCitizen", data=df)
    ab.bar_label(ab.containers[0])
    plt.title("Count of Customers by Senior Citizen")
    plt.show() 

 # 5.Compare churn percentages between senior citizens and non-senior citizens.
 
total_counts = df.groupby('SeniorCitizen')['Churn'].value_counts(normalize=True).unstack() * 100
fig, ax = plt.subplots(figsize=(4, 4))  # Adjust figsize for better visualization
total_counts.plot(kind='bar', stacked=True, ax=ax, color=['#1f77b4', '#ff7f0e'])  # Customize colors if desired
for p in ax.patches:
    width, height = p.get_width(), p.get_height()
    x, y = p.get_xy()
    ax.text(x + width / 2, y + height / 2, f'{height:.1f}%', ha='center', va='center')
plt.title('Churn by Senior Citizen (Stacked Bar Chart)')
plt.xlabel('SeniorCitizen')
plt.ylabel('Percentage (%)')
plt.xticks(rotation=0)
plt.legend(title='Churn', bbox_to_anchor = (0.9,0.9))  # Customize legend location
plt.show()

 # 6.Analyze the distribution of customer tenure and its relationship with churn.
 
   plt.figure(figsize=(10,5))
   sns.histplot(x="Tenure", data=df, bins=72, hue= "Churn")
   plt.show() 

 # 7.Analyze the relationship between contract type and churn. 
 
    plt.figure(figsize=(4,4))
    ab=sns.countplot(x="Contract", data= df, hue="Churn")
    ab.bar_label(ab.containers[0])
    ab.bar_label(ab.containers[1])
    plt.title("Count of Customers by Senior Citizen")
    plt.show()

# 8.Analyze the impact of various services on customer churn using count plots.

columns = ['PhoneService', 'MultipleLines', 'InternetService', 'OnlineSecurity', 
           'OnlineBackup', 'DeviceProtection', 'TechSupport', 'StreamingTV', 'StreamingMovies']
n_cols = 3
n_rows = (len(columns) + n_cols - 1) // n_cols  # Calculate number of rows needed
fig, axes = plt.subplots(n_rows, n_cols, figsize=(15, n_rows * 4))  # Adjust figsize as needed
axes = axes.flatten()
for i, col in enumerate(columns):
    sns.countplot(x=col, data=df, ax=axes[i], hue = df["Churn"])
    axes[i].set_title(f'Count Plot of {col}')
    axes[i].set_xlabel(col)
    axes[i].set_ylabel('Count')
for j in range(i + 1, len(axes)):
    fig.delaxes(axes[j])
plt.tight_layout()
plt.show()


# 9.Examine the relationship between payment method and customer churn.

 plt.figure(figsize=(6,4))
 ab = sns.countplot(x="PaymentMethod", data=df, hue="Churn")
 ab.bar_label(ab.containers[0])
 ab.bar_label(ab.containers[1])
 plt.title("Churn Customers by Payment Method")
 plt.xticks(rotation=45)
 plt.show()
