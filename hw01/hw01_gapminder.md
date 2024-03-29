Exploration of Gapminder
================
Dan Hadley
9/17/2019

## 1\. Introduction

We explore the gapminder dataset available in the gapminder package. All
analyses are performed using the `R` software with the following
packages:
[gapminder](https://cran.r-project.org/web/packages/gapminder/index.html),
[tibble](https://cran.r-project.org/web/packages/tibble/index.html),
[DT](https://cran.r-project.org/web/packages/DT/index.html),
[knitr](https://cran.r-project.org/web/packages/knitr/index.html).
<!--[ggplot2](https://cran.r-project.org/web/packages/ggplot2/index.html),-->

This exploration should give the reader an idea of the type of data the
`gapminder` dataset contains and some interesting analyses that can be
performed on the data.

## 2\. Overview

To start, we can view the column names in the dataset using the
`names()`
    function.

    ## [1] "country"   "continent" "year"      "lifeExp"   "pop"       "gdpPercap"

The columns in the dataset are Country, Continent, Year, Life
Expectancy, Population, and GDP per capita. To see the data type for
each column, we can view the structure of the dataset via the `str()`
function.

    ## Classes 'tbl_df', 'tbl' and 'data.frame':    1704 obs. of  6 variables:
    ##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
    ##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
    ##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
    ##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
    ##  $ gdpPercap: num  779 821 853 836 740 ...

The result shows the `gapminder` class as well as the data type for each
column. Note that both country and continent are labeled as factors.
Factor is a data type in `R` used for character data, essentially
treating each unique character entry as a group. The data type of each
column is useful when applying functions to column data.

To get a feel for the gapminder dataset, we can view the first 6 rows
using the `head()` function.

    ## # A tibble: 6 x 6
    ##   country     continent  year lifeExp      pop gdpPercap
    ##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ## 1 Afghanistan Asia       1952    28.8  8425333      779.
    ## 2 Afghanistan Asia       1957    30.3  9240934      821.
    ## 3 Afghanistan Asia       1962    32.0 10267083      853.
    ## 4 Afghanistan Asia       1967    34.0 11537966      836.
    ## 5 Afghanistan Asia       1972    36.1 13079460      740.
    ## 6 Afghanistan Asia       1977    38.4 14880372      786.

The result is a 6 row and 6 column object called a tibble. The dataset
contains information on the life expectancy (in years), population, and
GDP per capita (US$, inflation-adjusted) for 142 countries from 1952 to
2007 measured every 5 years. The complete `gapminder` data set has 1704
observations.

## 3\. Analysis

To get a feel for the dataset, the `summary()` function calclulates the
minimum, 3rd quartile, median, mean, 1st quartile, and maximum value for
all numeric columns. Columns with character data, often saved as the
factor data type in `R`, performs counts on the unique character
entries.

    ##         country        continent        year         lifeExp     
    ##  Afghanistan:  12   Africa  :624   Min.   :1952   Min.   :23.60  
    ##  Albania    :  12   Americas:300   1st Qu.:1966   1st Qu.:48.20  
    ##  Algeria    :  12   Asia    :396   Median :1980   Median :60.71  
    ##  Angola     :  12   Europe  :360   Mean   :1980   Mean   :59.47  
    ##  Argentina  :  12   Oceania : 24   3rd Qu.:1993   3rd Qu.:70.85  
    ##  Australia  :  12                  Max.   :2007   Max.   :82.60  
    ##  (Other)    :1632                                                
    ##       pop              gdpPercap       
    ##  Min.   :6.001e+04   Min.   :   241.2  
    ##  1st Qu.:2.794e+06   1st Qu.:  1202.1  
    ##  Median :7.024e+06   Median :  3531.8  
    ##  Mean   :2.960e+07   Mean   :  7215.3  
    ##  3rd Qu.:1.959e+07   3rd Qu.:  9325.5  
    ##  Max.   :1.319e+09   Max.   :113523.1  
    ## 

Africa has 624 observations, which is 276 more than the next continent,
Asia. For numerical data, `summary()` presents a quick snapshot of its
distribution. For example, we see that GDP per capita ranges from 24 USD
to 624 USD, and the mean (7215.3270812) is twice as large as the median
(3531.8469885). Thus, the GDP per capita data has a large positive skew.

### 3.1 Life Expectancy by Continent

Like `summary()`, boxplots provide a snapshot of the distribution of
data, allowing comparison across groups. In this case, we compare the
distribution of life expectancies by continent for four years: 1952,
1967, 1987, and 2007.

![](hw01_gapminder_files/boxplots-1.png)<!-- -->

From the boxplots, it is clear that life expectancies of Asian countries
have steadily increased since 1952, and the interquartile range has
gotten much smaller. This indicates that the difference between
countries with long and short life expectancies is shrinking.

### 3.2 Life Expectancy and GDP per Capita in 2007

The relationship between Life Expectancy and GDP per capita for the most
recent year, 2007, can be visualized with a scatterplot for all 142
countries.

![](hw01_gapminder_files/gdp-vs-lifeExp-1.png)<!-- -->

Japan had the highest life expectancy in 2007 of 82.6 years, and Norway
had the highest GDP per capita in 2007 at US$49357.19. Meanwhile,
Swaziland had the lowest life expectancy in 2007 at 39.6 years.

### 3.3 Life Expectancy and GDP per Capita for Canada

The relationship between life expectancy and GDP per capita for Canada
over time can be visualized by a scatterplot of the data for every 5
years from 1952 to 2007. The plot symbols are the years of the
observations, which indicate an increasing relationship over time.

![Plot of Life Expectancy (years) versus GDP per capita (USD) in Canada
every five years from 1952 to 2007](hw01_gapminder_files/Canada-1.png)
