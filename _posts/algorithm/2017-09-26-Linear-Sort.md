---
layout: post
title: Linear Sort
categories: Algorithm
---
Linear Sort는 길이 n의 배열을 원소 2개씩 비교해서 정렬한다.
+ Iime Complexity : θ(n^2)
+ Average Time Complexity = 존재하지 않을 경우 + 존재하는 데 중반 쯤에서 발견되는 경우  = n*(1/2) + n*(1/2) * (1/2) = (3/4)n

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
