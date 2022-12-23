

# Do we rate as we write?

Project for [Applied Data Analysis 2022](https://dlab.epfl.ch/teaching/fall2022/cs401/) at EPFL <br>
Team : **rakijada**.


## Table of Contents
---
- [Abstract](#abstract)
- [Research questions](#research-questions)
- [Data](#data)
- [Methods](#methods)
- [Navigating the repo](#navigating-the-repo)
- [Data Story](#data-story)
- [Authors](#authors)
- [References](#references)

## Abstract
---

We noticed our data consists of around 55% of reviews whose numeric aspect ratings almost coincide. Statistically, it is very unlikely that each beer aspect (Appearance, Aroma, Taste, Palate) follows the same pattern; thus we presume that human nature has a play. To reduce user bias, we employ a BERT-based model which extracts the sentiment percentage (positive/negative/neutral) for all four features. We propose a method that deducts which beer aspects and when make a significant difference in the reviews, based on the sentiments extracted. We go deeper to find out which _aspect characteristics_ map into a high rating. We cannot conduct this analysis globally since different beers may have different traits. That’s why we conduct our analysis for beer styles individually.

## Research questions
---

1. When people have a strong opinion on a certain product feature, they tend to rate all the other aspects similarly. Does this statement hold for our dataset? In other words, to what extent are numerical aspect grades similar for a given review, and is this trend present in a non-negligible-sized subset of reviews?
2. Do aspect-specific sentiments extracted from review text correspond to given numerical grades? If not, this is yet another indicator confirming the previous question's statement.
3. Which beer aspects are the most important for users? Namely, what are the aspects that correlate positively with their overall rating?
4. What keywords do reviewers use about these aspects that are decisive factors when they give good grades?

## Data
---

The dataset we will use consists of beer reviews from the BeerAdvocate website, because the main language is English. The number of reviews in the dataset is 8 million. We save ratings in pickles. These pickles have up to 4 GB which is feasible to place in a single dataframe.  
Additional note: In the initial analysis (_data_investigation.ipynb_) we concluded that reviews in _reviews.txt_ are a subset of reviews in _ratings.txt_ and represent the vast majority of ratings where the textual review is present. Since our analyses use the free-form text review we focus on _reviews.txt_.

### Feature extraction
---
We enrich our dataset with aspect-based sentiment scores using Aspect Based sentiment analysis[1]. This model generates the probabilities for neutral, positive, and negative sentiments toward four beer aspects. This method adds 4 x 3 features for a beer review. 


### Feasibility
---
- 4GB of reviews - RAM-friendly! The model for aspect-based sentiment is powerful, but it is time-consuming. During the observational study (see step 3 in methods), we will generate aspect sentiments for carefully selected pairs and only for some reviews.

## Methods
---

**Step 1: Data cleaning and preprocessing.**
Data cleaning and checking for inconsistencies are done in the notebook _data_investigation.ipynb_.

**Step 2: Temporal analysis.** Since we are interested in digging deep into trends, we perform a temporal analysis of the data. The introduction to this analysis is demonstrated in the notebook _data_investigation.ipynb_. We noticed general trends over months.

**Step 3: Review matching.** To eliminate subjectivity, we match reviews of the same user, as well as the same beer style, ABV (to avoid the known effect of alcohol percentage [2]) and the season in which the reviews were written. Additionally, we perform matching on the reviews that don't differ significantly in text length (for the sake of the unbiased results of the sentiment analyisis). We declare one beer rating as 'absolutely' better if all aspects are uniformly rated better. 

**Step 4: Feature extraction.** For the reviews present in matching, we generate three sentiments (positive, neutral and negative) for all four aspects as described in [feature extraction](#feature-extraction).

**Step 5: Comparing the text review aspects of matched reviews.** Based on the sentiment analysis, we introduce indicators for sentiments towards aspects (ie. indicator for a specific sentiment and aspect is 1 if score is higher than 0.9). We then compare distributions of these indicators in the better and worse reviews from matched pairs. We also find confidence intervals for differences in indicators between the better and the worse review.

**Step 6: Indicate the most infulential keywords in textual reviews.** For the most popular styles, we consider the most frequently appearing words and perform linear regression on them. From these results, we find words that significantly impact the rating. We also categorize these keywords by aspects.

**Step 7: Investigate seasonal keywords.** We repeat the similar procedure for each of the popular styles and compare the keywords that have a major change in frequency between the month with the highest average rating and the one with the lowest. We again perform linear regression on them and quantify their influence on the rating. 

**Step 8: Infer conclusions from the results and answer the research question.** 

**Step 9: Data story.**

## Organization within the team
---

Team : A(leksa), D(ubravka), La(zar), Lu(ka)

| Task                 | Asignee               |
| ---------------------- | ------------------------- |
| Temporal analysis | La, A |
| Find matching | D |
| Feature extraction | La |
| Perform observational study | Lu, La |
| Validate results of observational study  | A, D |
| Investigate general keywords | Lu, D |
| Explore seasonal keywords | La, A |
| Data story - appearance | D, La |
| Data story - text | Lu |
| Code validation  | A, D, Lu, La |

## Navigating the repo
---
- _data_import.ipynb_ : loading data, converting to pickles
- _data_investigation.ipynb_ : understanding data structure, cleaning, initial trends, inspect co-occurences of the same grades for aspects
- _absa_preparation.ipynb_ : running the aspect based sentiment analysis on the selected data
- _absa_analysis.ipynb_ : interpretation of the results of the aspect based sentiment analysis, relevance of aspects to the textual review and their effect on the rating
- _styles_investigation.ipynb_ : investigation of the most popular styles and keywords that most frequently appear in them 

## Data Story
---

Data story can be found on the link: https://dkutlesic.github.io/duda3/

## Authors
---
- Aleksa Milisavljević
- Dubravka Kutlešić
- Lazar Radojević
- Luka Radić

## References
[1] [Aspect based sentiment analysis](https://github.com/ScalaConsultants/Aspect-Based-Sentiment-Analysis)

[2] [What drives higher beer ratings? Evidence from big data](http://www.theibfr2.com/RePEc/ibf/ijmmre/ijmmr-v15n1-2022/IJMMR-V15N1-2022-1.pdf)
