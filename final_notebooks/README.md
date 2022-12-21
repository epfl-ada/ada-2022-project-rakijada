
# Do we rate as we write?

Project for [Applied Data Analysis 2022](https://dlab.epfl.ch/teaching/fall2022/cs401/) at EPFL <br>
Team : **rakijada**.


## Table of Contents
---
- [Abstract](#abstract)
- [Research questions](#research-questions)
- [Data](#data)
- [Methods](#methods)
- [Proposed timeline](#proposed-timeline)
- [Navigating the repo](#navigating-the-repo)
- [Authors](#authors)
- [References](#references)

## Abstract
---

We noticed our data consists of around 55% of reviews whose numeric aspect ratings almost coincide. Statistically, it is very unlikely that each beer aspect (Appearance, Aroma, Taste, Palate) follows the same pattern; thus we presume that human nature has a play. To reduce user bias, we employ a BERT-based model which extracts the sentiment percentage (positive/negative) for all four features. We also noticed that aspect-specific grades are higher on average during winter than in summer. Therefore, we propose a method that deducts which beer aspects and when make a significant difference in the reviews, based on the sentiments extracted. This could have a major marketing impact on the breweries. An “objectively” better-rated taste during winter advises commercials focused on the snowy atmosphere with one’s mouth in the forefront. Also, the results could hint at the aspect to invest in with the highest success probability, thus improving risk management.

## Research questions
---

1. When people have a strong opinion on a certain product feature, they tend to rate all the other aspects similarly. Does this statement hold for our dataset? In other words, to what extent are numerical aspect grades similar for a given review, and is this trend present in a non-negligible-sized subset of reviews?
2. Do aspect-specific sentiments extracted from review text correspond to given numerical grades? If not, this is yet another indicator confirming the previous question's statement.
3. Review text therefore "more objectively" conveys the consumer's experience. Which beer aspects are most important to customers? Which of them are mentioned most frequently? Do users speak of them in a positive or negative manner? Or perhaps some aspects yield a neutral viewpoint?
4. Is there a noticeable rating trend during the year? If so, is there a text-based aspect (or aspects) that differentiates between yearly trend periods? Does that aspect have a polarized sentiment?
5. If so, how can these aspects be employed for the breweries' marketing purposes to improve targeting and enhance beer production?

## Data
---

The dataset we will use consists of beer reviews from the BeerAdvocate website, because the main language is English. The number of reviews in the dataset is 8 million. We save ratings in pickles. These pickles have up to 4 GB which is feasible to place in a single dataframe.  
Additional note: In the initial analysis (_data_investigation.ipynb_) we concluded that reviews in _reviews.txt_ are a subset of reviews in _ratings.txt_ and represent the vast majority of ratings where the textual review is present. Since our analyses use the free-form text review we focus on _reviews.txt_.

### Feature extraction
---
We enrich our dataset with aspect-based sentiment scores using Aspect Based sentiment analysis[1]. This model generates the probabilities for neutral, positive, and negative sentiments toward four beer aspects. This method adds 4 x 3 features for a beer review. 

<!-- The motivation for generating the sentiments: 
- It helps us understand what aspects are commented more. The positivity/negativity shows that people are not neutral about the aspect!
- We demonstrated with the examples (in the notebook _data_investigation.ipynb_) that scores for an aspect sometimes differ from the user grade for that aspect because, indeed, the user has a different comment than the grade they gave.
- It maps free-text review which is hard to work with to numbers which we are interested in. -->

### Feasibility
---
- 4GB of reviews - RAM-friendly! The model for aspect-based sentiment is powerful, but it is time-consuming. During the observational study (see step 5 in methods), we will generate aspect sentiments for carefully selected pairs and only for some reviews.

## Methods
---

**Step 1: Data cleaning and preprocessing.**
Data cleaning and checking for inconsistencies are done in the notebook _data_investigation.ipynb_.

**Step 2: Temporal analysis.** Since we are interested in digging deep into trends, we perform a temporal analysis of the data. The introduction to this analysis is demonstrated in the notebook _data_investigation.ipynb_. We conclude general trends over the days and months.

**Step 3: Conduct statistical tests.** Examine if aspect ratings do not statistically differ.

**Step 4: Indicate the most commented aspects in textual reviews.** Compare distributions of aspect names (or their synonyms) in the comments. We extract aspect synonyms (up to five) from the [Thesaurus](https://www.thesaurus.com/) website. Then, we observe if these results match the temporal analysis done in step 2 and investigate similarities and/or differences.

**Step 5: Review matching.** To eliminate subjectivity, we will match reviews of the same user. Additionally, we will match on beer style and ABV to avoid the known effect of alcohol percentage [2]. After, we will declare one beer rating as 'absolutely' better if all aspects are uniformly rated better. 

**Step 6: Feature extraction.** For the reviews present in matching, we generate three sentiments (positive, neutral and negative) for all four aspects as described in [feature extraction](#feature-extraction).

**Step 7: Comparing the text review aspects of matched reviews.** We will divide our matched reviews into two periods - summer and winter. Then, we will examine if there is a difference between the observed text review aspects during these two periods. Using bootstrapping, we will determine if some effects are significantly stronger for one period.

**Step 8: Infer conclusions from the results and answer the research question.** 

**Step 9: Data story.**

## Proposed timeline
---
The deadline is December 23rd.

| Period                 | Description               |
| ---------------------- | ------------------------- |
| Nov. 7th - Nov. 13th | Cleaning and preprocessing (s1) |
| Nov. 14th - Nov. 20th | Temporal analysis (s2) |
| Nov. 21st - Nov. 27th | Tests (s3) and most commented aspects (s4) |
| Nov. 28th - Dec. 04th   | Start observational study (s5 and s6) |
| Dec. 5th -  Dec. 11th   |   Observational study (s7) and Answering questions (s8) |
| Dec. 12th -  Dec. 18th   | Conclusions for the research question (s8) and work on data story (s9) |
| Dec. 19th -  Dec. 23rd   |   Final checks and revisions |

## Organization within the team
---

Team : A(leksa), D(ubravka), La(zar), Lu(ka)

| Task                 | Asignee               |
| ---------------------- | ------------------------- |
| Temporal analysis | La, A |
| Tests | D |
| Most commented aspects | Lu |
| Feature extraction | A, La |
| Execute matching | D |
| Execute observational study | Lu, La |
| Validate results of observational study  | A, D |
| Data story - appearance | D, La |
| Data story - text | Lu |
| Code validation  | A, D, Lu, La |

## Navigating the repo
---
- _data_import.ipynb_ : loading data, converting to pickles
- _data_investigation.ipynb_ : understanding data structure, cleaning, initial trends, inspect co-occurences of the same grades for aspects
- _data_aspect_analysis.ipynb_ : shows examples and motivation of using aspect based sentiment analysis

## Authors
---
- Aleksa Milisavljević
- Dubravka Kutlešić
- Lazar Radojević
- Luka Radić


## References
[1] [Aspect based sentiment analysis](https://github.com/ScalaConsultants/Aspect-Based-Sentiment-Analysis)

[2] [What drives higher beer ratings? Evidence from big data](http://www.theibfr2.com/RePEc/ibf/ijmmre/ijmmr-v15n1-2022/IJMMR-V15N1-2022-1.pdf)