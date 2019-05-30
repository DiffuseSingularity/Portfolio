# Project_5_final_repo
# Project_5
Project 5 repository on restaurant inspections

## Problem Statement
Which features are most indicative of the best (or worst) restaurant grade? Are restaraunt inspections subject to bias? If so, what type?


## Important Notes on data
Here's a news article that goes into an editorial overview of the below! -

https://www.nytimes.com/2017/05/17/nyregion/new-york-today-what-do-restaurant-grades-mean.html

#### From the About_NYC_Restaurant_Inspection_Data_on_NYC_OpenData.docx file 

Last updated 09/24/2018?

This document contains a wealth of important info to contextualize this data.  The document firmly asserts one should read through this about doc before utilizing the data.  Some key points -

"only restaurants in an active status are included in the dataset."

"Keep in mind that thousands of restaurants start business and go out of business every year; only restaurants in an active status are included in the dataset. 

"Restaurants that go out of business are removed. "

"Establishments with inspection date of 1/1/1900 are new establishments that have not yet received an inspection. "

"Restaurants that received no violations are represented by a single row and coded as having no violations using the ACTION field."

"Because this dataset is compiled from several large administrative data systems, it contains some illogical values...data may also be missing"

"The Health Department’s Restaurant Grading website is here: 
http://www1.nyc.gov/site/doh/services/restaurant-grades.page"

"See the data dictionary file in the Attachments section of the OpenData website for a summary of data fields and allowable values."

"The dataset currently available on OpenData differs from previous versions in that administrative and other unscored violations are included. "

"The analyst must be familiar with the NYC restaurant letter grading program to be able to analyze this dataset correctly.  Background on how the program works can be found on the DOHMH website: 
https://www1.nyc.gov/site/doh/business/food-operators/letter-grading-for-restaurants.page"

#### GRADING SYSTEM
"restaurant letter grading began July 27, 2010. The program allows for a two-step inspection process, providing an opportunity for restaurants who do not receive an “A” on their initial inspection to be re-inspected.  This re-inspection occurs no less than 7 days after the initial inspection. 
A score of less than 14 points on either initial or re-inspection results in an “A” grade
On re-inspection, a score of 14-27 points means a restaurant receives both a “B” grade and a “Grade Pending” card
On re-inspection, a score of 28 or more points means a restaurant receives both a “C” grade and a “Grade Pending” card
Certain uncorrected violations may generate additional compliance inspections, which are ungraded.
The restaurant is instructed to post the grade card or the grade pending card, but some restaurants may post both."

#### WHEN IS THE NEXT INSPECTION
"If the initial score is less than 14 points, the next initial inspection occurs approximately 12 months later; if the higher of the scores is 14-27 points, the next initial will be 5 to 7 months after re-inspection; if the higher score is 28 or more points, the next initial inspection will occur 3 to 5 months after re-inspection. 
If a restaurant is closed on inspection, the process is a little different. "

"If a restaurant is closed on a re-inspection, it will get a reopening inspection before it is allowed to resume operations. The reopening inspection is not a gradable inspection and therefore the score will not determine the grade for the inspection cycle. If the restaurant passes the reopening inspection, the CURRENT GRADE field will be based on the re-inspection score the restaurant received before it was closed. 
If a restaurant is closed on an initial inspection, it will get a reopening inspection before it is allowed to resume operations. The reopening inspection is not a gradable inspection and therefore the score will not determine the grade for the inspection cycle. If the restaurant passes the reopening inspection, the previously posted grade card is taken down and it is given a “Grade Pending” card until a re-inspection determines the next grade. "

#### DISCREPANCIES BETWEEN SCORES AND GRADES
"The SCORE and GRADE fields may be inconsistent with each other because of limitations or errors in the data systems"

"There may also be cases where a grade card was given out but a record of that grade issuance is missing from the data system, and therefore missing from this dataset, even though the SCORE field is populated.  Note that when initial inspections are adjudicated down to the A range, the absence of an accompanying grade associated with that inspection is correct, because the grade would not be assigned until the re-inspection is performed. "

-----------------------------------------------------------


## Data Cleaning

We removed all variables with the imputed date 01-01-1900, indicating they have yet to be inspected as per the documentation.  After doing some cursory correlations, we saw that borough and grade had no particularly significant relationships.  We decided to use score, a much more complete variable which is the underlying weighted metric used to determine Grade, as our Y variable. We removed grade, grade date, and all other time related variables for the purposes of our model.  We removed the excessive sets of null rows for score, 18184 of the 381911 datapoints.  We compiled an address column by combining the street, building, and zipcode columns, which allowed us to compile a listing of unique addresses that Mitchell used for a google maps function.  

## Google maps function 

After combining the columns that included component parts of an address in order to generate a column with a complete address, we created a second data frame that strictly included every address only once. This was then passed into a function which both geocoded and plotted them on Google Maps.  


## Conclusions, Future Improvements -

Early on, we were able to determine that Grades were not significantly correlated with boroughs - none of the boroughs had correlations with Grade A, B, or C stronger than .01.  
Because of limitations in the data, specifically how it is computed from multiple sources aggregated together, there is a lot of missing grades and each datapoint is an individual violation, rather than an inspection date.  More cleaning must be done to combine these violations into violation dates, which would be performed by a for loop that would aggregate same restaurants with same violation dates and add up their scores.  This could then be imputed to be a restaurants actual score, and eliminate a lot of the missing Grades.  




A time series analysis on grades and number of inspections over time could be conducted, likely demonstrating that more inspections is associated with worse grades/scores, as the Department of Health conducts more inspections on worse performing restaurants.  Once the missing dates and grades are filled in/imputed, we would have a much more complete, conscise dataset.  We could also look atat violations per zipcode, and track rats/mice populations through the boroughs by zip code via restaurant violations.
