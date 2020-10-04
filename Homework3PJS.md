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
prediction rates of k = 1, 3, 5, 7 and 9

    ## [1] 1.0000000 0.3525155
    ## [1] 3.0000000 0.3441305
    ## [1] 5.0000000 0.3606708
    ## [1] 7.0000000 0.3700896
    ## [1] 9.0000000 0.3757179

``` r
dat_NYC <- subset(acs2017_ny, (acs2017_ny$in_NYC == 1)&(acs2017_ny$AGE > 20) & (acs2017_ny$AGE < 66))
# dat_NYCa <- subset(acs2017_ny, (acs2017_ny$in_NYC == 1)&(acs2017_ny$AGE > 24) & (acs2017_ny$AGE < 66))
# Bronx <- subset(acs2017_ny, (acs2017_ny$in_Bronx == 1)&(acs2017_ny$AGE > 24) & (acs2017_ny$AGE < 66))
attach(dat_NYC)
# attach(Bronx)
borough_f <- factor((in_Bronx + 2*in_Manhattan + 3*in_StatenI + 4*in_Brooklyn + 5*in_Queens), levels=c(1,2,3,4,5),labels = c("Bronx","Manhattan","Staten Island","Brooklyn","Queens"))
# ancestr1 <- factor(())
```

``` r
norm_varb <- function(X_in) {
  (max(X_in, na.rm = TRUE) - X_in)/( max(X_in, na.rm = TRUE) - min(X_in, na.rm = TRUE) )
}
```

``` r
is.na(OWNCOST) <- which(OWNCOST == 9999999)
# is.na(MIGPLAC1) <- which(MIGPLAC1 == 000 | MIGPLAC1 == 900 | MIGPLAC1 == 997 | MIGPLAC1 == 999)
# years <- norm_varb(YRSUSA1)
housing_cost <- OWNCOST + RENT
# norm_inc_tot <- norm_varb(INCTOT)
norm_householdinc <- norm_varb(HHINCOME)
norm_housing_cost <- norm_varb(housing_cost)
# norm_ancest <- norm_varb(anc1clean) 
norm_famsize <- norm_varb(FAMSIZE)
# traveltime <- norm_varb(TRANTIME)
```

``` r
data_use_prelim <- data.frame(norm_householdinc, norm_famsize, norm_housing_cost)
# norm_housing_cost, LINGISOL
good_obs_data_use <- complete.cases(data_use_prelim,borough_f)
# good_obs_data_use <- complete.cases(data_use_prelim,in_Brooklyn)
dat_use <- subset(data_use_prelim,good_obs_data_use)
y_use <- subset(borough_f,good_obs_data_use)
# y_use <- subset(in_Brooklyn,good_obs_data_use)
```
