---
layout: post
title: common mistakes
categories: TIL
---
1. fatal error : --unallowed tracking histories
> git pull oring branck --allowed-unrelated-histories

2. accidently pushed wrong commit
> git push origin +branchname

3. there can't be cast between two arrayList, unless use <? extends superType>

4. kotlin의 static은 Companion으로 처리하는데 자바에서 부르기 위해서 @JvmStatic()를 해줘야하고, 자바에서는 [파일이름].Companion.으로 접근해야 한다.

5. 파이썬에는 iter 가능한 element 중 가장 큰 N개를 뽑아주는 멋진 기능이 있다.
<code>
import random, heapq, string

cnt = 10
arr = []

while cnt > 0:
    element = [ random.choice(string.ascii_letters), random.uniform(0.0, 1.0)]
    arr.append(element)
    cnt -= 1

max_arr = []
N = 5
def get_max_N():
    for element in arr:
        print(element[0], element[1])
    print(heapq.nlargest(N, arr, lambda  s: s[1]))
</code>
<<<<<<< HEAD:_posts/etc/2018-02-27-git-logs.md
=======

<!-- Bootstrap -->
    <link href="../css/bootstrap.min.css" rel="stylesheet" media="screen">


<script src="http://code.jquery.com/jquery.js"></script>
    <script src="../js/bootstrap.min.js"></script>

1. ORA-00911: 문자가 부적합합니다
{% highlight jsp %}
String sql = "{}**;**"
{% endhighlight jsp %}
jsp에서 sql문 문자열에 ;가 들어가면 에러가 발생

2. purge recyclebin;
>>>>>>> 2281a30219515ce7cbd97da7117041fc7aea97ec:_posts/TIL/2018-02-27-error-logs.md
