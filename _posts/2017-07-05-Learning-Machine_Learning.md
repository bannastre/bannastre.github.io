---
layout: post
title: "Learning about Machine Learning"
date: 2017-07-05 T20:00:00Z
---

_Warning - this post is long and maybe a little arid.. there's an easter-egg at the end though so stick with it... <sub>or just scroll down ;)</sub>_

This week is another project week at [Makers Academy](http://www.makersacademy.com/), although this one has a twist. Previously we've had a project map to follow with some idea of what we are working towards, such as build Facebook using the Rails framework or implement a news summarisation app in JavaScript. This time, however, we have freedom to choose and with that a small group of us have chosen to look at Machine Learning.

As with most projects at this stage of our education, the kick-off began with a Rumsfeldian attempt to identify the known unknowns. That none of us have any experience or history with Machine Learning is undaunting having started every week for the last 9 with a new subject to sink our codey teeth into.

To place Machine Learning in context, we have to give a quick nod to AI as a whole. The imaginative goal of omniscient machines might not be in reach as yet but questions such as 'Where does general intelligence come from?' provide the inspiration for understanding how machines could learn.  Nvidia blog nicely on this and the [differences between narrow and general AI](https://blogs.nvidia.com/blog/2016/07/29/whats-difference-artificial-intelligence-machine-learning-deep-learning-ai/)

So join me in taking our first steps into Machine Learning and let's start with this wonderfully short definition from Tom Mitchell in [Machine Learning](https://www.amazon.com/dp/0070428077?tag=inspiredalgor-20):

"A computer program is said to learn from experience (E) with respect to some class of tasks (T) and performance measure (P), if its performance at tasks in T, as measured by P, improves with experience E."

Put even more simply, a program gains experience related to a task and outputs something measurable. Crucially, however, performance improves with experience. The question then arises, how does a program gain experience?

There are two distinct ways that experience is gained; supervised or unsupervised. In supervised learning, the computer is given a training set of data that is categorised by the programmer. The computer is then programmed to find similarities common to each categorisation, that it can then apply to any further target. In unsupervised learning, the computer is given a set of data and programmed to find similarities and categorise the data of its own accord.

In either case, the major dependency is data (experience improves performance, remember). That dependency raised our largest project hurdle as it's not long before the memory requirement outstrips the performance gain. Our project centered around the classification of news articles into those of good journalistic quality vs those of a more opinionated nature.

We took a supervised learning approach so we could more easily control the sources of data for training but soon learnt the major hurdle of this project.

After scraping various news sources we ended up with a huge dataset of 3,000 articles or 693,366 words.
[Scikit-Learn's documentation](http://scikit-learn.org/stable/tutorial/text_analytics/working_with_text_data.html) suggests that a bag-of-words implementation like this would usually have no fewer than 100,000 words referenced in a library. We had smashed that and library to find that storing 7 times that as type float32 would require 10,000 x 700,000 x 4 bytes = 28GB of RAM... totally unfeasible.

We overcame this hurdle by implementing something called a high-dimensional sparse dataset, which handles empty values. This does not mean that the values are missing, rather that we know they are empty.

In our implementation, each article's words are added to a dictionary of all words and assigned an integer to reference them by. The occurrence of each article's words is then counted for frequency. A multi-dimensional list is then created where each element is an article. Each of n articles is itself a list containing two integers,  

   [ [i<sub>1</sub>, j<sub>1</sub>] , [i<sub>2</sub>, j<sub>2</sub>] , [i<sub>3</sub>, j<sub>3</sub>] ... [i<sub>n</sub>,j<sub>n</sub>] ]  ,

where i is the integer referencing the word and j is the frequency of this word occurring in the article. Every article-list is the same length. Many of the j's in each article-list will be 0 because, of course, not all articles contain all words and it's these that are stored as sparse data.

There's far more to machine learning (and to this project) that I can put into one post but we went on to implement a Naive-Bayes approach to categorisation, which assumes that the presence of a particular feature in a class is unrelated to the presence of any other feature. e.g. a fruit may be considered to be an apple if it is red, round, 3-inches in diameter but it doesn't have to be all of these to be an apple. There's a more detailed explanation of that [here](https://www.analyticsvidhya.com/blog/2015/09/naive-bayes-explained/). We also experimented with Support Vector Machines, which are more accurate than Naive-Bayes although more complicated to implement.

All in all, the project has been about learning about machine learning and I am happy we have met this aim. Our machine learnt that there is a clear distinction between the vocabulary favoured by articles that are published on credible news outlets and those that are less credible. We can use that to classify whether a statement is likely to be more credible than another and we saw that the accuracy improved the more experience we fed our machine in training. We can't accurately say that an article is 'Fake News', but I think we can still rely on common sense to judge these [snippets of literary gold from a much-loved British rag](https://www.buzzfeed.com/tabathaleggett/ridiculous-daily-mail-headlines?utm_term=.jl7qmJy777#.cm45YKN888).
