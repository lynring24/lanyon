---
layout: post
title: table to outfile 
categories: data
tags: [database, sql]
---

There was a need to move a whole bunch of data from a table into other pc and I decided to make a outfile. 
```
SELECT * FROM  web 
INTO OUTFILE  YOUR_OUT_DATA_DIRECTORY
CHARACTER SET utf8
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
ESCAPED BY '\\'
LINES TERMINATED BY '\n';
```
While following other documents, there was an error message about
**MySQL secure-file-priv**. This is an option that manages input and output of data file
On cmd prompt, you could find out where that secure-file-priv option is written and the value.
The value will be a path that allows the i/o of file. Try using that path as an outfile path. 
