---
title: "Meteorites"
output: github_document
---

```{r message=FALSE, warning=FALSE}
library(tidyverse)
library(RColorBrewer)
library

meteorites <- readr::read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-06-11/meteorites.csv")

#only last 50 years and create "Big One!" categories :)
meteorites<- meteorites %>%
  filter(year %in% 1969:2019 & !is.na(year) & !is.na(mass)) %>%
  mutate(size= factor(ntile(mass, 5)))


#bar plot
p<- ggplot(meteorites, aes(x=year, fill=size)) + geom_bar(position="fill") + scale_fill_brewer(palette="Spectral") + ggtitle("Quantiles of Meteorite Size (mass in grams) over the Last 50 years") + xlab("Year") + ylab("Percent") + scale_y_continuous(labels = scales::percent_format(accuracy = 1))
p
```

