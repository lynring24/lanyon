---
layout: post
title: Linear Sort
categories: Algorithm
---
Linear Sort는 길이 n의 배열을 원소 2개씩 비교해서 정렬한다.
+ Iime Complexity : θ(n^2)

{% highlight java %}
public void LinearSort(int[] numbers) {
		for(int i=0; i <numbers.length-1;i++){
			for(int j=i+1;j<numbers.length;j++){
				if(numbers[i]>numbers[j]){
					int temp = numbers[i];
					numbers[i]=numbers[j];
					numbers[j]=temp;
				}
			}
		}
	}

{% endhighlight %}
