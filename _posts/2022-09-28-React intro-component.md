---
title: "React intro - component "

categories: [React]
comments: true

toc: true
toc_sticky: true

date: 2022-09-28
---

> ## 컴포넌트는 무엇인가?

<br/>

하나의 기능 구현을 위한 여러 종류의 코드 묶음, UI를 구성하는 필수 요소

<br/>

```jsx
const Component = () => {
  return (
    <>
      <div>{name}</div>
      <div>{age}</div>
    </>
  );
};
```

<br/>

![스크린샷 2022-09-28 23-00-55](https://user-images.githubusercontent.com/111376707/192799197-2e5cfd3a-126b-4448-acfa-e3ca130e2d12.png)

> 리액트를 이용하면, 각자 독립적인 기능을 가지며 UI의 한 부분을 담당하기도 하는 컴포넌트를 여러 개 만들고 조합하여 애플리케이션을 만들 수 있다.

<br/>

![스크린샷 2022-09-28 23-06-49](https://user-images.githubusercontent.com/111376707/192800643-a53cb8be-6821-4506-b087-6224d9912b3d.png)

> 모든 리액트 애플리케이션은 최소 한 개의 컴포넌트를 가지고 있으며, 이 컴포넌트는 애플리케이션 내부적으로는 근원(root)이 되는 역할을 한다. 이 최상위 컴포넌트는 근원의 역할을 하므로 다른 자식 컴포넌트를 가질 수 있으며, 이 계층적 구조(hierarchy)를 트리 구조로 형상화할 수 있다.
