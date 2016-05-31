# Stackoverflow and Developer Works Slack Bot
### A Slack bot built with Node-RED on IBM Bluemix
This bot will make a post in the chosen channel whenever a new question has been asked on the preset query for stackoverflow or developer works answers. The bot searches using a URL that is set in the Node-RED application. It compares the number of questions value stored in a database to the current number of questions from the search query and if there is an increase in the question count a message is posted. In the example provided for this guide, it queries the URL on 15 minutes intervals but this value can be changed from anywhere to 1 second to every 1000 hours.

This README will walk you through setting up this slack bot for your own personal slack channel.

###### Example query URLs:
Stackoverflow: http://stackoverflow.com/search?q=time
Developer Works Answers: https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=newest&q=java

##### Something To Note:
The instructions and images go through using and setting up both the stackoverflow and developer works bots, but you can remove the wire connecting the "Slack Response" node to either half of the application and then only the connecting part will remain operational. This gives you the ability to use either the stackoverflow query or the developer works query as opposed to both.

##### An example slack bot output (with a link to the preset query):
![alt tag](https://github.com/franklsm1/SO_DW_slackBot/blob/master/SODWexample.PNG)

## Slack Bot Import and Setup
##### 1.) Copy the contents of the slackBot.json file into your Node-RED editor using the import clipboard feature.

![alt tag](https://github.com/franklsm1/SO_DW_slackBot/blob/master/import.PNG)


##### After importing your flow should look similar to this:
![alt tag](https://github.com/franklsm1/SO_DW_slackBot/blob/master/DWSOflow.PNG)

##### 2.) Next you will need to update 3 nodes (4 more extra nodes if not using the Node-Red boilerplate).
  -For both the "SO search URL" and the "DW search URL" nodes you will need to replace the stackoverflow and developer works queries in the url variable. An example url is included in each node already.
  
  -For the "Slack Response" node you will need to enable incoming webhooks for your slack team if you have not done so already, https://my.slack.com/services/new/incoming-webhook/. Then you will need to replace the text of the URL field with the Webhook URL that was created for you.
  
  ![alt tag](https://github.com/franklsm1/SO_DW_slackBot/blob/master/webhookToken.PNG)
  
  -For all 4 of the sky blue Cloudant Database nodes you will need to select the cloudant DB service that is running with your Node-RED application and update the database name that is setup for your service (if using the Node-Red boilerplate in Bluemix the default DB service and DB name of the database should be updated automatically and nothing needs to be done).
  
##### 3.) Next you will need to create two new documents inside your cloudant DB:
  To create these documents you will need to click on the Cloudant NoSQL DB service from your bluemix dashboard.  Once clicked you will see a page that explains about your Cloudant NoSQL DB and it will contain a button that says "LAUNCH". Click that button. A new tab will not open with options for your Cloudant NoSQL DB. Click on the "nodered" database name, which is created by default as part of the boiler plate creation. Next click the plus symbol at the end of the "All Documents" tab, followed by clicking the "New Doc" tab that will appear. Then paste the following properties into the document and click the "Create Document" button. These steps will need to be done twice, once for each property.
  
######  Property 1:  
  {
    "_id": "SOCount",
    "count": 0
  }

######  Property 2:  
  {
    "_id": "DWCount",
    "count": 0
  }
  
  -The count values can be left at 0 (the bot will make an initial post to update the values) or you can set it to the current count of question results from your query.
  
  ![alt tag](https://github.com/franklsm1/SO_DW_slackBot/blob/master/DBCreate.png)
##### 4.) Finally deploy the application and your slack bot is up and running!
