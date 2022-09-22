---
title: "extends 키워드와 super키워드"

categories: [TIL]
comments: true

toc: true
toc_sticky: true

date: 2022-09-22
---

> ## extends

<br/>

- extends 키워드는 클래스를 다른 클래스의 자식으로 만들기 위해 class 선언 또는 class 식에 사용된다.

  <br/>

```javascript

class ChildClass extends ParentClass{...}
```

<br/>

> ## super

<br/>

- super 키워드는 부모 객체의 함수를 호출할 때 사용된다.
- super 키워드는 생성자 함수 내에서 한번만 사용될 수 있다.
- this 키워드가 사용되기 전에 호출되어야 한다. 전에 호출이 되면 참조오류가 발생한다.

<br/>

```javascript
class Student extends Human {
  // extends 키워드를 사용하여 Human(부모클래스)의 속성과 메소드를 Student(자식클래스)에 상속
  constructor(name, age, major) {
    super(name, age); // super 키워드를 사용하여 부모객체의 함수를 호출
    this.major = major;
  }

  study() {
    console.log(`${this.major}를 공부하였습니다.`);
  }
}
```

<br/>

**참조**

[mdn - super](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/super)

[mdn - extends](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes/extends)
