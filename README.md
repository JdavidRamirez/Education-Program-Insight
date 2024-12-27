# End-to-end-dataProject

**Objective**: Analyze and visualize attendance data for an educational project. This includes cleaning, transforming, and encoding data and generating insights through visualizations and statistical summaries.

The data collected for this project originates from an educational initiative focused on workshops about coding and new technologies conducted in various schools. The program required student participants to complete a project throughout four sessions.

### Table of Contents :

1. [Data Cleaning and Transformation](#data-cleaning-and-transformation)
2. Insert data from Google Collab into SQL Server Management.
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
