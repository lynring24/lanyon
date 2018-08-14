---
layout: post
title: Introduction of graduation project(SSOK)
categories: project
--- 

I've finally finished a graduation project with 2 team-mates.
Since some articles from university web page were messed up, we decide to build an android application which categories and recommends articles to the users. 
We scrapped the articles from the main bulletin board and boards from each department(Physics, Law etc). 
We also used the message(mobile) we've received.
### What we've done
Classification 
1. Naive Baysian 
---
data : 3,xxx
input : Title of the articles 
output :  ['공지', '취업] 
accuracy : 0.9x
---

2. MLP with keras
---
data : 2x,xxx
input : Title of the articles 
output :  ['공지', '학사', '학생'.. ] in 8 categories
accuracy : 0.9 , 0.85
---

3. Message Classfication 
Messages that students received from university were sent by the phone numbers of department.
The problem was that most of the departments use more than one numbers. To use the numbers for classification, normalization between department and phone numbers had to be done first. After that, match the recieved message's number with the list of department numbers. 

Recommendation
1. content based recommendation
2. coordination based recommendation
3. word recommendation working with word2vec

