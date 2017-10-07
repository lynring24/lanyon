---
layout: post
title: Quick Sort
categories: Algorithm
---

Quick Sort는 divide하면서 Merge Sort와는 다르게 combine이 아니라 분류를 하는 방식이다.
partition()은 기준 pivot의 값보다 작으면 왼쪽,크면 오른쪽으로 분류하고<br> pivot의 값이 들어있는 배열의 인덱스를 알려준다. 

<pre>
<code>
public void quickSort(int[] numbers, int low, int high){
  if(low<high){
    int pivot = partition(numbers, low,high);
    quickSort(numbers,low,pivot);
    quickSort(numbers,pivot+1,high);
  }
}
public int partition(int[] numbers, int start, int end){
  int key = numbers[start];

  while(start<end){
    for(;numbers[start]<key;start++);
    for(;numbers[end]>key;end--);
    int temp= numbers[start];
    numbers[start]=numbers[end];
    numbers[end]=temp;
  }
  numbers[start]=key;
  return start;

  </code>
  </pre>
{% endhighlight %}
