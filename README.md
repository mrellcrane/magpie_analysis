# Skill Proficiency Analysis

This repository contains a Python script that processes and visualizes skill proficiency data. The script reads raw data from JSON files, cleanses it, generates CSV reports, and produces a dual-axis visualization comparing average proficiency scores and the number of records per skill.

## Files

- **data.json** - Contains raw scores data.
- **skills.json** - Contains the definitions for skills.
- **proficiency.json** - Contains proficiency definitions.
- **main.py** - The Python script that performs the data processing and visualization.
- **time-series.csv** - Output CSV containing cleaned, time-sorted data.
- **proficiency_report.csv** - Output CSV summarizing average proficiency and record counts per skill.
- **dual_axis_visualization.png** - Visualization image showing the analysis results.

## Requirements

Ensure you have Python 3.x installed. The script depends on the following Python packages:

- [pandas](https://pandas.pydata.org/)
- [seaborn](https://seaborn.pydata.org/)
- [matplotlib](https://matplotlib.org/)

You can install these packages using pip like below:

pip install pandas seaborn matplotlib

Running the Script
Ensure that the required JSON files (data.json, skills.json, and proficiency.json) are located in the same directory as code.py.

To run the script, execute:

python code.py
