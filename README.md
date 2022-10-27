# Overview

Our group has been tasked with analyzing historical data from multiple sources regarding information about different movie productions. Our goal is to come up with three recommendations for the company Computing Vision in order to enter into the Movie Industry. Computing vision is a company that has seen the growth of companies creating video content and wanted to get in on the action however, they aren't sure of the best market entry strategy. We are going to define what success looks like in the movie indsutry but more specifically for this firm.

### Navigating the Repo

* The Visuals folder contains essential visuals that appear in the presentation or appendix
* Our Presentation is in PDF format [Presentation PDF File](./Capstone_presentation.pdf)

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

Our recommendations for this company will be based off of the Gross Margin which is portrayed as a percentage. The higher this percentage is the more the company is retaining for every dollar that is invested in the movie and as such is seeing a higher return on their investment. 

$Gross Margin = \frac{Gross Revenue - Production Budget}{Gross Revenue} x 100$

We want to investigate what a "Good Movie" i.e. a movie with a high Gross Margin is doing and try to emulate that. Thus we will explore the budget size, what directors are involved in those high margin films, and also what genres see the highest margin

# Data Understanding and Analysis

The data we chose to focus most of our efforts on came from:
* IMDB
* The Numbers
* TheMovieDB

Where most of our recommendations came from The Numbers which contains the Gross Revenue and Production Budget numbers as well as IMDB and TheMoviesDB which contained a lot of background information on the movies including ratings and genre. With more time we would like to explore what connections fan ratings have to the success of a movie as well as choice of director or actor.

With the information given we were able to explore connections between our definition of success, Gross Margin and Total Profit, and various features of the film industry such as budget size, genres, and what month to release in. 


## Data Visualizations

This visual shows us the average Gross Margin by budget size in bar chart format. 
![Mean Gross Margin by Budget Size](visuals/Mean_Gross_Margin_by_Budget_Size.png)

This visual shows how the mean gross margin changes by month.
![Mean Gross Margin by Month](visuals/Mean_Gross_Margin_by_Month.png)

The family genre is noticeably the highest for domestic profit

![Mean Domestic Profit by Genres](visuals/Mean_Domestic_Profit_by_Genre.png)


# Statistical Communication

The question we wanted to answer was whether producing a big budget film (production budget > \$50,000,000) or small budget film (production budget < \$10,000,000) would be better for Computing Vision. Being a new company with little experience in the Movie Indstury and no name sake, going all in on a large budget film is risky. 

The results of this are as follows:
    
$H_0:$ There is no difference between small and big budget mean worldwide gross profit margin 

$H_A:$ The mean Worldwide gross profit margins are different for small and big budget film
    
Results:
* p-value = 0.004565 < 0.05, < 0.10 thus at both a 90% and 95% confidence level we reject the null hypothesis
* We have evidence to support the claim that the mean gross margin for small budget films is larger than big budget films

Recommendation and Findings: 
With the information provided, we can state that the small budget film has a larger mean gross margin than big budget films and we recommend creating a movie with a budget less than $10 Million


# Conclusion

### Summary

Throughout our analysis we found many interesting items related to what makes a movie successful. For a company like Computing Vision, we believe the most relevant items will be financial success in the market as opposed to fan metrics such as average ratings. Because of this, we focused on Gross Margin and Total Profit to be indicators for our decisions. Through a series of data preparation, analysis, and visualization we were able to procure a set of three relevant recommendations for the firm to follow. 

### Relevant Findings
1. Produce a Small Budget Film
    * Small Budget Films have an average Gross Margin of 46.41% and Big Budgets is 40.33%
    * These results are significantly different based on our testing and as such we would recommend Small Budget
        * Thus a better chance to see return on money spent producing a film since average gross margin is larger
2. Create a movie in the Family genre
    * After some analysis we came to the conclusion that a Family movie would be the best movie to produce
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

