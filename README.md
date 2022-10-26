# Overview

Our group has been tasked with analyzing historical data from multiple sources regarding information about different movie productions. Our goal is to come up with three recommendations for the company Computing Vision in order to enter into the Movie Industry. Computing vision is a company that has seen the growth of companies creating video content and wanted to get in on the action however, they aren't sure of the best market entry strategy. We are going to define what success looks like in the movie indsutry but more specifically for this firm.

# Business Understanding

The key stakeholder is Computing Vision and their management team

The problem Computing Vision is faced with is that they want a piece of the movie market however don't know how to enter. We need to help them define what success means in this industry. With the data we have we want to explore whether financial metrics or fan (rating) metrics are a better indicator of success. We need to create actionable insights for Computing Vision to be able to decide what their entry strategy is going to be, and how to scale up once they are in the industry.

Key Business Questions: 
* What is success?
    * How much the movie grosses from “The Numbers”
    * The averaging rating / number of votes from IMDB database
    * Total Profit and Gross Margin based on budget size
* What do successful movies look like given our metrics
* How does genre impact the success of a movie (Based on Financial Metrics?
* Does director impact the rating and the net profitability?
* What time of the year (month) is best to release a movie?

While we may not touch on all of these, they are all things that could be consider as key questions for the firm. 

### What is Success?

We will define success in two ways. The first being the Gross Margin and the other being Total Profit. The Gross Margin calculations are detailed below. The reason we chose to focus on profitabilty metrics instead of ratings was because this company, computing vision, is trying to break into a well established market they want to ensure that the investment they put in is having a positive return. 

Our recommendations for this company will be based off of the Gross Margin which is portrayed as a percentage. The higher this percentage is the more the company is retaining for every dollar that is invested in the movie and as such is seeing a higher return on their investment. This is not necessarily equivalent to a standard ratio of Gross Margin which would include Net Sales and COGS however, considering the "Gross" columns of our data frame as a proxy for sales, and Production Budget as a proxy for COGS will yield similar results and actionable outcomes

$Gross Margin = \frac{Gross Revenue - Production Budget}{Gross Revenue} x 100$

This is an important metric, especially for a company about to enter an industry they have no presence in because it will help show how far their money goes to create profit. The higher this percentage the better the business will be doing because it is an indicator that retains more on each dollar of sales to its costs. This metric also allows us to take a standardized approach to comparing movies and their success. 

We want to investigate what a "Good Movie" i.e. a movie with a high Gross Margin is doing and try to emulate that. Thus we will explore the budget size, what directors are involved in those high margin films, and also what genres see the highest margin

# Data Understanding and Analysis

The data we chose to focus most of our efforts on came from:
* IMDB
* The Numbers
* TheMovieDB

Where most of our recommendations came from The Numbers which contains the Gross Revenue and Production Budget numbers as well as IMDB and TheMoviesDB which contained a lot of background information on the movies including ratings and genre.

#### IMDB Database information

These two database tables share a "movie_id" column, thus we can join on this key and take a look at movie information including name, release year, and genre as well as the average rating with the number of votes. We want to find a good balance of average rating as well as number of ratings since a small number of really high ratings could skew the interpretation of what a "good" movie is.

#### Rotten Tomatoes Movie Info Dataframe

This dataframe contains general information regarding the movies including rating, director, release date for theaters and DVD as well as the currency, box office, runtime and studio. There is a unique id column which we will not use as an index because it could be useful for combining data frames or doing different lookups

We may consider dropping currency, box office, and studio due to there being many missing values

Most columns are missing values and as such we will have to fill or deal with those missing values accordingly, this dataframe is related to the reviews data frame by the id column which relates to a unique id for each movie

#### Rotten Tomatoes Review Dataframe

The most important information from this dataframe will be the id which cooresponds to the movie that they are reviewing and the rating that they give it. We are missing about more than 10,000 ratings which is a considerable amount to discard, so we could fill these with the average value of the rating for the movie that they are reviewing. In order to make thge rating a useful variable we would have to apply a function to transform it from a string into a float rating value

A more advanced approach would be to conduct sentiment analysis and apply weights to the most common keywords found in a review at each score level and develop a heuristic to apply a score to the missing values based on the review that they left discarding all review entries without an actual review.

This data frame has a relation to the movie_info data frame since bothg come from rotten tomatoes. The id relates to the movie that each critic leaves a review for. 

#### The Movie DB Dataframe

This dataframe is not missing any values. It has information about genre ids and contains a unique id column along with the movie name, how many votes it received, and what the average vote value was. Vote seems to be this specific sites way of ranking the movies. 

#### The Numbers Movie Budgets Data Frame

This data frame is also not missing any values, it contains an ID for each movie, the title, production budget, how much the movie grossed domestically and how much it grossed worldwide

We will be transforming this data by making the budget and gross column integers as well as adding additional columns for profit and Gross Margin to help us in later analysis

#### Box Office Mojo Movie Gross Data Frame

This data frame is missing a lot of foreign gross values which could potentially be filled in by taking the difference from the budgets df ww_gross - domestic_gross, otherwise we will throw out those values because we can not estimate them.

We most likely will not use this data frame because the movie_budgets dataframe offer the same information and a bit more that is helpful to our analysis

## Data Visualizations


![Mean Gross Margin by Budget Size]("visuals/Mean Gross Margin by Budget Size.png")

![Mean Gross Margin by Month]("visuals/Mean Gross Margin by Month.png")

![Mean Domestic Profit by Genres]("visuals/Mean Domestic Profit by Genre.png")


# Statistical Communication

The question we wanted to answer was whether producing a big budget film (production budget > \\$100,000,000) or small budget film (production budget < \\$5,000,000) would be better for Computing Vision. Being a new company with little experience in the Movie Indstury and no name sake, going all in on a large budget film is risky. 

We looked at what percentage of small, medium, and large budget films produced a profit and to our surprise small budget films drastcially out perform big budget films. In fact, 47.90% of small budget films were profitable, and only 6.86% of big budget films were profitable. This led us to believe that producing small budget films would be better for Computing Vision.

To test this, we calculated what the average Gross Margin ratio was for each of the budget sizes by creating a categorical variable to indicate the budget category. After some analysis we ran a independent two sample t test because we did not have all movies created in this test however we wanted to see whether their average gross margins were significantly different. 

The results of this are as follows:
    
$H_0:$ There is no difference between small and big budget mean worldwide gross profit margin 

$H_A:$ The mean Worldwide gross profit margins are different for small and big budget film

We want to use statistical analysis rather than simply a graph because we want to conclude that the mean of both of these samples is the same. We did not analyze every movie to exist and as such we wanted to ensure that our information and the claims that we are making have a statistical backing.

This problem is suited for this analysis because we are observing two seperate groups - the small budget movies and the big budget movies. We are curious if there is a statistically significant difference between their average gross profit margins because we want to be able to make a recommendation to Computing Vision of how much to invest. As we saw above, gross margin correlates weak to moderately with total profit and thus we want to know if the gross margins are different for these two groups.

Limitations: 
* we are not sure what the sample was all we know is that it came from the file provided
* Only considered films with worldwide gross greater than zero (mathematical purposes)
* removed outliers who were 1.5 times the IQR removed from the data. 
* scale of these are drastically different: production budget has a moderate to strong positive correlation with total profit
    * This means regardless a big budget film will net more profit if proftitable
    
Results:
* p-value = 0.32316 > 0.5, > 0.10 thus at both a 90% and 95% confidence level we fail to reject the null hypothesis
* This indicates that we do not have evidence to support the claim that there is a significant difference between the two averages

Recommendation and Findings: With the information provided, the means from the two samples are not significantly different, meaning based on the given samples the mean gross profit margin for small budget films is comparable to that of a big budget film.  However, for a company such as Computing Vision making their first break into the film industry, beginning with a low budget film that has the potential to turn a high percentage of gross revenue into profits can be a great start. They can then look to scale up and produce bigger budget films as they become a better known name in the industry and get their legs under them in production.


# Conclusion

### Summary

Throughout our analysis we found many interesting items related to what makes a movie successful. For a company like Computing Vision, we believe the most relevant items will be financial success in the market as opposed to fan metrics such as average ratings. Because of this, we focused on Gross Margin and Total Profit to be indicators for our decisions. Through a series of data preparation, analysis, and visualization we were able to procure a set of three relevant recommendations for the firm to follow. 

### Relevant Findings
1. Produce a Small Budget Film
    * Small Budget Films have an average Gross Margin of 49.86% and Big Budgets is 53.13
    * These results are not significantly different based on our testing and as such we would recommend Small Budget
    * Small budget films have a higher probability of profit compared to big budget
        * Thus a better chance to see return on money spent producing a film
2. Create a movie in the Family genre
    * After some analysis we came to the conclusion that a drama movie would be the best movie to produce
        * Has the highest mean Domestic Profit
        * Matters because Small Budgets Films perform better domestically
    * Across the board in all level of analyses Foreign, Domestic, and Total Profit, Family topped the list
        * Family has the largest Gross Margin by a small amount compared to the Mystery Genre
        * The results comparing Family and mystery, and Family and TV Movie were not significant 
        * Then basing our recommendation off the Domestic Profit, we would still recommend a Family movie which has the highest domestic profit
3. Release your movie in May
    * We see that the summer months, which coincides to when school releases has a spike in average gross margin
        * To be most successful financially, May allows you to capture those months of high revnue
    * There is a dip in Aug, Sept, and Oct however dring the Holidays (Nov and Dec) there is another spike 
        * When releasing in May, you will capture both the summer and holiday high gross margins

