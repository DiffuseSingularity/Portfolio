## Introduction
Prior to my immersion in General Assembly's Data Science course, I was often left feeling frustrated in both work and passion projects when it came down to data management.  Issues would come up from membership databases, email marketing systems, websites, and social media pages, where I knew that someone with a stronger statistical background and coding skills would be able to ascertain insights beyond those that I could by looking at simple analytics provided by web platforms and doing limited cleaning and analytics via Excel.  This is what has compelled me to this project, exploring data and developing a model on a set of email newsletters sent to over 1,500 followers for my nonprofit collaborative arts group, Lightsource, facilitated by the email marketing platform, Mailchimp.  I intend to apply these principles to other email newsletters in my nonprofit network, on Mailchimp and beyond, as well as towards strategies oriented around social media communications on platforms such as Instagram and Facebook, to facilitate more meaningful connection between people and various mission oriented projects. 

### Original Problem Statement 

How can Natural Language Processing (NLP) and other data science techniques be applied to mass email communications, specifically in generating statistical models which can provoke insight on how to improve outreach metrics, specifically, subject titles and their impact on maximizing open rates, and minimizing bounced emails?


## Table Of Contents

##### Capstone_Instructional_Readme
Detailed instructions for this capstone project in a 5 part series of Readme's, provided by General Assembly.  Used to keep track of and break down the ideal process and timelines in performing this capstone project.

##### Lightsource_draft_EDA
Containing my initial data - 1)a table of users with their "Member Rating" anonymized by me, and summarized metrics for each campaign.  Pairplots, and an initial round of NLP and a linear regression model are included, though this was mostly shelved in favor of individuated data that needed cleaning (see "Gathering Data" below)

##### Lightsource_MailChimp_Data
Cleaned dataframes of Lightsource Mailchimp subscriber data (See "Cleaning and Merging) with anonymization process explained, EDA and Models included in folders and labeled as such.  MANY OF THE CODE IN FOLDERS BESIDES EDA AND MODELS WILL NOT WORK, as they have been stripped of their initial, sensitive data, and replaced with secured data with an identifier key ("email_id) in csv's.  In Lightsource_Campaign_Cleaned>>All_Campaigns_Cleaned, we can see the csv's of each campaign combined to form the final, concise dataframe with nearly 12,000 datapoints.   


### My Process

As we have only begun using Mailchimp around December 2018, I was compelled to create more data for this project, by creating some email campaigns for the upcoming Parade For Love our nonprofit, Lightsoure, was cosponsoring with some other aligned groups.  Once I had these results, I had a set of over 12 emails sent out to over 1,000 subscribers, meaning I have nearly 12,000 datapoints to work with, with at least 5 metrics to determine relationships of engagement with.

My metrics for email newsletters are opens, clicks, conversions/subscriptions, unsubscribes, delivery rate/bounces, and revenue generation. What words or phrases, and practices in general, are associated with what metrics?  It is most practical for me to focus on the metrics stated in my problem statement for the first component of this ongoing project - User open rates, unsubscribes, and service generated bounces.  Unsubscribes has to do with the body of emails, so open rates and bounces are the most pertinent variables to explore. 


#### Cleaning and Merging
   The data was not easy and concise to put together.  Various metrics for subscribers per email campaign were kept in individuated CSVs on our Mailchimp account.  Sometimes they didn't even have their own row, and needed to have a value imputed (a no opens csv, for example, had to be given an opens column with values of 0 for 0 email opens by a subscriber before merging to the opens dataframe).  Doing this with anonymization (below) proved to be a challenge.  The process is laid out in the dataframes for each campaign, but the original data is no longer there for anonymization purposes.  You can follow along with your own Mailchimp data or similar csv's.  Similarly to the anonymization process below, I was able to index all the summary campaign data, to each individual's metrics associated with the campaign.  One can also simply start from the completed and anonymized "campaign_sum_data.csv"and "Complete_Secure_Dataset.csv immediately.

#### Anonymization
Anonymization of sensitive information is Key to handling data like this.  I have access to names and emails, along with some addresses and other sensitive information, that would be unethical for me to share publicly.  Thus, each individual audience member's data is stripped of identifying information, and assigned a randomly generated key, that is attached to their email in a dictionary outside of this publicly available repo.

### Visualization
I explored various relationships with Seaborn primarily, both in the draft EDA and with the cleaned data.  The lack of relationship with successful opens and hard bounces, while there is a relationship with soft bounces, was interesting and spoke to the first few emails hard bouncing on defunct emails in the initial first few emails sent.  There are clear attrition rates of subscribers in the first couple of emails, marked by negative relationships in successful deliveries and other metrics over the first 5 email campaigns.  Most other observations were fairly intuitive. 

### Modeling

Regression modeling was attempted on the Subject Headers in relation to Opens, both with CountVectorizer and TfidfVectorizer.  The latter fared slightly better, but neither produced significant results.

Classification modeling was performed on Subject headers and bounce/successful send metrics.  They performed relatively well, but quite likely because the majority of emails do get sent through without being bounced.  The model was not much more predictive than the typical rate of sent versus bounced emails.  A more complex model is needed.  Perhaps these results are due to there being some seriously imbalanced classes, with about 30 sent emails for every bounced email.


## Future Developments

This entire project is the first part of a larger exploration of data science principles on nonprofit arts and education oriented outreach campaigns.  Many people are seeking meaningful experiences with likeminded people who want to affect change they can feel good about.  Many nonprofits are viewed as doing necessary but burdensome work.  In my experience, public service can be very fulfilling if planned with such an intention, and campaigned as both fun and prosocial.  This is what will drive me to continue developing these models.

A/B testing is a great way to generate more subject header and body data, and better reaching audiences by experimenting with different email formats and headers.  I only recently became aware that it was a free feature on Mailchimp - it could be relatively new.  Analytics on the bodies of emails may provide insight into other metric relationships that aren't as connected to subject headers, like multi-click rates within the body of emails.  Checking out Mailchimp's API key is worthwhile as well https://developer.mailchimp.com/documentation/mailchimp/guides/get-started-with-mailchimp-api-3/

Segmentation of audiences will enable better reaching of specific audiences, while developing additional metrics to run classification models upon.  An unsupervised learning model may enable me to see groupings and relationships beyond 2 dimensional ones that pairplots and other such 2D visualizations show.  This could be useful towards segmenting audiences.

A time series analysis can be conducted, to see if time during the day, days of the week, and seasons impact metrics, though more data would be ideal to conduct such analysis.

Social media analytics, especially Facebook data, would almost definitely be more immediately fruitful.  I have access to several pages with years of posting history, and a scraper in my Future Developments folder that can extract the emoji reactions to posts.  It is without a doubt Facebook added those to develop their data products more, we might as well see what we can get out of them as well.

Best practices from existing industries always provide useful resources, in combination with this quantitative research should net the results I seek. 

### Google Slides Presentation

https://docs.google.com/presentation/d/1RnNtMfY3xgnFoOBP-g_B8gy_DkBVFaL6bPVB5i0O0ic/edit?usp=sharing


Original Readme below
---------------------------------------------------
# Capstone Project

Your Capstone project is the culmination of your time at GA. You will be tasked with developing an interesting question, collecting the data required to model that data, developing the strongest model (or models) for prediction, and communicating those findings to other data scientists and non-technical individuals. This introductory document lays out the five consitutent portions of the project and their due dates.

## Your Deliverables

- A well-made predictive model using either structured or unstructured machine learning techniques (or other technique approved in advanced by the global instructors), as well as clean, well-written code. 
- A technical report aimed at fellow data scientists that explains your process and findings
- A public presentation of your findings aimed at laypeople. 

### **[Capstone, Part 1: Topic Proposals](./part_01/)**

In Part 1, get started by choosing **three potential topics and problems**, describing your goals & criteria for success, potential audience(s), and identifying 1-2 potential datasets. In the field of data science, good projects are practical. Your capstone project should be manageable and affect a real world audience. This might be a domain you are familiar with, a particular interest you have, something that affects a community you are involved in, or an area that relates to a field you wish to work in.

One of the best ways to test ideas quickly is to share them with others. A good data scientist has to be comfortable discussing ideas and presenting to audiences. That's why for Part 1 of your Capstone project, you'll be preparing a lightning talk in addition to your initial notebook outlining the scope of your project.  You will present your candidate topics in a slide deck, and should be prepared to answer questions and defend your data selection(s). Presentations should take no more than 3-5 minutes.

**The ultimate choice of topic for your capstone project is yours!** However, this is research and development work. Sometimes projects that look easy can be difficult and vice versa. It never hurts to have a second (or third) option available.

- **Goal**: Prepare a 3-5 minute lightning talk that covers three potential topics, including potential sources of data, goals, metrics and audience.
- **Due**: Apr 10, 2019

### **[Capstone, Part 2: Problem Statement + EDA](./part_02/)**

For Part 2, provide a clear statement of the problem that you have chosen and an overview of your approach to solving that problem. Summarize your objectives, goals & success metrics, and any risks & assumptions. Outline your proposed methods and models, perform your initial EDA, and summarize the process. **Your data should be in hand by this point in the process!**

**Again, your data should be in hand by this point the process!**

- **Goal**: Describe your proposed approach and summarize your initial EDA in a code submission to your local instructor ([submission link (LINK TBD)](#))
- **Due**: April 24, 2019

### **[Capstone, Part 3: Progress Report + Preliminary Findings](./part_03/)**

In Part 3, you'll create a progress report of your work in order to get feedback along the way. Describe your approach, initial results, and any setbacks or lessons learned so far. Your report should include updated visual and statistical analysis of your data. You’ll also meet with your local instructional team to get feedback on your results so far!

- **Goal**: Discuss progress and setbacks, include visual and statistical analysis, review with instructor. [Submit your progress update on this form (LINK TBD).](#)
- **Due**: May 6, 2019

### **[Capstone, Part 4: Report Writeup + Technical Analysis](./part_04/)**

By now, you're ready to apply your modeling skills to make machine learning predictions. Your goal for Part 4 is to develop a technical document (in the form of Jupyter notebook) that can be shared among your peers.

Document your research and analysis including a summary, an explanation of your modeling approach as well as the strengths and weaknesses of any variables in the process. You should provide insight into your analysis, using best practices like cross validation or applicable prediction metrics.

- **Goal**: Detailed report and code with a summary of your statistical analysis, model, and evaluation metrics.
- **Due**: May 14, 2019

### **[Capstone, Part 5: Presentation + Recommendations](./part_05/)**

Whether during an interview or as part of a job, you will frequently have to present your findings to business partners and other interested parties - many of whom won't know anything about data science! That's why for Part 5, you'll create a presentation of your previous findings with a non-technical audience in mind.

You should already have the analytical work complete, so now it's time to clean up and clarify your findings. Come up with a detailed slide deck or interactive demo that explains your data, visualizes your model, describes your approach, articulates strengths and weaknesses, and presents specific recommendations. Be prepared to explain and defend your model to an inquisitive audience!

- **Goal**: Detailed presentation deck that relates your data, model, and findings to a non-technical audience.
- **Due**: May 17, 2019
