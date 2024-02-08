---
layout: page
title: News in Podcasts after George Floyd's Murder
description:  
img: assets/img/2010_2023_series_plot.png
importance: 1 
category: 
related_publications: To update
---

Timeline: Nov. 2024 - Present

Introduction: Our dataset consists of one million podcasts transcripts divided into three timelines: before, between, and after the two weeks when George Floyd was murdered. We are curious about the changes that George Floyd's murder bring to the podcasts. Specifically, we focus on podcasts that talk about news, and such podcasts can belong to any category. There are few research questions we strive to answer:
1. How can we define news in podcasts and how does the definition of news shift in podcasts after George Floyd's murder. This is a challenging questions to ask and require my team to look at multiple raw transcripts and set a threshold for news.
2. After Floyd's death, where does news occur in non-news podcasts (in what non-news categories of podcasts are we finding news). We are blessed to have a noisy-labeled dataset where many podcasts are associated with categories like "Education", "Society", etc.
3. Following Floyd's death, what types of news are covered in non-news podcasts? What name entities and themes are included frequently?
4. We expected a regression discontinuity among podcasts following Floyd's death. This trend might be from the categories of podcasts, news, etc.  
5. How does the conversational dynamics and narrative styles in podcasts change after Floyd's death?  

Main content:
We have collected most of the transcripts we need. My task is to train a MiniLM on the labeled transcripts two weeks before and after Floyd was murdered, and use the data in-between the timeline to calibrate the model. After training and fine-tuning, our model will be able to predict where an input sentence is about news or not. Currently, I am looking at podcasts that are classified as news and not-news and try to formalize our definiton of news in the podcasts. This definition is subject to change as we progress on the project. 

Last update: Jan 28, 2024
