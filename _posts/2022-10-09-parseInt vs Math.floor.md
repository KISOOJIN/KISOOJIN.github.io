---
title: "parseInt vs Math.floor"

categories: [TIL]
comments: true

toc: true
toc_sticky: true

date: 2022-10-09
---

> ## parseInt() vs Math.floor()

<br>

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

**참고** [https://developer-alle.tistory.com/393]
