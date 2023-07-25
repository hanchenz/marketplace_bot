# Marketplace (Discord Bot)
Marketplace aims to simplify the process of buying/selling/trading items. This user-friendly tool is built using [JDA](https://github.com/DV8FromTheWorld/JDA) (Java Discord API), and all data is stored in [MongoDB Atlas](https://www.mongodb.com/atlas/database).

## Summary
Unlike other online marketplaces or discussion forums, our bot targets Discord users who are interested in integrating a C2C marketplace functionality into their server. This bot helps narrow the search for users looking to buy/sell within their interest-based communities. The bot assists in sharing and filtering listings, making the selling experience <b>easier</b> and the search for items <b>faster</b>.

Bot presentation:
- [YouTube Video Presentation](https://www.youtube.com/watch?v=vBgy_S-a8P8)

## Features
Marketplace Bot has the following features:
- [Create a Listing](#create-a-listing): Users can post their listing by filling out a form that inquires details of the item being sold.
- [View Your Own Listings](#view-your-own-listings): Users can review the listings they have already posted and delete the ones that are no longer active.
- [Search and Sort for Listings](#search-and-sort-listings): Users can search for specific listings that contain a keyword in the title and sort the results by date/price.
- [Update Your Location](#update-your-location): Users can add or update their approximate location that is displayed along with their listing, which informs other potential buyers where the item may be picked up/shipped from.
- [Create a New Channel](#create-a-new-trading-channel): A text channel with special permissions, where the bot can post users' listings, will be created in the server.

# Commands
The bot executes the following commands when the user enters them into the chat.
## Create a Listing
`/createlisting`: Displays a template for the user to fill out accordingly.<br><br>
![createListingCommand](images/createListingCommand.PNG)<br><br>

After filling out the template, the user can choose to post, edit, or cancel their listing. When posting the listing, it will be displayed in the designated trading channel.<br>

## View Your Own Listings
`/mylisting`: Sends the user a direct message containing all their listings within the server. User can choose to delete their listing.<br>
## Search and Sort Listings
`/searchlistings`: Allows users to search for listings containing a keyword in the title. Users can sort their search results with a select menu and are given the option to sort by price or date.<br><br>
![searchCommand](images/searchCommand.PNG)<br>
## Update Your Location
`/updatelocation`: Prompts the user to update their state and city through a direct message.<br><br>
![updateLocationState](images/updateLocationStates.PNG)<br><br>
![updateLocationCity](images/updateLocationCity.PNG)<br>
## Create a New Trading Channel
`/createtradingchannel`: Creates a new text-channel using a unique name defined by the user. This channel has special permissions where only the bot can send messages.<br><br>
![createTradingChannel](images/createTradingChannel.PNG)<br>
# Events
This section provides details of what would occur when specific [JDA Events](https://ci.dv8tion.net/job/JDA/javadoc/net/dv8tion/jda/api/events/Event.html) are triggered.
## Bot Joins Server

First, the server owner will receive the following DM from the bot:

![Screenshot (50)](https://user-images.githubusercontent.com/78775944/232926423-d039fda7-286d-4cd2-b9b9-d978e2218a4b.png)

If the owner selects "Bot Can Create The Channel", the bot will attempt to create a new text channel named "trading-channel". If a channel with that name already exists OR if "I'll Create The Channel" is selected, the server owner MUST call the command `/createtradingchannel` to create the trading channel. The owner MUST input a custom, unique name for the channel when calling the command. If they do not and they enter a name that already is present in the server, they will have to call the command again until a unique name is given.

Second, each member of the server, including the owner, will receive a DM from the bot asking the member to select the State and City they are located in from drop-down menus. An exact location is not necessary. The bot tracks this information to later attach it to listings created by members.

## Bot Leaves Server
Listings within the server will be deleted from the database. If the server owner decides to invite the bot back, previous information will no longer be available. User data will also be removed if the user is not a part of another server containing the bot.
## New Member Joins Server
The bot will send a greeting to the user's direct messages and ask the user to update their location.

## Member is Removed From Server
Only listings in the server belonging to the user will be removed from the database. User data will only be fully erased in the database if they do not belong to any other server containing the bot.
