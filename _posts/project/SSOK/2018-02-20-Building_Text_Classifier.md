---
layout: post
title: Introduction of graduation project(SSOK)
categories: project
--- 
<pre>
I've finally finished a graduation project with 2 team-mates. 
Since some articles from university web page were messed up, we decide to build an android application which categories and recommends articles to the users. 
We scrapped the articles from the main bulletin board and boards from each department(Physics, Law etc). 
We also used the message(mobile) we've received.
</pre>

## What we've done
### Classification 
1.Naive Baysian 
<table>
<tr><td>data</td><td>3,xxx</td></tr>
<tr><td>input</td><td>Title of the articles </td></tr>
<tr><td>output</td><td>['공지', '취업] </td></tr>
<tr><td>accuracy</td><td>0.9x</td></tr>
</table>

2.MLP with keras
<table>
<tr><td>data</td><td> 2x,xxx</td></tr>
<tr><td>input </td><td>Title of the articles </td></tr>
<tr><td>output</td><td>['공지', '학사', '학생'.. ] in 8 categories</td></tr>
<tr><td>accuracy </td><td> 0.9 , 0.85</td></tr>
</table>

3.Message Classfication 
<pre>
Messages that students received from university were sent by the phone numbers of department.
The problem was that most of the departments use more than one numbers. To use the numbers for classification, normalization between department and phone numbers had to be done first. After that, match the recieved message's number with the list of department numbers. 
</pre>

### Recommendation
1. content based recommendation
2. coordination based recommendation
3. word recommendation working with word2vec

