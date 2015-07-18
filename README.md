Conference Central
This is Project 4 - Conference Central
Version : 1.0.0
Author : Timothee Hack
==================================================================

This is project 4,  Conference Central, of the Udacity Fullstack nanodegree.
This project is deployed on Google App Engine at the following address : 
https://aelo-p4-confcentral.appspot.com/#/


TASK 1 :
---------------------
Design Choices :

I decided to implement a Speaker object, instead of just using a string for the speaker's name. The reasons for this are primarily :
1) A name is not suitable key to use for a speaker, it's possible there could be 2 speakers with the same name using the application. I chose to use the main email as a key instead, as that is certain to be unique.
2) There are several fields that would be interesting to keep related to a speaker, such as their title, biography, picture, etc. A speaker object is necessary for adding these fields, as well as fields we want to include in future improvements.

The functions for the retrieving sessions, sessions by speaker, sessions by type and speakers were designed to function without authentification. This it to allow user's who are not logged in to still be able to browse the list of conferences and sessions.
For creating a speaker or a session however, the user is required to be logged in.



TASK 3 :
---------------------

Query 1 (GetShortSessions) :
Returns a list of sessions belonging to conferences that the user is registered to, and that have a duration of an hour or less. This could be useful to offer as suggestions for quick sessions to join attend at the last minute.

Query 2 (_getUsersForConference) :
Returns a list of all the user profiles of the users attending a conference. This could be useful for the conference organizers to see the full list of attendees, and for the users to see who else is attending that they know.

Query Problem :
To get the sessions that are not workshops is easy. Simply need to query Session where typeOfSession != "Workshop". The problem lies with eliminating the ones that go past 7pm since we only have the start time as field, not the end time. We do have the duration, but that is not sufficient since it would require adding the duration to the start time in the query, which does not work with datastore's method of indexing data. 
The solution would be to add an endtime field to the Session object. Then we could query the Sessions that are not workshops and that starttime < 7pm and endtime is < 7pm.
