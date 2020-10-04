Homework 3
================
Patrick Sinclair

For the initial k-nn classification, the determining variables were
personal Income Total and Housing Cost, and the population was limited
to NYC residents between the ages of 21 and 65.

Which returned the following results:

    ##         Bronx     Manhattan Staten Island      Brooklyn        Queens 
    ##          4880          5250          1891         12416         10923

    ##         Bronx     Manhattan Staten Island      Brooklyn        Queens 
    ##    0.13800905    0.14847285    0.05347851    0.35113122    0.30890837

    ##     norm_inc      norm_housing_cost
    ##  Min.   :0.0000   Min.   :0.00000  
    ##  1st Qu.:0.9478   1st Qu.:0.02216  
    ##  Median :0.9731   Median :0.03083  
    ##  Mean   :0.9574   Mean   :0.41028  
    ##  3rd Qu.:0.9881   3rd Qu.:0.97507  
    ##  Max.   :1.0000   Max.   :1.00000

Using these variables and a training data set of 80% of the already
classified data points, the algorithm returned the following correct
prediction rates of k = 1, 3, 5, 7 and 9.

    ## [1] 1.0000000 0.3525155
    ## [1] 3.0000000 0.3441305
    ## [1] 5.0000000 0.3606708
    ## [1] 7.0000000 0.3700896
    ## [1] 9.0000000 0.3757179

The two variables good hand in hand - higher levels of income would
suggest higher housing costs for those households. Of the two variables,
I wanted to keep one constant and see how the predication rates would
change in response to one variable change. Instead of using Income
Total, which is per individual, I changed the variable to Household
Income. This variable has more connection to housing costs. Individuals
may work in low salaried positions but are still members of high income
households. Changing income total to household income produced the
following prediction rates.

    ## [1] 1.0000000 0.7312239
    ## [1] 3.0000000 0.4909851
    ## [1] 5.0000000 0.4711642
    ## [1] 7.0000000 0.4623284
    ## [1] 9.0000000 0.4557612

Including household income as a variable while holding housing cost
constant improves the algorithms’ ability to predict the classification
of observations into the boroughs overall, with a noticeable larger
uptick when k = 1. However, as the k number increases, our prediction
rate gets gradually less accurate. In the previous instance, there was a
slight uptick in k = 7 and k = 9. I would contend that the downward
trend in prediction rate is due to larger gaps between high income
households and low income households than the comparative gaps for
individuals.

I would like to try to get the algorithm to predict at rates about 0.5
for the higher k values. Initially I thought it would be best to include
a very different variable, such as linguistic isolation. Linguistic
isolation is the term used to describe homes in which no one over the
age of 14 spoke only English or spoke another language and English “very
well”. My assumption is that respondents in these households would
generally live near and around each other, to ensure they are in a
community in which they can interact and communicate with clearly and
easily. However, including this variable reduced the predictive
performance of the algorithm at all levels of k, by an average of 3.6%
(k = 1 by 4.5%).

This result was surprising at first though upon reflection, two issues
came to mind. The first is that the variable Linguistic Isolation is not
rich enough to provide points of different for the algorithm. Its
outcomes are either yes or no, essentially acting as a dummy variable.
0.8019705 of respondents are not linguistically isolated and would not
have to place as much importance on communication as a factor in
deciding where to reside.

``` r
norm_famsize <- norm_varb(FAMSIZE)
data_use_prelimhh <- data.frame(norm_householdinc, norm_famsize, norm_housing_cost)
# norm_housing_cost, LINGISOL
good_obs_data_use <- complete.cases(data_use_prelim,borough_f)
# good_obs_data_use <- complete.cases(data_use_prelim,in_Brooklyn)
dat_use <- subset(data_use_prelim,good_obs_data_use)
y_use <- subset(borough_f,good_obs_data_use)
# y_use <- subset(in_Brooklyn,good_obs_data_use)
```
