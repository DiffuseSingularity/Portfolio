

# Executive Summary 

This Natural Language Processing exercise on data generated via a Reddit API was made with the intention of presenting a beta feature for the social media-user submitted content oriented website, https://www.reddit.com.  This feature would assist users in posting their content in subreddits that would target the most appreciative and engaged audiences.

The feature was tested on the content of two subreddits, initially using the "Top" posts sorting algorithm, located at https://www.reddit.com/r/Futurology and https://www.reddit.com/r/Worldnews respectively.  The "hot" sorting algorithm was also used, and though I initially showed more interest in this more recent post oriented sorting algorithm, I ran into some technical issues getting as many posts as I did from /r/Worldnews as I did with the Top sorting method, so for this project, I focused on the Top sorting algorithm for expediency and consistency.  This allowed me to get very clean, even sets of data, with 996 rows of data from each subreddit, totalling 1992 rows, of very consistent data that needed nearly no cleaning, and was easily concatenated into one clean, concise dataframe.    While "Riley_project_intro.ipynb" contains info from Riley Dallas on web scraping, one of the lead course instructors for the General Assembly Data Science cohort this project was done in the context of, I opted instead to collect data using the package PRAW https://praw.readthedocs.io/en/latest/ to collect my data.  The results of the data collection are included in the "Reddit_API_Praw_Collection_and_Cleaning_Top_posts.ipynb" file, a nearly identical file "Reddit_API_Praw_Collection_and_Cleaning_Hot_posts.ipynb" contains the very similar process and initial analysis of posts obtained through the Hot sorting algorithm.  

Models_code.ipynb contains all the further analysis and testing of the mostly cleaned data from the prior files mentioned above, leading to our conclusions.  The hypothesis test was as follows - 

H0 - Our training data will not generalize well to our testing data, failing to produce a coefficient of determination (r2) higher than 0.75 for our classification model during testing 

H1 - Our training data will generalize well to our testing data, and will produce a r2 score higher than 0.75

Using Logistic Regression, as well as a Naive Bayes Multinomial model, we were able to accept the alternative hypothesis - our R2 scores for our testing data were .82 and .86 respectively, demonstrating that, even though these subreddits do have some overlap in new posts that one can see simply by looking at the pages through the URLs provided, most of the contents can be reliably determined to belong to one or the other with our basic machine learning approach.  Word clouds were also generated as helpful visualizations of prominent title terms in both subreddits.  I did include word clouds generated by the Hot sorting algorithm, to demonstrate the importance in selecting sorting algorithms when collecting our data.    

Of course, more complex models can be examined - hyperparameters of our models can be tuned, and further models may be examined.  StopWords was used to filter out common filler words that would add excess variance, and the number of variables included in our models were also manually tuned to reduce variance - they had well over 1000 words each after filtering out stop words, many of which were still adding variance to our model.  URL domains as a variable are also certainly another powerful way to tune our model, there are definitely websites which are more likely to be posted than others in various subreddits.  Finally, I believe it is key to test these models performance in relation to human performance - getting participants to decide which subreddits belong to which.  Since this is about efficacy, and not about how well the general populaton performs, enthusiastic, eager users of Reddit, "Redditors" could be easily recruited for such an experiment, to determine how well they fare sorting posts compared to our machine.  Their inputs could additionally be used to make our model more accurate.  


The slide deck for the associated presentation can be located here - 
[https://drive.google.com/open?id=10JUiy8UKQPqfPISpdfUVjsg6LhxNV1O4bepGWejCGFw]

BLOG POST DRAFT - 

As part of my immersive data science course at General Assembly, I designed a simple classification model in Python, using natural language processing, and basic machine learning techniques. This model would determine the origin of a reddit post- if it was from the /r/futurology, or /r/worldnews subreddit. The model succeeded, typically determining which post belonged where about 83 to 91% of the time. What caught my interest as I ran and reran my model was the wide range of variance in it's success-specifically how choosing different sorting algorithms on reddit dramatically affected my performance.
For anyone unfamiliar, Reddit is a user submitted content website, a social media site in the same way Youtube may also be considered social media. Users submit content, be it a link to video, audio, image, or text, or simply a written post by the user, to various subreddits (same as subforums in a forum) centered around content submitted by a community of posters. It's headline touts it as "The Front Page of the Internet". With over 300 million active users across over 150,000 subreddits, I would say they live up to their claim.
My Process
For my model, I selected these two subreddits that tend to share some similar content, but are distinct enough that someone familiar with the two subreddits could distinguish which post belongs where in many cases. One could say the measure of success for a machine learning model would be if it's performance is comparable to, or exceeds, skilled human performance. What else are we interested in machine learning, after all, than to sort information more effectively than we can?
I took advantage of an existing script, PRAW, or Python Reddit API wrapper, along with my Reddit API keys, available to all account holders, to effectively scrape my data - the recent posts in /r/futurology and /r/worldnews. Once I had saved my  data of interest - subreddit origin and post titles - within a Pandas Dataframe, I assigned the post titles to X, as my independent variable, which I am looking to assign to and determine a relationship with what subreddits they're likely to be in, my Y, or dependent variable. I utilized sci-kit learn to randomly assign my post titles to train test split and that will train my machine learning model with a portion of the data, with the posts attached to their actual subreddit of origin, creating a model to test on the remainder of the subreddit titles that are Not attached to their subreddit of origin. Prior to running the model, my post titles words were CountVectorized and transformed into machine readable tokens, meaning individuated variables that ignored punctuation to group similar words, and a logistic regression was used to classify my test data into which subreddit it is likely from 
I found another Medium article written about 3 years back, laying out the hot algorithm when Reddit's code was open source - as of 2016 this is no longer the case. The author rewrote the code from Pyrex (used to write Python to C extensions ), to Python, for readability, which can be viewed here : 

### Rewritten code from /r2/r2/lib/db/_sorts.pyx

from datetime import datetime, timedelta
from math import log

epoch = datetime(1970, 1, 1)

def epoch_seconds(date):
    td = date - epoch
    return td.days * 86400 + td.seconds + (float(td.microseconds) / 1000000)

def score(ups, downs):
    return ups - downs

def hot(ups, downs, date):
    s = score(ups, downs)
    order = log(max(abs(s), 1), 10)
    sign = 1 if s > 0 else -1 if s < 0 else 0
    seconds = epoch_seconds(date) - 1134028003
    return round(sign * order + seconds / 45000, 7
    


**The original README.md for the assigned project is located below**

- 
# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web APIs & Classification

### Description

In week four we've learned about a few different classifiers. In week five we'll learn about webscraping, APIs, and Natural Language Processing (NLP). Now we're going to put those skills to the test.

For project 3, your goal is two-fold:
1. Using Reddit's API, you'll collect posts from two subreddits of your choosing.
2. You'll then use NLP to train a classifier on which subreddit a given post came from. This is a binary classification problem.


#### About the API

Reddit's API is fairly straightforward. For example, if I want the posts from [`/r/boardgames`](https://www.reddit.com/r/boardgames), all I have to do is add `.json` to the end of the url: https://www.reddit.com/r/boardgames.json

To help you get started, we have a primer video on how to use Reddit's API: https://www.youtube.com/watch?v=5Y3ZE26Ciuk

---

### Requirements

- Gather and prepare your data using the `requests` library.
- **Create and compare two models**. One of these must be a Bayes classifier, however the other can be a classifier of your choosing: logistic regression, KNN, SVM, etc.
- A Jupyter Notebook with your analysis for a peer audience of data scientists.
- An executive summary of the results you found.
- A short presentation outlining your process and findings for a semi-technical audience.

**Pro Tip 1:** You can find a good example executive summary [here](https://www.proposify.biz/blog/executive-summary).

**Pro Tip 2:** Reddit will give you 25 posts **per request**. To get enough data, you'll need to hit Reddit's API **repeatedly** (most likely in a `for` loop). _Be sure to use the `time.sleep()` function at the end of your loop to allow for a break in between requests. **THIS IS CRUCIAL**_

**Pro tip 3:** The API will cap you at 1,000 posts for each subreddit (assuming the subreddit has that many posts).

**Pro tip 4:** At the end of each loop, be sure to save the results from your scrape as a `csv`: JSON from Reddit > Pandas DataFrame > CSV. That way, if something goes wrong in your loop, you won't lose all your data.

---

### Necessary Deliverables / Submission

- Code and executive summary must be in a clearly commented Jupyter Notebook.
- You must submit your slide deck.
- Materials must be submitted by **10:00 AM on Monday, April 8th**.

---

## Rubric
Your local instructor will evaluate your project (for the most part) using the following criteria.  You should make sure that you consider and/or follow most if not all of the considerations/recommendations outlined below **while** working through your project.

For Project 3 the evaluation categories are as follows:<br>
**The Data Science Process**
- Problem Statement
- Data Collection
- Data Cleaning & EDA
- Preprocessing & Modeling
- Evaluation and Conceptual Understanding
- Conclusion and Recommendations

**Organization and Professionalism**
- Organization
- Visualizations
- Python Syntax and Control Flow
- Presentation

**Scores will be out of 30 points based on the 10 categories in the rubric.** <br>
*3 points per section*<br>

| Score | Interpretation |
| --- | --- |
| **0** | *Project fails to meet the outlined expectations; many major issues exist.* |
| **1** | *Project close to meeting expectations; many minor issues or a few major issues.* |
| **2** | *Project meets expectations; few (and relatively minor) mistakes.* |
| **3** | *Project demonstrates a thorough understanding of all of the considerations outlined.* |


### The Data Science Process

**Problem Statement** 
- Is it clear what the goal of the project is?
- What type of model will be developed?
- How will success be evaluated?
- Is the scope of the project appropriate?
- Is it clear who cares about this or why this is important to investigate?
- Does the student consider the audience and the primary and secondary stakeholders?

**Data Collection** 
- Was enough data gathered to generate a significant result?
- Was data collected that was useful and relevant to the project?
- Was data collection and storage optimized through custom functions, pipelines, and/or automation?
- Was thought given to the server receiving the requests such as considering number of requests per second?

**Data Cleaning and EDA** 
- Are missing values imputed/handled appropriately?
- Are distributions examined and described?
- Are outliers identified and addressed?
- Are appropriate summary statistics provided?
- Are steps taken during data cleaning and EDA framed appropriately?
- Does the student address whether or not they are likely to be able to answer their problem statement with the provided data given what they've discovered during EDA?

**Preprocessing and Modeling** 
- Is text data successfully converted to a matrix representation?
- Are methods such as stop words, stemming, and lemmatization explored?
- Does the student properly split and/or sample the data for validation/training purposes?
- Does the student test and evaluate a variety of models to identify a production algorithm (**AT MINIMUM:** Bayes and one other model)?
- Does the student defend their choice of production model relevant to the data at hand and the problem?
- Does the student explain how the model works and evaluate its performance successes/downfalls?

**Evaluation and Conceptual Understanding** 
- Does the student accurately identify and explain the baseline score?
- Does the student select and use metrics relevant to the problem objective?
- Does the student interpret the results of their model for purposes of inference?
- Is domain knowledge demonstrated when interpreting results?
- Does the student provide appropriate interpretation with regards to descriptive and inferential statistics?

**Conclusion and Recommendations** 
- Does the student provide appropriate context to connect individual steps back to the overall project?
- Is it clear how the final recommendations were reached?
- Are the conclusions/recommendations clearly stated?
- Does the conclusion answer the original problem statement?
- Does the student address how findings of this research can be applied for the benefit of stakeholders?
- Are future steps to move the project forward identified?


### Organization and Professionalism

**Project Organization**
- Are modules imported correctly (using appropriate aliases)?
- Are data imported/saved using relative paths?
- Does the README provide a good executive summary of the project?
- Is markdown formatting used appropriately to structure notebooks?
- Are there an appropriate amount of comments to support the code?
- Are files & directories organized correctly?
- Are there unnecessary files included?
- Do files and directories have well-structured, appropriate, consistent names?

**Visualizations**
- Are sufficient visualizations provided?
- Do plots accurately demonstrate valid relationships?
- Are plots labeled properly?
- Are plots interpreted appropriately?
- Are plots formatted and scaled appropriately for inclusion in a notebook-based technical report?

**Python Syntax and Control Flow**
- Is care taken to write human readable code?
- Is the code syntactically correct (no runtime errors)?
- Does the code generate desired results (logically correct)?
- Does the code follows general best practices and style guidelines?
- Are Pandas functions used appropriately?
- Are `sklearn` and `NLTK` methods used appropriately?

**Presentation**
- Is the problem statement clearly presented?
- Does a strong narrative run through the presentation building toward a final conclusion?
- Are the conclusions/recommendations clearly stated?
- Is the level of technicality appropriate for the intended audience?
- Is the student substantially over or under time?
- Does the student appropriately pace their presentation?
- Does the student deliver their message with clarity and volume?
- Are appropriate visualizations generated for the intended audience?
- Are visualizations necessary and useful for supporting conclusions/explaining findings?


---

### Why we choose this project for you?
This project covers three of the biggest concepts we cover in the class: Classification Modeling, Natural Language Processing and Data Wrangling/Acquisition.

Part 1 of the project focuses on **Data wrangling/gathering/acquisition**. This is a very important skill as not all the data you will need will be in clean CSVs or a single table in SQL.  There is a good chance that wherever you land you will have to gather some data from some unstructured/semi-structured sources; when possible, requesting information from an API, but often scraping it because they don't have an API (or it's terribly documented).

Part 2 of the project focuses on **Natural Language Processing** and converting standard text data (like Titles and Comments) into a format that allows us to analyze it and use it in modeling.

Part 3 of the project focuses on **Classification Modeling**.  Given that project 2 was a regression focused problem, we needed to give you a classification focused problem to practice the various models, means of assessment and preprocessing associated with classification.   