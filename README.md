# ConferenceOrganization

Download and install Python 2.7 from https://www.python.org/downloads/ if not already installed on your machine 
Download and install Google App Engine SDK. The isntructions are provided here:
https://cloud.google.com/appengine/downloads
If using Windows or Mac, Google App Engine will have a nice GUI icon. If using Linux, use command line tools such as 
devappserver.py and appconfig.py
Install Git.
From the terminal, navigate to working directory, run “git clone http://github.com/uzmasyed00/ConferenceOrganization”. This will give you a directory named ConferenceOrganization.
In a web browser, go to "console.developers.google.com" and create a new project. Insert the project id in the application field in app.yaml in Conference Central directory.
Then, in Google App Engine launcher, add an existing application and navigate to the cloned directory.
Run the application.
In a browser of your choice,, navigate to localhost:port/_ah/api/explorer and start working with the end points.


#Task1

A session is implemented as a child of a conference entity. A websafe conference key is passed in the request that can be used to query the conference entity the key pertaains to. This key is then set as the parent of a session entity in the datastore.
Speaker is one of the properties of the session entity and is implemented as a string.

Session class represents a session entity with properties defined in models.py.

SessionName is a required property. Without a session name, it would not be easy for a user to identify a session.

Speaker is a repeated property so that there can be multiple speakers for a given session.

Duration has been defined of property type string although it could have been defined as an integer. I chose to have duration of type string so that user has flexibility to enter which ever units user wants to enter duration in (Be it hours, minutes etc).
If I had defined it as an integer, the unit of duration would be set and user would have to calculate the equivalent duration in the desired unit before entering it.
Although, going forward as the program evolves and duration is involved in any type of evaluation/computation or query, it would help if duration is of type integer.

TypeOfSession has been defined as string so that user has flexibility as to whatever session type user would like to create. Going forward, we might restrict user to select
from a list of specified sessions in which case it would be of type EnumProperty.

Date and time have been chosen as DateProperty and TimeProperty respectively to support queries that can be ordered/sorted by date and time.
Task 2:
addSessionToWishList - The input is a session form. Copy and paste the session key of the session from the datastore on localhost and add the sessionkey in the sessionkey field on the session form.
getSessionFromWishList - Gets user's sessions from the wishlist.

#Task 3 -  Additional queries
The 2 additional queries are as follows:
removeSessionFromUserWishList() - The user can remove any session that are there in the wish list. Copy and paste the session key of the session from the datastore on localhost and add the sessionkey in the sessionkey field on the session form.

getConferenceSessionBySessionName() - This query retrieves session based on SessionName provided. This can be useful if one needs to know details of a particular session.

#Task 3 - Query problem
The problem with implementing the given query is that inequality filters, in this case (< and != ) can not be applied to 2 different properties (start time and Type) at the same time. 
To solve the problem I thought of not using an inequality operator for one of the queries, so for example, use OR operator rather than != operator or IN operator across non-workshop sessions.
e.g :
Session.query().\
filter(Session.startTime < 19:00).\
filter(Session.Type IN (comma separated values of sessions that are not of type workshop).\

Note: Using the IN operator requires that all values in the list be knows. Thus, to achieve this, we can limit the user's options by providing a set of pre-defined values in a drop down list that the user can switch from. This will give the program control over what possible values of non-workshop sessions can be queried.





