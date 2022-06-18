---
layout: post
title: Ultra Running Visualization Brief
tags: [line chart, data brief]
comments: true
category: blog
---

![](/images/running_line_point.png)

#### 1) Description of Type of Graph

This is a line graph, which is good for comparing two numerical variables. Typically, we use line graphs when there is a correlation or continuation of the values on the x-axis. In addition, it also has a scatter plot overlaid on top to show individual data points, which good for looking at all individual data points and comparing two numerical values.

<br>

#### 2) Description of Data

The data is from the International Trail Running Association (ITRA). It was found on the Tidy Tuesday Github respository: https://github.com/rfordatascience/tidytuesday/tree/master/data/2021/2021-10-26. This data was encompassed in two data tables - one with information pertaining to the race (race id, race name, distance, elevation gained/loss, city, country, date, start time, number of aid stations, participants) and one pertaining to the participants (racer id, rank, runner, time, age, gender, nationality, time). After the data was read in, particpants without a distance or time for completion were removed from the analysis.
<br>

#### 3) Audience and Purpose

The purpose of this visualization is to see how men and women compared in ultra racing based on their pace, looking across different distances of races. We hypothesized that as the distance increased, pace would slow down. We were not sure how men or women performed when compared to each other.

<br>

#### 4) Representation Description

Line charts have numerical data on both x-axis and y-axis. They are good for comparing the relationship between two numerical variables, but also we can overlay single datapoints overlaying a line (mean) to see if the data follows a trend. If there are multiple groups that we want to compare, it is easy to distinguish various groups and show them in a way that makes it easier for comparison.

Scatterplots are good for looking at relationships between two numerical variables. This plots each individual data point so that we can examine whether there is a relationship between the two variables. This allows us to examine the raw data to see if there is a distinct pattern within the data across the two variables of interest. It can allow us to examine where there may be more or less data.

<br>

#### 5) What to Read and What to Look For

When first looking at a line chart, it is important to note the variables on the axes and the scales to which they exist. The next thing to note is how many lines are on the line plot! Typically, when there are multiple lines, this dictates different groups that we are comparing. Usually multiple lines are colored differently or the lines are dashed differently to distinguish the differing groups.

When first reading a scatterplot, it is important to note the two variables being compared in the x-axis and y-axis. It is also important to keep in mind what the scale is for each of the variables. After orienting to the variables being compared, we can examine the scatter points and see if there is a relationship or shape that the data points trend. We can also look to see whether there are data points that are outliers to the general pattern displayed between the variables.

From this visualization 

#### 6) Presentation Tips

**Annotation:** 

**Color:** 

**Composition:** 

<br>

#### 7) Variations and Alternatives



<br>

#### 8) How to Create the Graph 

````
## Read in data
ultra_rankings <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2021/2021-10-26/ultra_rankings.csv')
race <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2021/2021-10-26/race.csv')

## Join to get information on race/individual to calculate speed metrics
full <- left_join(ultra_rankings, race)
full[full==0] <- NA

## Calculate speed and distance in imperial terms
full <- full %>% 
  mutate(speed = ((time_in_seconds/60) / distance*0.621371), 
                        distance_mi = distance * 0.621371,) 
                        %>% drop_na()

full_sum <- full %>% 
  select(gender, distance_mi, gender, elev_gain_ft, speed) %>% 
  group_by(distance_mi, gender) %>% 
  summarise_all(.funs = mean)

## Initial plot
ggplot(full_sum, aes(distance_mi, speed, color=gender)) + 
  geom_smooth(se=F)

## Changed theme
ggplot(full_sum, aes(distance_mi, speed, color=gender)) + 
  geom_smooth(se=F) +
    theme_bw() +
  theme(panel.grid = element_blank()) +
  labs(x= "Distance (miles)",
       y= "Speed (min/mile)",
       title= "Comparing Distance and Speed") +
  scale_color_manual(values = c("steelblue3", "lightpink2"))
  
## Overlay scatter plot on line plot 
ggplot(full_sum, aes(distance_mi, speed, color=gender)) + 
  geom_smooth(se=F) + 
  geom_point(alpha=0.5) +
  theme_bw() +
  theme(panel.grid = element_blank()) +
  labs(x= "Distance (miles)",
       y= "Speed (min/mile)",
       title= "Comparing Distance and Speed") +
  scale_color_manual(values = c("steelblue3", "lightpink2"))
````

<br>




#### 9) Initial Plot and Improvements

![](/images/running_init.png)
![](/images/running_line.png)
