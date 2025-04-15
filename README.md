# Demographic Data Analyzer  

The Demographic Data Analyzer is a Python program that analyzes demographic data from a dataset containing information about individuals from various backgrounds. It uses the Pandas library to perform data processing and analysis, generating insights such as average age, education statistics, work hours, and salary information.  

## Overview  

This project calculates various demographic statistics based on the data provided in the `adult.data.csv` file. It answers key questions about the dataset, including:  

- The count of individuals from different races  
- The average age of men  
- The percentage of individuals with a Bachelor's degree  
- The percentage of individuals earning more than $50,000 based on their education level  
- The country with the highest percentage of individuals earning more than $50,000  
- The most popular occupation for individuals earning more than $50,000 in India  

## Features  

- Reads demographic data from a CSV file.  
- Analyzes and calculates demographic metrics, including race count, average age of men, education levels, work time, and income statistics.  
- Outputs results in a clear and readable format.  

## Installation  

To run this project, make sure you have Python installed on your machine. You will also need the Pandas library. You can install Pandas using pip:  

```bash  
pip install pandas

Usage
Here's how to use the Demographic Data Analyzer:

Import the necessary library:
import pandas as pd

Define the main function:
def calculate_demographic_data(print_data=True):  
    # Your code here
Run the function:
To execute the analysis, simply call the function:

Example
Below is the core function implementing the demographic data analysis:

import pandas as pd  

def calculate_demographic_data(print_data=True):  
# Read data from file  
df = pd.read_csv('/workspace/boilerplate-demographic-data-analyzer/adult.data.csv')  

# How many of each race are represented in this dataset?   
race_count = df['race'].value_counts()  

# What is the average age of men?  
average_age_men = df[df['sex'] == 'Male']['age'].mean()  

# What is the percentage of people who have a Bachelor's degree?  
percentage_bachelors = len(df[df['education'] == 'Bachelors']) / len(df) * 100  

# What percentage of people with advanced education make more than 50K?  
higher_education = len(df[df['education'].isin(['Bachelors', 'Masters', 'Doctorate'])])  
lower_education = len(df) - higher_education  
higher_education_rich = (len(df[(df['education'].isin(['Bachelors', 'Masters', 'Doctorate'])) & (df['salary'] == '>50K')]) / higher_education) * 100  
lower_education_rich = (len(df[(~df['education'].isin(['Bachelors', 'Masters', 'Doctorate'])) & (df['salary'] == '>50K')]) / lower_education) * 100  

# What is the minimum number of hours a person works per week?  
min_work_hours = df['hours-per-week'].min()  

# What percentage of the people who work the minimum number of hours per week have a salary of >50K?  
total_workers_min_work_hours = len(df[df['hours-per-week'] == min_work_hours])  
rich_workers_min_work_hours = len(df[(df['hours-per-week'] == min_work_hours) & (df['salary'] == '>50K')])  
rich_percentage = (rich_workers_min_work_hours / total_workers_min_work_hours) * 100  

# What country has the highest percentage of people that earn >50K?  
salary_counts = df.groupby(['native-country', 'salary']).size().unstack(fill_value=0)  
salary_counts['percentage_greater_50K'] = (salary_counts['>50K'] / (salary_counts['>50K'] + salary_counts['<=50K'])) * 100  
highest_earning_country = salary_counts['percentage_greater_50K'].idxmax()  
highest_earning_country_percentage = salary_counts['percentage_greater_50K'].max()  

# Identify the most popular occupation for those who earn >50K in India.  
india_high_earners = df[(df['native-country'] == 'India') & (df['salary'] == '>50K')]  
if not india_high_earners.empty:  
    top_occupation = india_high_earners['occupation'].value_counts().idxmax()  
    top_IN_occupation = india_high_earners['occupation'].value_counts().max()  

# Print results if print_data is True  
if print_data:  
    print("Number of each race:\n", race_count)  
    print("Average age of men:", average_age_men)  
    print(f"Percentage with Bachelors degrees: {percentage_bachelors}%")  
    print(f"Percentage with higher education that earn >50K: {higher_education_rich}%")  
    print(f"Percentage without higher education that earn >50K: {lower_education_rich}%")  
    print(f"Min work time: {min_work_hours} hours/week")  
    print(f"Percentage of rich among those who work fewest hours: {rich_percentage}%")  
    print("Country with highest percentage of rich:", highest_earning_country)  
    print(f"Highest percentage of rich people in country: {highest_earning_country_percentage}%")  
    print("Top occupations in India:", top_IN_occupation)  

return {  
    'race_count': race_count,  
    'average_age_men': average_age_men,  
    'percentage_bachelors': percentage_bachelors,  
    'higher_education_rich': higher_education_rich,  
    'lower_education_rich': lower_education_rich,  
    'min_work_hours': min_work_hours,  
    'rich_percentage': rich_percentage,  
    'highest_earning_country': highest_earning_country,  
    'highest_earning_country_percentage': highest_earning_country_percentage,  
    'top_IN_occupation': top_IN_occupation  
}

Contributing
If you would like to contribute to this project, feel free to fork the repository and submit a pull request. Contributions of any kind are welcome!

Acknowledgements
This project is built as part of the FreeCodeCamp curriculum.

This README file provides an overview, usage instructions, and features of your Demographic Data Analyzer project. If you need more modifications or additional information to be included, feel free to let me know!
