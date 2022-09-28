---
title: "React intro - 1 "

categories: [React]
comments: true

toc: true
toc_sticky: true

date: 2022-09-28
---

> ## React는 무엇인가?

React는 웹 프레임워크로, 자바스크립트 라이브러리의 하나로서 사용자 인터페이스를 만들기 위해 사용된다.

**리액트의 3가지 특징**

- 선언형(Declarative)
- 컴포넌트 기반(Component-Based)
- 범용성(Learn Once, Write Anywhere)

> 선언형

리액트는 한 페이지를 보여주기 위해 HTML/CSS/JS로 나눠서 적는 것보다 하나의 파일에 명시적으로 작성할 수 있게 JSX를 활용한 선언형 프로그래밍을 지향한다.

> 컴포넌트 기반

- 리액트는 하나의 기능 구현을 위해 여러 종류의 코드를 묶어둔 컴포넌트를 기반으로 개발한다. 컴포넌트로 분리하면서 서로 독립적이고 재사용이 가능하므로, 기능 자체에 집중하여 개발할 수 있다.
- 컴포넌트를 먼저 완성시키고, 레이아웃에 따라 유동적으로 컴포넌트의 위치를 변경할 수 있는 상향식 개발(Bottom-up)방식에 적합하다.
- 리액트 컴포넌트는 클래스형 컴포넌트와 함수형 컴포넌트 두 종류가 있다. 기존에는 클래스형 컴포넌트를 주로 사용했었지만, 최근에는 함수형 컴포넌트를 많이 사용한다.
- 모든 컴포넌트 위에는 최상위 컴포넌트가 존재한다.

> 범용성

리액트는 JavaScript 프로젝트 어디에든 유연하게 적용될 수 있다.
meta에서 관리되어 안정적이고, 가장 유명하며, 리액트 네이티브로 모바일 개발도 가능하다.

<br/>

**`map 메서드`를 이용한 반복**

React에서 여러 데이터를 렌더링 할 때 map 메서드를 이용한다.
왜 map 메서드를 이용하는 것일까?

킴코딩이 블로그 개발을 한다고 할 때를 예시로 들어보자!

```JSX

const posts = [
 { id: 1, title: "Hello World", content: "Welcome to learning React!" },
 { id: 2, title: "Installation", content: "You can install React via npm." },
];

function Blog() {
 return (
   <div>
     <div>
       <h3>{posts[0].title}</h3>
       <p>{posts[0].content}</p>
     </div>
     <div>
       <h3>{posts[1].title}</h3>
       <p>{posts[1].content}</p>
     </div>
   </div>
 );
}

```

> 블로그 포스트가 2개일 경우에는 모든 데이터를 직접 작성(하드코딩)으로 가능하다.
> 하지만, 블로그 포스트가 100개인 경우를 상상해보면 김코딩은 포스팅이 늘어날 때마다 매일 코드를 변경해야한다. 매우 비효율적인 방식이라고 말할 수 있겠다.
> 그리고 이러한 비효율적인 방식을 해결하기 위해 배열 메서드인 `map`을 활용하는 것이다.

<br/>

```JSX

function Blog() {
  const postToElement = (post) => (
    <div key ={post.id}>
      <h3>{post.title}</h3>
      <p>{post.content}</p>
    </div>
  );

  const blogs = posts.map(postToElement);

  return <div className="post-wrapper">{blogs}</div>;
}


```

<br/>

**key 속성**

React에서 map 메서드 사용 시, key 속성을 넣지 않으면 아래와 같이 리스트의 각 항목에 key를 넣어야 한다는 경고가 표시된다. key 속성의 위치는 map 메서드 내부에 있는 엘리먼트 즉, `첫 엘리먼트`에 넣어주어야 한다.

![스크린샷 2022-09-28 22-35-56](https://user-images.githubusercontent.com/111376707/192793083-6e44b57a-7e5d-4f02-8709-8cb7ae3c4a2f.png)

> key 속성값이 반드시 id가 되어야 하는가? id가 존재하지 않는다면 어떻게 해야하는가?

key 속성값은 가능하면 데이터에서 제공하는 id를 할당해야 한다. key 속성값은 id와 마찬가지로 변하지 않고, 예상 가능하며, 유일해야 하기 때문이다. 정 고유한 id가 없는 경우에만 배열 인덱스를 넣어서 해결할 수 있습니다. 배열 인덱스는 최후의 수단(as a last resort)으로만 사용합니다.
Math.random()등으로 무작위로 생성된 값을 key로 지정하게 되면, 컴포넌트 인스턴스와 DOM노드를 불필요하게 재생성하여 성능이 나빨질 수 있다.
