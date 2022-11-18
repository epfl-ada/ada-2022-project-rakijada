
# How to write and when to put an ad in front of your bar?

This Github repo presents the project which is a part of the [Applied Data Analysis 2022](https://dlab.epfl.ch/teaching/fall2022/cs401/) curriculum at the EPFL. Our team is called **rakijada**.


## Table of Contents
---
- [Abstract](#abstract)
- [Research questions](#research-questions)
- [Data and additional datasets](#data)
- [Methods](#methods)
- [Feasibility](#feasibility)
- [Proposed timeline](#proposed-timeline)
- [Navigating the repo](#navigating-the-repo)
- [Questions for TAs](#questions-for-tas)
- [Authors](#authors)

## Abstract
---
REMINDER: ABSTRACT UP TO 150 WORDS

Brewing process can be dated back to at least 2500 BC, so naturally, it has significantly transformed to this day, with its finesses still actively changing. Given the consumer-generated data, we aim to investigate which trends have emerged during the past couple of years and which of these changes were good/bad. This analysis could help breweries answer important questions: Which beer type and when should they focus their production on? Did some beers lose popularity - which aspect could be improved? What is the best period to invest in advertising?

## Research questions
---

In this project, we aim to analyze user interests and pick trends over the time the beer datasets are collected. More precisely, we wish to answer the following questions:
- Are the ratings given during cozy winter nights higher on average? Do they have more positive sentiments? ??
- What are the types of beer prevalent during different seasons? Do those have a particular style? Do they have more alcohol?
- Are there any local characteristic rating phenomena, such as peaks during weekends and public holidays? Do users then grade better, grade more, or show special sentiment towards specific aspects (taste, smell, aroma, palate, appearance)? Or is there a noticeable global trend over the years?
- It should be that a single beer is always the same. Are the sentiment trends of aspects of a beer constant over time? 
- Are the answers to the questions above independent of the country, namely, are the general trends the same per country or state?

These conclusions could help breweries adjust their production according to people’s preferences and improve targeting.

## Data
---

The dataset we will use for the project is beer reviews from BeerAdvocate websites. The number of reviews in the dataset is 8 million. We read txt ratings and reviews, convert them to dataframes and save them to pickle files which we use for later analysis. These pickles have up to 4 GB which is feasible to place in a single dataframe when working on it. We additionally have data about users and breweries, which are small CSV files (up to 30 MB). 
Additional note : In the initial analysis (_data_investigation.ipynb_) we concluded that reviews in _reviews.txt_ are subset of reviews in _ratings.txt_ and they represent the vast majority of ratings where the textual review is present. Since our analyses us free-form text we continue working with _reviews.txt_.

### Feature extraction
---
Notation: aspects are different metrics that user rated, i.e., Taste, Appearance, Aroma and Palate grades.
We enrich our dataset with aspect-based sentiment scores using Aspect Based sentiment analysis[1]. This model generates the scores for neutral, positive, and negative sentiments towards four aspects. This provides 4 x 3 features for beer review.

The motivation for generating the sentiments: 
- BeerAdvocate's rule: If a user only provides the overall grade, other aspects are graded equally. (7% of reviews have all grades equal between aspects!) This approximation can be wrong.
- It helps us understand what aspects are commented more. The positivity/negativity shows that people are not neutral about the aspect!
- We demonstrated with the examples (in the notebook _data_investigation.ipynb_) that scores for an aspect sometimes differ from the user grade for that aspect because, indeed, the user has a different comment than the grade they gave.
- It maps free-text review which is hard to work with to numbers which we are interested in.

### Feasibility
---
- 4GB of reviews - RAM frinedly!
The model for aspect based sentiment is powerful, but it is computationally extensive. During observational study (see step 5 in methods) we will generate aspect sentiments for carefully selected users. Therefore, the method is feasable. There exists alternative models (?list them?) with the same objective, so we can use them instead of [1]. 

### Additional datasets
---
We will use an additional dataset to determine the dates for [public holidays](https://www.kaggle.com/datasets/donnetew/us-holiday-dates-2004-2021) in the USA. For other countries, we will inspect the public holidays manually.

## Methods
---

**Step 1: Data pre-processing and feature extraction**
Data cleaning and checking for data inconsistencies are done in the notebook _data_investigation.ipynb_.
As explained in the [feature extraction](#feature-extraction), we generate aspect based sentiments for textual reviews.

**Step 2: Execute statistical tests** (e.g., t-test) to conclude are there differences in ratings during particual day, month and seasons for beers of particular style or ABV (level of alcohol).

**Step 3: General temporal analysis using the entire BeerAdvocate dataset** Since we are interested to dig deep into trends, we execute general temporal analysis on the data. The introduction to this analysis is demonstrated in the notebook _data_investigation.ipynb_. We conclude general trends over the days, months and years.

**Step 4: Specific temporal analysis using the entire BeerAdvocate dataset.** Investigate sentiments and ratings statistics during public holidays and weekends and conclude whether they differ to general statistics (by executing statistical tests). 

**Step 5: Observational study.** 

**Step 6: Infer conclusions from the results and answer research questions**

**Step 7: Data story**


## Proposed timeline
---
The deadline for the project is December 23rd. The proposed timeline is summarized in the table below.

| Period                 | Description               |
| ---------------------- | ------------------------- |
| Nov. 14th - Nov 20th | Feature extraction (sentiment of ascpects) (s1) and tests (s2) |
| Nov. 21st - Nov 27th | General (s3) and specific (s4) temporal analysis |
| Nov. 28st - Dec. 04th   | Observational study (s5) and start answering questions (s6) |
| Dec. 5th -  Dec 11th   |   Answering questions (s6) and start data story (s7) |
| Dec. 12th -  Dec 18th   | Conclusions for the research question and work on data story |
| Dec. 19th -  Dec 23th   |   Final checks and revisions |

## Organization within the team
---

Our team consists of 4 members : A(leksa), D(ubravka), La(zar), Lu(ka)

| Task                 | Asignee               |
| ---------------------- | ------------------------- |
| Feature extraction | A, La |
| Tests | D |
| Continue with general temporal analysis | A, Lu |
| Identify popular styles or alcohol levels over time | Lu |
| Holidays analysis | D, A |
| Observational study  | La, A |
| Data story - appearance | D, La |
| Data story - text | Lu |
| Code validation  | A, D, Lu, La |

## Navigating the repo
---
- _data_import.ipynb_ : loading data, converting to pickles
- _data_investigation.ipynb_ : cleaning, sorting out inconsistencies, initial temporal trends, examples with aspect sentiment scores

## Questions for TAs
---

## Authors
---
- Aleksa Milisavljevic
- Dubravka Kutlesic
- Lazar Radojevic
- Luka Radic


## References
[1] [https://github.com/ScalaConsultants/Aspect-Based-Sentiment-Analysis](https://github.com/ScalaConsultants/Aspect-Based-Sentiment-Analysis)

[2] 