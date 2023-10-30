# Mind Matters: Exploring the Relationship Between Mental Health and Academic Performance (CGPA) in College Students

### Analysing how Mental Health Issues correlate to CGPA ###

Students not only sacrifice their sleep, food, and all other activities, to devote themselves to academics, leaving their well-being and mental health behind. Peer pressure, combined with unrealistic academic deadlines and outputs, unworkable teams, and competitive spirit at the very age where our urge for self-discovery peaks. This leads to the mental burden, and stress if not well-taken care can end up with chronic anxiety, depression, and panic attacks.

To find out whether students' mental health affects their CGPA, we set out to ask some questions, our obvious choice was Reddit, where millions of users, can be chosen from specific demographics. We made a questionnaire using Google Forms, and uploaded them on the subreddit r/India, and also crossposted them on different subreddits, we also shared the questionnaire with our friends in the college to get their responses.

Caution : While the dataset was predominantly collected from online sources and surveying, it's important to acknowledge that the nature of self-reported data, as obtained from online surveys, might introduce certain biases. Participants may be more inclined to respond based on their own interests or experiences, potentially affecting the representativeness of the data.

<img width="1003" alt="Screenshot 2023-10-31 at 12 50 17 AM" src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/e76a550a-f215-4bd6-8a68-4884589ac51c">

### Data Description ###

Data Size: 270 Rows X 9 Columns

<img width="836" alt="Screenshot 2023-10-31 at 1 01 32 AM" src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/6cca047d-3e48-4f71-bbd7-c47fba6d4971">

### Data PreProcessing ###

Here we perform different data cleaning and processing, to get the dataset ready for further analysis and to get insights.

1. We are changing the Name of Columns in the Dataset and the order of columns for better readability
   ```
   df.columns = ['Gender', "Age", "Year of Study", 'CGPA', "Depression", "Anxiety", "Panic Attack", "Treatment", "Date"]
   change_column = ["Date", 'Gender', "Age", "Year of Study", "Depression", "Anxiety", "Panic Attack", "Treatment", "CGPA"]
   change_column = ["Date", 'Gender', "Age", "Year of Study", "Depression", "Anxiety", "Panic Attack", "Treatment", "CGPA"]
   df = df.reindex(columns=change_column)
   df.head(3)


   ```
   

2. We are converting TimeStamp into DateTime Object, extracting the date from it, and dropping the timestamp because it had no further use

    ```
   df['Timestamp'] = pd.to_datetime(df['Timestamp'], errors="coerce")
   df['Date'] = df['Timestamp'].dt.date
   df.drop('Timestamp', axis=1, inplace=True)
   ```
   
3. finding out the missing values and filling in the missing Values

   ```
   df.isnull().sum()
   df["Age"].fillna(df["Age"].mean(), inplace=True)
   df['Age'] = df['Age'].astype(int)
   ```
4. Changing the structure of CGPA, extracting only the CGPA and not the range
   ```
    df['CGPA'] = df['CGPA'].str.replace(r' - \d+\.\d+$', '', regex=True)
    df['CGPA'] = df['CGPA'].str.replace(r'- 4.00 ', '', regex=True)
   ```
5. Replacing the String in the "Year of Study" column and replacing it with an integer
   
   ```
     df['Year of Study'] = df['Year of Study'].replace({'year 1': 1, 'Year 1': 1, "year 2": 2, 'Year 2': 2, 'year 3': 3, 'Year 3': 3, 'Year 4': 4, "year 4":     4})
   ```

6. Changing the type of the columns in the data frame
   ```
     df['Age'] = df['Age'].astype(int)
     df['CGPA'] = df['CGPA'].astype(int)
   ```

### Data Analysis ###

We used Plotly, seaborn, and matplotlib for the generating plots, even though Plotly generates better plots than Seaborn in terms of visual aesthetics, We find it lacking in flexibility, so, we used both


Here we divided the Analysis part into three sections.
First Section to see the frequency of values in columns
Second Section to see the frequency of values in columns in relation to the other columns 
First Section to see the Correlations between columns and get insights

#### Section 1  ####


<table>
  <tr>
    <td align="center">
      <img src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/75d0e701-fc16-402c-91f1-d86795f3f945" alt="menVsWomen">
      <br>
      Men Vs Women
    </td>
    <td align="center">
      <img src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/70cf0eab-0ff9-4471-8cab-f27e0ea88fb4" alt="Age">
      <br>
      Age
    </td>
    <td align="center">
      <img src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/f0d84852-96e2-4979-b521-02668b3b4989" alt="YearofStudy">
      <br>
      Year of Study
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/2dfbe698-0891-45ce-b99c-489405f70387" alt="Depression">
      <br>
      Depression
    </td>
    <td align="center">
      <img src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/9577d75d-9bf0-4da5-a32c-398d74f992ee" alt="Anxiety">
      <br>
      Anxiety
    </td>
    <td align="center">
      <img src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/583e4e3e-92aa-4b1a-ba76-7ccf39c136ff" alt="Panic Attack">
      <br>
      Panic Attack
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/6f61caf4-a0f1-4c7e-ba3e-f58cf3c5b748" alt="Treatment">
      <br>
      Treatment
    </td>
  </tr>
</table>

#### Section 2 ####

1. Relation Between Age and Depression - Here we can see that there are more young students who suffer from depression, most likely case why this is because, probably young students have distorted view of depression, diagnosing themselves as being depressed even though they may be lonely, sad or even having a couple of bad days

![relation_age_depress](https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/65bc0e3b-572f-4372-8928-e1abc486a930)

2. Study year and students suffering from Depression and Anxiety

<table>
  <tr>
    <td align="center">
      <img src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/15b1446f-53a9-4d11-aa6e-82dc80cf6d34" alt="menVsWomen">
      <br>
     Year of Study vs Anxiety
    </td>
    <td align="center">
      <img src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/d1926e5c-1dd8-42b0-8443-56d2a3d71dc0" alt="Age">
      <br>
      Year of Study vs Depression
    </td>
  </tr>
</table>


3. How many who have Depression Anxiety and Panic Attacks taking treatment?
   There are 50 people who are suffering from Depression and also 50 people who are suffering from anxiety, some of these cases overlap, where people who are suffering from depression are also suffering from anxiety.
   and 14 people who are taking treatment
   We also see which gender is getting more treatment when they are suffering from a mental health problem
   
![treatment](https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/fd02a4e5-2496-4bf4-81c1-79b1723456cb)

4. Who gets more treatment? which year?
   Which year students are getting more treatment when they are suffering from a mental health problem

![study_treat](https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/11767a67-924b-4a4a-ac7f-2acf51b3250b)

#### Section 3 ####

In this Section we try to get insights into the data, we try to see whether mental health problems actually influence the CGPA

Few plots to better understand the data of CGPA

<table>
  <tr>
    <td align="center">
      <img src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/69e3f346-ac58-4571-8c4b-0a99d068ba4a" alt="menVsWomen">
      <br>
     Distribution of CGPA by Year of Gender
    </td>
    <td align="center">
      <img src="https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/7bb0ab39-f1af-4e36-bb2d-a70e79b013f0" alt="Age">
      <br>
      Distribution of CGPA by Year of Study
    </td>
  </tr>
</table>

1. Do people suffering from Depression Score Less?
   Surprisingly the answer we got is No, people suffering from depression score no less than people suffering from depression, there may be many reasons      for this, the top reason can maybe be the fact that people wrongly diagnose themselves as being depressed when they are probably just sad or maybe bad was something else going in their life when they gave the questionnaire, which maybe be biased. The finding is not counter-intuitive, because we were expecting these results when we were looking at the data.

Here we perform statistical analysis to find out whether there is the null hypothesis or the alternate hypothesis is true

Null Hypothesis - There is no significant difference in CGPA between depressed and not depressed individuals
Alternate Hypothesis - There is a significant difference in CGPA between depressed and not depressed individuals

Here we perform A two-sample t-test, also known as an independent samples t-test, which is a statistical hypothesis test used to determine if there is a significant difference between the means of two independent groups. This test is commonly used when you want to compare the means of two different populations or groups to determine if the difference between them is statistically significant.

   ```
   from scipy.stats import ttest_ind
   from scipy.stats import f_oneway
   
   dep_no = data[data["Depression"] == 'No']
   depression_data = data[data["Depression"] == 'Yes']

   t_stat, p_value = ttest_ind(depression_data["CGPA"], dep_no["CGPA"])
   if p_value < 0.05:
    print(f'There is a statistically significant difference in CGPA between depressed and not depressed individuals (p-value: {p_value}).')
   else:
    print(f'There is no statistically significant difference in CGPA between depressed and not depressed individuals (p-value: {p_value}).') 

   ```
> There is no statistically significant difference in CGPA between depressed and not-depressed individuals (p-value: 0.7383723404465734).

   ```
   sns.boxplot(x='Depression', y='CGPA', data=data)
   plt.title('CGPA vs Depression')
   plt.show()

   ```
 ![depression_p_test](https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/08102d4b-e84c-4465-bd19-3b619e507c04)

 2. Do people suffering from Anxiety score less?

   * Not surprisingly the answer is yes, people suffering from anxiety do score less than their peers, we can support the insight by taking when points into consideration.
   * First of all, people wrongly self-diagnosing anxiety is far less than people self-diagnosing depression, and people who have chronic anxiety do tend to know more about mental health problems, so they may answer the questionnaire objectively.
   * Anxiety is induced by stress, which is a common factor among all the students, and this can influence the academic output significantly. Anxiety has an impact on concentration level and also test performance level
   * Most importantly anxiety induces escapism, which may lead to procrastination and avoidance of projects and studying, students can negatively view whatever academic opportunities that can in their way.
   *  Anxiety also has a toll on sleep patterns, and most importantly students may lean into anything that may help them get away from anxiety - these can be alcohol, drugs - mostly weed, and constant partying.
    

   ```
   
   anx_no = data[data["anxiety"] == 'No']
   anxiety_data = data[data["Depression"] == 'Yes']

   t_stat, p_value = ttest_ind(anxiety_data["CGPA"], anx_no["CGPA"])
   if p_value < 0.05:
       print(f'There is a statistically significant difference in CGPA between Students suffering from anxiety and Students not suffering from anxiety(p-         value: {p_value}).')
   else:
       print(f'There is no statistically significant difference in CGPA between the groups (p-value: {p_value}).')
      
   ```
   >There is a statistically significant difference in CGPA between Students suffering from anxiety and Students not suffering from anxiety(p-value:          5.4222927421191395e-05).

![gpa_anxiety_test](https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/ef849895-3e48-437e-a2ac-73e1ffdc1db8)


3. Do students getting treatment score more than people who are not?

   The answer is no, well, one of the reasons why this might be is the limited amount of data that we have which can give improper results
   * But also might be due to the reason that treatments in mental health don't cure everything that a student has, and it may take a lot of time to regain or maintain a suitable academic performance
   * Each student's response to treatment is individual. What works for one student may not work as effectively for another. Factors like the severity of the condition, treatment compliance, and personal resilience play a significant role in treatment outcomes.
   * Academic challenges are multifaceted and can result from a combination of factors, including personal circumstances, study habits, family support, and environmental stressors. Mental health treatment may address one aspect but not the entire spectrum of academic challenges.
  

```
   dep_anx = data[(data['Depression'] == 'Yes') & (data['Anxiety'] == 'Yes')]

   depression_and_anxiety_treatment = dep_anx[dep_anx["Treatment"] == "Yes"]
   depression_and_anxiety_no_treatment = dep_anx[dep_anx["Treatment"] == "No"]

   t_stat, p_value = ttest_ind(depression_and_anxiety_treatment['CGPA'],
   depression_and_anxiety_no_treatment['CGPA'])


   if p_value < 0.05:
          print(f'There is a statistically significant difference in CGPA between the treatment and no-
            treatment groups (p-value: {p_value}).')
   else:
          print(f'There is no statistically significant difference in CGPA between the treatment and no-t              treatment groups ( (p-value: {p_value}).')

```
> There is no statistically significant difference in CGPA between the treatment and no-treatment groups ( (p-value: 0.7383723404465734).
> 
![treatment_test](https://github.com/NehalNetha/Mental-Health_Analysis/assets/84872197/77e5c202-8ab9-4d5d-bf9b-953f0ec8f9d9)

4.  Does Mental issues affect Gender in a different way, and its relation to CGPA

   We try to find whether women or men, cope better when it's mental health problems and perform better even    if they're suffering from one. I personally thought women would be able to cope much better than men, but    I turned out to be wrong, there's no statistically significant difference between gender and the ability
   to perform better in spite of mental health problems
   * The absence of a gender-based difference in coping with mental health problems and academic performance suggests that resilience and coping strategies are not inherently gender-dependent. Both men and women       have the capacity to handle challenges effectively.
   * Also the fact the academic pressure tends to be the same on both genders and also a lot of issues excluding some. This may lead to the overall same performance when it comes to academics

```
   f_stat, p_value = f_oneway(
       depression_data[depression_data['Gender'] == 'Male']['CGPA'],
       depression_data[depression_data['Gender'] == 'Female']['CGPA'],
       dep_no[dep_no['Gender'] == 'Male']['CGPA'],
       dep_no[dep_no['Gender'] == 'Female']['CGPA']
   )

   if p_value < 0.05:
       print(f'There is a statistically significant difference in CGPA among different groups (p-value:             {p_value}).')
   else:
       print(f'There is no statistically significant difference in CGPA among different groups (p-value:            {p_value}).')


```
   > There is a statistically significant difference in CGPA among different groups (p-value:             
     0.02399196377881738).



### Conclusion ###

Our analysis leads us to some key findings that shed light on mental well-being and academic performance. This may help better understand the implication of mental health on academic output among college students.

1. Number one is obviously the mental health issues being prevalent among students, and many of them not receiving any type of treatment.
2. Depression and Academic Performance: Surprisingly, we found no statistically significant difference in the academic performance (measured by CGPA) of students suffering from depression compared to those who are not. Several factors, including potential misdiagnoses, variations in personal experiences, and biases in self-reporting, may contribute to this finding.
3. Anxiety and Academic Performance: In contrast to depression, students suffering from anxiety tend to score lower in their CGPA compared to their peers. This insight aligns with the well-established connection between anxiety and reduced concentration, academic performance, and overall well-being. Stress-induced escapism, procrastination, and lifestyle choices such as substance use were observed as potential contributing factors.
4. Resilience Across Genders: Contrary to some stereotypes, our analysis showed that there is no statistically significant difference between genders in coping with mental health problems and their impact on academic performance. This suggests that resilience and coping strategies are not inherently gender-dependent, emphasizing that both men and women have the capacity to handle challenges effectively.



### Implications ###

Our findings have implications for educational institutions and students.

1. Most educational institutions burden students with more work for better academic output, this may be counter-productive as it can make students less attuned to their well-being and ignore all kinds of self-care which may lead to academic decline rather than better performance. A better option would be less important work, rather than giving rote work like writing a journal which doesn't have any kind of learning curve whatsoever, just jotting down whatever's on the screen to paper, work can be given that's interesting and creative.
2. Less lectures, and more time to explore, will be better given that this is the age of self-discovery and also because most of the students do learning outside the college.
3. Encouraging a balance between academic pursuits and well-being is essential. High-pressure academic environments should consider the potential impact on students' mental health and implement measures to reduce stress.

Our data is less and based on questionnaires, which can be very biased, further research and obtaining more data into this work will be crucial in further reporting our findings
