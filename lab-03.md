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

### Exercise 1

Each row is a different Nobel laureate. There are 935 observations with
26 variables.

### Exercise 2

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

![](lab-03_files/figure-gfm/living%20laureate%20location-1.png)<!-- -->

These results seem to replicate the data shown in the Buzzfeed article
(their first graph), but don’t necessarily support the overall headline
yet.

### Exercise 4

``` r
nobel_living_science <- nobel_living_science %>%
  mutate(born_country_us = if_else(born_country =="USA", "USA", "Other"))


ggplot(nobel_living_science, aes(x=born_country_us))+
  geom_bar()
```

![](lab-03_files/figure-gfm/laureate%20birth%20place-1.png)<!-- -->

``` r
count(nobel_living_science,born_country_us)
```

    ## # A tibble: 2 × 2
    ##   born_country_us     n
    ##   <chr>           <int>
    ## 1 Other             123
    ## 2 USA               105

105 living Nobel laureates were born in the U.s.

### Exercise 5

``` r
ggplot(nobel_living_science, aes(x=country_us, color=born_country_us, fill=born_country_us))+
  geom_bar()+
  facet_wrap(~category)+
  coord_flip()+
  labs(title = "Location of living Nobel laureate winner by field",
       y="Number of winners",
       x="USA vs. other")
```

![](lab-03_files/figure-gfm/laureate%20location%20and%20birth%20place-1.png)<!-- -->

Yes, these data support Buzzfeed’s claim. While the majority of winners
reside in the U.S. when they receive the award, the majority of winners
in all disciplines except economics were born outside of the U.S.

### Exercise 6

``` r
nobel_living_science %>% 
  filter(country_us=="USA" & born_country_us=="Other") %>%
  count(born_country) %>%
  arrange(desc(n))
```

    ## # A tibble: 21 × 2
    ##    born_country       n
    ##    <chr>          <int>
    ##  1 Germany            7
    ##  2 United Kingdom     7
    ##  3 China              5
    ##  4 Canada             4
    ##  5 Japan              3
    ##  6 Australia          2
    ##  7 Israel             2
    ##  8 Norway             2
    ##  9 Austria            1
    ## 10 Finland            1
    ## # … with 11 more rows

Germany and the United Kingdom are tied for the most Nobel laureates
being born there.
