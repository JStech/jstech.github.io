---
layout: comments
title: A Board Game Recommendation Engine
---

I decided to create a recommendation engine for board games, using data scraped
from [boardgamegeek.com][bgg]. My code is available [on GitHub][gh], but be
warned---I managed to get my IP blocked from BGG while collecting data. In my
defense:

 1. They have a [wiki page about data mining][dm] the site, and
 1. I was making 1 request per second, and downloaded less than 100MB of data.
    I could do that by hand.

My apologies to the Board Game Geek Powers That Be for my insolent behavior. I
promise to never do it again. Or I'll at least do it (even) slower.

### The data

Before I was blocked, I managed to scrape the ratings lists from 1,700 users who
had rated at least one game. Over 1,000 users had rated at least 10 games. There
are almost l2,000 games in the database, although I only used the 1,000
most-rated games for the user similarity measure (described below). All the web
scraping code is in Python 3, and I also used Python to parse the XML and write
the matrix of ratings to [HDF5][hd].

### The engine

A recommendation engine needs to do two things:

   1. Find other users who like the things you like, and
   1. Figure out what they really like that you've not yet rated.

However, the problem can be considered more simply as predicting the rating a
user would give to a game they've not yet rated. Once you've made those
predictions, you can simply recommend the games with the highest predicted
ratings.

I followed the outline described [in this post][dp], and implemented the
prediction engine in R. Users are represented as a vector of ratings, and the
similarity of two users is the cosine between their vectors. Then, a rating is
predicted by taking the average of other users' ratings, weighted by their
similarity with the user in question.

The issue of missing data is not addressed in the post linked above. I wrote a
modified cosine function to handle NA values. By default, the cosine function
returns NA if any of the inputs are NA, but I wanted it to project onto the
largest subspace with no missing data for a given pair of users, and calculate
the cosine of the projected vectors.

### Results

For testing purposes, my recommendation function predicts ratings for all games
for a given user. It ignores the user's true ratings in the process, which has
no effect on making recommendations, since you wouldn't recommend a game the
user has already rated, but allows honest comparisons between true and predicted
ratings for testing purposes.

Here are the 20 games with the highest predicted rating for a particular user,
along with the mean and standard deviation of their ratings.


    > r[1:20,]
       game predictedRating rating
    1    21        8.248609    8.0
    2    91        8.132131    9.0
    3     6        8.110919    8.5
    4    59        8.105064    8.5
    5     4        8.026672    9.0
    6     7        7.979619    9.0
    7    36        7.939304    9.0
    8    48        7.935049    9.0
    9    52        7.922401    8.0
    10   29        7.888088    9.5
    11   45        7.859293    9.0
    12   62        7.833052    9.0
    13  153        7.832915    9.0
    14   19        7.832199    7.5
    15  492        7.816715    NaN
    16   80        7.812988    NaN
    17   81        7.763401    9.0
    18    8        7.755711    9.0
    19  139        7.750971    8.5
    20  132        7.749858    NaN

    > mean(r$rating[!is.na(r$rating)])
    [1] 6.914315
    > var(r$rating[!is.na(r$rating)])^0.5
    [1] 1.489091

The list is sorted by predicted rating, so it's satisfying to see high true
ratings at the top of the list.

### Next steps

There are a couple things I'd like to do.

 1. Do some quantitative analysis of my results. I'm not ready to declare
    success as things stand currently---I need to consider what objective
    measures of success are appropriate.
 1. Do some qualitative analysis of my results: get some board game geek friends
    to send me a list of their favorite games, so I can make recommendations to
    them, and see what they think of the results.
 1. Use the id-to-name mappings that I stored away, so the results are a bit
    more interesting to look at.
 1. Try another method for comparison, such as a k-nearest neighbors algorithm.
 1. Get myself unblocked.

[bgg]: http://www.boardgamegeek.com
[gh]: https://github.com/JStech/bggrec
[dm]: http://boardgamegeek.com/wiki/page/Data_Mining
[hd]: http://www.hdfgroup.org/HDF5/
[dp]: http://www.dataperspective.info/2014/05/basic-recommendation-engine-using-r.html
