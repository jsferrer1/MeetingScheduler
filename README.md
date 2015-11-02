# Meeting Scheduler

## Table of Contents

* Introduction
* Pre-Requisites
* Running the Program


## Introduction

This application is a solution to the hard task of arranging a meeting to invite many people in different time zones with different work schedules. It uses Java & GSON to simplify the processing of hash tables.


## Pre-Requisites

  - JDK 1.7
  - gson-2.4.jar (included on the MeetingScheduler.jar)
  - commons-lang3-3.4.jar (included on the MeetingScheduler.jar)

## Running the Program

  1. Clone the `MeetingScheduler` repository or simply save the zip file to your local folder.
  
     ```
	 $ git clone https://github.com/jsferrer1/MeetingScheduler.git
     $ cd MeetingScheduler
     ```

  2. Edit the `config.properties` file to include the input parameters  
     
     ```
     attendees=John,Joshua,Jericho,James
     meetingLength=60
     possibleSlots=5
     startTimeFrame=2015-10-26 08:00am
     endTimeFrame=2015-10-26 5:00pm
     ```
     
     **Where**  
     attendees : list of attendees  
     meetingLength : meeting length (in minutes)  
     possibleSlots : Number of possible time-slots that should be found by program  
     startTimeFrame : Start of the timeframe  
     endTimeFrame : End of timeframe
     

  3. Edit the `schedules.json` file to include the details of the participants including their name, timezone, work hour, and meetings.  

	 ```
	 {"schedules":
	 [{	"id": "1",
	 	"name": "John",
	 	"timezone": "UTC",
	 	"workhours": "9am to 5pm",
	 	"meetings": [
	    { 
	 		"date": "2015-10-26",
	 		"starttime": "09:00am",
	 		"endtime": "10:00am"
	 	}]
	 }]}
	 ```
     
     **Where**  
     meetings : time-slots booked or scheduled meetings
     
     Note: It is assumed that `meetings` are already pre-converted to UTC timezone.  
     
     
  4. Run the java application  
  
     ```
     $ java -jar MeetingScheduler.jar
     ``` 
    
  5. Output should either show the available timeslots or possible timeslots with maximum attendees. Note that the application will skip the lunch hours from 12:00pm to 1:00pm.

	 Output with available timeslots:
  
     ```
     - - - - - OUTPUT - - - - -
	 Total Timeslot(s) Available: 2
	 ==> 2015-10-26 11:00AM to 12:00PM
	 ==> 2015-10-26 01:00PM to 2:00PM  
     ```

	 Output with no available timeslots, but with possible options. 
    
	 ```
	 - - - - - OUTPUT - - - - -
	 It's not possible to arrange a meeting with everyone in the selected timeframe.

	 However, there are timeslot(s) where maximum number of attendees are able to attend:: 3
	 ==> 3 participants(s) are able to attend on 2015-10-26 09:00AM to 10:00AM; Available: Joshua,Jericho,James; Unavailable: John.
	 ==> 3 participants(s) are able to attend on 2015-10-26 10:00AM to 11:00AM; Available: Joshua,Jericho,James; Unavailable: John.
	 ==> 3 participants(s) are able to attend on 2015-10-26 11:00AM to 12:00PM; Available: Joshua,Jericho,James; Unavailable: John.
	 ```

## Known Issue
    - If startTimeframe is 8:30am and meetingLength is 60minutes, some timeslots will not show on the lists of available timeslots. Workaround is to make the meetingLength more granular - that is, set the meetingLength to 30 minutes. 

     