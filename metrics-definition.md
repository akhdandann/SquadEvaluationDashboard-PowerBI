# Metric Definitions – Squad Evaluation Dashboard

This file documents all metrics used in the Squad Evaluation Dashboard, including core KPIs and supporting calculations used for team and sprint-level insights. All DAX formulas are assumed based on data context and can be customized to match your Power BI model.

> Note: All data is dummy and all names have been changed.

---

## 1. Happiness Metrics

### Avg_Happiness
- *Description:* Average happiness score submitted by squad members.
- *DAX:*
DAX
Avg_Happiness = AVERAGE(Survey[Happiness])


### Avg_Happiness_By_Sprint
- *Description:* Happiness trend over each sprint/iteration.
- *DAX:*
DAX
Avg_Happiness_By_Sprint = AVERAGEX(VALUES(Survey[Sprint]), CALCULATE(AVERAGE(Survey[Happiness])))


### Avg_Happiness_By_Role
- *Description:* Average happiness segmented by roles (e.g. Scrum Master, Squad Leader).
- *DAX:*
DAX
Avg_Happiness_By_Role = CALCULATE(AVERAGE(Survey[Happiness]), ALLEXCEPT(Survey, Survey[Role]))


---

## 2. Contribution & Satisfaction

### Avg_Contribution
- *Description:* Members' self-assessment of their contribution to the sprint.
- *DAX:*
DAX
Avg_Contribution = AVERAGE(Survey[Contribution])


### Avg_Tribe_Leader_Satisfaction
- *Description:* Satisfaction ratings provided by Tribe Leaders.
- *DAX:*
DAX
Avg_Tribe_Leader_Satisfaction = AVERAGE(LeaderSurvey[Satisfaction])


---

## 3. Commitment vs Delivery

### Commitment_Percentage
- *Description:* % of tasks committed relative to sprint goals.
- *DAX:*
DAX
Commitment_Percentage = DIVIDE([Committed_Tasks], [Total_Tasks], 0)


### Quick_Delivery_Percentage
- *Description:* % of committed tasks delivered on time.
- *DAX:*
DAX
Quick_Delivery_Percentage = DIVIDE([Delivered_On_Time], [Committed_Tasks], 0)


---

## 4. Agile Behavior Radar Indicators

### Avg_Quick_Delivery
DAX
Avg_Quick_Delivery = AVERAGE(Survey[QuickDelivery])


### Avg_Experimenting
DAX
Avg_Experimenting = AVERAGE(Survey[Experimenting])


### Avg_Feedback
DAX
Avg_Feedback = AVERAGE(Survey[Feedback])


### Avg_Appraisal
DAX
Avg_Appraisal = AVERAGE(Survey[Appraisal])


### Avg_Deliver_Great_Stuff
DAX
Avg_Deliver_Great_Stuff = AVERAGE(Survey[DeliverGreatStuff])


### Avg_NWOW
DAX
Avg_NWOW = AVERAGE(Survey[NWOW])


---

## 5. Feedback & Word Cloud Inputs

### Avg_Feedback_Appraisal
- *Description:* Peer feedback and retrospective appraisals.
- *DAX:*
DAX
Avg_Feedback_Appraisal = AVERAGE(Feedback[Score])


### WordCloud_Good, WordCloud_Bad, WordCloud_Improvement
- *Description:* Aggregated text fields grouped by feedback category.
- *Used In:* Word cloud visuals using Power BI text visuals or custom visuals.

---

## 6. Sprint Participation & Data Quality

### Submission_Count
- *Description:* Number of feedback forms submitted.
DAX
Submission_Count = COUNTROWS(Survey)


### Total_Members
- *Description:* Total expected squad members.
DAX
Total_Members = DISTINCTCOUNT(Squad[MemberID])


### Submission_Rate
- *Description:* Feedback participation rate.
DAX
Submission_Rate = DIVIDE([Submission_Count], [Total_Members], 0)


### Avg_Data_Entry
- *Description:* Average number of feedback items submitted.
DAX
Avg_Data_Entry = AVERAGE(DataEntry[Submitted])


---

## 7. Sprint Participation Tracking

### Total_Sprints
DAX
Total_Sprints = DISTINCTCOUNT(Survey[Sprint])


---

## 8. Rankings

### Top_Squad_Happiness
DAX
Top_Squad_Happiness = 
TOPN(5, VALUES(Squad[Name]), [Avg_Happiness], DESC)


### Bottom_Squad_Happiness
DAX
Bottom_Squad_Happiness = 
TOPN(5, VALUES(Squad[Name]), [Avg_Happiness], ASC)


### Top_Member_Happiness
DAX
Top_Member_Happiness = 
TOPN(5, VALUES(Survey[MemberName]), [Avg_Happiness], DESC)


### Bottom_Member_Happiness
DAX
Bottom_Member_Happiness = 
TOPN(5, VALUES(Survey[MemberName]), [Avg_Happiness], ASC)


---

## 9. Utility Metrics

### Avg_Submission_Per_Sprint
DAX
Avg_Submission_Per_Sprint = AVERAGEX(VALUES(Survey[Sprint]), [Submission_Count])


### Most_Active_Squad
DAX
Most_Active_Squad = 
TOPN(1, VALUES(Squad[Name]), [Submission_Count], DESC)


---
