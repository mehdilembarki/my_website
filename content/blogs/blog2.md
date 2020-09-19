---
categories:
- ""
- ""
date: "2017-10-31T22:26:09-05:00"
description: Lorem Etiam Nullam
draft: false
image: pic09.jpg
keywords: ""
slug: magna
title: Beer, wine and spirits
---
```{r, setup}
knitr::opts_chunk$set(
  message = FALSE, 
  warning = FALSE, 
  tidy=FALSE,     # display code as typed
  size="small")   # slightly smaller font for code
options(digits = 3)

# default figure size
knitr::opts_chunk$set(
  fig.width=6.75, 
  fig.height=6.75,
  fig.align = "center"
)
```


```{r load-libraries, warning=FALSE, message=FALSE, echo=FALSE}
library(tidyverse)  # Load ggplot2, dplyr, and all the other tidyverse packages
library(mosaic)
library(ggthemes)
library(lubridate)
library(fivethirtyeight)
library(here)
library(skimr)
library(janitor)
library(vroom)
library(tidyquant)
library(patchwork)

```



# Where Do People Drink The Most Beer, Wine And Spirits?



```{r load_alcohol_data}
library(fivethirtyeight)
data(drinks)

```



```{r glimpse_skim_data}
skim(drinks)
```
What are the variable types? Any missing values we should worry about?

Answer:

Variable types : character, numeric
There are no missing values

```{r beer_plot}

top25_beer_plot <- drinks %>% 
  top_n(25, beer_servings) %>% #ranked top 25 by beer servings
  ggplot(aes(
    x = beer_servings,
    y = reorder(country,beer_servings) #Ordered countries by beer servings
  )) +
  geom_col() +
  labs(
    x = "Beer Servings", 
    y = "Country", 
    title = "Top 25 Beer Consuming Countries") + #added labels to axis and title
  theme_minimal() +
  NULL

top25_beer_plot


```


```{r wine_plot}

#copied top 25 beer plot and replaced beer with wine
top25_wine_plot <- drinks %>% 
  top_n(25, wine_servings) %>% 
  ggplot(aes(
    x = wine_servings,
    y = reorder(country,wine_servings)
  )) +
  geom_col() +
  labs(
    x = "Wine Servings", 
    y = "Country", 
    title = "Top 25 Wine Consuming Countries") + 
  theme_minimal() +
  NULL

top25_wine_plot


```

```{r spirit_plot}

#copied top 25 beer plot and replaced beer with spirit
top25_spirit_plot <- drinks %>% 
  top_n(25, spirit_servings) %>% 
  ggplot(aes(
    x = spirit_servings,
    y = reorder(country,spirit_servings)
  )) +
  geom_col() +
  labs(
    x = "Spirit Servings", 
    y = "Country", 
    title = "Top 25 Spirit Consuming Countries") + 
  theme_minimal() +
  NULL

top25_spirit_plot

```

> IMPLICATIONS

- In the wine consumption rankings, 9 of the top 10 are European countries. Most areas of Europe (especially the low latitudes) are very suitable for growing grapes due to sufficient sunlight and fertile soil. The typical ones are Southern France, Portugal, Andorra, Italy, and Greece. This may develop the people's habit of drinking wine. Compared to wine, the high beer consuming countries are mainly in higher latitudes (north of the Alps), since wheat is widely planted and is an important raw material for beer in these countries. In addition, the beer ranking includes the most continents among other liquors, which may implicate that beer is the most widely accepted and accessible alcohol in the world.
- In the spirits consumption ranking, six of the top 25 are island countries in the Caribbean and the Pacific, and 11 of the top 25 are East European countries. This conforms to the origins of two very famous spirit types - rum and vodka.