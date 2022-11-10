# <p style="text-align: center;"> Brands sponsorships on Youtube :</p>

## Abstract 

  Advertising on Youtube is not something new given that its the second most visited website each day, making thus of it a huge platform for visibility for brands but over the last few years it has been apparent from an user point of view that the number of products and services being advertised directly in the videos has been increasing. This could be an issue since even when paying for the premium subscription of Youtube which is supposed to allow an user to bypass the ads, they're still subject to these in-videos sponsorships. We're thus wondering firstly in what way has the topic of sponsorship evolved through the years on Youtube but we could also ask ourselves what are the effect of sponsorships on the relative popularity and on the relative sentiment given by a certain content creator. 

### Research Questions

- Evolution of the type and number of brands that sponsors videos on Youtube
- Study on which type of video is more likely to be sponsored (Pourrait être marrant de train un model pour prédire ça :)
- Categorization of the type of brands that sponsors videos
- Effect of sponsorship on the metadatas (views / like ratio / subscribers) of a channel => Beneficial or more of a hinder
- Interpretation for the above questions

To tackle some of these questions we might need to obtain additional informations on the videos and channels that we are studying, luckily we're able to use the youtube API (https://developers.google.com/youtube/v3/getting-started) to fill any gaps in our data.

### Methods

Our first challenge to tackle is how to work with such a big dataset, for this issue we decided to use combinations of Pandas (https://pandas.pydata.org/docs/) for its ease of use  and PySpark (https://spark.apache.org/docs/latest/api/python/) to handle the big workload when we are doing computation on the entire set or on a big subset.

The second primary challenge to resolve our questions is that we need to filter out every videos that do not contain a sponsorship, but thanks to Youniverse, we have access to the description of each videos in the dataset which allow us to parse the description in search of URLs, by excluding other social medias (Twitter/Twitch/Instgram etc) we are thus able to extract the urls that are present in the description but that are not other social medias which by setting afew threshold we can consider they to likely be from sponsorships.
(We sadly aren't able to account for shortened URLs since they do not follow a fixed semantic)

                                                      
                                                      
