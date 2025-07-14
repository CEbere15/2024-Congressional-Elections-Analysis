# 2024-Congressional-Elections-Analysis
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


