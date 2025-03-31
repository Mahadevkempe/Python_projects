# Exploratory Data Analysis (EDA)

# Executive Summary:

# Objective:
 The analysis explores customer churn patterns, focusing on various factors such as payment methods, contract types, tenure, and demographic attributes. The goal is to identify which factors are most strongly associated with higher churn rates to guide customer retention strategies.
 
# Key Insights & Findings:
 
# ● Contract Type and Churn:
 ○ Customers on month-to-month contracts exhibit the highest churn rate, with 42% of such customers likely to churn.
 ○ Incontrast, customers on one-year and two-year contracts have churn rates of 11% and 3%, respectively.
 ○ Implication: Longer contract periods serve as a strong retention tool, as customers with extended commitments are far less likely to leave.
 
#  ● PaymentMethods and Churn:
 ○ Customers paying via electronic checks show the highest churn rate at 45%, while those using credit cards, bank transfers, or mailed checks have significantly lower churn
   rates, averaging around 15-18%.
 ○ Implication: The convenience, security, and trust issues related to electronic payments might be contributing factors. Encouraging customers to switch tomore stable 
   payment methods could reduce churn.
 
# ● ChurnbyTenure:
 ○ Customers with less than one year of tenure are the most likely to churn, with a 50% churn rate. Those with 1-3 years of tenure show a decreasing churn trend at 35%, 
   while customers who have been with the company for more than three years have a churn rate of just 15%.
 ○ Implication:
   Engaging customers early in their journey, especially within the first year, is critical for retention.
   
# ● ChurnbyInternet Service Type:
 ○ Customers using Fiber Optic services show a higher churn rate of 30%, compared to DSL customers with a churn rate of 20%.
 ○ Implication:
   This could be due to increased competition or dissatisfaction with service quality. Understanding customer satisfaction with service speed andreliability may help retain 
   fiber optic users.
 ● Senior Citizens and Churn:
 ○ Theanalysis reveals that senior citizens (aged 65+) have a churn rate of 41%, compared to a 26% churn rate among non-senior citizens.
 ○ Implication:
   Special retention programs and targeted customer service for senior customers may help reduce churn in this demographic. 
   
# Visualizations & Data Insights:

# ● BarCharts and Line Graphs:
 ○ Thevisual representation of churn by payment method clearly shows that customers using electronic checks churn almost three times as much as those using more traditional 
   or secure methods like credit cards.
 ○ Customertenure vs. churn rate visualizations reveal a clear declining trend in churn as customers' tenure increases, underscoring the need for early-stage customer 
   loyalty programs.
 
# ● Percentage Distribution of Churn Across Factors:
 ○ PaymentMethods:
   45% churn for electronic check users, 15% for credit card users.
 ○ Contract Types: 
   42% churn for month-to-month contracts, 11% for yearly contracts, 3% for two-year contracts.
 ○ Tenure: 
   50% churn in the first year, dropping to 15% after three years.Recommendations:
   
# ● PromoteLong-Term Contracts: 
   Offer incentives for customers to commit to longer contracts to reduce churn.
   
# ● AddressPayment Method Concerns:
   Implement campaigns encouraging customers to switch from electronic checks to more reliable payment methods.
   
# ● CustomerEngagement in Early Tenure: 
   Focus on improving the customer experience within the first year, as churn is highest in this period.
   
# ● Special Senior Citizen Retention Programs:
   Create personalized offers or assistanceprograms to retain the senior demographic. 

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

   # Plot
  fig, ax = plt.subplots(figsize=(4, 4))  # Adjust figsize for better visualization

  # Plot the bars
  total_counts.plot(kind='bar', stacked=True, ax=ax, color=['#1f77b4', '#ff7f0e'])  # Customize colors if desired

  # Add percentage labels on the bars
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

  # Number of columns for the subplot grid (you can change this)
  n_cols = 3
  n_rows = (len(columns) + n_cols - 1) // n_cols  # Calculate number of rows needed

  # Create subplots
  fig, axes = plt.subplots(n_rows, n_cols, figsize=(15, n_rows * 4))  # Adjust figsize as needed

 # Flatten the axes array for easy iteration (handles both 1D and 2D arrays)
 axes = axes.flatten()

 # Iterate over columns and plot count plots
 for i, col in enumerate(columns):
    sns.countplot(x=col, data=df, ax=axes[i], hue = df["Churn"])
    axes[i].set_title(f'Count Plot of {col}')
    axes[i].set_xlabel(col)
    axes[i].set_ylabel('Count')

 # Remove empty subplots (if any)
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
