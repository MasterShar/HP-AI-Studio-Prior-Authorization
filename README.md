# HP-AI-Studio-Prior-Authorization
HP AI Studio Prior Auth Data Science Project

import pandas as pd
import matplotlib.pyplot as plt

# Load data
df = pd.read_csv('Health_Plan_Prior_Authorization_Data_20250505 for Hackathon.csv')
df_clean = df.copy()

# Convert relevant columns to numeric
cols_to_numeric = [
    "Approval rate",
    "Initially denied then approved - approval rate",
    "Expedited - Avg response time",
    "Standard - Avg response time",
    "Extenuating circumstances - Avg response time",
]
for col in cols_to_numeric:
    df_clean[col] = pd.to_numeric(df_clean[col], errors='coerce')

    # Approval rate by carrier and service category
approval_by_carrier = df_clean.groupby('Carrier')["Approval rate"].mean().reset_index()
approval_by_service = df_clean.groupby('Service category')["Approval rate"].mean().reset_index()
approval_by_carrier, approval_by_service

# Top and bottom approval rates
top_approved = df_clean.sort_values("Approval rate", ascending=False).head(10)
low_approved = df_clean.sort_values("Approval rate", ascending=True).head(10)
top_approved[["Carrier", "Service category", "Code", "Description of service", "Approval rate"]], \
low_approved[["Carrier", "Service category", "Code", "Description of service", "Approval rate"]]

# Drug-specific trends
drug_trends = df_clean[df_clean["Drug name"].notnull()].groupby("Drug name")["Approval rate"].mean().reset_index().sort_values(by="Approval rate", ascending=False).head(10)
drug_trends

# Trends over time
approval_over_time = df_clean.groupby("Year")["Approval rate"].mean().reset_index()
approval_over_time
