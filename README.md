# Job-Portal-Analytics
### Live Project Demo  <a href="https://jobportal-analysis.netlify.app/"><strong>➥ JobPortal-Analytics</strong></a>

**Data Pre-Processing Guide:**
 
- This Python 3 environment comes with many helpful analytics libraries installed
 It is defined by the kaggle/python Docker image: https://github.com/kaggle/docker-python
 For example, here's several helpful packages to load

```
import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)
```

- Input data files are available in the read-only "../input/" directory
 For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory

```
import os
 for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))
```

- You can write up to 20GB to the current directory (/kaggle/working/) that gets preserved as output when you create a version using "Save & Run All" 
- You can also write temporary files to /kaggle/temp/, but they won't be saved outside of the current session

- To Display All columns in a Dataset
```
 import pandas as pd
 import numpy as np
 pd.set_option('display.max_columns', None)
```

- Give Path To Store Dataset
```
 df=pd.read_csv("/kaggle/input/job-description-dataset/job_descriptions.csv")
 df.head(2)
```

- To Check Number of Rows and Columns in Dataset
```
 print(f' The dataset has {df.shape[0]} rows and {df.shape[1]} columns.')
 df.shape
```

- To Display Number of Null Values in Dataset
```
 print(f' The dataset has {df.isna().sum().sum()} null values.')
```

- To Display Number of Null Values in Dataset
```
 df.dropna(inplace=True)
```

- To Display Number of Null Values in Dataset After dropping Null Values
```
print(f' The dataset has {df.isna().sum().sum()} null values.')
``` 

- To Display Number of Duplicate Values in Dataset
```
print(f' The dataset has {df.duplicated().sum()} duplicate values.')
```

 - To Display list of columns and with their Names in Dataset
```
print('List Of Columns:\n',df.columns)
```

 - To Display  statistical columns and with their Values in Dataset
```
print('Statistical Summary:\n',df.describe())
```

 - To Display Information Of all Columns (like: data types, null count)
```
df.info()
```

 - Final Step that you have to import your saved Data set ( what u have installed data and stored)
```
df.to_csv('mycsvfile.csv',index=False)
```
 
**Solution Summary by Task:**

- **Task 1:** the solution involves creating a visualization of the top 20 companies by applying filters where the role is ‘Experience Designer’, the job title is ‘UI/UX Designer’, and the company name must contain more than five characters. A bar or column chart in Tableau can be used for this ranking.

- **Task 2:** a more complex filtering logic is required. The dataset should be narrowed down to include candidates with B.Tech, M.Tech, or PhD qualifications, seeking full-time roles in African countries, with job titles starting with 'D', male preference, and company size above 80,000. Additional filters include contact names starting with 'A', and applications through the Indeed portal. A map visualization must be included and should respond to latitude and longitude clicks. The dashboard should only be displayed during the 3 PM to 6 PM IST window.


- **Task 3:** requires focusing on internship roles with latitude less than 10. Data from countries starting with A, B, C, or D should be excluded. Further constraints include job titles shorter than 10 characters and company size under 50,000. This dashboard must also be time-bound and displayed only between 3 PM to 5 PM IST.


- **Task 4** the solution involves identifying the top 10 companies for positions where the role is ‘Data Engineer’ and the job title is ‘Data Scientist’. The data must exclude Asian countries and focus only on female-preferred roles in countries that start with the letter ‘C’ and have latitude below 10. Only B.Tech qualifications should be considered, and the posting date must fall between 01/01/2023 and 06/01/2023. This visualization is also limited to the 3 PM to 5 PM IST time slot.

 
- **Task 5:** is a comparative analysis between India and Germany, focusing on B.Tech-qualified, full-time candidates with more than 2 years of experience. Job titles must be Data Scientist, Art Teacher, or Aerospace Engineer, and the salary must exceed $10,000. The chart should be color-coded to distinguish the two countries (e.g., orange for India, green for Germany) and must include only female-preferred postings from the Indeed portal, published before 08/01/2023. The dashboard should be shown only between 3 PM and 5 PM IST.


- **Task 6:** involves filtering data for Mechanical Engineer roles with experience over 5 years, in Asian countries, at companies with an exact size of 50,000. Salaries must be above $50,000, and work type should be either part-time or full-time. Only male-preferred roles from the Indeed portal are included, and all other qualifications must be ignored. The output must be limited to the 3 PM to 5 PM IST window.

 **Step-by-Step Guide for Each Task in Tableau**

**Task 1: Top 20 Companies by Experience Designer Role**
1. Load your dataset into Tableau (Excel/CSV).
2. Drag and drop fields: `Role`, `Job Title`, and `Company Name`.
3. Apply filters:
   - `Role = "Experience Designer"`
   - `Job Title = "UI/UX Designer"`
   - `LEN([Company Name]) > 5` (create calculated field)
4. Use `COUNTD([Company Name])` to get distinct companies.
5. Sort by count and limit to Top 20.
6. Use a **Bar Chart** or **Column Chart** to visualize.
7. Add meaningful titles and axis labels.


 **Task 2: Full-Time Jobs in African Countries**
1. Load the dataset and apply filters:
   - `Qualification IN ("B.Tech", "M.Tech", "PhD")`
   - `Work Type = "Full time"`
   - `Country` in African list
2. Create a time filter (Calculated Field):
IF HOUR([Application Time]) BETWEEN 15 AND 18 THEN "Show" ELSE "Hide" END

3. Add additional filters:
- `STARTSWITH([Job Title], "D")`
- `Gender = "Male"`
- `Company Size > 80000`
- `STARTSWITH([Contact Person], "A")`
- `Job Portal = "Indeed"`
4. To create a map:
- Double-click `Latitude` and `Longitude`
- Add action (on click) to show/hide detailed view.
5. Use the "Show" condition in filter to restrict to 3–6 PM IST.


**Task 3: Internships with Geographic and Character Limits**
1. Apply filters:
- `Work Type = "Intern"`
- `Latitude < 10`
- Country name not starting with A, B, C, D (use calc field):
  ```
  NOT STARTSWITH([Country], "A") AND NOT STARTSWITH([Country], "B") ...
  ```
- `LEN([Job Title]) < 10`
- `Company Size < 50000`
2. Create time filter (3 PM to 5 PM):
IF HOUR([Application Time]) BETWEEN 15 AND 17 THEN "Show" ELSE "Hide"

3. Filter on "Show" and build a basic bar or table chart.

---

**Task 4: Top 10 Companies – Data Scientist Role (No Asian Countries)**
1. Apply filters:
- `Role = "Data Engineer"`
- `Job Title = "Data Scientist"`
- Exclude Asian countries
- `Gender = "Female"`
- `STARTSWITH([Country], "C")`
- `Latitude < 10`
- `Qualification = "B.Tech"`
- `Posting Date` between `01/01/2023` and `06/01/2023`
2. Create a Top 10 Filter using `Top N` feature.
3. Use a Bar Chart for visualizing top companies.
4. Add 3–5 PM IST visibility using a time field filter.


**Task 5: India vs Germany Comparison (Experience & Salary Filters)**
1. Filter:
- `Country IN ("India", "Germany")`
- `Qualification = "B.Tech"`
- `Work Type = "Full time"`
- `Experience > 2`
- `Job Title IN ("Data Scientist", "Art Teacher", "Aerospace Engineer")`
- `Salary > 10000`
- `Gender = "Female"`
- `Job Portal = "Indeed"`
- `Posting Date < 08/01/2023`
2. Create calculated field:
IF [Country] = "India" THEN "Orange"
ELSEIF [Country] = "Germany" THEN "Green" END


3. Use color legend to visually differentiate countries.
4. Choose Side-by-side bars or Stacked bar chart.
5. Use calculated field to restrict visibility to 3–5 PM IST.


**Task 6: Mechanical Engineering Jobs in Asia**
1. Apply filters:
- `Company Size = 50000`
- `Job Title = "Mechanical Engineer"`
- `Experience > 5`
- `Country` from Asia
- `Salary > 50000`
- `Work Type IN ("Full time", "Part time")`
- `Job Portal = "Indeed"`
- `Gender = "Male"`
2. Use bar chart or table to present result.
3. Use time field to show data only between 3–5 PM IST.
4. Optionally add:
- Job count metric
- Average salary metric
5. Add interactivity with dashboard highlight or filter actions.
