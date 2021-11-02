---
layout: post
title: "타일 채우기 풀이"
date: 2021-11-03 02:11:26 +0900
categories: algorithm
---

[타일 채우기](https://www.acmicpc.net/problem/2133)
문제에 대한 풀이를 몇 개 찾아보니 제가 푼 방식과 조금 달랐습니다.
제 방식이 누군가에게는 좀 더 쉬울 수도 있다고 생각하여 풀이를 남깁니다.

## 상태

`n` 에서 타일을 3칸 모두 채우면 `n+1` 에 6가지 상태가 발생할 수 있습니다.

![타일채우기](/img/tri-tiling-solution/tri-tiling-solution-state-1.svg)

같은 모양의 상태를 합쳐서 좀 더 단순화 해봅니다. 4가지 상태로 정리됩니다.

![타일채우기](/img/tri-tiling-solution/tri-tiling-solution-state-2.svg)

## 점화식

N 이 증가함에 따라 각 상태별 경우의 수 변화는 다음과 같습니다.
A 는 공백이고 B 는 2가지 상태가 있기 때문에
A 에서 B 로 변할 때는 경우의 수가 2배가 됩니다.

![타일채우기](/img/tri-tiling-solution/tri-tiling-solution-diagram.svg)

위 도식을 파이썬 코드로 나타내면 아래와 같습니다.

{% highlight python %}
# n 번째 경우의 수 (A,B,C,D=0,1,2,3)
C[n][0] = C[n-1][1] + C[n-1][3]
C[n][1] = C[n-1][0] * 2 + C[n-1][2]
C[n][2] = C[n-1][1]
C[n][3] = C[n-1][0]
{% endhighlight %}

홀수 과정을 제거하면 코드가 더욱 간단해집니다.
{% highlight python %}
a, c = a * 3 + c, a * 2 + c
{% endhighlight %}