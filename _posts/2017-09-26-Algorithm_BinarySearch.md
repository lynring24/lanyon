---
layout: post
title: Binary Search(iteration/recursion)
categories: Algorithm
---
Binary Search는 길이 n의 정렬된 (정수) 배열 중에서 key의 인덱스 위치를 알려준다.
+ sorted array
+ wost case = O( log(n) )
+ best case = Ω( 1 )

### iteration을 사용한 binary Search
{% highlight java %}
public int binarySearch(int [] numbers, int low, int high, int key){
		while(low<high){
			int mid= Math.floorDiv(low+high,2);
			if(numbers[mid]==key)
				return mid;
			else if(key<numbers[mid])
				high=mid-1;
			else
				low=mid+1;
		}
		return -1;
	}
{% endhighlight %}

### recursion을 사용한 binary Search
{% highlight java %}
public int search(int [] numbers, int low, int high, int key){
		if(low>=high) return -1;
		else{
			int mid = Math.floorDiv(low+high,2);
			if(numbers[mid]==key)
				return mid;
			else if(key<numbers[mid])
				return search(numbers,low, mid-1,key);
			else
				return search(numbers,mid+1,high, key);
		}
	}
{% endhighlight %}
