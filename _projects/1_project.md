---
layout: page
title: Podcast Studies
description: Extensive analysis of over 28 million podcasts. 
img: assets/img/12.jpg
importance: 1
category: work
related_publications: To update
---

Late August, Ben (my PhD project leader) collected a giant raw dataset of millions of podcasts, with publish dates spanning from early 1990s to now. We are curious about how podcasts change over decades, in terms of their popular categories, used languages, explicit status, and even the time span of each podcast. 

I started by analyzing the time span of individual podcasts. However, since the "publish date" column had at least 3 different time formats, I cleaned the dataset first and fixed the format. Here's the trick I employed:

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

To make our analysis simpler, I got rid of all the timezone info in our dataset. To avoid NaT values after converting one date format, I merged three columns by .fillna(). This way, NaT will most likely get replaced by our target date format.     

After cleaning the dataset, I made a .csv file that contains podcasts sorted by their time span. I also made some really exciting plots about podcast trends over decades. More details will be updated. 
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




