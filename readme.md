# FordGoBike Analysis
## by Justin Brown


## Dataset

The following analysis is based on the data available for the GoBike Share program in the San Francisco area. It is provided here by Lyft. The data used below shows information about trips since 2017 including Start and End time and station, duration, rental type and bike information.

The data is stored in multiple CSV files using a ';' as the delimiter. The fact that the data has 4 million rows is very intriguing.  There is a lot of information here.  The fact that trips can be traced to specific bikes is interesting in terms of asset utilization.  Also the ability to see any trends related to day of week or yearly seasonality will be interesting.  A deeper look would be interesting to see actual patterns that exist between stations, which station pairs are connected for example.

I will focus mainly on trends related to daily, weekly and monthly patterns.  Having the start times for each rental will be key.  I will also briefly look to see if there are any interesting patterns causing certain specific bikes to be used more, and thus age more.  The bike ID will be useful for that investigation.

Due to the size of the data and the processing time required for the visualizations, I will take a random sample of 10% of the data for this analysis.


## Summary of Findings

Based on a view of the split between customer types, clearly the model is doing a good job of attracting subscribers to the product. Only 17% of the trips in the sampled data were taken by non-subscribers and the raw number demonstrate a large number of overall trips within the system.

Out of curiosity, the top 25 starting stations by trip count were charted. The Caltrain Station 2 at Townsend and 4th tops the charts as the busiest station with nearly 12,000 trips in the sampled data. Assuming the sample to be truly random, this would equate to over 110,000 trips in the full data set. Interestingly, the trip quantity drops rapidly, and by the time we reach the 25th busiest station, there are only 2,000 trips in the sampled data.

Plotting histogram of the trip durations, you can see the vast majority of the rentals last under 1000 seconds, but the tail is very long, with the longest rentals lasting 24 hours. Because the data in the tail becomes so small, this histogram was faceted into 4 sections to look for anomalous patterns in the tail. None are noted.

To see the entire distribution on one chart, and in doing so attempt to confirm the assessment that there are no anomalies across the full range of values for the duration, a log transformation is used.  As demonstrated in the faceted charts, no anomalous information is uncovered.  The resulting log-normal curve is a rational result given the data.

The numbers in a YoY bar chart demonstrate strong year over year growth.

As expected, volumes drop on the weekends. It is interesting that volumes on Sunday are comparable to the volumes on Saturday. I would have expected a more dramatic difference between the days.

The duration_sec veriable is very right skewed. This makes perfect sense, because it is reasonable that with the possibility of a full-day rental (86,400 seconds) and the most likely rental being for a commute or sight seeing (which would not last near that long) that the data would be mostly grouped in the 1 hour or less interval. Performing a log transformation, I was able to visualize all of the data on one chart to see that there were no obvious abnormalities.

I was surprised to see how few stations contained the vast majority of the trips. Not being familiar with the geography of the San Francisco area, this may make perfect sense. The only real wrangling performed on this data related to ensuring proper data types for the columns represented.

Gap in end times noted between the hours of approximately 1am to 5am for trips starting around 3pm and narrowing to a window of around 4am to 6am for trips beginning at 11pm. Sparsness of trips between midnight and 6am and lasted more than just a short while.

Adding a small amount of jitter and some significant transparency, it became clear that what looked like evenly spaced data on the previous charts is very heavily weighted toward the low end of the duration scale with the vast majority of rentals falling during the daylight hours and lasting longer, and a smaller number beginning into the late hours of the night and early hours of the morning, with those trips primarily being quite brief.

Taking a more precise look at the trips, the scale of the disparity between those trips during the daylight hours and those after around 8pm and before 7am is noted. In fact, there are so many trips represented in just the bottom row of the heat map, a deeper dive into that window of time is warranted to look for any unexpected patterns.

A heatmap of trips lasting less than 50 minutes in duration by hour of the day. No huge surprise, however some useful data found in this chart. With the minimim count required to appear on the map set at 100, we see that nothing appears at all with start times between 2am and 5am. And now the glob of data at the bottom of the previous charts starts to take some nice, predictable shape with some meaningful data quantified within. The number of trips heats up during the traditional commuting windows, with durations of the trips heating up in the 4-15 minute range. This data would tell business owners a lot about the characteristics of their riders.

Using faceting, broke up the previous heatmap into separate heatmaps for each weekday (and a final repeat of the previous chart), adding a third variable into the visualization. Two things are made clear from this exercise. First, the patterns in the weekend days is broken out from weekdays giving some insight into how those days differ from weekdays. And second, it shows a tremendously high degree of consistency from weekday to weekday, almost down to the 10s of riders in each cell. This suggests that, not only is the usage consistent, but very likely the specific riders using the bikes during the peak periods are highly consistent. Not too surprising since most riders in the system are subscribers and the most likely riders to become subscribers are those who have consistent use and those riders likely commuters, the very consumer type the product is aiming to target.

Using a heatmap to compare the correlation of many variables to other variables, an area for further (future) exploration is identified: the correlation between start and end station. Because the majority of rides are short in duration, the geographical radius of where a rider can reach within these durations would explain why a higher degree of correlation exists between these data points. However, understanding even within this correlation whether specific pairs of stations were even more highly correlated may identify information useful for logistics, or perhaps if there are unexpected correlations between stations that are significantly far in distance, it might suggest an opportunity for new products like motorized options.

## Key Insights for Presentation

Show log distribution of trip durations and discuss that there are no apparent anomalies.

Show heatmap showing rush hour peaks.

Show separate heatmaps by day of week to analyze consistencies and patterns.