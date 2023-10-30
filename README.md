# Mental-Health_Analysis

###Analysing how Mental Health Issues correlate to CGPA###

Students not only sacrifice their sleep, food, and all other activities, to devote themselves to academics, leaving their well-being and mental health behind. Peer pressure, combined with unrealistic academic deadlines and outputs, unworkable teams, and competitive spirit at the very age where our urge for self-discovery peaks. This leads to the mental burden, and stress if not well-taken care can end up with chronic anxiety, depression, and panic attacks.

To find out whether students' mental health affects their CGPA, we set out to ask some questions, our obvious choice was Reddit, where millions of users, can be chosen from specific demographics. We made a questionnaire using Google Forms, and uploaded them on the subreddit r/India, and also crossposted them on different subreddits, we also shared the questionnaire with our friends in the college to get their responses.

<img width="1003" alt="Screenshot 2023-10-31 at 12 50 17 AM" src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/e76a550a-f215-4bd6-8a68-4884589ac51c">

###Data Description###

Data Size: 270 Rows X 9 Coloumns

<img width="836" alt="Screenshot 2023-10-31 at 1 01 32 AM" src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/6cca047d-3e48-4f71-bbd7-c47fba6d4971">

###Data PreProcessing###

Here we perform different data cleaning and processing, to get the dataset ready for further analysis and to get insights.

1. We are changing the Name of Columns in the Dataset and the order of columns for better readbility
   ```
   df.columns = ['Gender', "Age", "Year of Study", 'CGPA', "Depression", "Anxiety", "Panic Attack", "Treatment", "Date"]
   change_column = ["Date", 'Gender', "Age", "Year of Study", "Depression", "Anxiety", "Panic Attack", "Treatment", "CGPA"]
   change_column = ["Date", 'Gender', "Age", "Year of Study", "Depression", "Anxiety", "Panic Attack", "Treatment", "CGPA"]
   df = df.reindex(columns=change_column)
   df.head(3)


   ```
   

2. We are converting TimeStamp into DateTime Object, extracting the date from it and dropping the timestamp because it had no further use

    ```
   df['Timestamp'] = pd.to_datetime(df['Timestamp'], errors="coerce")
   df['Date'] = df['Timestamp'].dt.date
   df.drop('Timestamp', axis=1, inplace=True)
   ```
   
3. finding out the missing values and filling the missing Values

   ```
   df.isnull().sum()
   df["Age"].fillna(df["Age"].mean(), inplace=True)
   df['Age'] = df['Age'].astype(int)
   ```
4. Changing the structure of CGPA, extracting only the cgpa and not the range
   ```
    df['CGPA'] = df['CGPA'].str.replace(r' - \d+\.\d+$', '', regex=True)
    df['CGPA'] = df['CGPA'].str.replace(r'- 4.00 ', '', regex=True)
   ```
5. Replacing the String in "Year of Study" column and replacing it with an integer
   
   ```
     df['Year of Study'] = df['Year of Study'].replace({'year 1': 1, 'Year 1': 1, "year 2": 2, 'Year 2': 2, 'year 3': 3, 'Year 3': 3, 'Year 4': 4, "year 4":     4})
   ```

6. Changing the type of the columns in the dataFrame
   ```
     df['Age'] = df['Age'].astype(int)
     df['CGPA'] = df['CGPA'].astype(int)
   ```

