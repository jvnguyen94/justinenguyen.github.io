---
layout: post
title: Animal Sounds Visualization
tags: [line chart, data brief]
comments: true
category: blog
---

<br>

![](/images/animal_sounds.png)

<br>

#### 1) Description of Type of Graph

This is a line graph, which is good for comparing two numerical variables. Typically, we use line graphs when there is a correlation or continuation of the values on the x-axis.

<br>

#### 2) Description of Data

The data is from the `sounds` dataset which is from the `wordbankr` database on R. This has information on development of children's vocabulary. We have information on individual children and when they were able to produce each sound.

<br>

#### 3) Audience and Purpose

The purpose of this visualization is to see how children developed vocabulary through being able to produce these animal sounds. We are interested in seeing which sounds are easier for children and how children were able to improve with each sound over time. The audience for this data set is speech pathologists who are tracking language development in children or parents who are interested in when their kids are able to produce different sounds compared to a benchmark population!

<br>

#### 4) Representation Description

Line charts have numerical data on both x-axis and y-axis. They are good for comparing the relationship between two numerical variables, but also we can overlay single datapoints overlaying a line (mean) to see if the data follows a trend. If there are multiple groups that we want to compare, it is easy to distinguish various groups and show them in a way that makes it easier for comparison.

<br>

#### 5) What to Read and What to Look For

When first looking at a line chart, it is important to note the variables on the axes and the scales to which they exist. The next thing to note is how many lines are on the line plot! Typically, when there are multiple lines, this dictates different groups that we are comparing. Usually multiple lines are colored differently or the lines are dashed differently to distinguish the differing groups.

From this visualization we see that the x-axis has age in months running across the bottom and the proportion of children able to produce the sound is on the y-axis. All the different sounds are different lines with different colors.

#### 6) Presentation Tips

**Annotation:** Annotation can be used to highlight each of the sounds. In this case, the annotation is in the legend of the graph. I kept it simple and had minimal annotation because it was easy to use the color to match with the sound in the legend and it is better to minimize text on the graph.

**Color:** Color can be used to break down categorical variables into subgroups. This is shown by the different lines that are in different colors. However, since yellow is a difficult color to see, I outline the points in black so that the data is not lost against the white background.

**Composition:** The composition of the graph can help make the point of your figure. If the differences amongst the groups are nuanced, you may not want to use an absolute scale for the numerical axis. However, if you do this, you need to be conscientious in making it clear that the axis is altered. The plot has very feint gridlines so we can clearly see all the means and the line trends for each of the sounds, but if we needed to look at the absolute proprotion, it is easy to trace it back to the y-axis to obtain a value by eye.

<br>

#### 7) Variations and Alternatives

A variation of the line plot is a bar chart. They both are able to show relationships between two numerical variables. However, it is important to note that barcharts take up more space visually than line charts. When choosing between the two, we should think about whether we are comparing amounts at a time point or whether we care about the end value at that time point. This point is clear with the animal sounds data.

<br>

#### 8) How to Create the Graph 

````
## Read in data
sounds <- read.csv(here::here("data", "animal_sounds_summary.csv"))


fct_reorder2(as.factor(sounds$sound), ## sound becomes factor
             sounds$age, ## x var
             sounds$prop_produce) %>% ## y var
  levels ## Grab the distinct levels produced
  

ggplot(sounds, aes(x = age, 
                   y = prop_produce, 
                   fill = fct_reorder2(sound, age, prop_produce))) +
  geom_smooth(aes(color = fct_reorder2(sound, age, prop_produce)),
              se = FALSE, lwd = .5, show.legend = FALSE) +
  geom_point(size = 2, shape = 21, color = "midnightblue") +
  labs(x = "Age (months)", 
       y = "Proportion of Children Producing", 
       fill = "sound") +
  scale_fill_viridis(discrete = TRUE) +
  scale_color_viridis(discrete = TRUE) +
  theme_bw()
````

<br>

#### 9) Initial Plot and Improvements

![](/images/animal_sounds_init.png)

The initial plot we generated from the data was a bar chart showing how children were able to produce different sounds based on their age. The sounds were initially split up so it was hard to compare whether one sound was more difficult to pronounce at a specific timepoint in the child's life. To rectify this, we overlayed all the sounds onto one plot and used a line graph because we care about the "end point" for the proportion of children that could produce the sound. The bar plot had too much visually and detracted away from what we were trying to show. We did not really care to show total amount, but how the values changed based on sound at that specific time point. The colors chosen for this plot are also very distinguishable from each other so it is easy to compare sounds at a specific time point.
