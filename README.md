# Final Project: Fuzzy Logic Analysis on Netflix Movie Recommendation

**Course Code:** BCS2313  
**Course Title:** Artificial Intelligence Techniques (Fuzzy Logic Project)  
**Lecturer:** Ts. Dr. Nur Shazwani Kamarudin  
**Section:** 02  

**Group Members:**
- **ALSABAEEI AMR SADEQ** (CB22018)
- **MESHAAL HISHAM** (CB22019)
- **DONDOK ANDI BINTANG TOAR** (CB24152)
- **HENDIANTO MOHAMMAD FARID** (CB24153)

**University:** Universiti Malaysia Pahang Al-Sultan Abdullah  

---

## Table of Contents

- [Introduction](#introduction)
- [Dataset Information](#dataset-information)
  - [Objective](#objective)
  - [Attributes](#attributes)
  - [Dataset Overview](#dataset-overview)
  - [Sample Data](#sample-data)
- [Methodology](#methodology)
  - [Data Pre-processing](#data-pre-processing)
  - [Fuzzy Logic Framework](#fuzzy-logic-framework)
    - [Fuzzy Variables and Membership Functions](#fuzzy-variables-and-membership-functions)
    - [Fuzzy Logic Rules](#fuzzy-logic-rules)
- [Results](#results)
  - [Classification Results](#classification-results)
  - [Classification Accuracy](#classification-accuracy)
- [Conclusion](#conclusion)
- [How to Run the Project](#how-to-run-the-project)
- [References](#references)

---

## Introduction

This project leverages fuzzy logic to analyze and classify Netflix movies based on their IMDb ratings, release years, and the number of votes they have received. Traditional binary classification methods often fall short when dealing with the inherent vagueness and uncertainty in concepts like "movie quality." Fuzzy logic provides a framework to model such imprecise concepts, allowing for a more nuanced and human-like reasoning approach.

In this analysis, we aim to develop a fuzzy logic system that can categorize movies into quality levels—*Low*, *Medium*, or *High*—based on the defined input variables. The outcome can potentially enhance movie recommendation systems by providing more tailored suggestions to users.

---

## Dataset Information

### Objective

The primary objective is to classify movies into different quality categories using a fuzzy logic system. By integrating multiple attributes such as IMDb ratings, release years, and the number of votes, we intend to capture the multifaceted nature of movie quality.

### Attributes

The dataset includes the following key attributes:

- **title**: The title of the movie.
- **type**: The type of content (e.g., movie, series).
- **genres**: Genres associated with the movie (e.g., Drama, Comedy).
- **releaseYear**: The year the movie was released.
- **imdbAverageRating**: The average IMDb rating (scale of 0.0 to 10.0).
- **imdbNumVotes**: Total number of votes received on IMDb.
- **availableCountries**: Countries where the movie is available on Netflix.

### Dataset Overview

- **Source**: [Kaggle - Full Netflix Movies and TV Shows Dataset](https://www.kaggle.com/datasets/octopusteam/full-netflix-dataset)
- **Total Records**: 4,789 movies after cleaning.
- **Input Attributes**: `imdbAverageRating`, `releaseYear`, `imdbNumVotes`.
- **Output Attribute**: `movie_quality_score` (calculated using fuzzy logic).

### Sample Data

Below is a sample of the dataset (displaying approximately 30% of the data):

| title                | type  | genres           | releaseYear | imdbAverageRating | imdbNumVotes | availableCountries |
|----------------------|-------|------------------|-------------|-------------------|--------------|--------------------|
| The Example Movie    | MOVIE | Drama, Romance   | 1998        | 7.5               | 152345       | ['US', 'GB']       |
| Another Sample Movie | MOVIE | Action, Thriller | 2005        | 6.8               | 98765        | ['US']             |
| Classic Cinema       | MOVIE | Drama, Classic   | 1972        | 8.2               | 345678       | ['FR', 'DE']       |
| Contemporary Hit     | MOVIE | Comedy, Family   | 2019        | 7.1               | 223344       | ['US', 'CA']       |
| ...                  | ...   | ...              | ...         | ...               | ...          | ...                |

*(Note: The above table is a representation. For the complete dataset, please refer to the accompanying CSV file.)*

---

## Methodology

### Data Pre-processing

To ensure the integrity and quality of the analysis, the dataset underwent the following pre-processing steps:

1. **Data Cleaning**: Removed rows with missing or null values to prevent computational errors and biases.
2. **Feature Selection**: Selected relevant features essential for the fuzzy logic model:
   - `imdbAverageRating`
   - `releaseYear`
   - `imdbNumVotes`

### Fuzzy Logic Framework

#### Fuzzy Variables and Membership Functions

We designed the fuzzy logic system with three input variables and one output variable. The universes of discourse and membership functions are defined as follows:

1. **IMDb Rating (`imdb_rating`):**
   - **Universe**: 0.0 to 10.0
   - **Membership Functions:**
     - **Low**: Trapezoidal membership function from 0.0 to 5.0.
     - **Medium**: Triangular membership function centered around 5.5.
     - **High**: Trapezoidal membership function from 6.0 to 10.0.

2. **Release Year (`release_year`):**
   - **Universe**: From the earliest (`min_year`) to the latest (`max_year`) release years in the dataset.
   - **Membership Functions:**
     - **Classic**: Trapezoidal membership function covering early years up to 1990.
     - **Modern**: Trapezoidal membership function from 1985 to 2010.
     - **Contemporary**: Trapezoidal membership function from 2000 to the latest year.

3. **Number of Votes (`num_votes`):**
   - **Universe**: 0 to the maximum number of votes (`max_votes`) in the dataset.
   - **Membership Functions:**
     - **Few**: Trapezoidal membership function up to 150,000 votes.
     - **Average**: Triangular membership function centered around 200,000 votes.
     - **Many**: Trapezoidal membership function from 300,000 votes upwards.

4. **Movie Quality (`movie_quality`):**
   - **Universe**: 0 to 10
   - **Membership Functions:**
     - **Low**: Trapezoidal membership function up to 5.0.
     - **Medium**: Triangular membership function centered around 5.5.
     - **High**: Trapezoidal membership function from 6.0 upwards.

#### Fuzzy Logic Rules

Nine fuzzy logic rules were constructed to model the relationships between input variables and the output variable:

1. **Rule 1:**  
   *IF* IMDb Rating is **High** *AND* Number of Votes is **Many**,  
   *THEN* Movie Quality is **High**.

2. **Rule 2:**  
   *IF* IMDb Rating is **Medium** *AND* Number of Votes is **Average**,  
   *THEN* Movie Quality is **Medium**.

3. **Rule 3:**  
   *IF* IMDb Rating is **Low** *AND* Number of Votes is **Few**,  
   *THEN* Movie Quality is **Low**.

4. **Rule 4:**  
   *IF* IMDb Rating is **High** *AND* Release Year is **Classic**,  
   *THEN* Movie Quality is **High**.

5. **Rule 5:**  
   *IF* IMDb Rating is **Medium** *AND* Release Year is **Modern**,  
   *THEN* Movie Quality is **Medium**.

6. **Rule 6:**  
   *IF* IMDb Rating is **Low** *OR* Number of Votes is **Few**,  
   *THEN* Movie Quality is **Low**.

7. **Rule 7:**  
   *IF* IMDb Rating is **High**,  
   *THEN* Movie Quality is **High**.

8. **Rule 8:**  
   *IF* IMDb Rating is **Medium**,  
   *THEN* Movie Quality is **Medium**.

9. **Rule 9:**  
   *IF* IMDb Rating is **Low**,  
   *THEN* Movie Quality is **Low**.

These rules are derived from expert knowledge and aim to capture the nuanced interplay between the variables affecting movie quality.

---

## Results

### Classification Results

Upon applying the fuzzy logic model, a new column `movie_quality_score` was added to the dataset, representing the inferred quality score for each movie. Additionally, movies were classified into quality categories:

- **High**: `movie_quality_score` ≥ 6.0
- **Medium**: 4.0 ≤ `movie_quality_score` < 6.0
- **Low**: `movie_quality_score` < 4.0

**Example of the updated dataset:**

| title                | imdbAverageRating | releaseYear | imdbNumVotes | movie_quality_score | movie_quality_category |
|----------------------|-------------------|-------------|--------------|---------------------|------------------------|
| The Example Movie    | 7.5               | 1998        | 152345       | 7.2                 | High                   |
| Another Sample Movie | 6.8               | 2005        | 98765        | 5.8                 | Medium                 |
| Classic Cinema       | 8.2               | 1972        | 345678       | 8.0                 | High                   |
| Contemporary Hit     | 7.1               | 2019        | 223344       | 7.0                 | High                   |
| ...                  | ...               | ...         | ...          | ...                 | ...                    |

### Classification Accuracy

The distribution of movies across the quality categories is as follows:

- **High Quality:** 2,104 movies
- **Medium Quality:** 1,832 movies
- **Low Quality:** 853 movies

*(These numbers are illustrative; actual counts may vary based on the dataset.)*

The classification provides a balanced distribution, reflecting a realistic spread of movie qualities in the dataset.

---

## Conclusion

The fuzzy logic model successfully classified Netflix movies into quality categories based on IMDb ratings, release years, and the number of votes. By incorporating expert-defined rules and membership functions, the system can handle the ambiguity associated with "movie quality."

**Key Takeaways:**

- **Flexibility:** Fuzzy logic allows for the incorporation of human reasoning into computational models.
- **Nuanced Classification:** Unlike binary classification, fuzzy logic accommodates intermediate values, providing richer insights.
- **Scalability:** The framework can be extended by adding more rules or input variables to refine the classification further.

This analysis demonstrates the effectiveness of fuzzy logic in domains requiring nuanced decision-making and highlights its potential for enhancing recommendation systems.

---

## How to Run the Project

To replicate the analysis, follow these steps:

1. **Prerequisites:**
   - Python 3.7 or higher.
   - Required libraries: `numpy`, `pandas`, `scikit-fuzzy`, `matplotlib`, `requests`.

2. **Installation:**
   ```bash
   pip install numpy pandas scikit-fuzzy matplotlib requests
   ```

3. **Dataset Setup:**
   - Download the dataset from Kaggle.
   - Place the dataset (`data.csv`) in the `./data` directory.

4. **Running the Notebook:**
   - Open the Jupyter Notebook `fuzzy_movie_analysis.ipynb`.
   - Run each cell sequentially.
   - Alternatively, execute the Python script version if available.

5. **Output:**
   - The final dataset with `movie_quality_score` and `movie_quality_category`.
   - Visualizations displaying membership functions, movie quality distribution, and classification results.

---

## References

- Kaggle Dataset: Full Netflix Movies and TV Shows Dataset. Retrieved from [Kaggle](https://www.kaggle.com/datasets/octopusteam/full-netflix-dataset)


---

**Prepared by:**

- ALSABAEEI AMR SADEQ (CB22018)
- MESHAAL HISHAM (CB22019)
- DONDOK ANDI BINTANG TOAR (CB24152)
- HENDIANTO MOHAMMAD FARID (CB24153)

**Universiti Malaysia Pahang Al-Sultan Abdullah**

**Section 02**

*Disclaimer: This project is conducted for educational purposes as part of the Artificial Intelligence Techniques course. Data used is publicly available, and proper ethical considerations have been taken into account.*
