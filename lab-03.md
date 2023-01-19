Lab 03 - Nobel laureates
================
Cat Seitz
01.19.23

### Load packages and data

``` r
library(tidyverse) 
```

``` r
nobel <- read_csv("data/nobel.csv")
```

## Exercises

### Exercise 1 - examine dataset

Each row is a different Nobel laureate. There are 935 observations with
26 variables.

### Exercise 2 - create new data frame

Code worked to create a new data frame with 228 observations.

``` r
nobel_living <- nobel %>% 
  subset(is.na(died_date)) %>%
  filter(gender != "org") %>%
  drop_na(country)
```

### Exercise 3

### Exercise 4

…

### Exercise 5

…

### Exercise 6

…
