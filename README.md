# Education Program insight

This project analyzes student attendance at workshops on software development, new technologies, and material prototyping for students from sixth to eleventh grade in some schools in Medellín. The project includes a decision tree that predicts which students are more likely to attend the four-session workshop.

## Table of Contents :

1. Data transformation and cleaning
2. Do Boys and Girls Attend School Equally?
3. Does Moving to Higher Grades Affect Attendance?
4. Is Age 15 a Turning Point for Attendance?
5. When Age and Grade Combine: What Happens to Attendance?
6. Who is more likely to attend the four-session workshop?
7. Model Performance


## Dataset

The data was collected in situ during the development of the workshops. It includes demographic and participation-related information for each student, such as age group, grade level, attendance per session, and whether they completed the full four-session workshop (assistance_4_attendance). This dataset enables the analysis and prediction of student engagement patterns across multiple workshop events.


## Results

The decision tree model predicts which students are more likely to complete the four-session workshop. It achieved an accuracy of 66.3%, with strong performance in identifying attendees (recall = 0.80). The model is useful for targeting engaged participants, though less effective at detecting non-attendance.

## Requirements

Python (Pandas, Matplotlib, Scikit-learn)
