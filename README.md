# Stackoverflow and Developer Works Slack Bot
### A Slack bot built with Node-RED on IBM Bluemix
The bot will make a post in the specified channel whenever a new question has been asked pertaining to the preset query in the Node-RED application. 

##### Something To Note:
The instructions and images go through using and setting up both the stackoverflow and developer works bot, but you can remove the wire connecting the "Slack Response" node to either half of the application and then only the connecting part will be operational. This gives you the ability to use either the stackoverflow query or the developer works query as opposed to both.

##### An example slack bot output (with a link to the preset query):
![alt tag](https://github.com/franklsm1/SO_DW_slackBot/blob/master/SODWexample.PNG)

# Slack Bot Import and Setup
##### 1.) Copy the contents of the slackBot.json file into your Node-RED editor using the import clipboard feature.

![alt tag](https://github.com/franklsm1/SO_DW_slackBot/blob/master/import.PNG)


##### After importing your flow should look similar to this:
![alt tag](https://github.com/franklsm1/SO_DW_slackBot/blob/master/DWSOflow.PNG)

##### 2.) Next you will need to update 3 nodes (4 extra if not using the Node-Red boilerplate).
  -For both the "SO search URL" and the "DW search URL" nodes you will need to replace the stackoverflow and developer works queries in the url variable. An example url is included in each node already.
  
  -For the "Slack Response" node you will need to enable incoming webhooks for your slack team if you have not done so already, https://my.slack.com/services/new/incoming-webhook/. Then you will need to replace the text of the URL field with the Webhook URL that was created for you.
  
  ![alt tag](https://github.com/franklsm1/SO_DW_slackBot/blob/master/webhookToken.PNG)
  
  -For all 4 of the sky blue Cloudant Database nodes you will need to select the cloudant DB service that is running with your Node-RED application and update the database name that is setup for your service (if using the Node-Red boilerplate in Bluemix the default DB service and DB name of the database should be updated automatically and nothing needs to be done).
  
##### 3.) Next you will need to create two new documents inside your cloudant DB with the following properties:
  
{
  "_id": "SOCount",
  "count": 0
}

{
  "_id": "DWCount",
  "count": 0
}
  
  -The count values can be left at 0 (the bot will make an initial post to update the values) or you can set it to the current count of question results from your query.
  
##### 4.) Finally deploy the application and your slack bot is up and running!
