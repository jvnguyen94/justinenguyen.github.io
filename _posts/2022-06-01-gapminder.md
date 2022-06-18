---
layout: post
title: Gapminder Visualization Brief
tags: [line chart, data brief]
comments: true
category: blog
---

<br>

![](/images/gap_asia.png)

<br>

#### 1) Description of Type of Graph

This is a line graph, which is good for comparing two numerical variables. Typically, we use line graphs when there is a correlation or continuation of the values on the x-axis.

<br>

#### 2) Description of Data

The data in the visualization is from the Gapminder dataset, which contains lots of historical data across many different countries from 1952 to 2007. 

<br>

#### 3) Audience and Purpose

The purpose of this visualization is to see if there is a correlation between fertility rate versus life expectancy in different regions of Asia in 1994 (arbitrarily picked year). Typically we see that fertility rate decreases as life expectancy increases. The audience for this could be anyone interested in socio-economics. 

<br>

#### 4) Representation Description

Line charts have numerical data on both x-axis and y-axis. They are good for comparing the relationship between two numerical variables, but also we can overlay single datapoints overlaying a line (mean) to see if the data follows a trend. If there are multiple groups that we want to compare, it is easy to distinguish various groups and show them in a way that makes it easier for comparison.

<br>

#### 5) What to Read and What to Look For

When first looking at a line chart, it is important to note the variables on the axes and the scales to which they exist. The next thing to note is how many lines are on the line plot! Typically, when there are multiple lines, this dictates different groups that we are comparing. Usually multiple lines are colored differently or the lines are dashed differently to distinguish the differing groups.

From this visualization, we see that Life expectancy is plotted on the x-axis while Fertility rate per 1000 is plotted on the y-axis. The regions of Asia are distinguished by dash types and colors. (I could not figure out how to combine the legends into a singular one... If I did that, the visualization will be better and less busy looking.) As you can see, there is a general trend of decreased fertility rate with countries that have higher life expectancy. 
<br>

#### 6) Presentation Tips

**Annotation:** Annotation was used to highlight the different regions within Asia. Perhaps the most important annotation is in the title because it tells you that we are looking at the relationship between fertility and life expectancy. The subtitle tells us that we are looking at regions of Asia in the year 1994.

**Color:** Color can be used to break down categorical variables into subgroups. This can allow you to study two categorical variables concurrently against the measurement value. Here we are using color to distinguish different regions of Asia.

**Composition:** There are a lot of regions of Asia, so the lines begin to make the plot look busy. I took out the gridlines so that we can focus on the data solely.

<br>

#### 7) Variations and Alternatives

A variation of the line plot is a bar chart. They both are able to show relationships between two numerical variables. However, it is important to note that barcharts take up more space visually than line charts. When choosing between the two, we should think about whether we are comparing amounts at a time point or whether we care about the end value at that time point. 

<br>

#### 8) How to Create the Graph 

````
data(gapminder)

## Drop NAs across all vars to quickly clean
gapminder <- gapminder %>% drop_na()

## data from 1994!!
gap_94 <- gapminder %>% filter(year == 1994) 

## year = 1994, region encompassing Asia!!
gap_94_asia <- gap_94 %>% filter(region == "Central Asia" | region == "Eastern Asia" | region == "South-Eastern Asia" | region == "Southern Asia" | region == "Western Asia")
  
good_gap <- ggplot(gap_94_asia, aes(life_expectancy, fertility)) + 
  geom_line(size=1, aes(color=region, linetype=region)) +
  labs(title = "Relationship between Fertility and Life Expectancy",
       subtitle = "Continent: Asia, Year: 1994",
       x = "Life Expectancy (years)", 
       y = "Fertility Rate (per 1000)",
       color = "Region") +
  theme_minimal() +
  theme(panel.grid.minor = element_blank(),
        panel.grid.major = element_blank(),
        axis.line = element_line(colour = "black")) +
  scale_color_brewer(palette = "Set1")

good_gap
````

<br>

#### 9) Initial Plot and Improvements

![](/images/gap_asia_init.png)

Above was the initial plot generated from the data. The line chart with default colors makes it hard to distinguish the different regions of Asia, especially when it is in a grayscale (printed black and white for example!) To overcome this barrier, I added another legend where we use different dash line types to distinguish the various regions. I also took out the gridlines because there are so many different regions we are comparing.
