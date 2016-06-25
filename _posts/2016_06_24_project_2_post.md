---
layout: post
title: The music of the '00s -- why did we like what we like?
---

The goal of this post is to jumpstart an awesome exploration of music and data from the '00s. This post is meant to serve as a companion writeup to the 'Are You Entertained?' podcast, in which we continue to address an omnipresent question in the industry- why do we like what we like?

_________
##STEP 1: Exploring the raw data...

There are a total of 83 columns with 76 of those containing rank values per week (76 weeks). I looked over the first ten rows of data. I observed that the values in the 'weeks' columns are relative ranks of tracks on the Billboard 100 chart for that week. The current dataset uses asterisks in place of missing values. I will need to replace asterisks with NaN. Also, it seems that the final columns (e.g., 68+ weeks) don't have any data (seems like all asterisks). I plan to look into this further somehow (like find total NA in column or something). Perhaps I can drop some columns if no values exist in them.

The strings in 'artist.inverted' column are not all formatted the same way. Not sure if that is going to matter during the data analysis (I suspect not, but duly noted). The column names do not contain unnecessary spaces nor are they unnecessarily long (in my opinion). However, I will rename the 'artist.inverted' column because that label is inaccurate (names for groups of artists, such as a band, are not inverted). I also don't like the dots in the column names. The dots in the column names might cause confusion while coding. I will need to reformat the values in the following columns: 'time', 'date.entered', 'date.peaked'. After reviewing the values in the 'date.entered' and 'date.peaked' columns, I think I am going to have to create another column using those two columns that will yield more informative date information for each week a track is on the billboard chart.

I also took a look at the data types of each column, and observed that I would have to change them for several columns. I also observed that some of the genres seem to overlap (e.g., Rock vs Rock'n'roll). Also, some artists have seemingly wrong genres listed (e.g., rock for a pop artist). However, this is not something I can fix since that's based on opinion (I think), and so I will just duly note this observation.

![Data Dictionary]({{ site.url }}/images/DataDictProj2.png)


________________
##STEP 2: Cleaning up the data...

Data Cleaning Tasks:

  1) replace asterisks with NaN
  2) check if final columns have any data
  3) standardize format of 'artist.inverted' column (optional)
  4) rename 'artist.inverted' column
  5) replace all dots in column names with underscores
  6) reformat the values in the following columns: 'time', 'date.entered', 'date.peaked'
  7) change data types for several columns
  8) group together overlapping categories in 'genres' if appropriate
  9) obtain more informative value from 'date.entered' and 'date.peaked' columns

________________
##STEP 3: Visualizing the data...

![Y1: Time Spent on BB Top 100]({{ site.url }}/images/y1.png)

![Y2: Time to reach peak on BB Top 100]({{ site.url }}/images/y2.png)

![Y1 v X1]({{ site.url }}/images/y1x1.png)

![Y2 v X1]({{ site.url }}/images/y1x2.png)

![Y1 v X2]({{ site.url }}/images/y2x1.png)

![Y2 v X2]({{ site.url }}/images/y2x2.png)

_______________________________
##STEP 4: Problem Statement

In exploring the questions of 'what made a hit soar to the top of the charts?' and 'how long did a hit stay there?', one first has to set definitons for what qualifies as a successful hit.

I am choosing 2 indicators for a successful hit, which will be the dependent variables of this study. Y1 = Amount of weeks a track took to rise to its peak in year 2000, and Y2 = Number of weeks a track was on the BB Hot 100 Chart for year 2000.

A successful track will have a small Y1 and large Y2.

Problem Statement: 
Does the genre of a song or its length (in seconds) influence the success of a hit? By comparing genre of song with Y1 and Y2, and track length in seconds with Y1 and Y2, we may observe whether a correlation exists with the independent variables. If a correlation is observed, further investigation is warranted.

Null Hypothesis 1: 
The genre of a song does not impact the success of a hit on the BB Top 100 chart.

Null Hypothesis 2:
The length of a song does not impact the success of a hit on the BB Top 100 chart.

Alternate Hypothesis 1:
The genre of a song does impact the success of a hit on the BB Top 100 chart.

Alternate Hypothesis 2:
The length of a song does impact the success of a hit on the BB Top 100 chart.

Sources support for Null Hypothesis:
http://www.wired.com/2014/07/why-are-songs-on-the-radio-about-the-same-length/

Sources support for Alternate Hypothesis:
http://www.motherjones.com/kevin-drum/2014/08/most-songs-are-three-minutes-long-because-thats-how-most-us-them

Risks:
-when reviewing weeks to reach peak position for songs, there is a risk that 2 songs that did not change much in rank could be considered equally successful by this measure, regardless of how how high or low ranks were. Another risk is that a song can take a long time to rise to its peak (which is penalized) in this measure, even though it rises many ranks.

and assumptions of data:
1) Assuming no situation where two songs from two different artists have the same title
2) Genre is a proxy for artist
    (discuss weird categorizing of some artists)


##Future Steps_______________________________________________________


-EDA
-2 tailed t-test for one-sample 
-model and see if it fits with data from future years


create a post describing each of the 5 steps above. Rather than writing a procedural text, imagine you're describing the data, visualizations, and conclusions you've arrived at to your peers. Aim for a minimum of 500 words.