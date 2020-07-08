# Youtube-Project
# Project Name A MUSICAL ANALYSIS
Preparing Billboard 100 and Youtube Statistics to Analyze Trends

This project is a part of the [Data Science Working Group](http://datascience.codeforsanfrancisco.org) at [Code for San Francisco](http://www.codeforsanfrancisco.org).  Other DSWG projects can be found at the [main GitHub repo](https://github.com/sfbrigade/data-science-wg).

#### -- Project Status: [Completed]

## Project Intro/Objective
The purpose of this project is showcase trends in Youtube and Billboard 100 lists by extracting, tranforming and loading data.

### Methods Used
### Technologies
* Python
* PostGres, MySql
* Pandas, jupyter


## Project Description
Step 1 Extracting the data
Data Source 1:
Trending YouTube Video Statistics (CSV)
-	We found a CSV dataset from Kaggle that provided “Trending YouTube Video Statistics” (link: https://www.kaggle.com/datasnaek/youtube-new). After downloading this csv file locally, we then proceeded to read the csv into our jupyter notebook using pandas (i.e. read_csv syntax).

Data Source 2:
YouTube Category IDs (JSON)
-	We downloaded a JSON dataset that provided information on YouTube category ids from the same kaggle website as above (link: https://www.kaggle.com/datasnaek/youtube-new). After downloading it locally, we imported the json file using the following syntax:
with open('US_category_id.json') as json_file:
  json_data = json.load(json_file)
-	After importing the JSON file, we needed to navigate into the json lists to track down category ids/titles. After finding where this information was located, we looped through the JSON to get a list of category id numbers and these corresponding category titles. This was done with the following syntax:
	items = json_data["items"]
ids = []
titles = []
for item in items:
    		ids.append(item["id"])
    		titles.append(item["snippet"]["title"])
titles
-	After completing the loop, we created a dataframe using pandas to story the list of ids and category names.
Data Source 3:
Billboard’s The Hot 100 List (HTML)
-	We webscraped the Billboard Trending 100 list (link: https://www.billboard.com/charts/hot-100) to find the trending songs and corresponding artists. To do this, we used the Beautiful Soup syntax taught in class.
-	The information was gathered using a “for loop,” and appending the found information to two empty lists (i.e. one list holds song information and another list holds artist information).
-	When scraping through a loop, we saved the resulting artist and song information in a table with two corresponding columns.
Step 2  Transforming the data
-	After reading our csv and json files into our jupyter notebook with pandas to separate dataframes, we then changed the headings of relevant columns as needed and configured the data types (i.e. using .astype(str).astype(int)) so that we would be able to work with the information.
-	We then merged both dataframes into one table for our use. We used a left join for this because we wanted to match information from the category id json file to the full csv of trending youtube statistics. The following syntax was used to complete this:
merged_df = pd.merge(youtubecsv_df, category_list, how = "left", on="cat_id")
-	When this was done, we were then able to filter the dataframe to just get the columns that we want to upload into our production database.
-	The Billboard information that we scraped using Beautiful Soup was also saved converted from a table to a dataframe.
Step 3 Loading the data
-	After transforming our data on jupyter notebook using pandas, we then created a corresponding schema in postgreSQL using Pg Admin 4.
-	Once this was done, we were able to use SQL Alchemy to load the data into Postgres. To do this, we needed to connect to the engine. Once connected, we checked our table was indeed present by using the following syntax:
engine.table_names()
-	After confirming we were connected to postgres, we were able to transforming our dataframes into databases using the to_sql syntax.

Next steps
The information gathered here could be further analyzed to determine whether there is any relation between songs/artists trending on YouTube and songs/artists that Billboard identifies as in their “Top 100” categorization.


(Provide more detailed overview of the project.  Talk a bit about your data sources and what questions and hypothesis you are exploring. What specific data analysis/visualization and modelling work are you using to solve the problem? What blockers and challenges are you facing?  Feel free to number or bullet point things here)

## Contributing Members
Yinka Adesanmi, Nitin Madaan, Yashwinie Shivanand


**Team Leads (Contacts) : [Full Name](https://github.com/[github handle])(@slackHandle)**

#### Other Members:

|Name     |  Slack Handle   | 
|---------|-----------------|
|[Full Name](https://github.com/[github handle])| @johnDoe        |
|[Full Name](https://github.com/[github handle]) |     @janeDoe    |

## Contact
* If you haven't joined the SF Brigade Slack, [you can do that here](http://c4sf.me/slack).  
* Our slack channel is `#datasci-projectname`
* Feel free to contact team leads with any questions or if you are interested in contributing!
