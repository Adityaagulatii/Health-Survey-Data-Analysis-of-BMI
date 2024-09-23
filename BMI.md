``` r
# Load the NHANES and dplyr packages
library(NHANES)
```

    ## Warning: package 'NHANES' was built under R version 4.2.3

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
# Load the NHANESraw data
data("NHANESraw")
glimpse(NHANESraw)
```

    ## Rows: 20,293
    ## Columns: 78
    ## $ ID               <int> 51624, 51625, 51626, 51627, 51628, 51629, 51630, 5163…
    ## $ SurveyYr         <fct> 2009_10, 2009_10, 2009_10, 2009_10, 2009_10, 2009_10,…
    ## $ Gender           <fct> male, male, male, male, female, male, female, female,…
    ## $ Age              <int> 34, 4, 16, 10, 60, 26, 49, 1, 10, 80, 10, 80, 4, 35, …
    ## $ AgeMonths        <int> 409, 49, 202, 131, 722, 313, 596, 12, 124, NA, 121, N…
    ## $ Race1            <fct> White, Other, Black, Black, Black, Mexican, White, Wh…
    ## $ Race3            <fct> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ Education        <fct> High School, NA, NA, NA, High School, 9 - 11th Grade,…
    ## $ MaritalStatus    <fct> Married, NA, NA, NA, Widowed, Married, LivePartner, N…
    ## $ HHIncome         <fct> 25000-34999, 20000-24999, 45000-54999, 20000-24999, 1…
    ## $ HHIncomeMid      <int> 30000, 22500, 50000, 22500, 12500, 30000, 40000, 4000…
    ## $ Poverty          <dbl> 1.36, 1.07, 2.27, 0.81, 0.69, 1.01, 1.91, 1.36, 2.68,…
    ## $ HomeRooms        <int> 6, 9, 5, 6, 6, 4, 5, 5, 7, 4, 5, 5, 7, NA, 6, 6, 5, 6…
    ## $ HomeOwn          <fct> Own, Own, Own, Rent, Rent, Rent, Rent, Rent, Own, Own…
    ## $ Work             <fct> NotWorking, NA, NotWorking, NA, NotWorking, Working, …
    ## $ Weight           <dbl> 87.4, 17.0, 72.3, 39.8, 116.8, 97.6, 86.7, 9.4, 26.0,…
    ## $ Length           <dbl> NA, NA, NA, NA, NA, NA, NA, 75.7, NA, NA, NA, NA, NA,…
    ## $ HeadCirc         <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ Height           <dbl> 164.7, 105.4, 181.3, 147.8, 166.0, 173.0, 168.4, NA, …
    ## $ BMI              <dbl> 32.22, 15.30, 22.00, 18.22, 42.39, 32.61, 30.57, NA, …
    ## $ BMICatUnder20yrs <fct> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ BMI_WHO          <fct> 30.0_plus, 12.0_18.5, 18.5_to_24.9, 12.0_18.5, 30.0_p…
    ## $ Pulse            <int> 70, NA, 68, 68, 72, 72, 86, NA, 70, 88, 84, 54, NA, N…
    ## $ BPSysAve         <int> 113, NA, 109, 93, 150, 104, 112, NA, 108, 139, 94, 12…
    ## $ BPDiaAve         <int> 85, NA, 59, 41, 68, 49, 75, NA, 53, 43, 45, 60, NA, N…
    ## $ BPSys1           <int> 114, NA, 112, 92, 154, 102, 118, NA, 106, 142, 94, 12…
    ## $ BPDia1           <int> 88, NA, 62, 36, 70, 50, 82, NA, 60, 62, 38, 62, NA, N…
    ## $ BPSys2           <int> 114, NA, 114, 94, 150, 104, 108, NA, 106, 140, 92, 12…
    ## $ BPDia2           <int> 88, NA, 60, 44, 68, 48, 74, NA, 50, 46, 40, 62, NA, N…
    ## $ BPSys3           <int> 112, NA, 104, 92, 150, 104, 116, NA, 110, 138, 96, 11…
    ## $ BPDia3           <int> 82, NA, 58, 38, 68, 50, 76, NA, 56, 40, 50, 58, NA, N…
    ## $ Testosterone     <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ DirectChol       <dbl> 1.29, NA, 1.55, 1.89, 1.16, 1.16, 1.16, NA, 1.58, 1.9…
    ## $ TotChol          <dbl> 3.49, NA, 4.97, 4.16, 5.22, 4.14, 6.70, NA, 4.14, 4.7…
    ## $ UrineVol1        <int> 352, NA, 281, 139, 30, 202, 77, NA, 39, 128, 109, 38,…
    ## $ UrineFlow1       <dbl> NA, NA, 0.415, 1.078, 0.476, 0.563, 0.094, NA, 0.300,…
    ## $ UrineVol2        <int> NA, NA, NA, NA, 246, NA, NA, NA, NA, NA, NA, NA, NA, …
    ## $ UrineFlow2       <dbl> NA, NA, NA, NA, 2.51, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ Diabetes         <fct> No, No, No, No, Yes, No, No, No, No, No, No, Yes, No,…
    ## $ DiabetesAge      <int> NA, NA, NA, NA, 56, NA, NA, NA, NA, NA, NA, 70, NA, N…
    ## $ HealthGen        <fct> Good, NA, Vgood, NA, Fair, Good, Good, NA, NA, Excell…
    ## $ DaysPhysHlthBad  <int> 0, NA, 2, NA, 20, 2, 0, NA, NA, 0, NA, 0, NA, NA, NA,…
    ## $ DaysMentHlthBad  <int> 15, NA, 0, NA, 25, 14, 10, NA, NA, 0, NA, 0, NA, NA, …
    ## $ LittleInterest   <fct> Most, NA, NA, NA, Most, None, Several, NA, NA, None, …
    ## $ Depressed        <fct> Several, NA, NA, NA, Most, Most, Several, NA, NA, Non…
    ## $ nPregnancies     <int> NA, NA, NA, NA, 1, NA, 2, NA, NA, NA, NA, NA, NA, NA,…
    ## $ nBabies          <int> NA, NA, NA, NA, 1, NA, 2, NA, NA, NA, NA, NA, NA, NA,…
    ## $ Age1stBaby       <int> NA, NA, NA, NA, NA, NA, 27, NA, NA, NA, NA, NA, NA, N…
    ## $ SleepHrsNight    <int> 4, NA, 8, NA, 4, 4, 8, NA, NA, 6, NA, 9, NA, 7, NA, N…
    ## $ SleepTrouble     <fct> Yes, NA, No, NA, No, No, Yes, NA, NA, No, NA, No, NA,…
    ## $ PhysActive       <fct> No, NA, Yes, NA, No, Yes, No, NA, NA, Yes, NA, No, NA…
    ## $ PhysActiveDays   <int> NA, NA, 5, NA, NA, 2, NA, NA, NA, 4, NA, NA, NA, NA, …
    ## $ TVHrsDay         <fct> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ CompHrsDay       <fct> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ TVHrsDayChild    <int> NA, 4, NA, 1, NA, NA, NA, NA, 1, NA, 3, NA, 2, NA, 5,…
    ## $ CompHrsDayChild  <int> NA, 1, NA, 1, NA, NA, NA, NA, 0, NA, 0, NA, 1, NA, 0,…
    ## $ Alcohol12PlusYr  <fct> Yes, NA, NA, NA, No, Yes, Yes, NA, NA, Yes, NA, No, N…
    ## $ AlcoholDay       <int> NA, NA, NA, NA, NA, 19, 2, NA, NA, 1, NA, NA, NA, NA,…
    ## $ AlcoholYear      <int> 0, NA, NA, NA, 0, 48, 20, NA, NA, 52, NA, 0, NA, NA, …
    ## $ SmokeNow         <fct> No, NA, NA, NA, Yes, No, Yes, NA, NA, No, NA, No, NA,…
    ## $ Smoke100         <fct> Yes, NA, NA, NA, Yes, Yes, Yes, NA, NA, Yes, NA, Yes,…
    ## $ SmokeAge         <int> 18, NA, NA, NA, 16, 15, 38, NA, NA, 16, NA, 21, NA, N…
    ## $ Marijuana        <fct> Yes, NA, NA, NA, NA, Yes, Yes, NA, NA, NA, NA, NA, NA…
    ## $ AgeFirstMarij    <int> 17, NA, NA, NA, NA, 10, 18, NA, NA, NA, NA, NA, NA, N…
    ## $ RegularMarij     <fct> No, NA, NA, NA, NA, Yes, No, NA, NA, NA, NA, NA, NA, …
    ## $ AgeRegMarij      <int> NA, NA, NA, NA, NA, 12, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ HardDrugs        <fct> Yes, NA, NA, NA, No, Yes, Yes, NA, NA, NA, NA, NA, NA…
    ## $ SexEver          <fct> Yes, NA, NA, NA, Yes, Yes, Yes, NA, NA, NA, NA, NA, N…
    ## $ SexAge           <int> 16, NA, NA, NA, 15, 9, 12, NA, NA, NA, NA, NA, NA, NA…
    ## $ SexNumPartnLife  <int> 8, NA, NA, NA, 4, 10, 10, NA, NA, NA, NA, NA, NA, NA,…
    ## $ SexNumPartYear   <int> 1, NA, NA, NA, NA, 1, 1, NA, NA, NA, NA, NA, NA, NA, …
    ## $ SameSex          <fct> No, NA, NA, NA, No, No, Yes, NA, NA, NA, NA, NA, NA, …
    ## $ SexOrientation   <fct> Heterosexual, NA, NA, NA, NA, Heterosexual, Heterosex…
    ## $ WTINT2YR         <dbl> 80100.544, 53901.104, 13953.078, 11664.899, 20090.339…
    ## $ WTMEC2YR         <dbl> 81528.772, 56995.035, 14509.279, 12041.635, 21000.339…
    ## $ SDMVPSU          <int> 1, 2, 1, 2, 2, 1, 2, 2, 2, 1, 1, 1, 2, 2, 1, 1, 1, 1,…
    ## $ SDMVSTRA         <int> 83, 79, 84, 86, 75, 88, 85, 86, 88, 77, 86, 79, 84, 7…
    ## $ PregnantNow      <fct> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, U…

## 2. Visualize survey weight and strata variables

```{=html}
<p>
```
The glimpse() function reveals that the NHANESraw data contains many
health measurement variables, including a sampling weight variable
WTMEC2YR.\</p?\>

```{=html}
<p>
```
Since the NHANESraw data spans 4 years (2009--2012) and the sampling
weights are based on 2 years of data, a new weight variable needs to be
created to scale the sample across the full 4 years. Currently, the
weights sum to 2 times the US population number. To adjust this, the
2-year weight is divided in half so that the total sum of the weights
equals the US population.
```{=html}
</p>
```
```{=html}
<p>
```
The NHANES data has oversampled some geographic regions and specific
minority groups. Examining the distribution of sampling weights for each
race reveals that Whites are undersampled and have higher weights, while
oversampled groups like Black, Mexican, and Hispanic individuals have
lower weights, since each sampled person in these minority groups
represents fewer US people.
```{=html}
</p>
```
``` r
# Load the ggplot2 package
library(ggplot2)
```

    ## Warning: package 'ggplot2' was built under R version 4.2.3

``` r
# Use mutate to create a 4-year weight variable and call it WTMEC4YR
NHANESraw <- NHANESraw %>% mutate(WTMEC4YR = WTMEC2YR/2)

# Calculate the sum of this weight variable
NHANESraw %>% summarize(sum(WTMEC4YR))
```

    ## # A tibble: 1 × 1
    ##   `sum(WTMEC4YR)`
    ##             <dbl>
    ## 1      304267200.

``` r
# Plot the sample weights using boxplots, with Race1 on the x-axis
ggplot(NHANESraw, aes(x = Race1, y = WTMEC4YR)) + geom_boxplot()
```

![](BMI_files/figure-markdown/unnamed-chunk-2-1.png) \## 3. Specify the
survey design
```{=html}
<p>
```
The survey package will be used to specify the complex survey design
that will be applied in later analyses. It is essential to specify the
design so that the sampling weights and design are used correctly in the
statistical models.
```{=html}
</p>
```
```{=html}
<p>
```
The NHANESraw data includes a strata variable SDMVSTRA, and a cluster ID
variable (also known as a primary sampling unit, PSU), SDMVPSU, that
accounts for the design effects of clustering. These clusters (PSUs) are
nested within strata.
```{=html}
</p>
```
``` r
# Load the survey package
library(survey)
```

    ## Warning: package 'survey' was built under R version 4.2.3

    ## Loading required package: grid

    ## Loading required package: Matrix

    ## Loading required package: survival

    ## 
    ## Attaching package: 'survey'

    ## The following object is masked from 'package:graphics':
    ## 
    ##     dotchart

``` r
# Specify the survey design
nhanes_design <- svydesign(
    data = NHANESraw, 
    strata = ~SDMVSTRA, 
    id = ~SDMVPSU, 
    nest = TRUE, 
    weights = ~WTMEC4YR)

# Print a summary of this design
summary(nhanes_design)
```

    ## Stratified 1 - level Cluster Sampling design (with replacement)
    ## With (62) clusters.
    ## svydesign(data = NHANESraw, strata = ~SDMVSTRA, id = ~SDMVPSU, 
    ##     nest = TRUE, weights = ~WTMEC4YR)
    ## Probabilities:
    ##      Min.   1st Qu.    Median      Mean   3rd Qu.      Max. 
    ## 8.986e-06 5.664e-05 1.054e-04       Inf 1.721e-04       Inf 
    ## Stratum Sizes: 
    ##             75  76  77  78  79  80  81  82  83  84  85  86  87  88  89  90  91
    ## obs        803 785 823 829 696 751 696 724 713 683 592 946 598 647 251 862 998
    ## design.PSU   2   2   2   2   2   2   2   2   2   2   2   3   2   2   2   3   3
    ## actual.PSU   2   2   2   2   2   2   2   2   2   2   2   3   2   2   2   3   3
    ##             92  93  94  95  96  97  98  99 100 101 102 103
    ## obs        875 602 688 722 676 608 708 682 700 715 624 296
    ## design.PSU   3   2   2   2   2   2   2   2   2   2   2   2
    ## actual.PSU   3   2   2   2   2   2   2   2   2   2   2   2
    ## Data variables:
    ##  [1] "ID"               "SurveyYr"         "Gender"           "Age"             
    ##  [5] "AgeMonths"        "Race1"            "Race3"            "Education"       
    ##  [9] "MaritalStatus"    "HHIncome"         "HHIncomeMid"      "Poverty"         
    ## [13] "HomeRooms"        "HomeOwn"          "Work"             "Weight"          
    ## [17] "Length"           "HeadCirc"         "Height"           "BMI"             
    ## [21] "BMICatUnder20yrs" "BMI_WHO"          "Pulse"            "BPSysAve"        
    ## [25] "BPDiaAve"         "BPSys1"           "BPDia1"           "BPSys2"          
    ## [29] "BPDia2"           "BPSys3"           "BPDia3"           "Testosterone"    
    ## [33] "DirectChol"       "TotChol"          "UrineVol1"        "UrineFlow1"      
    ## [37] "UrineVol2"        "UrineFlow2"       "Diabetes"         "DiabetesAge"     
    ## [41] "HealthGen"        "DaysPhysHlthBad"  "DaysMentHlthBad"  "LittleInterest"  
    ## [45] "Depressed"        "nPregnancies"     "nBabies"          "Age1stBaby"      
    ## [49] "SleepHrsNight"    "SleepTrouble"     "PhysActive"       "PhysActiveDays"  
    ## [53] "TVHrsDay"         "CompHrsDay"       "TVHrsDayChild"    "CompHrsDayChild" 
    ## [57] "Alcohol12PlusYr"  "AlcoholDay"       "AlcoholYear"      "SmokeNow"        
    ## [61] "Smoke100"         "SmokeAge"         "Marijuana"        "AgeFirstMarij"   
    ## [65] "RegularMarij"     "AgeRegMarij"      "HardDrugs"        "SexEver"         
    ## [69] "SexAge"           "SexNumPartnLife"  "SexNumPartYear"   "SameSex"         
    ## [73] "SexOrientation"   "WTINT2YR"         "WTMEC2YR"         "SDMVPSU"         
    ## [77] "SDMVSTRA"         "PregnantNow"      "WTMEC4YR"

## 4. Subset the data

```{=html}
<p>
```
Analysis of survey data requires careful consideration of the sampling
design and weights at every step. Something as simple as filtering the
data becomes complicated when weights are involved.
```{=html}
</p>
```
```{=html}
<p>
```
When examining a subset of the data (i.e., the subpopulation of adult
Hispanics with diabetes, or pregnant women), it must be explicitly
specified in the design. Simply removing that subset of the data through
filtering the raw data is not appropriate because the survey weights
will no longer be correct and will not add up to the full US population.
```{=html}
</p>
```
```{=html}
<p>
```
BMI categories differ for children and young adults younger than 20, so
the data will be subsetted to only analyze adults of at least 20 years
of age.
```{=html}
</p>
```
``` r
# Select adults of Age >= 20 with subset
nhanes_adult <- subset(nhanes_design, Age >= 20)

# Print a summary of this subset
summary(nhanes_adult)
```

    ## Stratified 1 - level Cluster Sampling design (with replacement)
    ## With (62) clusters.
    ## subset(nhanes_design, Age >= 20)
    ## Probabilities:
    ##      Min.   1st Qu.    Median      Mean   3rd Qu.      Max. 
    ## 8.986e-06 4.303e-05 8.107e-05       Inf 1.240e-04       Inf 
    ## Stratum Sizes: 
    ##             75  76  77  78  79  80  81  82  83  84  85  86  87  88  89  90  91
    ## obs        471 490 526 500 410 464 447 400 411 395 357 512 327 355 153 509 560
    ## design.PSU   2   2   2   2   2   2   2   2   2   2   2   3   2   2   2   3   3
    ## actual.PSU   2   2   2   2   2   2   2   2   2   2   2   3   2   2   2   3   3
    ##             92  93  94  95  96  97  98  99 100 101 102 103
    ## obs        483 376 368 454 362 315 414 409 377 460 308 165
    ## design.PSU   3   2   2   2   2   2   2   2   2   2   2   2
    ## actual.PSU   3   2   2   2   2   2   2   2   2   2   2   2
    ## Data variables:
    ##  [1] "ID"               "SurveyYr"         "Gender"           "Age"             
    ##  [5] "AgeMonths"        "Race1"            "Race3"            "Education"       
    ##  [9] "MaritalStatus"    "HHIncome"         "HHIncomeMid"      "Poverty"         
    ## [13] "HomeRooms"        "HomeOwn"          "Work"             "Weight"          
    ## [17] "Length"           "HeadCirc"         "Height"           "BMI"             
    ## [21] "BMICatUnder20yrs" "BMI_WHO"          "Pulse"            "BPSysAve"        
    ## [25] "BPDiaAve"         "BPSys1"           "BPDia1"           "BPSys2"          
    ## [29] "BPDia2"           "BPSys3"           "BPDia3"           "Testosterone"    
    ## [33] "DirectChol"       "TotChol"          "UrineVol1"        "UrineFlow1"      
    ## [37] "UrineVol2"        "UrineFlow2"       "Diabetes"         "DiabetesAge"     
    ## [41] "HealthGen"        "DaysPhysHlthBad"  "DaysMentHlthBad"  "LittleInterest"  
    ## [45] "Depressed"        "nPregnancies"     "nBabies"          "Age1stBaby"      
    ## [49] "SleepHrsNight"    "SleepTrouble"     "PhysActive"       "PhysActiveDays"  
    ## [53] "TVHrsDay"         "CompHrsDay"       "TVHrsDayChild"    "CompHrsDayChild" 
    ## [57] "Alcohol12PlusYr"  "AlcoholDay"       "AlcoholYear"      "SmokeNow"        
    ## [61] "Smoke100"         "SmokeAge"         "Marijuana"        "AgeFirstMarij"   
    ## [65] "RegularMarij"     "AgeRegMarij"      "HardDrugs"        "SexEver"         
    ## [69] "SexAge"           "SexNumPartnLife"  "SexNumPartYear"   "SameSex"         
    ## [73] "SexOrientation"   "WTINT2YR"         "WTMEC2YR"         "SDMVPSU"         
    ## [77] "SDMVSTRA"         "PregnantNow"      "WTMEC4YR"

``` r
# Compare the number of observations in the full data to the adult data
nrow(nhanes_design)
```

    ## [1] 20293

## 5. Visualizing BMI

```{=html}
<p>
```
svydesign() is utilized to structure the survey data appropriately, but
how does this contribute to understanding the full US population?
Through survey methods, the sampling weights can be used to estimate the
true distributions of measurements within the entire population. This
approach is effective for calculating various statistics such as means,
proportions, and standard deviations.
```{=html}
</p>
```
```{=html}
<p>
```
Survey methods will be used to estimate the average BMI in the US adult
population and to create a weighted histogram of the distribution.
```{=html}
</p>
```
``` r
# Calculate the mean BMI in NHANESraw
bmi_mean_raw <- NHANESraw %>% 
    filter(Age >= 20) %>%
    summarize(mean(BMI, na.rm=TRUE))
bmi_mean_raw
```

    ## # A tibble: 1 × 1
    ##   `mean(BMI, na.rm = TRUE)`
    ##                       <dbl>
    ## 1                      29.0

``` r
# Calculate the survey-weighted mean BMI of US adults
bmi_mean <- svymean(~BMI, design = nhanes_adult, na.rm = TRUE)
bmi_mean
```

    ##       mean     SE
    ## BMI 28.734 0.1235

``` r
# Draw a weighted histogram of BMI in the US population
NHANESraw %>% 
  filter(Age >= 20) %>%
    ggplot(mapping = aes(x = BMI, weight = WTMEC4YR)) + 
    geom_histogram()+
    geom_vline(xintercept = coef(bmi_mean), color="red")
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

    ## Warning: Removed 547 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](BMI_files/figure-markdown/unnamed-chunk-5-1.png) \## 6. Is BMI lower
in physically active people?
```{=html}
<p>
```
The distribution of BMI appears as expected, with most people under 40
kg/m`<sup>`{=html}2`</sup>`{=html} and a slight positive skewness due to
a few individuals having much higher BMI. Now, the question of interest
is whether the distribution of BMI differs between people who are
physically active versus those who are not. This can be visually
compared using a boxplot and formally tested for differences in mean
BMI.
```{=html}
</p>
```
``` r
# Load the broom library
library(broom)

# Conduct a t-test comparing mean BMI between physically active status
survey_ttest <- svyttest(BMI~PhysActive, design = nhanes_adult)

# Use broom to show the tidy results
tidy(survey_ttest)
```

    ## # A tibble: 1 × 8
    ##   estimate statistic  p.value parameter conf.low conf.high method    alternative
    ##      <dbl>     <dbl>    <dbl>     <dbl>    <dbl>     <dbl> <chr>     <chr>      
    ## 1    -1.85     -9.72 4.56e-11        32    -2.23     -1.46 Design-b… two.sided

## 7. Could there be confounding by smoking? (part 1)

```{=html}
<p>
```
The relationship between physical activity and BMI is likely not as
straightforward as "if you exercise, your BMI will lower." Many other
lifestyle or demographic variables could confound this relationship.
Smoking status is one such variable. It raises questions such as whether
someone who smokes is more or less likely to be physically active, and
whether smokers are more likely to have higher or lower BMI. These
relationships can be examined in the survey data
```{=html}
</p>
```
```{=html}
<p>
```
First, the relationship between smoking and physical activity will be
examined.
```{=html}
</p>
```
``` r
# Estimate the proportion who are physically active by current smoking status
phys_by_smoke <- svyby(~PhysActive, by = ~SmokeNow, 
                       FUN = svymean, 
                       design = nhanes_adult, 
                       keep.names = FALSE)

# Print the table
phys_by_smoke
```

    ##   SmokeNow PhysActiveNo PhysActiveYes se.PhysActiveNo se.PhysActiveYes
    ## 1       No    0.4566990     0.5433010      0.01738054       0.01738054
    ## 2      Yes    0.5885421     0.4114579      0.01163246       0.01163246

``` r
# Plot the proportions with y-label
ggplot(data = phys_by_smoke, 
       aes(y = PhysActiveYes, x = SmokeNow, fill = SmokeNow)) +
    geom_col() +
    ylab("Proportion Physically Active")
```

![](BMI_files/figure-markdown/unnamed-chunk-7-1.png) \## 8. Could there
be confounding by smoking? (part 2)
```{=html}
<p>
```
Now, the relationship between smoking and BMI will be examined.
```{=html}
</p>
```
``` r
# Estimate mean BMI by current smoking status
BMI_by_smoke <- svyby(~BMI, by = ~SmokeNow, 
      FUN = svymean, 
      design = nhanes_adult, 
      na.rm = TRUE)
BMI_by_smoke
```

    ##     SmokeNow      BMI        se
    ## No        No 29.25734 0.1915138
    ## Yes      Yes 27.74873 0.1652377

## 9. Add smoking in the mix

```{=html}
<p>
```
It was observed that people who smoke are less likely to be physically
active and have a lower BMI on average. Additionally, people who are not
physically active tend to have a higher BMI on average. These seemingly
conflicting associations prompt a closer examination of how these
factors interact. To gain a better understanding, BMI can be compared by
physical activity, stratified by smoking status.
```{=html}
</p>
```
```{=html}
<p>
```
Previously, a simple t-test was used to compare mean BMI between
physically active and non-physically active people. To adjust for
smoking status, as well as other potential confounders or predictors of
BMI, a linear regression model with multiple independent variables can
be utilized. When dealing with survey data, a weighted linear regression
method, which is a special case of generalized linear models (GLMs), is
employed.
```{=html}
</p


```r
# Fit a multiple regression model
mod1 <- svyglm(BMI ~ PhysActive*SmokeNow, design = nhanes_adult)
# Tidy the model results
tidy_mod1 <- tidy(mod1)
tidy_mod1
```

```
## # A tibble: 4 × 5
##   term                      estimate std.error statistic  p.value
##   <chr>
```
                        <dbl>     <dbl>     <dbl>    <dbl>

## 1 (Intercept) 30.5 0.210 146. 2.62e-44

## 2 PhysActiveYes -2.35 0.236 -9.97 4.96e-11

## 3 SmokeNowYes -2.24 0.267 -8.40 2.26e- 9

## 4 PhysActiveYes:SmokeNowYes 1.00 0.344 2.92 6.52e- 3


    ```r
    # Calculate expected mean difference in BMI for activity within non-smokers
    diff_non_smoke <- tidy_mod1 %>% 
        filter(term=="PhysActiveYes") %>% 
        select(estimate)
    diff_non_smoke

    ## # A tibble: 1 × 1
    ##   estimate
    ##      <dbl>
    ## 1    -2.35

``` r
# Calculate expected mean difference in BMI for activity within smokers
diff_smoke <- tidy_mod1 %>% 
    filter(term%in%c("PhysActiveYes","PhysActiveYes:SmokeNowYes")) %>% 
    summarize(estimate = sum(estimate))
diff_smoke
```

    ## # A tibble: 1 × 1
    ##   estimate
    ##      <dbl>
    ## 1    -1.35
