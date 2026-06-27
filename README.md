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

```markdown
| Column       | Description |
|--------------|-------------|
| show_id      | Unique ID for every Movie / TV Show |
| type         | Identifier — Movie or TV Show |
| title        | Title of the content |
| director     | Director(s) of the Movie / Show |
| cast         | Actors involved |
| country      | Country where the content was produced |
| date_added   | Date it was added on Netflix |
| release_year | Actual release year (ranges from 1925 to 2021) |
| rating       | TV Rating — e.g., TV-MA, TV-14, PG-13, R |
| duration     | Total duration — minutes (Movies) or seasons (TV Shows) |
| listed_in    | Genre / Category |
| description  | Short synopsis of the title |
```


Dataset Size: 8,807 rows × 12 columns

Dataset Source: https://d2beiqkhq929f0.cloudfront.net/public_assets/assets/000/000/940/original/netflix.csv

How to Download DataSet: After clicking on the above link, you can download the files by right-clicking on the page and clicking on "Save As", then naming the file as per your wish, with .csv as the extension.

------------------------------------------------------------------------------------------------------------------------------------------------------------------
🛠️ **Tools & Technologies Used**

```markdown
| Tool         | Purpose                                      |
|--------------|----------------------------------------------|
| Python 3     | Core programming language                    |
| Pandas       | Data loading, cleaning, and wrangling        |
| NumPy        | Numerical operations                         |
| Matplotlib   | Building plots and charts                    |
| Seaborn      | Statistical and aesthetic visualizations     |
| Google Colab | Cloud-based Jupyter notebook environment     |
```


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

**Step 2 — Data Shape, Types & Missing Values**

**What was done**:


1. Checked shape using df.shape → (8807, 12)
2. Checked data types using df.dtypes
3. Ran df.isnull().sum() to detect missing values
4. Ran df.describe(include='all') for a full statistical summary


**Data Types Found**:


1. release_year — integer (only numerical column)
2. All other 11 columns — object (text/string)


**Missing Values Detected**:
```markdown
| Column      | Missing Count | % Missing |
|-------------|---------------|------------|
| director    | 2,634         | ~30%       |
| cast        | 825           | ~9.4%      |
| country     | 831           | ~9.4%      |
| date_added  | 10            | ~0.11%     |
| rating      | 4             | ~0.05%     |
| duration    | 3             | ~0.03%     |
| All others  | 0             | 0%         |
```

**Observation**:

Missing values in director, cast, and country are expected — many older or regional titles have incomplete metadata. Missing values in date_added, rating, and duration are negligible. No imputation was performed as these do not affect the overall analysis significantly.

**Statistical Summary Highlights**:

1. release_year ranges from 1925 to 2021, mean ≈ 2014
2. Most common content type: Movie (6,131 out of 8,807)
3. Most common rating: TV-MA (3,207 titles)
4. Most common country: United States (2,818 titles)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------

**Step 3 — Non-Graphical Analysis: Value Counts & Unique Attributes**

**What was done**:


1. Used df['column'].value_counts() on key columns
2. Used df.nunique() to check number of unique values per column


**Content Type Breakdown**:

| Type    | Count        |
|---------|-------------|
| Movie   | 6,131 (~70%) |
| TV Show | 2,676 (~30%) |

**Top 5 Countries by Content Count (before unnesting)**:

| Country         | Count |
|----------------|------:|
| United States  | 2,818 |
| India          | 972   |
| United Kingdom | 419   |
| Japan          | 245   |
| South Korea    | 199   |

**Most Common Ratings**:

| Rating | Count | Audience              |
|---------|------:|------------------------|
| TV-MA   | 3,207 | Mature Adults (18+)    |
| TV-14   | 2,160 | Teenagers (14+)        |
| TV-PG   | 863   | Parental Guidance      |
| R       | 799   | Restricted             |
| PG-13   | 490   | Parents Cautioned      |

**Top Genres (listed_in)**:

| Genre                                 | Count |
|--------------------------------------|------:|
| Dramas, International Movies         | 362   |
| Documentaries                        | 359   |
| Stand-Up Comedy                      | 334   |
| Comedies, Dramas, International Movies | 274 |
| Kids' TV                             | 220   |


**Unique Value Counts**:

1. 4,528 unique directors
2. 7,692 unique cast entries
3. 748 unique countries
4. 514 unique genre combinations
5. 17 unique rating categories

**Observation**:

Movies significantly outnumber TV Shows. The US dominates content production. Netflix primarily targets teen and adult audiences. Dramas, International Movies, and Documentaries are the most common genres.

----------------------------------------------------------------------------------------------------------------------------------------------------------------


**Step 4 — Visual Analysis (Univariate & Bivariate)**

Pre-Processing Done Before Visualization

Before creating charts, the following pre-processing steps were performed:


1. Date Parsing — Converted `date_added` from string to datetime format and extracted `year_added` and `month_added` as new columns
2. Duration Extraction — Used regex (`str.extract(r'(\d+)')`) to extract numeric minutes from movie duration strings
3. Handling Missing Values — Filled `NaN` in `cast`, `director`, and `country` with `'Unknown'` to prevent errors during unnesting
4. Column Unnesting — Split and exploded the multi-valued columns using `.str.split(', ')` and `.explode()`:
   i. `country_df` — one row per country per title
   ii. `director_df` — one row per director per title
   iii. `cast_df` — one row per actor per title


This unnesting was critical — for example, a movie with 3 country co-productions appears 3 times in `country_df`, allowing accurate per-country frequency analysis.

------------------------------------------------------------------------------------------------------------------------------------------------------------------

**4.1 Univariate Analysis**

A) **Distribution of Release Year (Histogram + KDE)**


1. Content is heavily right-skewed toward recent years
2. Minimal content before 1990
3. Sharp spike from 2015 onwards — when Netflix scaled globally and began producing originals
4. Peak release years: 2017, 2018, 2019


B) **Distribution of Movie Duration (Histogram + KDE)**


1. Bell-shaped curve centered around 90–100 minutes
2. Most movies fall between 80 and 120 minutes
3. Very short films (<60 min) and very long films (>200 min) are rare
4. This reflects the standard feature-film format audiences prefer


C) **Count of Titles by Release Year (Countplot)**


1. Confirms the exponential growth in content after 2015
2. 2018 and 2019 are the highest content-addition years


D) **Top 10 Countries by Content Count (after unnesting)**


1. United States far ahead of all others
2. India is a clear second — showing Netflix's heavy investment in Bollywood
3. UK, Canada, France, Japan, Spain, South Korea, Germany follow
4. South Korea showing notable presence — hinting at the K-drama boom


E) **Top 10 Actors on Netflix (after unnesting)**


1. Indian actors dominate: Anupam Kher (highest), Shah Rukh Khan, Akshay Kumar, Naseeruddin Shah, Om Puri, Julie Tejwani, Rupa Bhimani
2. Japanese actor Takahiro Sakurai and Yuki Kaji also appear — indicating anime depth
3. This confirms Netflix's deep investment in Indian and Japanese content

--------------------------------------------------------------------------------------------------------------------------------------------------------------

**4.2 Bivariate Analysis**

A) **Boxplot — Movie Duration**


1. IQR (middle 50%) is approximately 85 to 115 minutes
2. Median movie duration ≈ 98–100 minutes
3. Several outliers above 250–300 minutes — these are documentaries or special productions
4. Outliers were retained as they represent valid, real content


B) **Movies vs TV Shows Over Years (Countplot with hue)**


1. Until 2015, TV Shows were very few compared to Movies
2. From 2016 onwards, TV Shows increased significantly
3. This shows Netflix's strategic pivot toward episodic, binge-worthy content
4. TV Shows drive subscriber retention better than one-time movies


C) **Country vs Content Type (Top 5 Countries)**


1. United States — Movies dominate heavily, small TV Show count
2. India — Almost entirely Movies (Bollywood influence)
3. United Kingdom — More balanced between Movies and TV Shows
4. Canada — Movies dominant
5. This reveals Netflix's US and India focus is primarily movie-driven


-----------------------------------------------------------------------------------------------------------------------------------------------------------------





















