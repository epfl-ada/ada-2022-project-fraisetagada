# Sponsorships on Youtube

## Abstract 

With the rise of YouTube since 2005, content creators rose to fame with an expanding follower base. Businesses saw this as an opportunity to sponsor their content, exploring marketing potential with creators. Nowadays, sponsorships are a common practice on the platform with many YouTubers making a living off of them.

But this practice does not come without its downsides. Spectators paying for a premium YouTube subscription are often annoyed by the ads that are forced upon them by their favorite YouTubers. Many creators have been accused of promoting services that they do not believe in, or even worse, that may be harmful to their audience.

This project aims to explore the relationship between YouTubers and their sponsors, and to determine whether or not sponsorships are beneficial to content creators. We hope to provide YouTubers with more information about their potential sponsors, and help them make more informed decisions.

## Research Questions

For our analysis, we firstly analyse the context of sponsorships on YouTube:
- What are the different **types of sponsorships** on YouTube?
- What **brands** are sponsoring YouTubers?
- What are the **most common sponsorships**?
- How did these questions **evolve over time**?

We then analyse the relationship between videos and their sponsors: 
- What are the most **common sponsorships** for each **category** of YouTube videos?
- Which types of videos are **more likely to be sponsored**?
- Which types of videos are **targeted** by specific brands **over time**?

Finally, we focus on the primary recipients of the sponsorships, namely the YouTubers. We try to answer the following final question:
- Do sponsorships help content creators build a stronger community, or do they actually have some downsides?

## Datasets and Additional Datasets

### Datasets

[YouNiverse](https://github.com/epfl-dlab/YouNiverse) is a dataset containing large-scale channel and video metadata from English-Speaking
YouTube. It contains 3 datasets which are useful for our research:

- **Channel data**: Contains data for each channel, from $2004$ to mid $2019$.
- **Video metadata**: Contains metadata for each video, from mid $2005$ to end of $2019$.
- **Time Series data**: Contains data for each channel at some time points, from early $\textbf{2015}$ to end of $2019$.

For the **first two parts** of this project, we mainly depend on the **video metadata** which helps us understand the context of sponsorships since the very beginning of YouTube. For the **last question**, we use the **time series dataset** provided to us, since it has more relevent information about the YouTubers and their channels. By focusing on data from $2015$ to $2019$, we have a more recent view of the YouTube ecosystem, which is more relevant to our research.

### Additional Datasets

If needed, we might also use the [YouTube API](https://developers.google.com/youtube/v3/docs/members). This API enables us to get more fine-grained information about sponsorships such as the duration of the ad, the exact name of the sponsor, etc. But since it only allows us to request $10000$ queries per day, we might only use it for small-scale analysis.

### Libraries and Tools

To work with such a large dataset, we use a combination of [pandas](https://pandas.pydata.org/docs/) for its ease of use and [pyspark](https://spark.apache.org/docs/latest/api/python/) to handle the big workload when doing heavy computation on the entire dataset. Visualization is done with [matplotlib](https://matplotlib.org/3.3.3/contents.html) and [seaborn](https://seaborn.pydata.org/). Most of the statistical analysis will be done either with [statsmodel](https://www.statsmodels.org/stable/index.html) or by using the [classification and regression add-on of spark](https://spark.apache.org/docs/latest/ml-classification-regression.html#linear-regression).

### Data Preprocessing

For the **first two parts** of this project, we mainly depend on the **video metadata** which helps us understand the context of sponsorships since the very beginning of YouTube. For the **last question**, we use the **time series dataset** provided to us, since it has more relevent information about the YouTubers and their channels. By focusing on data from $2015$ to $2019$, we have a more recent view of the YouTube ecosystem, which is more relevant to our research.

When a video is sponsored, content creators usually mention it in the video description alongside with a link. We use this information to detect sponsorships by using **regular expressions** to find URLs.
We prealably establish a csv file **invalid_urls.csv** containing the recurrent URLs that Youtubers put on their descriptions like Youtube link, Twitter link, etc, so we filter them out to not consider them as potential sponsor urls. However, the list isn't exhaustive and it could remain urls that aren't sponsor. Ton encounter that, we will look to a list on internet containing the sponsor that are the most use between 2005 and 2019.

Unfortunately, many links retrieved are not directly related to sponsorships. We **filter out URLs that match with a list of unrelevent links** such as the creator's social media accounts, other videos, etc. This list is not exhaustive, but it is a good starting point.

Finally, to enrich our data, we **resolve shortened URLs**. This is done by using the Bitly API to resolve *bit.ly* URLs. Some other tools such as the [unshortenit](https://pypi.org/project/unshortenit/) Python library, or the Google URL Shortener API could also be used in the future.

To further enhance our set of features, we could add the **ratio of likes to dislikes** to videos, or the **relative increase or decrease in the number of subscribers** for channels in a given time period.



## Methods

To estimate the effect of sponsorships on the relative popularity of a content creator, we will be using **pairing** using **propensity scores**. We will be using **t-tests** to compare features of a video with a sponsorships and a similar video without sponsorship. We could also use **regression** to estimate the effect of sponsorship on the popularity of a video, by using the number of views as a proxy for popularity.

To answer the question about the types of videos that are more likely to be sponsored, we will use a **classification** approach, such as a **decision tree** or a **random forest**. We will use the **information gain** as a metric to evaluate the quality of the split.

Using **linear regression** we'll see if we can manage to get some insight on the effect of sponsorships on the popularity of a given video/ a given channel by using metrics such a **like per view** or even **dislike per view**.

## Proposed Timeline

| Week | Tasks |
|------|------|
| Nov 21 | Continue preprocessing of Bitly links and find a way to restraint our investigation of sponsor video by selecting videos containing URLs that are frequently present. |
| Nov 28 | Extract the brands that sponsored video and categorise them |
| Dec 5  | Find the most common sponsorships for each categories of YouTube videos|
| Dec 12 | Make a timeseries analysis of the evolution of sponsorships|
| Dec 19 | Analyse the impact of sponsorships on videos content creators and their community and look if it conducts to build a stronger relation between them or it could have some downsides |
| Dec 23 | Make the website |

## Organization within the team

| Week | Name | Tasks |
|------|------|-------|
| Nov 21 | Arnaud  | Finish the bitly conversion to website links|
|        | Ozan    | Generate a list of potential sponsor URLs|
|        | Yassine | Generate a graph of videos urls|
|        | Antoine | Bring meaningful visualisation about potential sponsors URLs |
| Nov 28 | All  | Categorization of the most frequent sponsored|      
| Dec 5  | Arnaud  | Find which kind of videos are most likely to be sponsored|
|        | Ozan    | Find what are the most common sponsorships among each video categories|
|        | Yassine | Look at what type of sponsors are used on each categories|
|        | Antoine | Visualise the most common sponsorships|
| Dec 12 | Arnaud  | Apply machine learning method whether a video could be sponsored and whether it has a positive or negative impact |
|        | Ozan    | Apply machine learning method whether a video could be sponsored and whether it has a positive or negative impact |
|        | Yassine | Establish propensity score and make t-test|
|        | Antoine | Establish a final conclusion|
| Dec 19 | All | Bring all the results together in a beautiful website|
     

### Note concerning the github organozation

We organized our work in a way that all the analysis can be find together in a single notebook called **Final_Analysis** but if one want to take a closer look at a specific type of analysis, they can find the seprated notebook where the analysis took place in the folder **Analysis**.

### Questions for TAs (optional)
- Any comments or advices will be greatly appreciated! :)
                                               