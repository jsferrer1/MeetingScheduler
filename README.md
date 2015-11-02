# Meeting Scheduler

## Table of Contents

* Introduction
* Pre-Requisites
* Running the Program


## Introduction

This application is a solution to the hard task of arranging a meeting to invite many people in different time zones with different work schedules. It uses Java & GSON to simplify the processing of hash tables.


## Pre-Requisites

  - JDK 1.7
  - gson-2.4.jar
  - commons-lang3-3.4.jar

## Running the Program

  1. Clone the `MeetingScheduler` repository or simply save the zip file to your local folder.
  
     ```
	 $ git clone <> MeetingScheduler
     $ cd MeetingScheduler
     ```

  2. Edit the `config.properties` file to include the input parameters  
     
     ```
     attendees=John,Joshua,Jericho,James
     meetingLength=60
     possibleSlots=3
     ```
     
     **Where**  
     attendees : list of attendees  
     meetingLength : meeting length (in minutes)  
     possibleSlots : Number of possible time-slots that should be found by program  

  3. Edit the `schedules.json` file to include the details of the participants including their name, timezone, work hour, and meetings.  

	 ```
	 {"schedules":
	 [{	"id": "1",
	 	"name": "John",
	 	"timezone": "PHT",
	 	"workhours": "9am to 5pm",
	 	"meetings": [
	    { 
	 		"date": "2015-10-26",
	 		"starttime": "09:00am",
	 		"endtime": "10:00am"
	 	}]
	 }]}
	 ```
     
  4. Run the java application  
  
     ```
     $ java -jar MeetingScheduler.jar
     ``` 
    
  5. Output should either show the available timeslots or possible timeslots with maximum attendees.

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