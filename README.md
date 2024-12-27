# End-to-end-dataProject

**Objective**: Analyze and visualize attendance data for an educational project. This includes cleaning, transforming, and encoding data and generating insights through visualizations and statistical summaries.

The data collected for this project originates from an educational initiative focused on workshops about coding and new technologies conducted in various schools. The program required student participants to complete a project throughout four sessions.

### Table of Contents :

1. [Data Cleaning and Transformation](#data-cleaning-and-transformation)
2. [Insert data from Google Collab into SQL Server Management](#insert-data-from-google-collab-into-sql-server-management)
3. Data visualization Poer BI.
4. Data insights.

## Data Cleaning and Transformation

  This step involves using Python in Google Colab to clean, preprocess, and explore the dataset. Tasks 
  include  normalizing formats and calculating relevant metrics such as student ages and attendance 
  summaries. [Link to the file](EducationProgramInsight.ipynb)

```python

#Import libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from datetime import datetime
from dateutil.relativedelta import relativedelta

```
**Note:** Schools shared the student information contained in these files and includes personal student data. This project will only utilize the information strictly necessary for its intended purposes.

```python

#Import CSV files from URLs into two separate DataFrames (bd1 and bd2).

bd1=pd.read_csv('https://docs.google.com/spreadsheets/d/e/2PACX-1vS9IwGj-SwAzPqx6_gNwxigmdziGS0Cgu7-UQqaRp5lyUOs41pkbirF8vIgQxlbsmFMr1nimwC_sHbQ/pub?gid=260434784&single=true&output=csv')
bd2=pd.read_csv('https://docs.google.com/spreadsheets/d/e/2PACX-1vSbbYrc301ntoQC-3hdbLjR9UtcBCVpm3fnJrCJSEtQw5-M6bevEnCiCK8L_iWpZLKfklnbHtrXFvR9/pub?gid=0&single=true&output=csv')

```
Data kept:
* `Fecha evento:` Date of students workshop attendance. Type(Date)
* `N° De Documento:`Unique identification number assigned to each student. Type(INT)
* `Genero:`The student's gender (e.g., Male, Female). Type(Object)
* `Fecha de Nacimiento:`The date of birth of the student. Type(Date)
* `Grado:`The academic grade or year of the student (e.g., 8th grade, 9th grade) Type(OBJECT)
* `Asistencia:` Indicates whether the student attended the workshop (e.g., Yes/No). Type(OBJECT)


```python

#Keep only the necessary columns related to event dates, student information, and attendance.
bd1=bd1[['Fecha evento','N° de Documento','Genero','Fecha de Nacimiento','Grado','Asistencia']].copy()
bd2=bd2[['Fecha evento','N° de Documento','Genero','Fecha de Nacimiento','Grado','Asistencia']].copy()
```
```python
#Merge the two DataFrames into one (df) for further analysis.
df=pd.concat([bd1,bd2], ignore_index=True)

#Convert string-based date columns into DateTime objects for easier manipulation.
df['Fecha evento']=pd.to_datetime(df['Fecha evento'])
df['Fecha de Nacimiento']=pd.to_datetime(df['Fecha de Nacimiento'],format="mixed")

#Calculate students' ages in years and months as of the current date and store the results in a new column, Edad.
from datetime import datetime

# Function to calculate the age in years and months
def calculate_age(birthdate):
    today = datetime.today()
    years = today.year - birthdate.year
    months = today.month - birthdate.month

    # Adjust if the birthdate's month hasn't occurred yet this year
    if months < 0:
        years -= 1
        months += 12

    # Calculate age in years and months as a decimal (e.g., 15.6)
    return years + months / 12

# Apply the function to the 'birth_date' column
df['Edad'] = df['Fecha de Nacimiento'].apply(calculate_age)

#Convert categorical data (Asistencia and Genero) into numerical formats for analysis.
# Map 'Yes' to 1 and 'No' to 0
df['Asistencia'] = df['Asistencia'].map({'SI': 1, 'NO': 0})
df['Genero']= df['Genero'].map({'M':1,'F':0})

#Create  an Events column to track the number of workshops attended by each student.
df["Events"] = df.groupby('N° de Documento').cumcount() + 1

#Remove rows with invalid event counts (Events > 4) or grades with insufficient representation.
df=df[df['Events']<=4]
df['Events'].value_counts()

df=df[df['Grado']!='8']
df=df[df['Grado']!='9']
df=df[df['Grado']!='8-2']

```
## Insert data from Google Collab into SQL Server Management

```SQL
CREATE TABLE WorkshopAttendance (
    Fecha_evento DATE,
    N_Documento INT,
    Genero VARCHAR(1),
    Fecha_Nacimiento DATE,
    Grado VARCHAR(10),
    Asistencia VARCHAR(2),
    Edad INT,
    Events INT
);

```
