---
layout: post
title: 10. Feature Extration
categories: TIL
---

Image Segmentationd을 통해서 물체를 배경으로부터 분리하여 인식하고 boundary를 얻었다. Feature extration을 통해서는 물체의 특징점을 찾는다. 
1. 물체의 boundary를 찾았다면 하나의 물체라고 인식
2. 그 물체(혹은 boundary)로 부터 어떤 특징점을 얻는가
3. 물체를 boundary가 아닌 영역으로 추출했을 때 어떤 특징들이 있는지

## Feature Extraction 
Feature Extraction은 물체를 찾는 detection와 물체에 대해 설명을 하는 description으로 나뉜다. <br>
예를 들어 물체의 모서리(corner)라는 특징을 사용해서 삼각형과 사각형을 설명한다면, 삼각형은 모서리가 3개인 도형이고 사각형은 모서리가 4개인 도형이라 설명 할 수 있다. 

## BOUNDARY FOLLOWING  
물체의 둘레를 따라 경계를 탐색하는 방법이다. <br>

### 컴퓨터에게 원을 설명하기 위한 알고리즘 

1. 시작점은 전체 이미지의 가장 왼쪽 가장 상위에 있는 점 
2. 이미지(b)를 기준으로 c에서 시작해서 8 방면에 있는 점들을 시계방향(오른쪽)을 탐색 
3. 가장 먼저 만난 값이 1인 점을 edge라 가정을 하고 b로 마킹, c는 b 하나 전 점으로 마킹 
4. b가 b0일때, 다시 말해 수렴할 때까지 2, 3을 반복한다. 
 
> c =  물체 || 배경, b = edge 
> edge를 찾을 때 하나의 segment라고 인지한다.

{% highlight java %}
do  {
    for ( n : = c to n[7]  ) {
          if ( n[i] == 1) {
                b_new = n [i];
                c = n [i-1];
                break;
          }
    }
} while ( b != b0 );
{% endhighlight %}

## SIGNATURE 
2차인 영상을 1차로 변환한다.
좌표 = 중심으로부터 거리를 계산 가능하다.
원 : 원 = 거리가 일정 
사각형은  = 중심으로부터 거리가 반복적이다.  range = [r : root(2)*r]
각 좌표와 중점의 거리 차를 구해서 좌표대신 할당한다.

영상 물체의 edge가 구불구불해도 1차 좌표축에 표현이 가능하다. 


## BOUDNARY FEATURE DESCRIPTORS 
바운더리들의 특징을 어떻게 묘사하는가 
```
diameter 직경 : max of distance btwn pi, pj
계산을 다 해봐서 가장 두 점의 차가 큰 경우 
길이 m   = major axis 가장 거리가 긴 좌표축 
 tan (0) = y/x
(0) = (tan-1) = y/x
minor axis major에 직교하는 경우 

statistic moments 
nth modment of z : n제곱시의 표준 편차 같은 느낌 
```

## REGION FEATURE DECRIPTORS : 영역 찾기 
```
p = 둘레길이 
compactness = p^2 / a
```
면적이 같을 때, 주변 둘레가 더 클면 클수록 compact하다고 한다. 가령, 같은 크기의 오렌지와 포도를 경우,  boundary가 더 컴팩트한 물체를 오렌지라고 할 수 있다.  

```
circularity  : 4* PI* A  / p^2얼마나 더 각진지 
A= r^2 * pi
4* PI* A  / p^2 
if  p = 2*pi* r:
 4 * pi*pi*r ^2 / (2*pi*r)^2 == 1
```
> **원**일 때는 circularity = 1   
> **사각형**이라면 circularity =  4*pi*1/16 < 1   
> **삼각형**이라면  circularity = (root(3) /4 )* 4* pi / 9  > 1   
> 1에 가까울 수록 원이 된다.   

```
lim 1 = circle
effective diameter : 면의 지름 근삿값
eccentricity : 타원 
maximum distance ( axis 와 관련된 ) 를 찾고, a의 axis를 둔다. 

Texture  : frequency ( 머리카락, 나뭇잎)
p : histogram을 합 1로 argmax 

relative intensity = 평균에서의 분포 
```
variance가 클수록 r(z)가 커지고, 작을 수록 r(z)가 0에 가까워진다. 강약이 있을수록 이미지에 앙약이 생긴다.

```
Standard deviation : 평균에서 얼마나 차이가 나는 가
R(normalized) : smooth 0에 가까움 
third moment : 식에 p = 3 대입 -> 평균 대비 밝은지 어두운지
uniformity : smooth할 수록 값이 크다 .
반대로 entropy : 값들끼리 대비가 클수록 값이 크다.
```
