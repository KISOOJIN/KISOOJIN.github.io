---
title: "parseInt vs Math.floor"

categories: [TIL]
comments: true

toc: true
toc_sticky: true

date: 2022-10-09
---

> ## parseInt() vs Math.floor()

<br/>

백준 문제를 풀다가 parseInt를 사용했는데 런타임오류로 Math.floor()를 대신 사용해서 해결할 수 있었고 parseInt()와 Math.floor()의 차이점을 알고 싶어서 구글링하다가 관련된 블로그를 확인하여 궁금증을 풀 수 있었다.
밑에 블로그에서 소개하는 사이트에서 직접 어떤 메소드가 더 빠른지 눈으로 확인할 수 있어서 더욱 도움이 되었다!😊

<br/>

JavaScript로 positive decimal number를 내림할 때 Math.floor랑 parseInt 를 사용할 수 있는데, `Math.floor`가 parseInt보다 빠르다.

그리고 Math.floor 보다 `~~ 라는 연산자`를 사용하면 더 빠르다.
<br/>

> 참고로 ~ tilde 연산자는 Bitwise NOT 이라는 자바스크립트 연산자이고 두개 연달아서 붙여 양수 앞에서 사용하면, Math.floor와 동일한 효과가 있다.
> ~연산자를 음수 앞에 사용하면 -(n+1)의 값으로 변환된다.

<br/>

```javascript
~~2.2 === 2; // true
~~3.5 === 3; // true
~~4.6 === 4; // true
```

<br/>

```javascript
~1 === 0; // true
~2 === -3; // true
~3 === -4; // true
```

<br/>

[참고한 블로그 및 사이트](https://developer-alle.tistory.com/393)
