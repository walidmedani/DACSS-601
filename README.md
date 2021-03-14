# DACSS-601
Projects and homework assignments for DACSS-601 taught by Meredith Rolfe

---
title: "Homework_3"
author: "Walid Medani"
date: "3/13/2021"
output:
  html_document:
    df_print: paged
  tufte::tufte_handout:
    citation_package: natbib
    latex_engine: xelatex
  tufte::tufte_book:
    citation_package: natbib
    latex_engine: xelatex
  tufte::tufte_html: default
urlcolor: blue
fontsize: 18pt
monofont: Times New Roman
runningheader: Univariate statistics
link-citations: yes
---

```{css}
.chunkcolor {
background-color: MistyRose;
}
```

```{r warning=TRUE, include=FALSE}
library(tidyverse)
library(tinytex)
library(kableExtra)
library(dplyr)
```

```{r read file, class.source="chunkcolor", include=FALSE}
chinaprojects<- read_csv("Source_Data.csv")
```

# Introduction


The following data-set is the pre-merged version taken from AidData, a research lab at William & Mary. It observes China's government-financed development projects abroad between 2000-2014. This data-set includes 3,485 projects that are worth $273.6 billion in total financing and observes these projects over 20 different variables. 

We will be using the two variables <h style="color:brown">'transactions_start_year'</h> and <h style="color:brown">'total_commitments'</h> to examine some descriptive statistics.

```{r variables, class.source="chunkcolor"}
select(chinaprojects, transactions_start_year, total_commitments)%>%
head()%>%
kbl()%>%
kable_classic("striped", full_width = F)
```


## Descriptive Statistics
Below we will examine some descriptive statistics of the variable <h style="color:brown">'total_commitments'</h> and <h style="color:brown">'transactions_start_year'</h>.


```{r stats of total commitments, class.source="chunkcolor"}
summarize(chinaprojects, Mean = mean(total_commitments, na.rm = TRUE), Median = median(total_commitments, na.rm = TRUE), StandardDev = sd(total_commitments, na.rm = TRUE), IQR = IQR(total_commitments, na.rm = TRUE))%>%
kbl(format.args = list(decimal.mark = '.', big.mark = ","))%>%
kable_classic(full_width = F)
```
Frequency of projects by year:
```{r frequency of projects, class.source="chunkcolor"}
table(chinaprojects$transactions_start_year)%>%
kbl()%>%
kable_classic(full_width = F)
```
Percentage of spending by year
```{r percentages, class.source="chunkcolor"}
prop.table(xtabs(total_commitments ~ transactions_start_year, chinaprojects))*100
```

Graph:
```{r graphsfsfsa, class.source="chunkcolor"}
ggplot(chinaprojects, aes(transactions_start_year, fill= total_commitments)) + 
geom_bar() +
  labs(title="Bar Chart", 
       subtitle="Chinese Abroad Project Spending by Year", 
       caption="Source: AidData by William & Mary")
```

# Sources

[Original publication](https://www.aiddata.org/data/chinas-public-diplomacy-dashboard-dataset-version-1-0)

[Pre-merged data](https://www.aiddata.org/data/geocoded-chinese-global-official-finance-dataset)
