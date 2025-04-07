# --- Imports ---
import pandas as pd
import json
import seaborn as sns
import matplotlib.pyplot as plt

# --- File Constants ---
DATA_FILE = 'data.json'
SKILLS_FILE = 'skills.json'
PROFICIENCY_FILE = 'proficiency.json'
TIME_SERIES_OUTPUT_CSV = 'time-series.csv'
PROFICIENCY_REPORT_OUTPUT_CSV = 'proficiency_report.csv'

# 1.1: Consume raw data (data.json)
with open(DATA_FILE, 'r') as f:
    raw_data_content = json.load(f)
df_raw = pd.DataFrame(raw_data_content['scores'])

# 1.2: Validate / cleanse raw data
df_cleaned = df_raw.dropna(subset=['skill']).copy()  # Remove rows with missing 'skill'
df_cleaned['score'] = pd.to_numeric(df_cleaned['score'], errors='coerce')  # Convert 'score' to numeric

# 1.3: Output time series CSV (sorted by index assumed to be the time sequence)
df_timeseries_sorted = df_cleaned.sort_index(ascending=True)
df_timeseries_sorted.to_csv(TIME_SERIES_OUTPUT_CSV, index=True)

# --- Requirement: Output a proficiency by skill CSV ---

# 2.3: Consume skills and proficiency definitions
with open(SKILLS_FILE, 'r') as f:
    skills_data_content = json.load(f)
skills_list = skills_data_content.get('skills', [])

with open(PROFICIENCY_FILE, 'r') as f:
    proficiency_data_content = json.load(f)
proficiency_list = proficiency_data_content.get('proficiency', [])

# 2.4 & 2.5: Calculate number of records and average proficiency for each skill
proficiency_summary = df_cleaned.groupby('skill').agg(
    number_of_records=('skill', 'size'),
    average_proficiency=('score', 'mean')
).reset_index()

# 2.6: Output the proficiency report to CSV
proficiency_summary.to_csv(PROFICIENCY_REPORT_OUTPUT_CSV, index=False)

# Prepare data for plotting: sort the aggregated data by 'skill'
df_plot = proficiency_summary.sort_values(by='skill')

# Create dual-axis visualization
fig, ax1 = plt.subplots(figsize=(12, 8))
sns.set_theme(style="whitegrid")

# Bar chart: Average Proficiency per Skill
sns.barplot(
    data=df_plot,
    x='skill',
    y='average_proficiency',
    color='skyblue',
    ax=ax1
)
ax1.set_xlabel('Skill', fontsize=12)
ax1.set_ylabel('Average Proficiency Score', fontsize=12, color='blue')
ax1.tick_params(axis='y', labelcolor='blue')

# Line chart: Number of Records per Skill on second axis
ax2 = ax1.twinx()
sns.lineplot(
    data=df_plot,
    x='skill',
    y='number_of_records',
    color='red',
    marker='o',
    ax=ax2
)
ax2.set_ylabel('Number of Records', fontsize=12, color='red')
ax2.tick_params(axis='y', labelcolor='red')

plt.title('Skill Proficiency Analysis: Average Score vs. Number of Records', fontsize=16)
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.savefig('dual_axis_visualization.png')
plt.show()
