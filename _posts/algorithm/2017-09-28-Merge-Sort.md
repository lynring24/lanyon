---
layout: post
title: Merge Sort
categories: Algorithm
tags: [algorithm, sort]
---
Merge Sort는 길이 n의 정렬된 (정수) 배열을 Divide & Conquer 방식으로 정렬한다.<br>
 Time Complexity : θ(n^2)

{% highlight java %}
public void mergeSort(int[] numbers,int low, int high) {
		if(low<high){
			int mid=Math.floorDiv(low+high,2);
			mergeSort(numbers,low,mid); // Divide
			mergeSort(numbers,mid+1,high); // Divide
			merge(numbers,low,mid,high); // Combine(Conquer)
		}
	}

public void merge(int[] numbers,int low, int mid, int high){
		int leftIndex=low;
		int rightIndex=mid+1;
		int tempIndex=0;
		int [] tempArray = new int [numbers.length];

		while(leftIndex<=mid && rightIndex<=high){
			if(numbers[leftIndex]<numbers[rightIndex])
				tempArray[tempIndex++]=numbers[leftIndex++];
			else
				tempArray[tempIndex++]=numbers[rightIndex++];
		}
		if(leftIndex>mid){
			while(rightIndex<=high)
				tempArray[tempIndex++]=numbers[rightIndex++];
		}
		else{
			while(leftIndex<=mid)
				tempArray[tempIndex++]=numbers[leftIndex++];
		}

		for(tempIndex=0; low<=high;tempIndex++)
			numbers[low++]=tempArray[tempIndex];

	}
{% endhighlight %}

### MergeSort Time Complexity

Key instruction으로 time complexity을 찾든 전체 instruction을 다 고려하든 사실 차이가 없다.
key instruction 인덱스의 값들(두 개씩)의 비교다.
Divide 할 떄는 따로 비교가 없지만 Combine을 할때는 비교를 한다.
f(n)= Divide하고 Combine을 하는 데 든 비용이라고 가정하면,
전체 Time Complexity인 T(n)은
T(n)=2*T(n/2)+f(n) 이다. (T(1)은 상수)
Best case 와 worst case는 f(n) 중 while( leftIndex<=mid && rightIndex<=high)에 따라 결정된다.

+ Best case<br>
	 왼쪽이든 오른쪽이든 한쪽만 옮기면 되는 경우<br>
	비교 : n/2
+ Worst case<br>
	왼쪽 오른쪽을 모두 비교해야하는 경우 <br>
	비교 : n

따라서 T(n)=2*T(n/2)+ c*n //c는 상수
<pre>
<code>
let n=2^k,
	T(n)= 2*T(n/2)+ c*n
		  = 2*(2*T(n/2^2)+ c*n/2)+ c*n
			= 2*(2*(2*T(n/2^3)+ c*n/2^2)+ c*n/2)+ c*n
			= (2^k) * T( n/(2^k) ) + c*n*k
			= n*T(1)+ n*c*(log2(n))
		--> θ(n*log2(n))
</code>
</pre>
