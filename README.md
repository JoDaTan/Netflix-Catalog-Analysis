# Netflix Catalog Exploratory Data Analysis
Ever wondered what makes Netflix’s library so diverse and fascinating? This project uses Python visualization libraries (Matplotlib, Seaborn and Plotly express) and analysis to dig into the details of movies and series, uncovering patterns in content type, release year, country, genre, actors, directors, ratings, and durations.

### Project Overview
The aim of this project is to use Python data analysis and visualization techniques to explore Netflix's catalog of movies and series and identify patters or trends.

### About the Dataset
The dataset (netflix.csv) provides detailed information about the movies and series available on Netflix's platform. It includes a variety of metadata that can be used for analyzing trends, exploring patterns, and gaining insights into Netflix's content catalog. The dataset contains the following columns:
- Show_Id: A unique identifier for each show.
- Category: Indicates whether the content is a movie or a series.
- Title: The title of the movie or series.
- Director: The director(s) of the content (if applicable).
- Cast: Key actors featured in the content.
- Country: The country where the movie or series was produced.
- Release_Date: The date the content was released (2008 - 2021)
- Rating: The content's rating (e.g., PG, R).
- Duration: The runtime of movies or the number of seasons for series.
- Type: Specifies the genre of the content.
- Description: A brief summary or synopsis of the content.

### Tools Used
- Pandas: for data cleaning and analysis
- Seaborn: for data visualization
- Plotly express: Geographical visualization

### Data Cleaning & Preprocessing
The following operations were done on the dataset to make it valid and ready for analysis.
- Data loading and exploration
- Data cleaning:
    - removing leading and trailing spaces in the Release_Date column
    - data type conversion
    - removal of duplicates
    - checking for null/missing values

### Exploratory Data Analysis
- What is the volume of the netflix catalog?
- What is the ratio of movies to series on Netflix?
- What is the most popular genre?
- Netflix content distribution by ratings
- Who is the most popular actor and how many movies/series did they feature in?
- Who is the most popular director?
- What year has the most movies/series on netflix?
- Are there any monthly trends?
- Geographical distribution of contents

### Data Analysis
- ```# using a countplot, I visualize the distribution of Netflix Movies v Series
  fig = plt.figure(figsize = (6,3))
  sns.set_style('ticks')
  sns.countplot(data = netflix, x = netflix['Category'])
  plt.title('Distribution of Netflix content by Category')
  plt.show()

- ```netflix['Type'] = netflix['Type'].astype('category')
  netflix['Type'].value_counts().head(10)

- ```fig = plt.figure(figsize = (10,3))
  sns.set_style('ticks')
  sns.countplot(data = netflix, x = netflix['Rating'])
  plt.title('Distribution of Netflix content by Rating')
  plt.show()

- ```Since there are a number of actors for each movie/series in the dataset,
  I'll need a list t collect all actors for all the movie/series that appear in the dataset

  cast = netflix.dropna(subset=['Cast'])
  flat_cast_list = netflix['Cast'].apply(lambda x:x.strip().split(',') if isinstance(x, str) else []).sum()

  next I need to count the number of times an actor appears in the list, this will give me number of movies they occur in

  from collections import Counter
  actor_count = Counter(flat_cast_list)
  top_10_actors = actor_count.most_common(10)
  print(top_10_actors)
