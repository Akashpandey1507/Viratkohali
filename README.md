# Viratkohali


![image](https://github.com/Akashpandey1507/Viratkohali/assets/124170332/dbad20ac-1593-4b70-9e3c-af93a06cb27d)


# Python_Script:

# %% [markdown]
# # Virat Kohali Centuries (75)

# %% [markdown]
# ![image.png](attachment:image.png)

# %% [markdown]
# Virat Kohli, the Indian cricket sensation, has achieved a remarkable feat by scoring 75 centuries in international cricket. Known for his exceptional batting skills and unwavering determination, Kohli has left an indelible mark on the cricketing world.
# 
# With his aggressive yet calculated approach, Kohli has consistently displayed a hunger for runs and an ability to dominate the opposition. His centuries have come across all formats of the game, including Test matches, One Day Internationals (ODIs), and Twenty20 Internationals (T20Is).
# 
# Kohli's century tally is a testament to his consistency and adaptability across different conditions and against various opponents. He has a knack for rising to the occasion in crucial matches and has been a key contributor to India's success on numerous occasions.
# 
# Beyond the sheer number of centuries, Kohli's innings have often been a masterclass in batting technique and shot selection. He combines classic stroke play with modern aggression, making him a complete batsman in every sense.
# 
# Kohli's records and achievements go beyond the number of centuries. He has amassed numerous accolades and has consistently been ranked among the top batsmen in the world. His passion for the game, coupled with his relentless pursuit of excellence, has made him an inspiration for aspiring cricketers worldwide.
# 
# In summary, Virat Kohli's 75 centuries stand as a testament to his exceptional talent, consistency, and dedication to the sport. His achievements have etched his name among the all-time greats of the game and have made him a source of pride for his country, India.

# %% [markdown]
# # Importing important Liabraries for analysis and visualisations

# %%
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

# %% [markdown]
# # File path

# %%
file = r'd:\rg67266\Downloads\Virat-Kohli-International-Cricket-Centuries.csv'

# %% [markdown]
# # Read the CSV Datasets

# %%
df = pd.read_csv(file)

# %%
df

# %% [markdown]
# # Check the columns and rows

# %%
df.shape

# %% [markdown]
# # Columns

# %%
df.columns

# %% [markdown]
# # Renaming the Columns

# %%
df = df.rename(columns={
    'No.' : "Century No"
})

# %%
df.columns

# %% [markdown]
# # Checking the null columns or rows

# %%
df.isnull().sum()

# %%
missing_values = df.isnull()
missing_values

# %%
# Transpose the boolean DataFrame to match the shape of the input data
missing_values = missing_values.transpose()


# %%
plt.figure(figsize=(25,10)) # for inscrease the size of graph
plt.title('Checking the Null Values in DataFrames' , fontsize=25)

# Visualize the missing values using a heatmap
sns.heatmap(missing_values)
plt.show()

# %% [markdown]
# * There is no any Null values in datasets 

# %% [markdown]
# # Check the info with Datatypes

# %%
df.info()

# %% [markdown]
# # Focusing On:
# * Need to change data type of columns 'Runs' and 'Date'

# %% [markdown]
# # Changing the Data Types of columns 'Runs' and 'Date'

# %%
df['Date'] = pd.to_datetime(df['Date'])

# %%
df['Runs'] = df['Runs'].str.replace("*",'')

# %%
df['Runs'] = df['Runs'].astype(np.int64)

# %%
df.info()

# %% [markdown]
# # Data Analysis with EDA

# %% [markdown]
# # Q1: What are the countries name where Virat Kohali withwhome against made Centuries?

# %%
plt.figure(figsize=(25, 10))  # Increase the size of the graph
plt.title('All Century Counts against Country', fontsize=25)

ax = sns.countplot(data=df, x='Against')

plt.xlabel('Country', fontsize=15)  # Set x-axis label
plt.ylabel('Count', fontsize=15)  # Set y-axis label

# Add text annotations to the bars
for p in ax.patches:
    ax.annotate(format(p.get_height(), '.0f'), (p.get_x() + p.get_width() / 2, p.get_height()), ha='center', va='center', xytext=(0, 10), textcoords='offset points')

plt.show()

# %% [markdown]
# # Result:
# * Virat has made most 16 century against Austrlia in all formate
# * Srilanka is the secend high with 15 century in all formate

# %% [markdown]
# # Q2: what are the Most Runs of Only century of Virat Kohali against Countries?

# %%
againt_run = df.groupby('Against')['Runs'].sum()
againt_run

# %%

plt.figure(figsize=(25, 10))  # Increase the size of the graph
plt.title('Most Runs with total of Centuries against Country', fontsize=25)
plt.xlabel('---------------------------------------------------------------------------------------- Countries --------------------------------------------------------------------------------------------',fontsize=20)
plt.ylabel('------------------------Total of Centuries-----------------------------',fontsize=20)


sns.lineplot(x=againt_run.index, y=againt_run.values, color='g', markers=True, marker='o', linewidth=3, markersize=10)



# %% [markdown]
# # Result:
# * Virat has beat most of runs against Sri Lanka with 2007 runs only in century number
# * and Secend one in Austrila with 2003 Runs in century number

# %% [markdown]
# # Q3: Best inning for Centuries?

# %%
def inn(data):
    if data == 1:
        return "First Inning"
    elif data == 2:
        return "Second Inning"
    elif data == 3:
        return "Third Inning"
    elif data == 4:
        return "Forth Inning"

# %%
df['Inning'] = df['Innings'].apply(inn)

# %%
df.columns

# %%
column = list(df.columns)
new_column = column[0:5] + column[-1:] + column[5:-1]
df[new_column]

# %%
inning = df.groupby('Inning')['Runs'].count()
inning

# %%

plt.figure(figsize=(25, 10))  # Increase the size of the graph
plt.title('Most Runs with total of Centuries in Inning', fontsize=25)
plt.xlabel('---------------------------------------------------------------------------------------- Countries --------------------------------------------------------------------------------------------',fontsize=20)
plt.ylabel('------------------------Total of Centuries-----------------------------',fontsize=20)


sns.lineplot(x=inning.index, y=inning.values, color='b', markers=True, marker='o', linewidth=3, markersize=10)




# %% [markdown]
# # Result:
# 
# * 41 century made in second inning by Virat Kohali

# %% [markdown]
# # Q4: Which one are the Best ground for Virat Kohali for Century in all over the world.

# %%
grouped_data = df.groupby('Ground')['Runs'].count()
grouped_data

# %%


plt.figure(figsize=(10, 10))  # Set the size of the pie chart
plt.title('Count of Runs by Ground')  # Set the title of the pie chart

# Create the pie chart
plt.pie(grouped_data, labels=grouped_data.index, autopct='%1.1f%%')

plt.axis('equal')  # Equal aspect ratio ensures a circular pie
plt.show()

# %% [markdown]
# # Result
# * The number of century made by kohali with equal number in home or away with 35 century.

# %%
vanue = df.groupby('Venue')['Runs'].count().reset_index()
vanue

# %%

plt.figure(figsize=(25, 25))  # Set the size of the bar plot
plt.title('Most Centuries made on Which Ground in all over the world', fontsize=25)  # Set the title of the bar plot
plt.xlabel('Runs', fontsize=20)  # Set x-axis label
plt.ylabel('Venue', fontsize=20)  # Set y-axis label

ax = sns.barplot(data=vanue, y='Venue', x='Runs')

# Add text annotations to the bars
for p in ax.patches:
    ax.annotate(format(p.get_width(), '.0f'), (p.get_width(), p.get_y() + p.get_height() / 2), ha='left', va='center', xytext=(5, 0), textcoords='offset points')

plt.show()


# %% [markdown]
# # Result:
# * Most highest number of Century in Adelaide Oval, Adelaide in Austrlia with 5 Centuries.
# * and Secend one is Sher-e-Bangla Cricket Stadium, Dhaka in Bangladesh with 4 Centuries.

# %% [markdown]
# # Q5: What is result of centuries number in winning or lossing cose

# %%

plt.figure(figsize=(25, 10))  # Increase the size of the graph
plt.title('All Century Counts in favor of Result', fontsize=25)

ax = sns.countplot(data=df, x='Result')

plt.xlabel('Result', fontsize=15)  # Set x-axis label
plt.ylabel('Count', fontsize=15)  # Set y-axis label

# Add text annotations to the bars
for p in ax.patches:
    ax.annotate(format(p.get_height(), '.0f'), (p.get_x() + p.get_width() / 2, p.get_height()), ha='center', va='center', xytext=(0, 10), textcoords='offset points')

plt.show()


# %% [markdown]
# # Result:
# * Virat has made 50+ centuries in winning favour

# %% [markdown]
# # Q6: Which year is the best for Virat for Centuries?

# %%
df['Years'] = df['Date'].dt.year

# %%

plt.figure(figsize=(25, 10))  # Increase the size of the graph
plt.title('All Century Counts in Years-Wise', fontsize=25)

ax = sns.countplot(data=df, x='Years')

plt.xlabel('Years', fontsize=15)  # Set x-axis label
plt.ylabel('Count', fontsize=15)  # Set y-axis label

# Add text annotations to the bars
for p in ax.patches:
    ax.annotate(format(p.get_height(), '.0f'), (p.get_x() + p.get_width() / 2, p.get_height()), ha='center', va='center', xytext=(0, 10), textcoords='offset points')

plt.show()

# %% [markdown]
# # Result:
# * for Virat Kohali's best year for centuries are 2017 and 2018 with equal number of 11.

# %% [markdown]
# # Q7: Total Centuries of Virat kohali

# %%
print(f'Total Century of Virat Kohali is: {df.shape[0]}')

# %% [markdown]
# # Q8: Last 5 cennturies against which countries?

# %%
last5 = df.tail()
last5

# %%
plt.figure(figsize=(25, 10))  # Set the size of the bar plot
plt.title('Most Centuries made on Which Ground in all over the world', fontsize=25)  # Set the title of the bar plot
plt.xlabel('Runs', fontsize=20)  # Set x-axis label
plt.ylabel('Venue', fontsize=20)  # Set y-axis label

ax = sns.barplot(data=last5, x='Against', y='Runs')

# Set label numbers on the bars
for p in ax.patches:
    ax.annotate(format(p.get_height(), '.0f'), (p.get_x() + p.get_width() / 2., p.get_height()),
                ha = 'center', va = 'center', xytext = (0, 10), textcoords = 'offset points', fontsize=12, color='black')

plt.show()



# %% [markdown]
# # Result:
# * Last 5 centuries where is 186 against Auctralia in Narendra Modi Statdium is high number.

# %%
df



