import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Generate synthetic customer data
np.random.seed(42)
num_customers = 500

# Random customer attributes
customer_ids = np.arange(1, num_customers + 1)
ages = np.random.randint(18, 65, num_customers)
spending_scores = np.random.randint(1, 100, num_customers)
tenure = np.random.randint(1, 10, num_customers)
customer_support_calls = np.random.randint(0, 10, num_customers)
churn = np.random.choice(["Yes", "No"], num_customers, p=[0.3, 0.7])  # 30% churn rate

# Create DataFrame
df = pd.DataFrame({
    "Customer_ID": customer_ids,
    "Age": ages,
    "Spending_Score": spending_scores,
    "Tenure": tenure,
    "Support_Calls": customer_support_calls,
    "Churn": churn
})

# **1. Pie Chart for Churn Distribution**
plt.figure(figsize=(6, 6))
df["Churn"].value_counts().plot.pie(autopct="%.1f%%", colors=["red", "green"], labels=["Churned", "Retained"])
plt.title("Customer Churn Distribution")
plt.ylabel("")  # Remove default label
plt.show()

# **2. Bar Plot for Churn by Tenure**
plt.figure(figsize=(8, 5))
sns.barplot(x=df["Tenure"], y=df["Spending_Score"], hue=df["Churn"], palette=["red", "green"])
plt.xlabel("Customer Tenure (Years)")
plt.ylabel("Spending Score")
plt.title("Spending vs. Tenure (Churn vs. Retention)")
plt.legend(title="Churn Status")
plt.show()

# **3. Line Plot for Customer Support Calls & Churn**
plt.figure(figsize=(8, 5))
sns.lineplot(x=df["Support_Calls"], y=df["Spending_Score"], hue=df["Churn"], palette=["red", "green"])
plt.xlabel("Support Calls Received")
plt.ylabel("Spending Score")
plt.title("Impact of Support Calls on Churn")
plt.show()
