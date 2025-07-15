# 2024 Congressional Elections Analysis
A deep analysis on the 2024 Senatorial and House of Representatives elections. Analyzing district leaning, campaign finances, incumbent data, election results and presidential results.


## Overview

### Summary

This data project was made with the goal of gaining insights into the performances of each party, nominee in the 2024 Congressional Elections. It's made to be a deep analysis on the 2024 Senatorial and House of Representatives elections. Analyzing district leaning, campaign finances, incumbent data, election results and presidential results.

### Tools
- Excel - Data Cleaning / Preperation
  - Used to compile datasets from multiple sources and organize them in worksheets.
- DB Browser (SQLite) - Data Analysis, Exploration and Manipulation
  - Used for querying, exploring, and manipulating the data into a more usable format for insights.
- Python - Data Analysis and Visualization
  - Employed to create charts and visualizations that would be challenging to produce in Tableau, along with performing statistical analyses to understand how variables might have affected the number of votes.
- Tableau - Dashboard Creation
  - Utilized for visualizing the dataset and creating a dashboard.

</br>

### Data Dictionary
#### 2024 Nominees


| Column       | Data Type       | Description                                                                      |
|-------------------|-------------|-----------------------------------------------------------------------------|
| `ID`      | Text     | The index for the nominees.        |
| `Nominee`    | 	Text | The name of the nominee.     |
| `Party`| Text | Name of the main party that the nominee is the nominee of.|
|`Gender`| Text | The gender of the nominee.|
| `State`      | Text     | The state that the nominee's race is being contested in.  |
| `Region`| Text | Region denoting which Census designated division the state is located in .|
| `Wider Region` | Text     | Region denoting which Census designated region the state is located in.           |
| `Type`      | Text     | The type of seat being contested (i.e. House, Senate, Delegate).|
| `Class` | Text | The Senate class that the seat being contested belongs to.|
| `Race`      | Text     | The seat code for the race that is being contested.|
| `Incumbent`      | Boolean  | Whether the nominee is an incumbent for that constituency being contested.|
| `Victor`      | Boolean  | Whether the nominee won the race, or made it to the runoff.|
| `Votes`      | Integer     | The amount of votes the nominee won in the race.|
| `Share`      | Text     | The share of the votes that the nominee won.|
| `Total`      | Integer     | The total votes casted for the race.|
| `Held By`      | Text     | The party that holds the seat being contested.|
| `Hometown`      | Text     | The city and state where the nominee is registered to live in.|
| `Election Day`      | Datetime     | The date in which the election took place.|
| `Election Year`      | Integer     | The election year that the election took place in.|
| `Year Type`      | Text     | The type of election year the race took place in (i.e. Midterm or Presidential).|
| `Last Election`      | Datetime     | The last time the constituency had an election.|
| `Final`      | Boolean  | Whether the result is the final one, or if there is a runoff after.|
| `Special`      | Boolean  | Whether this race is a special election.|
| `Runoff`      | Boolean  | Whether this race is a runoff to figure out the final winner.|

</br>

#### Incumbents


| Column       | Data Type       | Description                                                                      |
|-------------------|-------------|-----------------------------------------------------------------------------|
| `ID`      | Text     | Index for incumbents.        |
| `Race`      | Text     | Constituency that the last incumbent represented.        |
| `Seat Holder`    | 	Text | The last person to hold the seat.     |
| `Gender`| Text | Gender of the last person to hold the seat.|
|`Term Start`| Datetime | The day that the incumbent was sworn into Congress.|
|`Birthday`| Datetime | The day the incumbent was born.|
| `Decision`      | Text     | The incumbent's decision and outcome coming into the next election.  |
| `Days of Term`| Integer | The amount of days since the last incumbent was sworn in and election day.|
| `Age` | Text     | The age of the last incumbent.  |
| `Swearin` | Text     | The age of the last incumbent when they were sworn in.  |
| `Original`      | Text     | Whether this election was the first (non-special or a runoff).|

</br>

#### PVI


| Column       | Data Type       | Description                                                                      |
|-------------------|-------------|-----------------------------------------------------------------------------|
| `ID`      | Text     | Index for PVI.        |
| `Race`      | Text     | Constituency that PVI is rating.        |
| `PVI Lean`    | 	Text | The Lean of the Cook PVI.     |
| `PVI`| Integer | Actual quantifible number of Cook PVI.|
|`Cook Rating`| Text | The rating given to the constituency by Cook Political Report (Lean, Solid, Likely).|

</br>
#### Presidential


| Column       | Data Type       | Description                                                                      |
|-------------------|-------------|-----------------------------------------------------------------------------|
| `Row`      | Text     | Index for district's Presidential results.        |
| `Race`      | Text     | Constituency that the Presidential performance is being analyzed.        |
| `District Winner`    | 	Text | The Presidential candidate that won the district (Trump or Harris).     |
| `Democratic Votes`| Integer | Votes won by the Democratic nominee in district.|
|`Dem Percent`| Text | Percentage of votes won by the Democratic nominee in district.|
| `Republican Votes`| Integer | Votes won by the Republican nominee in district.|
|`Rep Percent`| Text | Percentage of votes won by the Republican nominee in district.|
| `Other Votes`| Integer | Votes won by the other nominees in district.|
|`Other Percent`| Text | Percentage of votes won by the other nominee in district.|
| `All VOtes` | Integer     | Overall votes in the district.  |
| `Presidential Margin` | Text     | Margin of victory for the District Winner in the district.  |
| `Original`      | Text     | Whether this election was the first (non-special or a runoff).|

</br>
## Data Manipulation

### Categorizing Parties and Ranking Nominees
```sql
CREATE View Ordered AS 
SELECT Nominee, Party, Gender, State, Region, WiderRegion, Type, Race, Class, Incumbent, Victor, Votes, Share, Total, 
    dense_rank() OVER (PARTITION BY Race ORDER BY Votes DESC) AS Standing, Heldby, Hometown, ElectionDay, ElectionYear, YearType, LastElection, 
    Final, CASE
        WHEN Party IN ('Democratic', 'Democratic-Farmer-Labor', 'Democratic-Nonpartisan League', 'Popular Democratic Party', 'Democratic (Write-In)') THEN 'Democratic Party'
        WHEN Party IN ('Republican', 'Republican (Write-In)', 'New Progressive Party') THEN 'Republican Party'
        WHEN Party IN ('Free Libertarian', 'Libertarian') THEN 'Libertarian Party'
        WHEN Party in ('Reform') then 'Reform Party'
        WHEN Party in ('Constitution', 'American Independent', 'American Constitution Party', 'U.S. Taxpayers', 'Independent American') THEN 'Constitution Party'
        WHEN Party in ('Green', 'Mountain', 'D.C. Statehood Green', 'Pacific Green', 'Independent Green', 'Desert Greens') then 'Green Party'
        WHEN Party = 'Conservative' THEN 'Conservative Party'
        WHEN Party IN ('Young Socialist Alliance', 'Communist', 'Socialist Equality', 'Socialist', 'Socialist Labor', 'Peace And Freedom', 'Socialist Workers', 'Liberty Union') THEN 'Socialist Parties'
        WHEN Party IN ('No Party', 'No Party Affiliation', 'Other', 'Nominated by Petition', 'Conneticut for Lieberman', 'Write-In', 'Independent Political Choice', 'No Party Preference', 'Independent', 'Independent Constitutional Candidate', 'Independent Party of Delaware', 'Independence', 'Nonpartisan', 'No Political Party', 'Unaffiliated') THEN 'Independent'
        ELSE 'Other Minor Parties'
    END AS Category, Special, Runoff 
FROM Nominee-2924
ORDER BY Race, State;


```



This SQL query creates a view that selects all the columns from the Nominee, and creates a normalized designation for party affiliation called Categorym while also ranking nominees in each race by Standing. 



</br>

### Creating Margins for Each Race


```sql
-- Creating view for all first place nominees
CREATE VIEW NRanks1 AS SELECT * FROM Ordered WHERE Standing = 1

-- Creating view for all second place nominees
CREATE VIEW NRanks2 AS SELECT * FROM Ordered WHERE Standing = 2

-- Creating a iew for Margins based on first place share - second place share
CREATE VIEW Margs AS SELECT a.Race,  a.Share - b.Share AS Win
FROM NRanks1 a 
JOIN NRanks2 b ON a.Race = b.Race
```

These queries create views for all nominees who had a Standing of 1 or 2 in each election. Then a new view is created that takes 1's and subtracts their share of the votes by 2's, creating margins of victory for each race. 


### Joining Each Margin with Their Race



## Exploratory Data Analysis

### PVI

```py
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Assuming PVI is your dataframe
# Step 1: Extract the first word from Cook Rating
PVI['Cook_Category'] = PVI['Cook Rating'].str.split().str[0]

# Step 2: Create boxplots grouped by the first word of Cook Rating
# Separate plots by PVI Lean and measure by PVI
plt.figure(figsize=(14, 8))
sns.boxplot(x='Cook_Category', y='PVI', hue='PVI Lean', data=PVI)

# Improve plot appearance
plt.title('PVI Distribution by Cook Rating Category and PVI Lean')
plt.xlabel('Cook Rating Category (First Word)')
plt.ylabel('PVI Value')
plt.xticks(rotation=45)
plt.legend(title='PVI Lean')
plt.tight_layout()

# Optional: Add a stripplot to see individual data points
# sns.stripplot(x='Cook_Category', y='PVI', hue='PVI Lean', 
#               data=PVI, dodge=True, alpha=0.3, jitter=True)

plt.show()

# Optional: Display summary statistics
print(PVI.groupby(['Cook_Category', 'PVI Lean'])['PVI'].describe())

```

<img width="1389" height="790" alt="PVI by Cook Rating & Leaning" src="https://github.com/user-attachments/assets/eddb9bf5-902f-4952-b07f-68dbd3674ed0" />

### Description: 
<img width="941" height="573" alt="Cook Rating Description" src="https://github.com/user-attachments/assets/7c5443db-b63c-429a-958a-6abcb61bc332" />

