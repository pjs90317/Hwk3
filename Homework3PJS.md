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

    ## [1] 1.0000000 0.7318556
    ## [1] 3.0000000 0.4948159
    ## [1] 5.0000000 0.4817066
    ## [1] 7.0000000 0.4657371
    ## [1] 9.0000000 0.4631152

Including household income as a variable while holding housing cost
constant improves the algorithms’ ability to predict the classification
of observations into the boroughs overall, with a noticeable larger
uptick when k = 1. However, as the k number increases, our prediction
rate gets gradually less accurate. In the previous instance, there was a
slight uptick in k = 7 and k = 9. I would contend that the downward
trend in prediction rate is due to larger gaps between high income
households and low income households than the comparative gaps for
individuals.

I would like to try to get the algorithm to predict at rates at or above
0.5 for the higher k values. Initially I thought it would be best to
include a very different variable, such as linguistic isolation.
Linguistic isolation is the term used to describe homes in which no one
over the age of 14 spoke only English or spoke another language and
English “very well”. My assumption is that respondents in these
households would generally live near and around each other, to ensure
they are in a community in which they can interact and communicate with
clearly and easily. However, including this variable reduced the
predictive performance of the algorithm at all levels of k, by an
average of 3.6% (k = 1 by 4.5%).

This result was surprising at first though upon reflection, two issues
came to mind. The first is that the variable Linguistic Isolation is not
rich enough to provide points of different for the algorithm. Its
outcomes are either yes or no, essentially acting as a dummy variable.
0.8019705 of respondents are not linguistically isolated and would not
have to place as much importance on communication as a factor in
deciding where to reside.

Seeing the results of including linguistic isolation prompted a step
back. Focusing on interval or ratio variables, similar to income and
cost, might yield better results from the algorithm. Rather than nominal
variables such as birthplace or commute methods, I looked for interval
variables related to the household.

I selected family size as the next variable. Generally speaking, having
a larger family would imply the need for a larger dwelling, further
implying a higher housing cost. Larger families with children would
likely tend to live near each other, for school zoning, using child care
facilities and having children in communities with other children.
Smaller families without children, or houses of adults would find these
considerations less important and would live in other places.

To test whether family size would have a meaningful impact on the
prediction rate, I included it as a third variable for the algorithm to
consider.

    ## [1] 1.0000000 0.7554523
    ## [1] 3.0000000 0.4700274
    ## [1] 5.0000000 0.4619235
    ## [1] 7.0000000 0.4551305
    ## [1] 9.0000000 0.4472649

The results are interesting. The algorithm becomes more accurate when k
= 1. For higher values of k, the algorithm is slightly *less* accurate.
However, the deviation between prediction rates of higher values of k is
smaller when family size is included. Despite the prediction rates being
an average of 0.0094864 lower than those produced without family size
included, there is less variation in the rates as k increases 0.009698
compared to 0.014804.

It is clear from the three different combinations of variables that as k
increases, the ability of the algorithm to correctly classify the
observations decreases. Understanding the context of the different
variables allows us to continue to refine the algorithm iteration after
iteration to improve its accuracy of classifying the test data. However,
as we include more variables, it gives the algorithm more points of
difference to assess when processing test or unclassified data.

Similarly, we could use a high proportion of our data set to train the
algorithm but would it leave us a with a meaningful amount of
observations upon which to test the algorithm? If the test set is small
and homogeneous, we could well be fooled into thinking the algorithm is
more than satisfactory in classifying values but when applied to large
unclassified sets of data falls short of the predication rates produced
during the test.

Reducing the error in the prediction rate the known data may increase
potential error in classifying unknown data. If the algorithm has been
programmed to factor in particular variables using someone’s intuition,
applying the knowledge and context that they have of the data set, the
algorithm is susceptible to the biases that the programmer holds about
the data set. Household income may not be the best indicator for borough
prediction because of New York City’s public housing policies, today and
through the twentieth century.
[Here](http://assets.press.princeton.edu/chapters/i10548.pdf),
(Schalliol, pp.6-7) is an interesting map of current and defunct public
and subsidized housing throughout the five boroughs. The map quickly
displays the concentration of subsidized housing throughout
mid-Brooklyn, the top of Manhattan and throughout the Bronx, alongside
the lack of it in Staten Island. Without reviewing similarly relevant
information prior to training any algorithm, previous assumptions made
about a data set may not be given adequate scrutiny.

The trade off between classifying the training data and the test data
comes from:

  - Knowing and understanding the context of the data
      - does the programmer have the relevant knowledge to identify a
        minimum number of useful variables?
      - conversely, does the same programmer have the vision to exclude
        un-useful observations?
  - Utilizing enough classified observations to train the algorithm
    whilst maintaining a larger enough test set to adequately test the
    algorithm.

Referring to the
[map](http://assets.press.princeton.edu/chapters/i10548.pdf), it seems
apparent the algorithm could be trained to classify the neighborhoods.
Removing household income and replacing it with another variable may
give us insight into the locations of different groups. Combining
housing cost, family size and ancestry may shine a little on whether
people of differing ancestries tend to reside near those of similar
backgrounds. If that is the case, the prediction rates could also
indicate which neighborhoods tend to see that phenomenon.

    ## Morris Heights         Inwood    Fort Greene  Crown Heights 
    ##            484            608            702            579

    ## Morris Heights         Inwood    Fort Greene  Crown Heights 
    ##      0.2039612      0.2562158      0.2958281      0.2439949

    ##  norm_famsizenh    norm_housing_costnh norm_householdincnh
    ##  Min.   :0.09091   Min.   :0.00000     Min.   :0.0000     
    ##  1st Qu.:0.72727   1st Qu.:0.01927     1st Qu.:0.9049     
    ##  Median :0.90909   Median :0.02602     Median :0.9497     
    ##  Mean   :0.84940   Mean   :0.20803     Mean   :0.9239     
    ##  3rd Qu.:1.00000   3rd Qu.:0.03363     3rd Qu.:0.9760     
    ##  Max.   :1.00000   Max.   :1.00000     Max.   :1.0000

    ## [1] 1.0000000 0.7292007
    ## [1] 3.0000000 0.4665579
    ## [1] 5.0000000 0.4959217
    ## [1] 7.0000000 0.4714519
    ## [1] 9.0000000 0.4926591

The sample of 4 neighborhoods returns higher prediction rates as k
increases. However, the sample size of the neighborhoods is too small to
generalize for the entire city. The selection of the neighborhoods
reflects my bias; Inwood is where I live in Manhattan, Morris Heights is
across the bridge in The Bronx, nearby to a university and community
college, Fort Greene and Crown Heights were selected to demonstrate
potential differences of household income in nearby neighborhoods in a
single borough. Predicting neighborhoods for New York City may be more
accurate if variables like ancestry were included but given the
transient nature of many of the city’s inhabitants and recent shocks to
the real estate market, it is likely the predictions of the algorithm
would hold only for a short period of time.

**Bibiliography** Schalliol, D. (2016). Affordable Housing in New York:
The People, Places, and Policies That Transformed a City (Bloom N. &
Lasner M., Eds.). Princeton; Oxford: Princeton University Press.
<http://assets.press.princeton.edu/chapters/i10548.pdf>
