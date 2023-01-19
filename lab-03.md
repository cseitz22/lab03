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

``` r
nobel_living <- nobel_living %>%
  mutate(country_us = if_else(country =="USA", "USA", "Other"))

nobel_living_science <- nobel_living %>%
  filter(category %in% c("Physics", "Medicine", "Chemistry", "Economics"))
```

### Exercise 3

``` r
ggplot(nobel_living_science, aes(x=country_us))+
  geom_bar()+
  facet_wrap(~category)+
  coord_flip()+
  labs(title = "Location of living Nobel laureate winner by field",
       y="Number of winners",
       x="USA vs. other")
```

![](lab-03_files/figure-gfm/living%20winners%20location-1.png)<!-- -->

These results seem to replicate the data shown in the Buzzfeed article
(their first graph), but don’t necessarily support the overall headline
yet.

### Exercise 4

…

### Exercise 5

…

### Exercise 6

…
