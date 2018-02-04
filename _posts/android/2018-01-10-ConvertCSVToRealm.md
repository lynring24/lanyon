---
layout: post
title: Import Excel data to Realm
categories: Android
---
For a project, I had to import excel data to Realm. Sure there were some examples and works done in excel to SQLite, but our team was using Realm for android database so I had to struggle to find a way for making a excel data to Realm. <dir>
<dir>
By searching few days I've found out that Realm is not that friendly with importing and exporting data in other forms than .realm itself. There were CoCoa-Converter for Swift and Objective-C but there were no offical converter yet<dir>
To Approach from excel to realm:
+ excel file to JSON, JSON to Realm (There are some APIs and libraries)
+ Dynamic Realm (The document said this will be used in .csv or .txt but I could rarely find the data)
+ excel to .csv , read csv line one by one and insert them
<dir>
The last option is what I've used. In my case the data was a 1K lines and column was no more than 3, so it was not a big expense to read the line one by one. <dir>
CSV file distributes data by ','.
+ Add Assert folder to main
+ convert excel file to csv file (if need, encode in UTF-8 before)
+ add the csv file to Assert folder
+ call getAssert.openfile(csvfile) to open a csvfile and InputStreamReader()/BufferedReader()
+ read line one by one and split by ','
+ Create Realm object and setData for own Object


Then the rest of the process is same with Realm insertion everyone knows.
