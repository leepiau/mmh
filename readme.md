# A Look into Music and it's effects on Mental Health
[JDE03] Data Engineering Project

### 1. Overview

Can music improve an individual's mood and overall mental health? If so, what music can someone listen to in order to counter certain mental conditions?

We seek to analyse the results from a survey of respondents regarding listening habits and mental health conditions, and based on the results, recommend tracks from Spotify for the user based on her condition.

### 2. Data Sources

Mental Health Survey Data from Kaggle
https://www.kaggle.com/datasets/catherinerasgaitis/mxmh-survey-results/data

Spotify
https://open.spotify.com/

### 3. Methodology/Approach/Challenges/Findings

Full presentation here:
https://github.com/leepiau/mmh/blob/main/presentation/mmh_project.pptx

Summary:
1. MxMH dataset retrieved from Kaggle as .csv file
2. Three songs per each of 16 genres retrieved from Spotify via API
3. Data cleaned and transformed using Python, SQL 
4. Data is loaded into data store (ElephantSQL DB)
5. Data made available to Data Analyst 
6. Data made available to Recommendation Engine
7. Recommendation Engine calls Spotify API for other recommendations

### 6. Next Steps/Conclusion
- more visualisation
- better genre/track recommendations
- normalize track data, code ready

## Source Code Files:
1.survey_dataset_etl.ipynb
    - here we retrieve the mental health survey dataset, clean, transform and load the data into db
1a_create_views.ipynb
    - here we create lightweight views to rank the most popular genres per age group & mental health condition.
2.spotify_tracks_etl.ipynb
    - here we retrieve tracks from Spotify for each genre
3.analyses.ipynb
    - here we perform some analyses
4.recommend_tracks.ipynb
    - here we carry out the magical recommendations based on user input
5.Phase 2_normalize_spotify_tracks_data.ipynb
    - normalize the table continue track data
    
******************

# Project Start
Get survey data on mental health and music
Download .csv from:
https://www.kaggle.com/datasets/catherinerasgaitis/mxmh-survey-results/data

#### In Python:


```python
# Example python code:

# Step 1: import libraries
import pandas as pd
from sqlalchemy import create_engine

# Step 2: Read the CSV file
df = pd.read_csv('your_file.csv')

# Step 3: Drop unnecessary columns
df = df.drop(columns=['Timestamp', 'BPM', 'Permission'])

# Step 4: Rename the columns
df = df.rename(columns={'old_name1': 'new_name1', 'old_name2': 'new_name2'})

# Step 5: data cleaning (null, duplicates)
.
.
.

# Step 6: create new column (age_group) 

# Step 7: Create a connection to the PostgreSQL database
engine = create_engine('postgresql://username:password@localhost:5432/mydatabase')

# Step 8: Create new tables in PostgreSQL
commands = (# TABLE 1: results
            '''Create TABLE IF NOT EXISTS weather(id SERIAL PRIMARY KEY,
                                                age INT,
                                                streaming_service VARCHAR,
                                                hours INT,
                                                .
                                                .
                                                .
                                                .
                                                .);''')

# Step 9: Copy the data to the PostgreSQL table
df.to_sql('table_name', engine, if_exists='replace', index=False)
```

### Option A:

1. Extract 3 song recommendations from Spotify for each genre
2. Copy data into a table

### Create some visualisations:

1. most used streaming service
2. listen to music while working
3. fav genre by age group that improves mental health conditions, per mental health condition

### User Interaction:

1. Request input 'Are you affected by any of the following? 1.Anxiety 2.Depression 3.Insomnia 4.OCD 5. I'm feeling fine'
2. Based on answer, 
    if Option A (above) was chosen:
        search in tables for 3 song recommendations for the particular condition
    else 
        make an api call to spotify to get 3 song recommendations for the particular condition

** END **
