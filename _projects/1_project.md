---
layout: page
title: Podcast Studies (Over 3 decades)
description: Extensive analysis of over 28 million podcasts. 
img: assets/img/2010_2023_series_plot.png
importance: 1
category: 
related_publications: To update
---
Timeline: August 2024 - November 2024

Background: From August 2024, my PhD mentor, Ben, undertook the monumental task of gathering a comprehensive raw dataset, which includes millions of podcasts. These podcasts, ranging from the early 1990s to the present day, offer a rich tapestry of information. We are intrigued by the evolution of podcasts over the decades, especially in terms of their popular categories, languages used, explicit status, and the duration of each podcast.

Main Content: After importing the .csv file into a data frame (referred to as “df”), we focused on the columns ‘categories’, ‘language’, ‘explicit_x’, and ‘pubDate’. Given our interest in the temporal changes in podcasts, my initial task was to clean the “pubDate” column, which contained at least three different time zone formats. To resolve this, I devised a pipeline to eliminate all the timezone information from the “pubDate” column. The details of this pipeline will follow.


```
# -------- Clean date format: ----------

# Date formats:
date_formats_with_offset = "%a, %d %b %Y %H:%M:%S %z"
date_formats_without_offset = "%a, %d %b %Y %H:%M:%S %Z"
date_format_without_tzone = '%Y-%m-%d %H:%M:%S'

# clean date using only one format, leaving NaTs for unmatched format 
df['date_formats_with_offset'] = pd.to_datetime(df['pubDate'], errors='coerce', format=date_formats_with_offset, utc=True).dt.tz_localize(None)
df["date_formats_without_offset"] = pd.to_datetime(df['pubDate'], errors='coerce', format=date_formats_without_offset, utc=True).dt.tz_localize(None)
df["date_formats_without_PDT"] = pd.to_datetime(df['pubDate'].replace({'PDT':'-07:00','PST':'-08:00'}, regex=True), errors='coerce', utc=True).dt.tz_localize(None)


# Merge 3 columns  
df["date_format_same"] = df['date_formats_with_offset'].fillna(df["date_formats_without_offset"])
df['date_format_same_final'] = df["date_formats_without_PDT"].fillna(df["date_format_same"])

# -------- date format cleaned ----------

```

To prevent NaT values after converting one date format into our target date format, I merged three columns using .fillna(). This approach ensures that NaT will most likely be replaced by our target date format. 'date_format_same_final' is the column with finalized time format.      

After standardizing the time format, I developed another pipeline to filter out podcasts from our dataset that were not published consistently. The inconsistency in podcast publication is likely attributable to erroneous publish dates considering that I set a relatively low threshold for inconsistency: if the difference between the median and minimum publish dates, or the difference between the maximum and median publish dates, exceeds 7000 days, the podcast is deemed inconsistent (I carefully chose 7000 days after many experiments). This approach helps ensure that our analysis is based on reliable and consistent data.

```
# The DataFrame is grouped by ‘podcast title’, ‘category’, ‘language’, and ‘explicit’ columns. For each group, the minimum, maximum, and median ‘publish date’ are calculated.
grouped = df.groupby(['podcast title', 'category', 'language', 'explicit'])['publish date'].agg(['min', 'max', 'median'])

# Time Span Calculation of each podcast:
grouped['time span'] = grouped['max'] - grouped['min']

# Set up criteria for podcast consistency and filter out those that are inconsistent:
grouped['median - min'] = abs(grouped['median'] - grouped['min'])
grouped['max - median'] = abs(grouped['max'] - grouped['median'])
consistent_podcasts = grouped[(grouped['median - min'] < pd.Timedelta('7000D')) & 
                             (grouped['max - median'] < pd.Timedelta('7000D'))]
                             
# Sorting and Resetting Index: The consistent podcasts are sorted in descending order based on their time span. The index of the DataFrame is then reset:                              
consistent_sorted_podcasts = consistent_podcasts.sort_values('time span', ascending=False)
consistent_sorted_podcasts = consistent_sorted_podcasts.reset_index()

```
This was the end of my data cleansing stage (it worked although might not be exhaustive). After that, I was able to do multiple exciting analysis. 

More details and plots are to update:       
     
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1990_2023_lang_series_plot.png" title="Popular Language Analysis" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The trend of podcast languages from 1990 - 2023.
</div>

<!-- You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal its glory in the next row of images. -->

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1990_2023_series_plot.png" title="Popular Categories since 1990" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Popular Podcast Categories from 1990 - 2023.
</div>




