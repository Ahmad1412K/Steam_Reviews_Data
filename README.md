# Steam_Reviews_Data
This dataset contains a collection of user reviews of video games in the Steam Store with a plethora of information about each review such as the name of the game, app ID, the review text from 100 accounts or less, like/dislike, timestamp of review created, timestamp of review updated, etc, scraped from the STEAM API.

The data is stored in MongoDB where each record represents a game and has a name, ID, and review data collected from STEAM API, the number of reviews had been limited to only 100 user reviews for each game
this is the general schema for the records
```
{
  'appId' : appId,
  'name'  : Game Name,
  'reviews' : {
    'success' : 1 if the query was successful
    'query_summary' :{
        'num_reviews' : The number of reviews returned in this response
        'review_score' : The review score
        'review_score_desc' : The description of the review score
        'total_positive' : Total number of positive reviews
        'total_negative' : Total number of negative reviews
        'total_reviews' : Total number of reviews matching the query parameters
    }
    'cursor' : The value to pass into the next request as the cursor to retrieve the next batch of reviews
    'reviews' : {
        'recommendationid' : The unique id of the recommendation
        'author' : {
            'steamid' : the user’s SteamID
            'num_games_owned' : number of games owned by the user
            'num_reviews' : number of reviews written by the user
            'playtime_forever' : lifetime playtime tracked in this app
            'playtime_last_two_weeks' : playtime tracked in the past two weeks for this app
            'playtime_at_review' : playtime when the review was written
            'last_played' : time for when the user last played
            }
        'language' : language the user indicated when authoring the review
        'review' : text of written review
        'timestamp_created' : date the review was created (unix timestamp)
        'timestamp_updated' : date the review was last updated (unix timestamp)
        'voted_up' : true means it was a positive recommendation
        'votes_up' : the number of users that found this review helpful
        'votes_funny' : the number of users that found this review funny
        'weighted_vote_score' : helpfulness score
        'comment_count' : number of comments posted on this review
        'steam_purchase' : true if the user purchased the game on Steam
        'received_for_free' : true if the user checked a box saying they got the app for free
        'written_during_early_access' : true if the user posted this review while the game was in Early Access
        'developer_response' : text of the developer response, if any
        'timestamp_dev_responded' : Unix timestamp of when the developer responded, if applicable
  }
  }
}
```
## Potential Applications
potential applications that may use it are:

*  **Recommendation Systems For Steam Games**

*  **Word Cloud Generation Models**

*  **Monitoring Customer Sentiment**

*  **Analyzing Trends Between Users**

## Usage
Simply run the Python notebook and follow the instructions in it, you can make some modifications like:
### Update the SteamIDs.csv file with more games
This can be accomplished in multiple ways, maybe manually downloading a list like I did, or you can take a more sophisticated approach like using the steamgriddb module which gives you access to data about all Steam games, or you can generate a list using the Steam API https://api.steampowered.com/ISteamApps/GetAppList/v2/ 
### Configure how many reviews for each game 
This can be accomplished by changing the num_per_page parameter in the API URL

## Database
The notebook includes the code that adds the data collected to a MongoDB database as is, you just need to configure the database it self and then add the list of reviews to it
