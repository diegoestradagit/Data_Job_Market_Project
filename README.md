## Overview
Welcome to my analysis of the data job market, focusing on data analyst roles. This project was created out of a desire to navigate and understand the job market more effectively. It delves into the top-paying and in-demand skills to help find optimal job opportunities for data analysts.

The data sourced from [Luke Barousse's Python Course](https://www.lukebarousse.com/python) which provides a foundation for my analysis, containing detailed information on job titles, salaries, locations, and essential skills. Through a series of Python scripts, I explore key questions such as the most demanded skills, salary trends, and the intersection of demand and salary in data analytics.

## The Questions to Analyze
Below are the questions I want to answer in this project:

1. What are the skills most in demand for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for data analysts to learn? (High Demand AND High Paying)

## Tools Used in the Project
* Python Programming Language: Special emphasis on the following libraries:
    * Pandas
    * Matplotlib
    * Seaborn
* Jupyter Notebooks
* Visual Studio Code
* Git & GitHub

# The Analysis
Each Jupyter notebook for this project aimed at investigating different aspects of the data job market. Here’s how I approached each question:

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles (Data Analyst, Data Engineer and Data Scientist). I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This visualizations highlight the most popular job titles and their top skills, showing which skills one should pay attention to depending on the role you are targeting.

View my notebook with detailed steps here:
[2_Skill_Demand](Project\2_Skill_Demand.ipynb).

### Visualizing the Data

```
# Plot skills_percent to get top 10 skills by Job Title
fig, ax = plt.subplots(1, len(job_titles), figsize=(17, 8), sharex=True)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(10)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

plt.show()
```
### Results

![Visualization of Top Skills For Data Workers](https://github.com/diegoestradagit/Diego_Python_Project/blob/main/Project/Images/skill_demand_by_data_role.png?raw=true)

*Bar graph visualizing the salary for the top 3 data roles and their top 5 skills associated with each.*

### Insights
* SQL is the most requested skill for Data Analysts and Data Engineers, with it in over half the job postings for both roles. For Data Scientists, Python is the most sought-after skill, appearing in 72% of job postings.

* Both SQL and Python are the most frequently requested skills across all three roles (Data Analyst, Data Engineer, Data Scientist), underscoring their essential role in data-related job positions. However, it does have more promincence in Data Science and Engineering roles.

* Role-Specific Tools and Technologies:
    
    * **Data Analysts**: High demand for tools like Excel and Tableau, alongside SQL.
    * **Data Engineers**: Significant demand for cloud platforms (AWS, Azure) and big data technologies (Spark, Hadoop, Kafka).
    * **Data Scientists**: High demand for statistical and machine learning tools, with Python and R being particularly important.

* **Emerging Skills**: Data Engineers and Data Scientists show a growing need for cloud-related skills and machine learning frameworks (e.g., AWS, TensorFlow), indicating the importance of these technologies in advanced data roles.

## 2. How are in-demand skills trending for Data Analysts?
To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the job postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023. to identify whether they're decreasing in demand or not.

View my notebook with detailed steps here:
[3_Skills_Trend](Project\3_Skills_Trend.ipynb).

### Visualizing the Data

```
from matplotlib.ticker import PercentFormatter

df_plot = df_DA_US_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, legend='full', palette='tab10')

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()
```
### Results
![Visualization of Skills Trend for Data Analysts](https://github.com/diegoestradagit/Diego_Python_Project/blob/main/Project/Images/monthly_trend_hard_skills_data_analysts.png?raw=true)

*Bar graph visualizing the trending top skills for data analysts in the US in 2023.*

### Insigths
* SQL remains the most consistently demanded skill throughout the year, although it shows a gradual decrease in demand.
* Excel experienced a significant increase in demand starting around September, surpassing both Python and Tableau by the end of the year.
* Both Python and Tableau show relatively stable demand throughout the year with some fluctuations but remain essential skills for data analysts. Power BI, while less demanded compared to the others, shows a slight upward trend towards the year's end.

## 3. How well do jobs and skills pay for Data Analysts?
Probably the question that will sway the most people when choosing which skill to learn or what role to aim for. To identify the highest-paying roles and skills, I only got jobs in the United States and looked at their median salary. But first I looked at the salary distributions of common data jobs like Data Scientist, Data Engineer, and Data Analyst, to get an idea of which jobs are paid the most, using a box plot.

View my notebook with detailed steps here: [4_Salary_Analysis](Project\4_Salary_Analysis.ipynb).


### Visualizing the Data
```
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)

ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```
### Results
![Salary Distribution of Data Jobs](https://github.com/diegoestradagit/Diego_Python_Project/blob/main/Project/Images/salary_distribution_jobs.png?raw=true)
*Box plot visualizing the salary distributions for the top 6 data job titles.*

### Insights
* There's a significant variation in salary ranges across different job titles. Senior Data Scientist positions tend to have the highest salary potential, with up to $600K, indicating the high value placed on advanced data skills and experience in the industry. Nonetheless, it´s important to note these are significant outliers and the normal upper range is closer to $280K.

* Senior Data Engineer and Senior Data Scientist roles show a considerable number of outliers on the higher end of the salary spectrum, suggesting that exceptional skills or circumstances can lead to high pay in these roles. In contrast, Data Analyst roles demonstrate more consistency in salary, with fewer outliers.

* The median salaries increase with the seniority and specialization of the roles. Senior roles (Senior Data Scientist, Senior Data Engineer) not only have higher median salaries but also larger differences in typical salaries, reflecting greater variance in compensation as responsibilities increase.

### Highest Paid & Most Demanded Skills for Data Analysts
Next, I narrowed my analysis and focused only on data analyst roles. I looked at the highest-paid skills and the most in-demand skills. I used two bar charts to showcase these.

#### Visualizing the Data
```
fig, ax = plt.subplots(2, 1)  

# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue='median', ax=ax[0], palette='dark:b_r')

# Top 10 Most In-Demand Skills for Data Analysts
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='light:b')

plt.show()
```
### Results
Here's the breakdown of the highest-paid & most in-demand skills for data analysts in the US:
![Visualization of Highest Paid Skills for Data Analysts](https://github.com/diegoestradagit/Diego_Python_Project/blob/main/Project/Images/highest_paid_skills_data_analysts.png?raw=true)

*Two separate bar graphs visualizing the highest paid skills and most in-demand skills for data analysts in the US.*

### Insights
* The top graph shows specialized technical skills like AWS and Azure (cloud technologies), as well as Python are associated with higher salaries, some reaching up to over $100K, suggesting that advanced technical proficiency can increase earning potential.

* The bottom graph highlights that foundational skills like Excel, PowerPoint, and SQL are the most in-demand, even though they may not offer the highest salaries. This demonstrates the importance of these core skills for employability in data analysis roles.

* There's a clear distinction between the skills that are highest paid and those that are most in-demand. Data analysts aiming to maximize their career potential should consider developing a diverse skill set that includes both high-paying specialized skills and widely demanded foundational skills.

## 4. What are the most optimal skills to learn for Data Analysts?

To identify the most optimal skills to learn (the ones that are the highest paid and highest in demand), I calculated the percent of skill demand and the median salary of these skills. To easily identify which are the most optimal skills to learn.

View my notebook with detailed steps here: [5_Optimal_Skills](Project\5_Optimal_Skills.ipynb).

### Visualizing Data
```
from adjustText import adjust_text
import matplotlib.pyplot as plt

plt.scatter(df_DA_skills_high_demand['skill_percent'], df_DA_skills_high_demand['median_salary'])
plt.show()
```
### Results
![Visualization 1 of Most Optimal Skills](https://github.com/diegoestradagit/Diego_Python_Project/blob/main/Project/Images/most_optimal_skills_data_analysts_1.png?raw=true)
*A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in the US.*

### Insights
* The skill Oracle appears to have the highest median salary of nearly $97K, despite being less common in job postings. This suggests a high value placed on specialized database skills within the data analyst profession.

* More commonly required skills like Excel and SQL have a large presence in job listings but lower median salaries compared to specialized skills like Python and Tableau, which not only have higher salaries but are also moderately prevalent in job listings.

* Skills such as Python, Tableau, and SQL Server are towards the higher end of the salary spectrum while also being fairly common in job listings, indicating that proficiency in these tools can lead to good opportunities in data analytics.

### Visualizing the Different Technologies
Let's visualize the different technologies as well in the graph. We'll add color labels based on the technology (e.g., {Programming: Python})

```
from matplotlib.ticker import PercentFormatter

# Create a scatter plot
scatter = sns.scatterplot(
    data=df_DA_skills_tech_high_demand,
    x='skill_percent',
    y='median_salary',
    hue='technology',  # Color by technology
    palette='bright',  # Use a bright palette for distinct colors
    legend='full'  # Ensure the legend is shown
)
plt.show()
```
![Visualization 2 of Most Optimal Skills](https://github.com/diegoestradagit/Diego_Python_Project/blob/main/Project/Images/most_optimal_skills_data_analysts_2.png?raw=true)
*A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in the US with color labels for technology.*

### Insights:
* The scatter plot shows that most of the programming skills (colored blue) tend to cluster at higher salary levels compared to other categories, indicating that programming expertise might offer greater salary benefits within the data analytics field.

* The database skills (colored green), such as Oracle and SQL Server, are associated with some of the highest salaries among data analyst tools. This indicates a significant demand and valuation for data management and manipulation expertise in the industry.

* Analyst tools (colored orange), including Tableau and Power BI, are prevalent in job postings and offer competitive salaries, showing that visualization and data analysis software are crucial for current data roles. This category not only has good salaries but is also versatile across different types of data tasks.

## Insights
This project provided several general insights into the data job market for analysts:

* Skill Demand and Salary Correlation: There is a clear correlation between the demand for specific skills and the salaries these skills command. Advanced and specialized skills like Python and Oracle, Azure and AWS often lead to higher salaries.
* Market Trends: There are changing trends in skill demand, highlighting the dynamic nature of the data job market. Keeping up with these trends is essential for career growth in data analytics.
* Economic Value of Skills: Understanding which skills are both in-demand and well-compensated can guide data analysts in prioritizing learning to maximize their economic returns. Sometimes, a trade-off between effort and reward of learning a skill has to be considered before choosing which skill is best to learn.

## Conclusion
This exploration into the data analyst job market has been incredibly informative, highlighting the critical skills and trends that shape this evolving field. The insights I got enhance my understanding and provide actionable guidance for anyone looking to advance their career in data analytics. As the market continues to change, ongoing analysis will be essential to stay ahead in data analytics. This project is a good foundation for future explorations and underscores the importance of continuous learning and adaptation in the data field.



