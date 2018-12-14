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
We use Wiki Portal Curent Event (https://en.wikipedia.org/wiki/Portal:Current_events) for scrapping information on certain dates. 


# Contribution of Each Member 
  * **Nicolas Gandar** : Datastory Writting / WebScrapping / Correlation / Backgroung historical research ...
  * **Jean-Baptiste Prost** : Datastory Writting / Word2Vec / WebScrapping / Bokeh plotting ...
  * **Antoine Spahr** :  Correlation / D3 Plots / WebPage construction / Datastory Writting ...

Everyone has help/supervised/developped the work of each other

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
