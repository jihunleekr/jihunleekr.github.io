---
layout: post
title: "default 값 넣는 용도로 논리 OR 연산자를 사용하면 안되는 이유"
date: 2022-04-09 17:31:00 +0900
categories: javascript
---

## 사용하면 안되는 상황
`borderRadius` 를 이용해서 박스를 그리려는 상황입니다.
사용자가 설정한 값이 있다면 `userBorderRadius` 에 할당되어 있는 상황입니다.

{% highlight javascript %}
// 실제 코드
let borderRadius = userBorderRadius || 4;
{% endhighlight %}

{% highlight javascript %}
// 위 코드의 동작을 설명하는 코드
let borderRadius = Boolean(userBorderRadius) ? userBorderRadius : 4;
{% endhighlight %}

`||` 연산자는 `userBorderRadius` 가 `0` 이어도 (각진걸 좋아하는 사용자겠죠)
`borderRadius` 에 `4` 를 할당하게 되어 버그가 발생합니다.

## 개선
해결방안은 널병합 연산자(`??`) 를 사용하는 것입니다. 널병합 연산자가 생긴 이유를 찾아보지는 않았지만 
아마도 `||` 을 default 값 넣는 용도로 사용하는 과정에서 버그가 많이 발생되어 만들어진 것 같네요.

{% highlight javascript %}
// 실제 코드
let borderRadius = userBorderRadius ?? 4;
{% endhighlight %}

{% highlight javascript %}
// 위 코드의 동작을 설명하는 코드
let borderRadius = (userBorderRadius === undefined || userBorderRadius === null) ? userBorderRadius : 4;
{% endhighlight %}