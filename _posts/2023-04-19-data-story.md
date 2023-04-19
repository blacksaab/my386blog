---
layout: post
title:  "Utah's Unperdictable Weather"
author: David Yankura
description: An exploration of Utah's Historic Weather and Snowfall patterns. 
image: /assets/images/ski_lift.jpg
---


<!-- Create a graphic that tells a coherent story with data.  Often the story can be the answer to the main question you had in mind when you were first motivated to collect your data.  Your story need not be amazingly interesting.  It should, however, be complete and straightforward. 
You may create up to two graphics if it an additional graphic is absolutely necessary to sufficient convey your story.  
You can create a dashboard to help tell your story, but you should still have a static graphic that is representative and tells the complete story, if only about a part of your data.  
The graphic should be (mostly) self-contained and viewers should be able to understand the story from the graphic alone.  
Create a blog post that:
    summarizes your entire project (from data collection to now 1-2 paragraphs),
    summarizes your data story (1 paragraph)
    shows your graphic
    has a link to the github repository(s) that contain(s) all the work associated with your project(s) 
Your graphic and blog post will be graded based on:
    Visual aesthetics
    Graphic suitability
    Completeness of story
    Meeting the posted guidelines
You will be ALSO be graded for your entire blog:
    Your blog should be something that you would be able to share with prospective employers 
    Your blog should have a name that is not related to a single assignment or class
    Your blog picture / title / description should not be the default
    Your blog should have a place for readers to leave comments
    Your blog should have an informative "about me"  -->

## The Question

I love to ski, and as an avid skiier I set out to see if I could use weather data from the previous summer to predict how much powder there will be during the following ski season. 


## The Data 

I found data from <a href="https://www.ncdc.noaa.gov/cdo-web/search">the NOAA</a> which includes observations from 71 weather stations around Utah County, Utah from January 1, 1990 through March 30, 2023. 

Each station recorded the following variables each day: 
- PRCP = Precipitation inches to hundredths on Daily Form pdf file
- SNOW = Snowfall inches to tenths on Daily Form pdf file
- SNWD = Snow depth inches on Daily Form pdf file
- TMAX = Maximum temperature Fahrenheit to tenths on Daily Form pdf file
- TMIN = Minimum temperature Fahrenheit to tenths on Daily Form pdf file

Originally I attempted to average the data across all stations, but this was a mistake. As time went on some stations went out of comission, and new stations were built. Specifically, newer stations tended to be built at higher altitudes in the mountains, meaning that as time went on average temperature across all stations dropped and the amount of snow rose. This was due entirely to the change is the sampling population and did not reflect actual weather patterns. 

Finally, I decided to only use stations that were at least 2000 m in elevation, and were up and running for the entire span of my analysis (1990-2022). 

| Station Name                | Designation |
| --------------------------- | ----------- |
| BRIGHTON, UT US             | USS0011J57S |
| LOOKOUT PEAK, UT US         | USS0011J64S |
| MILL D NORTH, UT US         | USS0011J65S |
| PARLEY S SUMMIT, UT US      | USS0011J52S |
| SILVER LAKE BRIGHTON, UT US | USC00427846 |
| SNOWBIRD, UT US             | USS0011J42S |

By restricting my analysis to stations all located above 2000 m, I was only viewing weather data from mountainous areas pertinent to my motivating question (think skiing). And, by only viewing data from stations that were operational for the entire period, I avoided influencing my data by changing my sample population. 

## The Analysis 

<!-- talk about how you transformed data -->
I used data from the 6 stations to create a dataframe where each row is a season with the following variables: 
- `Season_Number` - integer - Year for ski season. Since ski seasons typically stretch over two years, I let this be the year in which the season started. So, the ski season that went from October 1992 through April 1993 would have a `Season_Number` of 1992. 
- `Snow_Season` - boolean - False if the row represents the summer season (April - August) and True if row the represents the snow season (September - March). 
- `AVERAGE_TMAX` - float - The average daily maximum for the season across all stations (F$^\circ$). To get this value, the daily maximum temperature was averaged across all stations, and then the daily average minimum temperatures were averaged across the entire season. 
- `AVERAGE_TMIN` - float - The average daily minimum temperature for the season across all stations (F$^\circ$). To get this value, the daily minimum temperature was averaged across all stations, and then the daily average minimum temperatures were averaged across the entire season. 
- `TOTAL_PRCP` - float - Total average precipitation for each season. To get this value, the daily precipitation was averaged across all stations for each day, and then each day in the season was summed. 
- `TOTAL_SNOW` - float - Total average snowfall for each season. To get this value, the daily snowfall was averaged across all stations, and then the daily average was summed for the entire season. 

Transforming the data into this format was incredibly obnoxious, but well worth it. We am investigating if weather from the summer can indicate what the weather will be like the following winter (in Utah valley); so, now that we have summary statistics for each summer and winter season, we can attempt to answer this question. 

<!-- talk about what you found from your transformed data -->
After all of this tedious work, I was able to generate the following graphic: 

![Summer Temperature vs Winter Snow from 1990 through 2022](https://raw.githubusercontent.com/blacksaab/my386blog/main/assets/images/Post_3c/Plot_Main.jpg)

Based on this data, there is absolutey no correlation between temperature in the summer, and snowfall the following season. And although it doesn't make for the most exciting graphic, it really is an amazing attribute of Utah's weather. 

I was curious if perhaps I was simply using the wrong metric; perhaps the total average precipitation over the summer would be a better predictor of total average snowfall come winter. 

![Summer Precipitation vs Winter Snowfall from 1990 through 2022](https://raw.githubusercontent.com/blacksaab/my386blog/main/assets/images/Post_3c/Side_Fig.jpg)

However, based on this plot there is also no correlation between the amount of precipitation in the summer and the amount of snowfall the next winter. 

It is not altogether surprising, but it is somewhat disappointing, that the amount of snowfall in Utah is not so simple to predict. It would be interesting to investigate Utah's snowfall patterns further using more-sophisticated techniques. 

<a href="https://github.com/blacksaab/my386blog/tree/main/assets/code">Repository with associated work for this analysis</a>

<!-- ![Snowfall from 1990 through 2022](https://raw.githubusercontent.com/blacksaab/my386blog/main/assets/images/Post_3c/third_fig.jpg) -->



