🎬 **Netflix Content Strategy Analysis — Exploratory Data Analysis (EDA)**

📌 Business Problem: Analyze the data and generate insights that could help Netflix in deciding which type of shows/movies to produce and how they can grow the business in different countries.

Netflix is one of the most popular media and video streaming platforms in the world. As of mid-2021, they have over 10,000 movies and TV shows on their platform and over 222 million subscribers globally.

With increasing competition in the streaming market, Netflix needs to make data-driven decisions on:
1. What type of content to produce
2. Which genres and ratings perform best
3. Which countries to focus on for growth
4. How viewing preferences have shifted over time
   
This project analyzes Netflix's entire content library to answer exactly these questions — using data, not assumptions.

---------------------------------------------------------------------------------------------------------------------------------------------------



🗂️ **Table of Contents**

1. About the Dataset
2. Tools & Technologies Used
3. Project Workflow
4. Step 1 — Problem Statement & Basic Metrics
5. Step 2 — Data Shape, Types & Missing Values
6. Step 3 — Non-Graphical Analysis
7. Step 4 — Visual Analysis
8. Step 5 — Missing Value & Outlier Check
9. Step 6 — Insights from Analysis
10. Step 7 — Business Insights
11. Step 8 — Recommendations
12. How to Run This Project
13. Author

---------------------------------------------------------------------------------------------------------------------------------------------------------

📊 **About the Dataset**

The dataset contains a list of all movies and TV shows available on Netflix, along with detailed metadata for each title.

1. show_id: Unique ID for every Movie / TV Show
2. type: Identifier — Movie or TV Show
3. title: Title of the content
4. director: Director(s) of the Movie / Show
5. cast: Actors involved
6. country: Country where the content was produced
7. date_added: Date it was added on Netflix
8. release_year: Actual release year (ranges from 1925 to 2021)
9. rating: TV Rating — e.g. TV-MA, TV-14, PG-13, R
10. duration: Total duration — minutes (Movies) or seasons (TV Shows)
11. listed_in: Genre / Category
12. description: Short synopsis of the title

Dataset Size: 8,807 rows × 12 columns

Dataset Source: https://d2beiqkhq929f0.cloudfront.net/public_assets/assets/000/000/940/original/netflix.csv

How to Download DataSet: After clicking on the above link, you can download the files by right-clicking on the page and clicking on "Save As", then naming the file as per your wish, with .csv as the extension.

------------------------------------------------------------------------------------------------------------------------------------------------------------------
🛠️ **Tools & Technologies Used**

1. Python 3: Core programming language
2. Pandas: Data loading, cleaning, and wrangling
3. NumPy:Numerical operations
4. Matplotlib: Building plots and charts
5. Seaborn: Statistical and aesthetic visualizations\
6. Google Colab: Cloud-based Jupyter notebook environment

-----------------------------------------------------------------------------------------------------------------------------------------------------------------

🔄 **Project Workflow**:

**Load Data → Explore → Clean → Preprocess → Visualize → Insights → Recommendations**

The project follows a structured EDA approach across 8 clearly defined steps, matching the evaluation criteria of the case study.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Step 1 — Problem Statement & Basic Metrics:**

**What was done**:
1. Loaded the Netflix CSV dataset using pd.read_csv()
2. Displayed the first and last few rows using df.head() and df.tail()
3. Confirmed the dataset has 8,807 rows and 12 columns
4. Identified two content types: Movies and TV Shows
5. Noted that the dataset spans content from the early 1940s to 2021


**Key Observation**:

The dataset is rich with metadata covering country of production, genre, rating, duration, and date added — all of which are useful for strategic content decisions.

--------------------------------------------------------------------------------------------------------------------------------------------------------------




















