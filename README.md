# TwitterAPI_dashboard
Using the twitter API v2 to analyze engagement trends in tweets and users, and visualizing the data as a Tableau dashboard.

## tweet_collector.ipynb
This Python notebook makes the API calls to twitter and appends the responses to a JSON file (stored in the 'json_response' folder), which is then parsed to create CSV files (the default results for the Kellogg's strike topic are stored in the 'CSV' folder, the two test results are stored in 'Test' and 'Test2') that are structured for a relational model, which can then be imported into Tableau to generate the dashboard. There are headings, descriptions and comments throughout the notebook explaining how the code works.

To test this notebook, fill out these variables and then run every cell:
<ul>
 <li> Go to the heading 'Build a query and specify number of API calls'. In the string variable 'topic', specify query parameters to search for the tweet you want. It can be as simple as a single keyword or a hashtag. OR operators and brackets work, if no operators are specified between keywords an AND operator is implied. The sample query is 'KelloggsStrike OR KelloggStrike OR BoycottKelloggs OR (Kellogg (strike OR striking OR boycott OR scab))'.
  For more details on how to build a more complex query, check https://developer.twitter.com/en/docs/twitter-api/tweets/search/integrate/build-a-query. 
  Then specify how many API calls you would like to make in variable 'n' (up to 450). Note that making 450 calls would take around 5-10 minutes.
  This will print n lines of '200' to signal that the API call was successful.
 <li> Go to the heading 'For testing, specify the new test folder name in the variable 'folderName'. A new test folder will be created containing the newly generated CSV files. If the folder already exists then overwrite the CSV files in the specified folder.
</ul>
## Dashboards
The screenshots of the dashboards are included in the folder: the default Dashboard_Kelloggs, and the tests Dashboard_Amazon, and Dashboard_Environment. If there is access to Tableau, the Twitter_Dashboard workbook is also included. 

## Plan
### Original plan and timeline
The project option I’ve chosen is to explore a social media API and use it to collect data for a dashboard. The social media site of interest is Twitter. I am using the Twitter API v2 to collect data, and Tableau to visualize the dashboard. 

I want to look at what engagement looks like under a certain topic. The sample topic I’ve chosen is the recent Kellogg’s strike. I collected tweet and user information for almost 45000 tweets under this topic, and some of the information I’ve visualized in my dashboard include:
<ul>
 <li>What are the top trending hashtags included in tweets on this topic? (frequency of hashtags included in tweets over time)
 <li>engagement with tweets under a certain topic/hashtag (number of retweets and likes)
 <li>what do these tweets include (links, media, geolocations)
the profile of the tweet (verified? how many followers?)
</ul>

week 8: explore the APIs that Twitter offers and see how i can incorporate the endpoints that they offer into the dashboard
week 9: Try to request some information with the APIs (no data processing yet) and get the information on Tableau (software for visualizing dashboards). Look at the raw data and try to make sense of it and make notes of any trends I see
week 10: After I know what kind of data I can request, plan out what filters I will have in the dashboard and see which filters can be used together to best communicate my findings
week 11: Create dashboard and implement filters
week 12: Complete dashboard
week 13: submit presentation
week 14: submit final deliverables
### Plan changes and improvements since the presentation milestone:
<ul>
 <li> From the feedback, I have figured out how to request more than 100 tweets. For a topic, I can return up to 45000 tweets.
From the feedback, and also following my original plan, I added sentiment analysis of tweets. For simplicity I am using the SentimentIntensityAnalyzer from the nltk package, so no training is required.
 <li> Since there is a much larger dataset to work with, relying on Tableau to join the data to overcome nesting is not feasible. So I have parsed the JSON file and generated CSV files that are structured for a relational model.
 <li> Instead of presenting multiple topics in a dashboard, I’ve decided to only focus on one topic at a time, which the sample topic is the Kellogg’s strike discussion. Previously I planned to look at multiple trending topics at a time. However, working with the original dataset made me realise that with multiple topics, the trends were confusing and muddy. A better approach would be focus on one topic at a time.
</ul>

## Testing
<table>
  <tr>
    <th>Features</th>
    <th>Testing notes</th>
  </tr>
  <tr>
    <td>Connected to the API and specified query parameters to return the information I want</td>
    <td>I used a different query for testing, this time using a broader topic: ‘Amazon’. I tested it with the maximum number of API calls to see if it would yield exactly 45000 tweets since the query is a lot less specific. However, it only yielded 44885 tweets, which is less than the number of tweets returned by my default query, which is 44903. The third test with an even broader query keyword ‘environment’ returned 44869 tweets. I quickly realized that the limit of 45000 is not reached due to the fact that this API endpoint only returns tweets within the week.</td>
  </tr>
  <tr>
    <td>Utilized pagination: every API request returns up to 100 tweets. For every response from an api request,check if there is a next token, include that in the query to request for the next 100 tweets. This allows collection of up to 45000 tweets every 15 minutes, as only 450 request are allowed in this time frame.</td>
    <td>Pagination works well with both the default and the test queries when making the maximum number of API calls.</td>
  </tr>
   <tr>
    <td>Parsed the returned nested JSON file to generate CSV files that are structured for a relational model, so that the data is easier to visualize on Tableau.</td>
    <td>Since the structure of the JSON file for both the default and test queries are the same, there was no issue parsing all the JSON files to generate CSV files.</td>
  </tr>
   <tr>
    <td>Sentiment score calculation for each text</td>
    <td>While this is a ready-to-use sentiment analyzer, no training is needed and there are no errors. However, sometimes the score does not reflect the exact sentiment of the tweet. A lot of tweets received positive scores when the sentiment is very negative. Some examples found in Tweet.csv are:
‘RT @WorkingFamilies: Never believe a company that says it can't afford to pay all of its employees good wages and supply good benefits when…’: 0.8269
‘RT @INAFLCIO: Friends don’t let friends buy Kellogg’s. #BoycottKelloggs https://t.co/U2pmtQzjCI’: 0.7351</td>
  </tr>
 </tr>
   <tr>
    <td>Graphs and filters on Tableau to represent all the information collected</td>
    <td>Since the structure of the CSV files for both the default and test queries are the same, there was no issue rendering the same graphs and filters for the different datasets.</td>
  </tr>
</table>
## Project report
Contains all the readme information as well as extra comments and analysis on the data.
   
