Homework 3
================
Patrick Sinclair

For the initial k-nn classification, the determining variables were
personal Income Total and Housing Cost, and the population was limited
to NYC residents between the ages of 21 and 65.

Which returned the following results:

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
