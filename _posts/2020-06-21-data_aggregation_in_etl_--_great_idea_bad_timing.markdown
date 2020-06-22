---
layout: post
title:      "Data Aggregation in ETL -- Great Idea, Bad Timing"
date:       2020-06-21 21:58:31 -0400
permalink:  data_aggregation_in_etl_--_great_idea_bad_timing
---


## The Context
A colleague and I were recently tasked to come up with some data trends regarding the film industry as part of a Flatiron School Data Science project. We're both fairly inexperienced with this type of investigation and with the language and libraries used to conduct it. However, part of the learning process is digging in to the behemoth of your interest area and getting your hands dirty with questions and missteps. For a little context, 3 weeks before this project, we had little, if any, Python experience, and no Pandas (a Python library used to manipulate and analyze tabular data) experience, at all. The last time I took a statistics course was nearly a decade ago and my colleague, though he does analysis for work, does it using fancy tools like Tableau that can take some of the heavy lifting away.

## Great Idea
We were given roughly ten csv (comma separated values) files of film data--from budgets to ratings to directors (just ID's, not names). My original thinking was that we would import all ten into dataframes in Pandas, clean them (by getting rid of 0's, dealing with null values and duplicates, and the like), then, finally, send those all to individual SQL (structured query language) databases for later querying. This type of data preparation is called ETL (extract, transform, load) because you extract data, you transform it through manipulations and various cleaning techniques, and you load the product of transformation to a storage location (like a database) for others to access.

My partner asked what I thought of aggregating the data and saving that as a csv. Three considerations went into my ultimate yes:

1. I didn't think it would take that long. It's a simple merge that will act as a neat little reference for us, I thought.
2. I thought it would improve data retention during cleaning by allowing us to see that certain rows still had value despite nulls or zeroes. Indeed, we might even be able to increase the statistical power of imputations through KNN (k-nearest neighbor).
3. Lastly, I thought we could use the insights from aggregation, match them to the original tables, and, *then*, send them to SQL databases.

I replied "I can see the value in that," and we were off.

## Bad Timing
All of those assumptions were wrong. I can't stress that enough. They were all...all of them...so very wrong.

### Too much time spent
It took around one-and-a-half to two out of the seven days we had to do the project to aggregate the data.

A lot of this had to do with inexperience with the tools. It often felt like I was learning how to do dataframe manipulations from Google rather than Flatiron and that process is highly unpredictable. Something that seems obvious can take hours to look up and tweak and something that seems like you might never figure it out takes ten minutes to find.

Another contributing factor was the inherent inefficiency of this approach when working on a team. While one person is combining a set of tables, those tables, effectively, become unavailable. This is because any changes might affect the merge process and, also, each team member is working with their own version of the tables. While it's technically possible to keep feeding in refreshed, cleaned tables to the merge workflow, it would defeat the purpose of the merge and would likely take more adeptness with dataframes to pull off.

Compare this to cleaning each table separately and sending it to SQL (structured query language) databases. Each team member can pick a given set of tables to work through without any merge conflict concerns. Then, once sent to SQL, later table joins (basically, the data aggregation we were doing with the csv's) can happen on the fly with clean data prepped for analysis.

### K Nearest...Nope
Having spent days aggregating the data, it felt, at least, like we had committed to this track and must stay the course. But surely we might find redemption in increased cleaning power. Quite the opposite. We actually introduced a good deal of dirt to the data including occasional horrifying situations where the same movie might appear 60 times, throwing off wide-net searches for correlations or similar anomalies popping up at the *end* of analyses.

Indeed, because of the size of the aggregated files, they felt unweildy, unintuitive, and cluttered. Moreover, because of the time commitment to aggregation (and, no small amount of anxiety on my part), it felt like there was no time to take advantage of fancy things like KNN. So, in one fell swoop, we eliminated the key value proposition of the aggregated data.

### Matchmaker, Make Me a Match
Finally, for the reasons described above (namely, time and how we had none), there was no matching back to original tables. Again, this had to do with inexperience with dataframe manipulation. I frequently found myself flabbergasted as to how I was going to change the structure of a dataframe to suit my needs. This made me very hesitant to take on any unnecessary or seemingly complicated jobs. My skill improved, throughout, but not in a very deeply technical and organized way (e.g. like when I took Python from University of the People). It felt more like I was a high school student drinking Red Bull the night before the final paper is due. So, I avoided the ambitious stuff.

Furthermore, there was no reason to match back to original tables because, as I mentioned, we didn't perform any cleaning that leveraged the power of the aggregated data.

## There's a lesson here
The most obvious lesson here is: don't aggregate data before cleaning when you have a short timeline--or, maybe, it's simply: don't aggregate data before cleaning. Full stop. More broadly, you might say: don't deviate from standards of practice (like cleaning and loading to a database before aggregating), especially when you don't know what you're doing. However, I think that presupposes that you know enough to know the standards of practice or that you know you don't know what you're doing. No, I think the real lesson from this foray into ETL data aggregation is that it pays to have a clear picture of the standards of practice and a strong familiarity with the tools you're using. Some of that comes with experience--like learning little tricks of the trade or Google searches--but some of it is foundational knowledge that needs to be learned in a formal and structured way. So, for me, this was only the beginning of a long journey; but I'm hoping to turn this misstep into a cool dance move...or maybe just a skip.
