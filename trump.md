---
title: "Analyse textuelle des tweets de Donald Trump"
author: "Jonathan DAHAN"
output:
  revealjs::revealjs_presentation:
    theme: default
    highlight: pygments
    center: true 


---   

## Introduction   

<br>   

- Journalistes + Donald Trump = Love Story   
- Data: quel genre d'histoire ?
- R Code:   
- Slides: rpubs


## Extraction des tweets   

<br>   


```r
library(twitteR)
library(dplyr)
library(purrr)

options(httr_oauth_cache=T)
setup_twitter_oauth(
  consumer_key="o4cuWyNkxWF2GjwthiQpehKsO",
  consumer_secret="o0YBmF6g59PPt4Y0vSy3t9dqduhX1lVPbm7oQe9lvXBxNgM3wZ",
  access_token="1380513698-dMEYAgdUc5fSSETy88HEkWVYokzayaoKSlf26fb",
  access_secret="IF4qVTnodXXuU39MvmrWtRfP8LD6TOLV5Jd5y3RHeK76F"
)
tweets<-userTimeline("realDonaldTrump", n = 3200)
tweets_df<-tbl_df(map_df(tweets, as.data.frame))
```



## On obtient quoi ?   

<br>   


|                   text                    |  favorited  |  favoriteCount  |       created       |                                     statusSource                                     |
|:-----------------------------------------:|:-----------:|:---------------:|:-------------------:|:------------------------------------------------------------------------------------:|
| FAKE NEWS - A TOTAL POLITICAL WITCH HUNT! |    FALSE    |      96302      | 2017-01-11 01:19:23 | <a href="http://twitter.com/download/android" rel="nofollow">Twitter for Android</a> |

Table: Table continues below

 

|  retweetCount  |  isRetweet  |
|:--------------:|:-----------:|
|     30080      |    FALSE    |
## Activité   

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4-1.png)

## À quelle heure ?   


![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5-1.png)

## Tweets nocturnes   
![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-1.png)



## Popularité   

<br>   

- nombre moyen de retweets par tweet ?  
- nombre moyen d'ajouts en favoris par tweet ?  
    

## Popularité   

<br>   

- RTs/Tweet: 19418   
- FVs/Tweet: 73318
   


## Top RTs/Tweet   

<br>   



|                text                |  favorited  |  favoriteCount  |       created       |                                     statusSource                                     |  retweetCount  |
|:----------------------------------:|:-----------:|:---------------:|:-------------------:|:------------------------------------------------------------------------------------:|:--------------:|
| TODAY WE MAKE AMERICA GREAT AGAIN! |    FALSE    |     573876      | 2016-11-08 06:43:14 | <a href="http://twitter.com/download/android" rel="nofollow">Twitter for Android</a> |     345630     |

Table: Table continues below

 

|  isRetweet  |
|:-----------:|
|    FALSE    |


## Top FV's/Tweet   

<br>   


|                                                                     text                                                                     |  favorited  |  favoriteCount  |       created       |
|:--------------------------------------------------------------------------------------------------------------------------------------------:|:-----------:|:---------------:|:-------------------:|
| Such a beautiful and important evening! The forgotten man and woman will never be forgotten again. We will all come together as never before |    FALSE    |     634231      | 2016-11-09 06:36:58 |

Table: Table continues below

 

|                                     statusSource                                     |  retweetCount  |  isRetweet  |
|:------------------------------------------------------------------------------------:|:--------------:|:-----------:|
| <a href="http://twitter.com/download/android" rel="nofollow">Twitter for Android</a> |     221418     |    FALSE    |


## Trump, il poste quoi ?   
![plot of chunk unnamed-chunk-10](figure/unnamed-chunk-10-1.png)


## Des hashtags ?   
![plot of chunk unnamed-chunk-11](figure/unnamed-chunk-11-1.png)

## Combien de caractères ?   
![plot of chunk unnamed-chunk-12](figure/unnamed-chunk-12-1.png)




## D'où sont postés les tweets ?   

<br>   


| Source     |  %   |
|:-----------|:----:|
| Android    | 50.9 |
| iPhone     | 42.8 |
| Web Client | 5.8  |
| iPad       | 0.3  |
| Periscope  | 0.1  |
| Twitter    | 0.1  |

## Fil quotidien   


![plot of chunk unnamed-chunk-14](figure/unnamed-chunk-14-1.png)



## Hypothèse   

<br>   

- Presse: iPhone=équipe de campagne, Android: Trump   
- http://www.theverge.com/2015/10/5/9453935/donald-trump-twitter-strategy   
- https://www.cnet.com/news/trumps-tweets-android-for-nasty-iphone-for-nice/   


## Retweets manuels   

![plot of chunk unnamed-chunk-15](figure/unnamed-chunk-15-1.png)



## Partage d'images/liens    
![plot of chunk unnamed-chunk-16](figure/unnamed-chunk-16-1.png)

## Tweets / iPhone   

<br>   

- Annonces, événements...
- "Join me in Florida this Saturday at 5pm for a rally at the Orlando-Melbourne International Airport! "   

   
## Tweets / Android    

<br>   

- d'un autre type...   
- "The FAKE NEWS media (failing @nytimes, @NBCNews, @ABC, @CBS, @CNN) is not my enemy, it is the enemy of the American People!"   


## Ratio log-odds   

- mots qui ont le plus de chances d'être postés par l'iPhone/Android ?   
- exemples: "fake", "illegal"   


## Ratio log-odds   

<br>   

$$\log_2(\frac{\frac{\mbox{# in Android} + 1}{\mbox{Total Android} + 1}} {\frac{\mbox{# in iPhone} + 1}{\mbox{Total iPhone} + 1}})$$   

## Comparaison   

![plot of chunk unnamed-chunk-17](figure/unnamed-chunk-17-1.png)

## Contenu   

<br>   

- iPhone: plus de hashtags   
- iPhone: plus de mots à charge émotionnelle négative ("fake", "illegal","badly", "failing")    
- Android: plus de mots pour des annonces ("7pm", "3pm", "join", "tickets")   

## Sentiments   

<br>   

- NRC Word-Emotion Association Lexicon   
- à chaque mot est associé le sentiment qu'il produit   
- "trust", "fear","negative", "sadness", "anger", "surprise", "positive", "disgust", "joy", "anticipation"   

## De quoi ça a l'air ?   

<br>   
  

|  word   |  sentiment  |
|:-------:|:-----------:|
|  fake   |  negative   |
| illegal |    anger    |
| illegal |   disgust   |
| illegal |    fear     |
| failing |    fear     |
| failing |    anger    |
| failing |   sadness   |


## Combien de mots / catégorie ?   


|  statusSource  |  sentiment   |  words  |
|:--------------:|:------------:|:-------:|
|    Android     |    anger     |   219   |
|    Android     | anticipation |   228   |
|    Android     |   disgust    |   153   |
|    Android     |     fear     |   213   |
|    Android     |     joy      |   162   |
|    Android     |   negative   |   398   |
|    Android     |   positive   |   404   |
|    Android     |   sadness    |   219   |
|    Android     |   surprise   |   103   |
|    Android     |    trust     |   274   |

## Sentiments: et Marine ?   

<br>

FEEL: http://www.lirmm.fr/~abdaoui/publications/FEEL.pdf   

<br>   


|  joy  |  fear  |  sadness  |  anger  |  surprise  |  disgust  |
|:-----:|:------:|:---------:|:-------:|:----------:|:---------:|
|  16   |   76   |    67     |   69    |     49     |    42     |
