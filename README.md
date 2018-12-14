# Russian Trolls, Pols and Approval Rate

**Find the Datastory Webpage [here](https://adarussiantrolltweetanalysis2018.github.io)**

# Abstract
The outcome of the 2016 US election were a surprise, few experts predicted a Trump win. Since then, it has been revealed that the Russian might have had an influence on the election through their action on social media. To test this claim, we will compare the IRA dataset and the "2016 Elections Poll". Moreover, the scope of the tweets dataset does no stop to the election. The dataset was last updated on March 2018, so we can also draw insights from the current presidency. We want to compare this with historical approval rates of Obama, since the trolls date all the way back from 2012. Is there a correlation between the russian tweets and the approval raitings ?


# Research questions
First, we will classify and understand the dataset.
1. We want to start by defining the classes: what are the words associated with "RightTroll" or "LeftTroll". What is a typical right/left troll? 
2. Quantify each variables. # of tweets by subject/target.

Correlation: we want to understand the effect of the tweets.
1. How does a tweet activity correlates with approval ratings? Is it significant?
2. Is the tweet effect more important during an election campaign or a president's tenure?
3. Are tweets more influential against Trump, Obama or Clinton?


# Dataset
We will use the IRA dataset given in the course.
We will use two additionals datasets from FiveThirtyEight: "2016 Election Poll" (https://www.kaggle.com/fivethirtyeight/datasets) and "Trump Approval Rates" (https://projects.fivethirtyeight.com/trump-approval-ratings/?ex_cid=rrpromo)

# A list of internal milestones up until project milestone 2
**Done** Filter/clean tweets (Non english) and select relevant ones (politically involved). Group the tweets by time period. Filter/Clean approvals rate: selecting Trump presidency. Filter/Clean 2016 election poll dataset. 

   * Data cleaning: the data is already pretty clean. We've just selected the relevant part (right and left english political trolls).              
   * Tweet activity is represented as the number of tweet per day.
   * We try to find events related to strong tweet acitvity (by googling).
   * Election polls data are also cleaned. Focus was given on adjusted polls (rather than raw polls). As the data collected different polls per day (from different pollster), we average them by day. To smooth the graph of approval over time, we perform a rolling-mean over a week.
   * Tweet activity, polls and polls variation are ploted (together and in scatter plots) to get insight in the realtion they might have. This is done for election and presidency time.<br>
For now, we have no corelation.
   * Word analysis: the tweets are cleaned. Frequent words and hastags for both categories are extracted. A Word2Vec model is build to represent words as "concepts". Unfortunately, plotting words space on 2D (after PCA) does not enable to observe clear cleasters. But the model works well, as it can get similar words togethers. The tweets are then represented in the words space (clusters cannot be observed). A first draft of a classifier is done.

Notebooks:
   * Poll_Description_Analysis: This notebooks analyzes the election polls and introduces the research of correlation with the tweets.
   * TrumpPresidency: Introduces Trump's approval ratings, a "key_hashtags" dataframe useful to understand trending topic and a preliminary version of the "events" dataframe to understand tweet density peaks. 
   * Word2vec: Imports and cleans the tweet datatsets and analyzes the contents. 


**To do:**
  * explore different time-shift for the correlation (to confim that there are no correlations).
  * Try different variables that could correlate with the polls.
  * Focus more on the hastags. We are building a list of key events that happened during the campaign/ Trump presidency. We are also building a method de highlight the most used tweets per day. This can help providing insight into the cause of big spikes.
  * Try to find a discriminative dimensions in the Word2Vec space that could differentiate Right vs Left trolls.
  

# Contribution of Each Member 
  * **Nicolas Gandar** : Datastory Writting
  * **Jean-Baptiste Prost** : Datastory Writting
  * **Antoine Spahr** : Polls Descriptive Analysis / D3 Plots / WebPage construction / Datastory Writting

# Data analysis procedure:
`PreProcess_Word2vec_TopWords`
In this notebook we focused on the treatment of the tweet’s content.
* First, the tweets are cleaned and tokenized.
* Then a Word2vec model is used to represent each word in a 200 dimensions vector according to it linguistic context.  We were hopping that the model would enable to observe cluster of similar words. To do so, we reduced to output 9 component with a PCA. We 2d-plotted each combinaison of those nine components but none of them gave a clear clustering. We could assed that the model was effective by simply looking at similar words by their *cosine similarity*.
* The most popular words, hashtags and mentioning were computed in this notebook. Moreover,  we have assigned a  continuous *score* characterizing each expression by it troll orientation (right or left). this provided additional information on the vocabulary used by the two trolls category.
* Finally, we displayed the top hashtag per day.


`WebScrap`
In this notebook, we defined the (23)  topics of the tweets.
* A first short keyword list for each topic was first written. Then, the same Word2vec model was used to extend the list. The model enables to find similar words in our vocabulary. As a result, the lists were enriched by ten folds.
* As we noticed that each tweets topic over time had spiking behavior, we wanted to understand what were the cause of those peaks. Hence, we implemented an *event detector* function. We defined a adapting threshold to each topic : *mean ± 2.25 * standard deviation* . When a spikes crosses the threshold, the date is retrieved and the corresponding page on [Wiki Portal CurrentEvents](https://en.wikipedia.org/wiki/Portal:Current_events)  is scrapped. Then, we look for potential word matching between the content of the topic list and the content of each paragraph of the web page text. If  a sufficient match occurs, an event is detected. <br> The function could still to be optimized but some very interesting output are provided

`Poll_Descriptive_Analysis` and `TrumpPresidency`
Those notebook integrates data from several pollsters during the election campaign (autumn 2017) and the Trump’s presidency respectively. They follow the same structure:
* 
