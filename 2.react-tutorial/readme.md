# 들어가기 전에
- 이 포스팅은 https://reactjs.org/tutorial/tutorial.html 에 있는 포스팅을 번역한 것입니다. 오역이나 의역이 있을 수 있습니다. 지적해주시면 확인 후 바로 정정하겠습니다.

- original source of this posting is from https://reactjs.org/tutorial/tutorial.html If the original author requests deletion, it will be deleted immediately.

- Translated by Jake Seo (서진규)

	- https://velog.io/@jakeseo_me
	- https://github.com/n00nietzsche
    
> 리액트 튜토리얼 공식문서 (번역)

# 튜토리얼을 시작하기 전에

이 튜토리얼을 진행하며 우리는 작은 게임을 만들어볼 것입니다. 게임을 만든다는 것이 별로 흥미롭게 느껴지지 않을 수 있지만 일단 한번 만들어보세요. 튜토리얼 동안 우리가 배우는 기술은 리액트 앱을 만드는데 있어서 매우 근본적인 기술입니다. 완벽히 이해하고 마스터한다면 리액트에 대한 깊은 이해가 생길 것입니다.

> 이 튜토리얼은 무언가 하면서 배우는 사람들을 위해 디자인되었습니다. 맨땅에서 개념부터 배우고 싶으신 분들은 [step-by-step 가이드](https://reactjs.org/docs/hello-world.html) 를 참고해주세요. 이 튜토리얼과 가이드는 상호보완적이라는 것을 알게 될 것입니다.

이 튜토리얼은 몇가지 섹션으로 나누어져있습니다.

- `튜토리얼을 위한 세팅` 에서는 튜토리얼을 따라가기 위한 시작점을 제공할 것입니다.
- `개요` 에서는 리액트 핵심 요소들 : components, props, state 에 대해 알려줄 겁니다.
- `게임 완성하기` 에서는 리액트 개발에서 쓰이는 일반적인 테크닉에 대해 알려줄 겁니다.
- `시간여행 추가하기` 에서는 리액트의 특별한 힘에 대한 더 깊은 이해를 줄 것입니다.

이 튜토리얼에 있는 모든 가치를 끌어내기 위해 모든 섹션을 한번에 완성할 필요는 없습니다. 1~2 섹션이라도 괜찮으니 할 수 있는 만큼 하세요.

## 우리는 무엇을 만드나요?

이 튜토리얼에서, 우리는 리액트를 이용하여 인터렉티브한 틱택토 게임을 만들 것입니다.

여기서 우리가 만들 [최종 결과물](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)을 확인할 수 있습니다. 코드가 잘 이해되지 않거나 익숙하지 않은 문법이 나왔더라도 걱정하지 마세요! 이 튜토리얼의 목표는 그것들을 알려주는 것이니까요.

이 튜토리얼을 계속하기 전에 틱택토 게임이 어떤 것인지 확인하는 것을 추천합니다. 게임을 유심히 보면 오른쪽에 숫자로된 리스트가 있다는 것을 눈치챘을 것입니다. 그 리스트는 게임에서 움직였던 모든 기록을 갖고 있습니다. 그리고 게임이 진행되며 업데이트됩니다.

틱택토 게임이 뭔지 대충 알았다면 끄셔도 좋습니다. 이 튜토리얼에서는 우리는 더 간단한 템플릿부터 시작할 것입니다. 다음 단계는 게임을 만들기 위한 셋팅입니다.

## 튜토리얼에 필요한 선수지식

일단 HTML과 자바스크립트에 대해서는 어느정도 안다고 생각하고 진행할 것이지만 다른 언어를 하다가 왔다고 해서 튜토리얼을 진행할 수 없는 것은 아닙니다. 또 함수, 오브젝트, 배열 그리고 클래스와 같은 개념에 대해서도 어느정도 친숙하다고 가정할 것입니다.

자바스크립트를 다시 봐야할 것 같다면 [이 가이드](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)를 추천드립니다. 또 최신 자바스크립트 버전인 ES6에서 사용되는 개념들을 다룰 것이라는 걸 알아두세요. 이 튜토리얼에서 우리는 [화살표 함수](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions), [클래스](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes), [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let), [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)를 사용할 것입니다. [Babel REPL](https://babeljs.io/repl/#?presets=react&code_lz=MYewdgzgLgBApgGzgWzmWBeGAeAFgRgD4AJRBEAGhgHcQAnBAEwEJsB6AwgbgChRJY_KAEMAlmDh0YWRiGABXVOgB0AczhQAokiVQAQgE8AkowAUAcjogQUcwEpeAJTjDgUACIB5ALLK6aRklTRBQ0KCohMQk6Bx4gA)을 이용하여 ES6코드가 어떻게 컴파일되는지 확인할 수 있습니다.

# 튜토리얼 세팅하기

이 튜토리얼을 무사히 마치기 위해선 2가지 방법이 있습니다 : 브라우저에 코드를 작성할 수도 있고, 컴퓨터에 로컬 개발 환경을 구축할 수도 있습니다.

## 옵션 1 : 브라우저에 코딩하기

튜토리얼을 시작하기 위한 가장 빠른 방법입니다!

먼저 [스타터 코드](https://codepen.io/gaearon/pen/oWWQNa?editors=0010) 창을 새 탭에 띄우고, 새 탭이 빈 코드 창을 띄우게 하세요. 이 튜토리얼에서 우리는 리액트 코드를 편집할 것입니다.

옵션 1을 선택하셨다면 옵션 2는 스킵하시고 `개요`파트로 가셔도 됩니다.

## 옵션 2 : 로컬 개발 환경

옵션 : 이건 다분히 개인이 선택해야 할 문제입니다. 이번 튜토리얼에선 절대 필수가 아닙니다.

이 세팅은 더 많은 작업을 요구하지만 우리가 에디터를 이용해 모든 튜토리얼을 끝낼 수 있게 만들어줍니다. 다음과 같이 작업하시면 됩니다.

1. 최신 버전의 [노드js](https://nodejs.org/en/)가 설치되었는지 확인해주세요.
2. [Create React App 설치 가이드](https://reactjs.org/docs/create-a-new-react-app.html#create-react-app)를 따르시고 새 프로젝트를 만드세요.

```bash
npx create-react-app my-app
```
3. 새 프로젝트의 `src/` 폴더 내부의 모든 파일을 지워주세요.

> 알아둬야 할 것 :
> src 폴더 전체를 지우지 마세요. 그냥 안에 있는 파일만 지우세요. 안에 있는 소스파일들은 다음 스텝에서 우리가 새로 작성할 예제로 채울 것입니다.

4. `index.css`파일을 `src/` 폴더에 [이 CSS코드](https://codepen.io/gaearon/pen/oWWQNa?editors=0100)로 추가해주세요.
5. `index.js`파일을 `src/` 폴더에 [이 JS코드](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)로 추가해주세요.
6. `src/`폴더에 `index.js` 파일의 맨 위에 이 3줄을 추가해주세요.

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
```

이제 프로젝트 폴더에서 `npm start`를 입력하고 브라우저에서 `http://localhost:3000`으로 접속하면 빈 틱택토 게임을 볼 수 있을 것입니다.

문법 하이라이팅을 위해서 [이 가이드](https://babeljs.io/docs/en/editors/)를 따라하시는 것을 권장합니다.

## 도와주세요! 여기서 막혔어요!

막혔다면 [커뮤니티 서포트 리소스](https://reactjs.org/community/support.html)를 확인하세요. 특히, [Reactiflux Chat](https://discordapp.com/invite/0ZcbPKXt5bZjGY5n)은 즉각적인 도움을 받기에 아주 좋은 곳입니다. 만일 답을 받지 못하거나 계속 막혀있다면 이슈를 올려주세요. 저희가 도와드리겠습니다!

# 개요

이제 세팅이 끝났습니다. 리액트의 개요로 가봅시다!

## 리액트란 무엇인가요?

리액트는 UI를 만들기 위한 선언형이고 효율적이며 유연한 자바스크립트 라이브러리입니다. '컴포넌트'라고 불리는 작고 분리된 코드로부터 우리가 복잡한 UI들을 조립하게 해줄 것입니다. 

리액트는 몇가지 다른 종류의 컴포넌트를 갖고 있습니다. 하지만 우리는 `React.Component` 하위 클래스들부터 다뤄보겠습니다.

```javascript
class ShoppingList extends React.Component {
	render() {
		return (
			<div className="shopping-list">
				<h1>Shopping List for {this.props.name}</h1>
				<ul>
					<li>Instagram</li>
					<li>WhatsApp</li>
					<li>Oculus</li>
				</ul>
			</div>
		)
	}
}
```

우리는 곧 이상한 XML같은 태그를 찾게 될 것입니다. 우리는 우리가 스크린에서 무엇을 보길 원하는지 컴포넌트를 이용해 리액트에게 말합니다. 우리의 데이터가 바뀔 때, 리액트는 효율적으로 우리의 컴포넌트를 업데이트하고 재렌더링합니다.

여기 ShoppingList는 **리액트 컴포넌트 클래스** 또는 **리액트 컴포넌트 타입**입니다. 컴포넌트는 `props`라 불리는 파라미터를 받으며 `render`메소드를 통해 보여줄 뷰의 계층을 리턴합니다.

`render` 메소드는 우리가 화면에서 무엇을 보길 원했는지에 대한 *기술(description)* 을 반환합니다. 리액트는 description을 받고 결과를 보여줍니다. `render`는 무엇을 렌더링할지에 대한 간단한 description인 **리액트 엘리먼트**를 반환합니다. 대부분의 리액트 개발자들은 이 구조를 더욱 쉽게 쓸 수 있게 만들어주는 'JSX'라고 불리는 특별한 문법을 사용합니다. `<div />` 문법은 빌드될 때 `React.createElement('div')`의 형태로 변환됩니다. 위의 예제는 사실 다음 코드와 동일합니다.

```javascript
return React.createElement('div', {className: 'shopping-list'},
                           React.createElement('h1', /* ... h1 children ... */),
                           React.createElement('ul', /* ... ul children ... */)
                           );
```

[풀버전은 여기](https://babeljs.io/repl/#?presets=react&code_lz=DwEwlgbgBAxgNgQwM5IHIILYFMC8AiJACwHsAHUsAOwHMBaOMJAFzwD4AoKKYQgRlYDKJclWpQAMoyZQAZsQBOUAN6l5ZJADpKmLAF9gAej4cuwAK5wTXbg1YBJSswTV5mQ7c7XgtgOqEETEgAguTuYFamtgDyMBZmSGFWhhYchuAQrADc7EA)에 있습니다.

만일 `createElement()`에 대해 더 상세히 알고 싶으시다면, [API 레퍼런스](https://reactjs.org/docs/react-api.html#createelement)를 참조하세요. 튜토리얼에서는 함수를 직접 호출하지 않고 계속 JSX를 사용할 것입니다.

JSX에는 자바스크립트의 모든 힘이 담겨있습니다. 어떤 자바스크립트 표현식이라도 JSX의 괄호 안에 넣을 수 있습니다. 각각의 리액트 엘리먼트는 우리가 저장할 수 있고 어딘가로 넘길 수 있는 자바스크립트 오브젝트입니다. 

위의 `ShoppingList` 컴포넌트는 `<div />`나 `<li />` 같은 빌트인 DOM만을 렌더링하지만 우리는 커스텀 리액트 컴포넌트도 조합하고 렌더링 할 수 있습니다. 예를 들면, `<ShoppingList/>`를 적음으로써 우린 ShoppingList 전체 내용을 한번에 참조 할 수도 있습니다. 각각의 리액트 컴포넌트는 캡슐화되어 있고 독립적으로 동작할 수 있습니다. 이러한 특성은 우리가 간단한 컴포넌트로부터 복잡한 UI를 만들 수 있게 허용해줍니다.

## 스타터 코드 살펴보기

만일 **브라우저**에서 튜토리얼을 진행 중이라면, 이 [스타터 코드](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)를 새 탭에서 열어주세요. 로컬에서 진행한다면 프로젝트 폴더의 `src/index.js`파일을 열어주세요. 

이 스타터 코드는 우리가 만들 게임의 기반이 되는 코드입니다. CSS 스타일링은 제공되어 있으니 우리는 리액트를 배우는 것과 틱택토 프로그래밍을 하는 것에만 집중하면 됩니다.

코드를 살펴보면 우리는 3가지 리액트 컴포넌트를 발견할 수 있습니다.

- Sqaure
- Board
- Game

Square 컴포넌트는 하나의 `<button>`을 렌더링하고 Board 컴포넌트는 9개의 Square 컴포넌트를 렌더링합니다. 게임 컴포넌트는 placeholder 를 가진 Board를 렌더링합니다. 이 컴포넌트는 우리가 나중에 수정하게 될 것입니다. 현재에는 어떠한 상호작용하는 컴포넌트도 존재하지 않는 상태입니다.

## Props를 통한 데이터 전달

이제 본격적으로 처음 시작하기 위해, 데이터를 Board 컴포넌트에서 Square 컴포넌트로 옮겨봅시다.

튜토리얼을 진행하며 코드는 복사 붙여넣기를 하기보다 손으로 직접 치는 것을 강력히 권장합니다. 손으로 치는 과정은 우리에게 머슬 메모리를 개발시키고 더 깊은 이해를 할 수 있게 도와줍니다.

Board의 `renderSquare` 메소드에서, Square에 `value`라 불리는 prop을 전달하기 위해 코드를 잠시 변경해주세요.

```js
class Board extends React.Component {
	renderSquare(i) {
		return <Square value={i} />;  
    }
}
```

Square의 `render` 메소드가 그 값을 보여줄 수 있도록 `{/* TODO */}` 부분을 `{this.props.value}`로 바꿔주세요.

```js
class Square extends React.Component {
	render() {
		return (
			<button className="square">
				{this.props.value}
			</button>
		)
	}
}
```

이전:

![before_prop.png](https://images.velog.io/post-images/jakeseo_me/0de28e20-5e40-11e9-8e03-551282fb0315/beforeprop.png)

이후:

![after_prop.png](https://images.velog.io/post-images/jakeseo_me/1817ed90-5e40-11e9-8e03-551282fb0315/afterprop.png)

[현재까지 한 전체 코드 보기](https://codepen.io/gaearon/pen/aWWQOG?editors=0010)

축하합니다! 방금 부모 Board 컴포넌트에서 자식 Square 컴포넌트로 prop을 넘기는데 성공하였습니다. prop을 넘기는 것은 리액트 앱에서 부모에서 자식으로 정보가 어떻게 흘러가는지를 설명합니다.

## 상호작용하는 컴포넌트 만들기

Square 컴포넌트를 클릭했을 때 그 자리에 'X'가 채워지도록 만들어봅시다. 처음으로 Square 컴포넌트의 `render` 함수에서 리턴되는 버튼 태그를 변경합시다.

```js
class Square extends React.Component {
	render() {
		return (
			<button className="square" onClick={function () { alert('click'); }}>
				{this.props.value}
			</button>
		)
    }
}
```

Square에 있는 버튼을 클릭하게되면 alert 메세지를 볼 수 있을 것입니다.

> **알아두기**
> 타이핑을 더 적게하고 [this의 헷갈리는 사용법](https://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/)을 피하기 위해서 우리는 이벤트 핸들러에 [화살표 함수](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)를 쓸 것입니다. 
```js
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={() => {alert('click')}>
        {this.props.value}
      </button>
    );
  }
}
```
> `onClick={() => alert('click')}`가 어떻게 쓰였는지 알아봅시다. `onClick`의 prop으로 우리는 함수를 넘겨주었습니다. 리액트는 클릭이 발생한 후에 이 함수를 실행할 것입니다. `() =>`을 적는 걸 까먹고 `onClick={alert('click')}` 만 적지 않도록 조심하세요. 흔히들 하는 실수입니다. 그리고 매번 컴포넌트가 재렌더링 될 때마다 alert가 일어날 것입니다.

다음 단계로 우리는 Square 컴포넌트가 클릭됐을 때, 클릭됐던 것을 기억하게 만들고 "X"마크를 채우고 싶습니다. 무언가를 기억하기 위해 컴포넌트는 **상태(state)** 라는 것을 사용합니다.

리액트 컴포넌트는 생성자에 `this.state`를 세팅함으로써 상태를 가질 수 있습니다. `this.state`는 정의된 리액트 컴포넌트 내부의 private 하게 적용된다고 생각하시면 됩니다. Square의 현재 값을 `this.state`에 저장해봅시다. 그리고 Square가 클릭됐을 때 그것을 변경해봅시다.

먼저, 클래스에 상태를 초기화하는 생성자를 만들 것입니다.

```js
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,  
    };
  }
  
  render() {
    return (
      <button className="square" onClick={() => alert('click')}>
        {this.props.value}
      </button>
    );
  }
}
```

> **알아두기** 
자바스크립트 클래스에서 하위 클래스의 생성자를 정의할 때는 항상 `super`를 호출해야 합니다. 생성자를 가진 모든 리액트 컴포넌트 클래스들은 `super(props)`를 호출하면서 시작해야 합니다.

이제 우리는 클릭됐을 때, 현재 상태의 값을 나타내주기 위해 Square의 `render` 메소드를 수정할 것입니다.

- `<button>`태그 안에 있는 `this.props.value`를 `this.state.value`로 바꿔주세요.
- `onClick={...}` 이벤트 핸들러를 `onClick={() => this.setState({value: 'X'})}`로 바꿔주세요.
- `className`과 `onClick`을 각각 다른 줄에 표기하는 것이 가독성이 좋습니다.

모든 변경이 끝난 후에, Square의 `render` 메소드에 의해 반환되는 `<button>`태그는 다음과 같이 작성됩니다.

```js
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,  
    };
  }
  
  render() {
    return (
      <button
        className="square"
        onClick={() => this.setState({value: 'X'})}
      >
        {this.state.value}
      </button>
    );
  }
}
```

Square의 `render`메소드 내부에 있는 `onClick`핸들러에서 `this.setState`를 호출함으로써, 우리는 리액트에게 `<button>`이 클릭될 때마다 Square를 재렌더링하라고 말합니다. 업데이트 이후, Square의 `this.state.value`는 `'X'`가 될 것입니다. 우리는 게임보드에서 `X`를 볼 수 있습니다. 아무 Square나 클릭하면 `X`가 나타납니다.

컴포넌트에서 `setState`를 호출하면, 리액트는 자동적으로 자식 컴포넌트도 업데이트합니다.

[전체 코드 보기](https://codepen.io/gaearon/pen/VbbVLg?editors=0010)

## 개발자 도구

[Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)과 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)를 위한 리액트 개발자 도구 확장 프로그램은 우리가 리액트 컴포넌트의 트리를 검사할 수 있게 해줍니다.

![ReactComponentTree.png](https://images.velog.io/post-images/jakeseo_me/50989c50-5eae-11e9-b696-9d59f07ba0b0/ReactComponentTree.png)

리액트 개발자 도구는 컴포넌트가 가진 props와 state를 체크하는 것도 가능하게 합니다.

리액트 개발자 도구 설치 후에, 페이지에 있는 요소를 오른쪽 클릭 후에 "검사" 기능을 실행해보세요. 가장 오른쪽 탭에 리액트 탭이 있을 것입니다.

**하지만 코드펜에서 동작하게 만드려면 몇가지 추가적인 작업이 필요합니다.**

1. 회원가입 후 로그인하고 이메일을 확인하세요. (이메일이 안보이면 스팸메일함도 확인해보세요.)
2. "Fork" 버튼을 클릭하세요.
3. "Change View"를 클릭한 후에 "Debug mode"를 선택하세요.
4. 새로 열린 탭 속 개발자 도구에 리액트 탭이 보일 것입니다.

# 게임 완성하기

이제 우리 틱택토 게임의 기본적인 뼈대를 만들었습니다. 완전한 게임을 만들기 위해, 우리는 "X"와 "O"를 보드에 표현해야 하고 승자가 누구인지 가려내야 합니다.

## State 끌어 올리기

현재, 각각의 Square 컴포넌트는 Game의 state를 갖고 있습니다. 승자를 가려내기 위해서는 각 9개의 Square들의 값을 한 곳에 모아야 합니다. 

우리는 Board가 각각 Square에게 Square의 상태를 물어야 한다고 생각할 수도 있습니다. 리액트에서는 이러한 접근법도 가능하지만 권장하지 않습니다. 왜냐하면 코드가 이해하기 어려워지고 버그를 만들기 쉬우며 리팩토링하기도 어려워지기 때문입니다. 최고의 접근법은 게임의 상태를 각각의 Square에서 관리하는 것이 아닌 부모 Board 컴포넌트에서 관리하는 것입니다. Board 컴포넌트는 prop을 넘김으로써 각각의 Square에게 무엇을 보여줄지 말할 수 있습니다. [우리가 각각의 Square에 번호를 넘겼던 것 처럼](https://reactjs.org/tutorial/tutorial.html#passing-data-through-props)요.

**여러 자식에서 데이터를 수집하기 위해 또는 서로 통신하는 2개의 자식 컴포넌트를 갖기 위해 부모 컴포넌트에서 shared state를 선언할 필요가 있습니다. 부모 컴포넌트는 props를 사용하여 state를 자식 컴포넌트에 넘길 수 있습니다. 이것은 자식 컴포넌트와 각각 다른 컴포넌트들, 부모 컴포넌트와의 싱크를 유지시킬 것입니다.** 

State를 부모 컴포넌트로 끌어 올리는 것은 리액트 컴포넌트가 리팩토링 될 때 흔히 있는 일입니다. 이번 기회를 통해 연습해봅시다.

Board의 생성자를 추가하고 초기 state에 9개의 Square에 들어갈 9개의 null 배열을 넣어봅시다. 

```js
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),  
    };
  }
  
  renderSquare(i) {
    return <Square value={i} />;  
  }
}
```

나중에 Board를 채울 때, `this.state.squares` 배열은 이런 형식으로 보이게 될 것입니다.
```js
[
  'O', null, 'X',
  'X', 'X', 'O',
  'O', null, null,
]
```

Board의 `renderSquare` 메소드는 현재 이 상태입니다.

```js
renderSquare(i) {
  return <Square value={i} />;  
}
```

시작할 때, 우리는 Board에서 모든 Square에서 값을 보여주도록 prop을 아래로 전달했습니다. 다른 이전 단계에서 우리는 숫자를 Square의 자체 상태에 의해 결정되는 "X"마크로 바꾸었습니다. 그게 지금 Square가 Board에서 prop으로 전달된 `value`를 무시하는 이유입니다.

우린 다시 prop 전달 매커니즘을 이용할 것입니다. 우리는 각각의 Square에게 현재 값(`'X'`, `'O'`, or `null`)에 대한 지시를 하기 위해 Board를 수정할 것입니다. 우리는 Board의 constructor에 이미 `squares` 배열을 정의했습니다. 그리고 우리는 Board의 `renderSquare` 메소드가 이것을 읽어들이게 수정할 것입니다.

```js
renderSquare(i) {
  return <Sqare value={this.state.squares[i]} />;
}
```

[전체 코드는 여기서 확인할 수 있습니다.](https://codepen.io/gaearon/pen/gWWQPY?editors=0010)

각각의 Square는 `'X'`, `'O'` 또는 `null`의 `value` prop을 받게 될 것입니다.

다음으로, 우리는 Square가 클릭됐을 때 일어나는 일을 변경해주어야 할 필요가 있습니다. Board 컴포넌트는 현재 어떤 Square 컴포넌트가 차있는지에 대한 정보를 갖고 있습니다. Square가 Border의 state를 업데이트 할 수 있도록 하는 방법을 만들 필요가 있습니다. state는 이것을 정의하는 컴포넌트에 private하게 여겨지기 때문에 우리는 Square에서 Board의 state를 바로 업데이트 할 수 없습니다.

대신, 우리는 Board에서 Square로 함수를 넘길 것입니다. 우리는 Square가 클릭됐을 때, Sqaure가 그 함수를 호출하도록 할 것입니다. 우리는 Board안의 `renderSquare` 메소드를 다음과 같이 수정할 것입니다.

```js
renderSquare(i) {
  return (
    <Square
      value={this.state.squares[i]}
      onClick={() => this.handleClick(i)}
    />
  );
}
```

> **알아둘 것**
> 우리는 우리는 반환된 원소를 가독성을 위해 여러 줄로 나누었습니다. 그리고 괄호를 추가하여 자바스크립트에서 `return`과 줄이 바뀌는 곳 뒤에 세미콜론을 추가할 필요가 없게 만들었습니다.

지금 우리는 2개의 props를 Board에서 Square로 보낼 것입니다. `value`와 `onClick`을 보낼 것입니다. `onClick` prop은 Square가 클릭됐을 때 불러오는 함수입니다. 우리는 Square를 다음과 같이 변경할 것입니다.

- Square의 `render` 메소드 속의 `this.state.value`를 `this.props.value`로 
- Square의 `render` 메소드 속의 `this.setState()`를 `this.props.onClick()`로 
- Square의 `constructor`를 지울 것입니다. 왜냐하면 Square는 더이상 Game의 상태를 따라갈 필요가 없으니까요.

이러한 변화 후에는 Square의 코드는 다음과 같을 것입니다.

```js
class Square extends React.Component {
  render() {
    return (
      <button 
        className="square" 
        onClick={() => {this.props.onClick()}}
      >
        {this.props.value}
      </button>
    );
  }
}
```

Square가 클릭됐을 때, Board에 의해 제공된 `onClick` 함수가 호출됩니다. 여태까지 어떻게 만들었는지 하나하나 짚어봅시다.

1. 내부(built-in) DOM `<button>` 컴포넌트의 `onClick` prop이 React에게 클릭 이벤트 리스너를 준비하라고 알립니다.
2. 버튼이 클릭됐을 때, 리액트가 Square의 `render()` 메소드에 정의된 `onClick` 이벤트 핸들러를 호출할 것입니다.
3. 이 이벤트 핸들러는 `this.props.onClick()`을 호출합니다. Square의 `onClick` prop은 Board에 의해 구체화됩니다. 
4. Board가 `onClick={() => this.handleClick()}`를 Square로 넘깁니다. Square가 클릭됐을 때, `this.handleClick(i)`를 호출합니다.
5. 우리는 아직 `handleClick()` 메소드를 정의하지 않았습니다. 그래서 우리의 코드는 동작하지 않고 망가질 것(crash)입니다. 지금 square를 클릭하면, 우리는 "this.handleClick is not a function"과 같은 빨간 에러 화면을 볼 수 있을 것입니다.

> **알아둬야 할 것**
> 리액트에서 DOM `<button>` 원소의 `onClick` 속성은 특별한 의미를 갖습니다. 이것은 빌트인(built-in) 컴포넌트이기 때문입니다. Square 같은 커스텀 컴포넌트의 경우, 이름은 우리 마음대로 짓습니다. 우리는 Square의 `onClick` prop이나 Board의 `handleClick` 메소드에 아무런 이름이나 줄 수 있습니다. 그래도 코드는 똑같이 동작할 것입니다. 리액트에서는, 이벤트를 나타내는 props는 `on[Event]`와 같은 형식으로 이름을 짓는 것이 규칙입니다. 그리고 그 이벤트를 다루기 위한 메소드는 `handle[Event]` 처럼 이름을 짓습니다.

우리가 Square를 클릭할 때, 우리는 `handleClick`을 아직 정의하지 않았기 때문에 빨간색 에러 메시지를 보게 될 것입니다. 우리는 `handleClick`을 Board 클래스에 추가할 것입니다.

```js
class Board extends React.Component {
  constructor (props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),  
    }
  }
  
  handleClick(i) {
    const squares = this.state.squares.slice(); // 배열을 복사해서 쓰기 위해...
    squares[i] = 'X';
    this.setState({squares: squares});
  }
  
  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={()=>this.handleClick(i)}
      />
    );
  }
  
  render() {
    const status = 'Next player: X';
    
    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

[여태까지의 모든 코드 보기](https://codepen.io/gaearon/pen/ybbQJX?editors=0010)

이렇게 코드를 변경한 뒤에, 이전과 같이 Square를 클릭해서 Square의 내용을 채울 수 있습니다. 하지만, 이제 상태는 개개의 Square 컴포넌트가 아닌 Board 컴포넌트에 저장됩니다. Board의 상태가 변화될 때마다, Square 컴포넌트는 자동으로 재렌더링됩니다. Board 컴포넌트에 모든 Square의 상태를 저장하는 것은 나중에 Board 컴포넌트가 승자를 결정하게 해줍니다.

Square 컴포넌트가 더이상 상태를 저장하지 않기 때문에, Square 컴포넌트는 Board 컴포넌트로부터 값을 받고 클릭됐을 때, Board 컴포넌트에게 알리는 역할만 합니다. 리액트 용어로는 Square 컴포넌트는 현재 **제어된 컴포넌트(Controlled Components)** 입니다. Board는 그들을 모두 제어할 권한을 가집니다.

알아둬야 할 것은 `handleClick`에서 우리는 `squares` 배열의 복사본을 만들기 위해 `.slice()`를 호출했습니다. 이것은 현재 존재하는 array 대신 복사본 array를 수정하기 위함입니다. 왜 이렇게 구현하는지는 다음 섹션에서 설명하겠습니다.

## 불변성은 왜 중요한가

이전 코드 예제에서, 존재하는 배열 대신 새로 생성한 배열을 변경하기 위해 `.slice()`를 이용해 `squares`의 복사본을 만들기를 제안했습니다. 우리는 이제부터 불변성, 그리고 왜 불변성이 중요한지에 대해서 배워볼 것입니다.

데이터를 변경하기 위해서는 일반적으로 두가지 방법이 있습니다. 첫번째 방법은 데이터의 값을 직접 *변경*하는 것입니다. 두번째 방법은 데이터를 변경된 새 복사본으로 교환하는 것입니다.

### 데이터를 직접 변경 (with Mutation)

```js
var player = {score: 1, name: 'Jeff'};
player.score = 2;
// Now player is {score: 2, name: 'Jeff'}
```

### 데이터의 복사본으로 대체 (without Mutation)

```js
var player = {score: 1, name: 'Jeff'};

var newPlayer = Object.assign({}, player, {score: 2});
// player변수에는 아무런 변화도 일어나지 않습니다.
// 하지만 newPlayer 변수에는 {score: 2, name: 'Jeff'} 의 값이 들어있습니다.

// 만일 object spread 문법을 사용했으면 다음과 같이 코딩할 수도 있습니다.
// var newPlayer = {...player, score: 2};
```

이 소스는 결과는 같지만 mutation(가변성)을 이용하지 않았습니다(원래 있던 데이터도 변경하지 않았습니다.). 우리는 아래 기재된 몇가지 이점을 얻습니다.

### 복잡한 특징들이 간단해집니다.

불변성은 복잡한 특징들을 구현할 때 훨씬 간단해지게 만들어줍니다. 이 튜토리얼 뒤에, 틱택토 게임의 게임 히스토리를 다시 살펴보고 이전 움직임으로 다시 갈 수 있는 "time travel" 이라는 특징을 구현할 것입니다. 이 기능은 게임을 만들 때만 사용하는 것이 아닙니다. 무언가를 취소(undo)하고 다시(redo)하는 것과 같은 행동은 어플리케이션에서 일반적인 요구사항입니다. 직접적인 데이터 변경을 피하는 것은 우리에게 이전 게임 히스토리 버전을 갖고 있다가 나중에 다시 사용하는 것을 가능하게 합니다.


### 변경사항을 발견합니다.

변화가 가능한 객체에서 변화를 감지하는 것은 어렵습니다. 왜냐하면 직접 변화되기 때문입니다. 변경사항을 발견하는 것은 이전 복사본과 비교될 변화 가능한 객체 그리고 순회할 전체 객체 트리를 필요로 합니다.

변화하지 않는 객체에서 변화를 감지하는 것은 상대적으로 더 쉽습니다. 만일 참조되는 변화하지 않는 객체가 이전 객체와 다르다면, 객체는 변화한 것입니다.

### 리액트에서 재렌더될 때를 결정합니다.

불변성의 주된 장점은 리액트에서 순수한 컴포넌트를 작성하는 것을 도와준다는 것입니다. 불변하는 데이터는 변화가 일어났는지 파악하는 것을 더 쉽게 해주어 컴포넌트가 재렌더링이 필요할 때를 결정하는 것을 돕습니다.

`shouldComponentUpdate()`에 대해서도 배울 수 있고 [https://reactjs.org/docs/optimizing-performance.html#examples] 게시글을 보며 어떻게 순수 컴포넌트를 만드는지 배울 수도 있습니다.

### 함수 컴포넌트

우리는 이제 Square를 **함수 컴포넌트**로 변경할 것입니다.

리액트에서, **함수 컴포넌트**는 상태를 가지지 않고 `render` 메소드만 갖는 컴포넌트를 작성하는 간단한 방법입니다. `React.Component`를 상속하는 클래스를 정의하는 것 대신에 `props`를 input으로 받고 렌더링 할 것을 리턴하는 함수를 작성할 수 있습니다. 함수 컴포넌트는 클래스를 작성하는 것보다는 코드가 더 짧습니다. 그리고 많은 컴포넌트들은 이 방식으로 표현될 수 있습니다.

Square 클래스를 다음과 같은 함수로 고쳐봅시다.

```js
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}> 
    </button>
  );
}
```

우리는 `this.props`를 `props`로 바꾸었습니다.

[현재까지의 모든 코드 보기](https://codepen.io/gaearon/pen/QvvJOv?editors=0010)

>**알아둬야 할 것**
우리가 Square 컴포넌트를 함수 컴포넌트로 변경했을 때, 우리는 `onClick={() => this.props.onClick()}` 에서 더 짧게 `onClick={props.onClick}`으로 고쳐줬다는 것을 기억합시다. (양쪽에 있던 괄호들이 다 사라졌다는 것을 기억하세요.)

## 각자의 턴 갖기

이제 틱택토 게임에서 확실한 결점을 고칠 차례입니다. 보드에 "O"가 마킹되지 않는 것입니다.

우리는 처음 움직임의 기본값을 "X"로 설정할 것입니다. Board 생성자의 초기 상태를 수정함으로써 우리는 기본 값을 설정할 수 있습니다.

```js
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }
```

매번 플레이어가 움직일 때마다, `xIsNext`는 어떤 플레이어가 다음인지를 판단하기 위해 뒤집(flipped)힐 것입니다. 그리고 게임의 상태는 저장될 것입니다. 우리는 `xIsNext`의 값을 뒤집기 위해 Board 컴포넌트의 `handleClick` 함수를 업데이트 할 것입니다.

```js
handleClick(i) {
  const squares = this.state.squares.slice();
  squares[i] = this.state.xIsNext ? 'X' : 'O';
  this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
}
```

이렇게 바꾸면 "X"와 "O"가 차례로 턴을 갖습니다. 직접 클릭 해보세요.

어느 플레이어가 다음 턴인지 보여주기 위해 Board 컴포넌트의 `render`에서 "status" 텍스트를 바꿔봅시다.

```js
render() {
  const status = `Next player: ${this.state.xIsNext ? 'X' : 'O'}`; 
  //나머진 그대로...
}
```

변경사항을 적용한 후에는 Board 컴포넌트는 이러한 모양일 것입니다.

```js
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
        squares: squares,
        xIsNext: !this.state.xIsNext,
      });
  }

  renderSquare(i) {
    return <Square 
              value={this.state.squares[i]}
              onClick={()=>this.handleClick(i)}
            />;
  }

  render() {
    const status = `Next player: ${this.state.xIsNext ? 'X' : 'O'}`;

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

[여기까지의 모든 코드 보기](https://codepen.io/gaearon/pen/KmmrBy?editors=0010)

## 승자 결정하기

이제 우리는 다음에는 어떤 플레이어의 턴인지 보여줄 것입니다. 한쪽이 게임에서 승리하면 승리한 것을 보여주고 더이상 턴이 진행되지 않도록 할 것입니다. 파일의 끝에 아래의 도우미 함수를 복사하고 붙여넣으세요. 

```js
function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

9개의 Squares 컴포넌트가 주어졌을 때, 이 함수는 승자를 체크하고 `'X'`, `'O'`, `'null'`을 적절하게 반환할 것입니다.

우리는 Board의 `render`함수에서 한 플레이어가 승리하였는지 체크하기 위해 `calculateWinner(squares)`를 호출할 것입니다. 만일 한 플레이어가 이겼다면, 우리는 "Winner: X" 또는 "Winner : O"와 같은 텍스트를 보여줄 수 있을 것입니다. Board의 `render`함수에서 `status` 선언을 다음과 같이 바꿀 것입니다.

```js
const winner = calculateWinner(this.state.squares);
let status;

if(winner) 
  status = 'Winner: ' + winner;
else
  status = `Next player: ${this.state.xIsNext ? 'X' : 'O'}`
```

우리는 이제 Board 컴포넌트의 `handleClick` 함수를 변경할 수 있습니다. 만일 누군가가 게임을 승리하거나 모든 Square가 가득 찼을 때, 리턴을 더 빨리 함으로써, 클릭을 무시할 수 있습니다.

```js
handleClick(i) {
  const squares = this.state.squares.slice();

  if(calculateWinner(squares) || squares[i])
    return;

  squares[i] = this.state.xIsNext ? 'X' : 'O';
  this.setState({
    squares: squares,
    xIsNext: !this.state.xIsNext,
  });
}
```

[지금까지 작성한 모든 코드 보기](https://codepen.io/gaearon/pen/LyyXgK?editors=0010)

축하합니다! 이제 틱택토 게임을 만드는데 성공했습니다. 그리고 지금 막 React의 기본을 배웠습니다. 진짜 승자는 당신입니다!

# 시간여행 추가하기

마지막 과제로, "과거로 돌아가는 것"이 가능하도록 만들어봅시다. 게임에서 이전 움직임으로 돌아가는 것입니다.

## 움직임 History 저장하기

우리가 만일 `squares` 배열을 변경한다면, 시간여행을 구현하기는 매우 어려울 것입니다.

하지만, 우리는 매번 이동 후에 `squares` 배열의 새로운 복사본을 만들기 위해서 `slice()` 함수를 이용하였습니다. 그리고 그것을 불변하도록 다뤘습니다. 이것은 우리에게 `squares` 배열의 모든 지난 버전을 저장할 수 있도록 해주었습니다. 그리고 이미 진행된 차례들 사이로 돌아다닐 수 있도록 해줍니다.

우린 지난 `squares` 배열을 `history`라 불리는 배열에 저장할 것입니다. `history` 배열은 처음부터 끝까지 모든 board 컴포넌트의 상태를 보여줍니다. 그리고 다음과 같은 형태를 지닙니다.

```js
history = [
  // Before first move
  {
    squares: [
      null, null, null,
      null, null, null,
      null, null, null,
    ]
  },
  // After first move
  {
    squares: [
      null, null, null,
      null, 'X', null,
      null, null, null,
    ]
  },
  // After second move
  {
    squares: [
      null, null, null,
      null, 'X', null,
      null, null, 'O',
    ]
  },
  // ...
]
```

이제 우리는 어떤 컴포넌트가 `history` 상태를 가질지 결정해야 합니다.

## 다시 한번, 상태 끌어올리기

우리는 가장 상위레벨 컴포넌트인 Game 컴포넌트가 이전 움직임들을 보여주길 원합니다. 이렇게 하기 위해서는 `history`에 접근이 필요합니다. 그래서 우리는 `history` 상태를 가장 상위 레벨 게임 컴포넌트에 위치시킬 것입니다.

`history` 상태를 게임 컴포넌트에 위치시키려면 자식 컴포넌트인 Board 컴포넌트에서 squares 상태를 지우는게 좋습니다. 위에서 했던 Square 컴포넌트에서 Board 컴포넌트로의 ["상태 끌어올리기"](https://reactjs.org/tutorial/tutorial.html#lifting-state-up)처럼 우리는 Board 컴포넌트에 있는 상태를 가장 상위 Game 컴포넌트로 올릴 것입니다. 그렇게 되면 Game 컴포넌트는 Board 컴포넌트의 데이터에 대한 모든 것을 제어할 수 있습니다. 그리고 Board 컴포넌트에게 history에서 이전 차례들을 렌더링하라고 지시해봅시다.

처음으로 우리가 할 일은 Game 컴포넌트 생성자에 초기 상태를 셋팅하는 것입니다.

```js
class Game extends React.Component {
  constructor(props){
    super(props);
    this.state = {
      history : [{
        squares: Array(9).fill(null)
      }],
      xIsNext: true,
    }
  }

  render() {
    return (
      <div className="game">
        <div className="game-board">
          <Board />
        </div>
        <div className="game-info">
          <div>{/* status */}</div>
          <ol>{/* TODO */}</ol>
        </div>
      </div>
    );
  }
}
```

우리는 `squares`를 받는 Board 컴포넌트를 작성할 것이고 `onClick` props를 Game 컴포넌트로부터 받을 것입니다. 지금 우리는 많은 Squares 컴포넌트를 위해 Board 내부에 단 하나의 핸들러만 갖고 있습니다. 어떤 Square가 클릭됐는지 표시하기 위해 우리는 각각 Square의 위치를 `onClick` 핸들러로 넘겨야 합니다. Board 컴포넌트는 다음과 같이 변경하면 됩니다.

- Board 컴포넌트 내부 `constructor`는 삭제하세요.
- Board 컴포넌트의 `renderSquare` 내부의 `this.state.squares[i]`를 `this.props.squares[i]`로 교체하세요.
- Board 컴포넌트의 `renderSquare` 내부의 `this.handleClick(i)`을 `this.props.onClick(i)`로 교체하세요.

Board 컴포넌트의 코드는 다음과 같이 변했을 것입니다.
```js
class Board extends React.Component {

  handleClick(i) {
    const squares = this.props.squares.slice();

    if(calculateWinner(squares) || squares[i])
      return;

    squares[i] = this.props.xIsNext ? 'X' : 'O';
    this.setState({
        squares: this.props.squares,
        xIsNext: !this.props.xIsNext,
      });
  }

  renderSquare(i) {
    return <Square 
              value={this.props.squares[i]}
              onClick={()=>this.props.onClick(i)}
            />;
  }

  render() {
    const winner = calculateWinner(this.state.squares);
    let status;

    if(winner) 
      status = 'Winner: ' + winner;
    else
      status = `Next player: ${this.state.xIsNext ? 'X' : 'O'}`

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

이제 우리는 게임의 상태를 결정하고 보여주는 가장 최근 히스토리 엔트리를 사용하기 위한 Game 컴포넌트의 `render` 함수를 업데이트 할 것입니다.

```js
render() {
  const history = this.state.history;
  const current = history[history.length - 1];
  const winner = calculateWinner(current.squares);

  let status;

  if(winner) 
    status = 'Winner: ' + winner;
  else
    status = `Next player: ${this.state.xIsNext ? 'X' : 'O'}`


  return (
    <div className="game">
      <div className="game-board">
        <Board 
          squares={current.squares}
          onClick={(i) => this.handleClick(i)}
        />
      </div>
      <div className="game-info">
        <div>{status}</div>
        <ol>{/* TODO */}</ol>
      </div>
    </div>
  );
}
```

Game 컴포넌트는 이제 game의 상태를 렌더링합니다. 우리는 이제 Board의 `render` 메소드에서 대응하는 부분의 코드를 삭제해야 합니다. 리팩토링 이후, Board의 `render` 메소드는 다음과 같습니다.

```js
render() {
  return (
    <div>
      <div className="board-row">
        {this.renderSquare(0)}
        {this.renderSquare(1)}
        {this.renderSquare(2)}
      </div>
      <div className="board-row">
        {this.renderSquare(3)}
        {this.renderSquare(4)}
        {this.renderSquare(5)}
      </div>
      <div className="board-row">
        {this.renderSquare(6)}
        {this.renderSquare(7)}
        {this.renderSquare(8)}
      </div>
    </div>
  );
}
```

마지막으로, 우리는 Board 컴포넌트에서 Game 컴포넌트로 `handleClick` 메소드를 옮길 필요가 있습니다. 또 `handleClick` 메소드를 수정할 필요도 있습니다. 왜냐하면 Game 컴포넌트의 상태는 다르게 구조화되어 있으니까요. Game 컴포넌트의 `handleClick` 메소드 내부에서 우리는 `history`에 새로운 `history` 엔트리를 합칠(concatenate) 것입니다.

```js
handleClick(i) {
  const history = this.state.history;
  const current = history[history.length - 1];
  const squares = current.squares.slice();
  
  if(calculateWinner(squares) || squares[i]) {
    return;  
  }
  squares[i] = this.state.xIsNext ? 'X' : 'O';
  this.setState({
    history: history.concat([{
      squares: squares,
    }]),
    xIsNext: !this.state.xIsNext,
  });
}
```

> **알아둬야 할 것**
> 아마 우리에게 더욱 친숙한 배열의 `push()` 메소드와 다르게, `concat()` 메소드는 원본 배열을 변경하지 않습니다. 그래서 불변성을 지키기 위해 이걸 더 선호할 것입니다.

이 지점에서, Board 컴포넌트는 `renderSquare`와 `render` 메소드가 필요합니다. 게임의 상태와 `handleClick` 메소드는 Game 컴포넌트 안에 있는 것이 좋습니다.

[지금까지의 모든 코드 보기](https://codepen.io/gaearon/pen/EmmOqJ?editors=0010)

## 이전 움직임들 보여주기

우리가 틱택토 게임의 히스토리를 기록하고 있기 때문에, 이제 플레이어에게 지난 움직임의 기록을 보여주는 것도 가능합니다.

우리는 리액트 컴포넌트가 자바스크립트 1급 객체라는 사실을 배웠습니다. 리액트 컴포넌트를 어플리케이션 내부에서 어디든 보낼 수 있습니다. 리액트에서 여러 개의 아이템들을 랜더하기 위해, 우리는 리액트 원소들의 배열을 사용할 수 있습니다. 

자바스크립트에서, 배열은 데이터를 다른 데이터로 맵핑하는데 쓰이는 `map()` 메소드를 갖고 있습니다. 예를 들면,

```js
const numbers = [1, 2, 3];
const doubled = numbers.map(x => x * 2); // [2, 4, 6]
```

`map` 메소드를 이용하여, 우리는 스크린에 버튼을 보여주면서 움직임의 히스토리를 리액트 원소로 맵핑할 수 있습니다. 그리고 이전 움직임으로 점프하기 위한 버튼들의 리스트를 보여줄 수 있습니다.

그럼 Game의 `render`메소드에서 `history`를 `map` 해봅시다. 

```js
render() {
  const history = this.state.history;
  const current = history[history.length - 1];
  const winner = calculateWinner(current.squares);
  
  const moves = history.map((step, move) => {
    const desc = move ?
      'Go to move #' + move :
      'Go to game start';
    return  (
      <li>
        <button
          onClick={() => this.jumpTo(move)}>
          {desc}
        </button>
      </li>
    );
  });

  let status;

  if(winner) 
    status = 'Winner: ' + winner;
  else
    status = `Next player: ${this.state.xIsNext ? 'X' : 'O'}`


  return (
    <div className="game">
      <div className="game-board">
        <Board 
          squares={current.squares}
          onClick={(i) => this.handleClick(i)}
        />
      </div>
      <div className="game-info">
        <div>{status}</div>
        <ol>{moves}</ol>
      </div>
    </div>
  );
}
```

[여기까지의 전체 코드는 여기에서](https://codepen.io/gaearon/pen/EmmGEa?editors=0010)

틱택토 게임의 히스토리에서 각 움직임을 위해 우리는 `<button>`을 포함한 리스트 아이템 `<li>` 를 이용합니다. 버튼은 `this.jumpTo()` 메소드를 호출하는 `onClick` 핸들러를 갖고 있습니다. 우리는 아직 `jumpTo()`메소드를 구현하지 않았습니다. 지금은, 게임에서 일어난 움직임들의 리스트를 봐야 합니다. 그리고 개발자 도구 콘솔이 말하는 경고를 봅시다.

> **Warning: Each child in an array or iterator should have a unique "key" prop. Check the render method of "Game".**

위의 경고의 의미에 대해서 한번 논의해봅시다.

## 키 집기

우리가 리스트를 렌더링할 때, 리액트는 각 렌더링된 리스트 아이템의 정보에 대해 저장합니다. 우리가 리스트를 업데이트할 때, 리액트가 어떤 것이 바뀌었는지 알아낼 수 있어야 합니다. 우리는 리스트의 아이템들을 추가하고 제거하고 다시 배열하고 업데이트할 수도 있었습니다.

다음 코드를

```js
<li>Alexa: 7 tasks left</li>
<li>Ben: 5 tasks left</li>
```

다음과 같이 고친다고 상상해보세요.

```js
<li>Ben: 9 tasks left</li>
<li>Claudia: 8 tasks left</li>
<li>Alexa: 5 tasks left</li>
```

업데이트된 카운트들이 있고, 사람의 관점에서는 Alexa와 Ben의 숫자가 바뀌었다고 말할 수도 있을 것입니다. 그리고 Alexa와 Ben 사이에 Claudia가 생겼습니다. 하지만, 리액트는 컴퓨터 프로그램이고 우리가 의도한 바를 알지 못합니다. 리액트는 우리의 의도를 모르기 때문에, 우리는 각 형제 리스트 아이템이 서로 구분할 수 있도록 *key* 프로퍼티를 명기할 필요가 있습니다. 한가지 옵션은 `alexa`, `ben`, `claudia`와 같이 문자열을 쓰는 것입니다. 만일 우리가 데이터베이스에서 Alexa, Ben, Claudia와 같은 데이터를 나열한다면 DB내부의 ID가 키가 될 수도 있습니다.

```js
<li key={user.id}>{user.name}: {user.taskCount} tasks left</li>
```

리스트가 재렌더될 때, 리액트는 각 리스트 아이템의 키를 받습니다. 그리고 키를 매칭시키기 위해 이전 리스트의 아이템을 찾습니다. 만일 현재 리스트가 이전에 존재하지 않던 키를 갖고 있으면, 리액트는 컴포넌트를 생성합니다. 만일 현재 리스트가 이전에 갖고 있던 키를 잃어버린다면, 리액트는 이전 컴포넌트를 제거합니다. 만일 두 개의 키가 매치된다면, 일치하는 컴포넌트는 움직이게 됩니다. 키는 리액트에게 재 렌더링 사이에서 상태를 유지할 수 있게 하는 각 컴포넌트의 독립성에 대해 전달합니다. 만일 컴포넌트의 키가 바뀐다면, 컴포넌트는 파괴되고(destroyed) 새로운 상태로 재생성될 것입니다.

리액트에서 `key`는 특별하고 예약(reserved)된 프로퍼티입니다. (더 고급기능인 `ref`와 마찬가지죠.) 한 엘리먼트가 만들어졌을 때, 리액트는 `key` 프로퍼티를 추출합니다. 그리고 반환되는 엘리먼트에 `key`를 직접 저장합니다. `key`가 `props`처럼 보이겠지만, `key`는 `this.props.key`와 같은 방법으로 참조가 불가능합니다. 리액트는 자동적으로 `key`를 어떤 컴포넌트를 업데이트시킬지 결정하는 데에 이용하거든요. 컴포넌트는 자신의 `key`를 질의할 수 없습니다.

**우리가 동적인 리스트를 만들 때, 키를 할당하는 것은 매우 권장됩니다.** 만일 적절한 키가 없다면, 적절한 키를 갖도록 다시 재구성하는 것을 고려하기 바랍니다.

어떤 키도 명기되어있지 않다면, 리액트는 경고 메시지를 송출하고 배열의 인덱스 값을 기본 키 값으로 사용합니다. 리스트 아이템을 재정렬하거나 추가하거나 삭제하려고 할 때, 배열 인덱스를 키로 사용하는 것은 문제가 있을 수 있습니다. 명시적으로 `key={i}`라고 지정하는 것은 경고 메시지는 없앨 수 있지만 인덱스를 키로 이용할 때와 같은 문제를 지닙니다. 그래서 대부분의 경우에는 권장되지 않습니다.

`key`는 전역적으로 유니크할 필요가 없습니다. 컴포넌트와 동등한 레벨의 리스트 사이에서만 유니크하면 됩니다.

## 시간여행 구현하기

틱택토 게임 히스토리에서, 각각의 이전 움직임들은 관련된 유니크한 ID를 갖습니다. 이것은 움직임의 연손적인 숫자입니다. 움직임들은 중간에 재정렬되거나 삭제되거나 추가되지 않습니다. 그래서 인덱스를 키로 사용해도 안전합니다.

Game 컴포넌트의 `render` 메소드에서, 우리는 `<li key={move}>`와 같은 형태로 키를 추가할 것입니다. 이후 리액트에서 키에 대한 경고메시지는 사라질 것입니다.

```js
const moves = history.map((step, move) => {
  const desc = move ?
    'Go to move #' + move :
    'Go to game start';
  return (
    <li key={move}>
      <button onClick={() => this.jumpTo(move)}>
        {desc}
      </button>
    </li>
  );
});
```

[여기까지의 코드 보기](https://codepen.io/gaearon/pen/PmmXRE?editors=0010)

리스트의 아무 버튼만 눌러도 에러가 날 것입니다. 왜냐하면 `jumpTo` 메소드가 정의되지 않았기 때문입니다. `jumpTo` 메소드를 구현하기 전에 현재 몇번째 step을 보고있는지 나타내기 위해 `stepNumber`를 먼저 Game 컴포넌트의 상태에 추가할 것입니다.

먼저, `stepNumber: 0`를 Game 컴포넌트의 `constructor`에 초기 상태로 추가하세요.

```js
class Game extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      history: [{
        squares: Array(9).fill(null)  
      }],
      stepNumber: 0,
      xIsNext: true,
    };
  };
}
```

다음으로 `stepNumber`를 업데이트하기 위해 Game 컴포넌트에 `jumpTo` 메소드를 정의할 것입니다. 우리는 또 만일 우리가 변경하는 `stepNumber`가 짝수라면, `xIsNext`를 true로 설정할 것입니다.

```js
handleClick(i) {
  // 이 메소드의 내용은 그대로 유지합니다.
}

jumpTo(step) {
  this.setState({
    stepNumber: step,
    xIsNext: (step % 2) === 0,
  });
}

render() {
  // 이 메소드의 내용은 그대로 유지합니다.
}
```

이제 Square를 클릭할 때 작동하는 Game 컴포넌트의 `handleClick` 메소드에 몇가지 변화를 줄 것입니다.

우리가 추가한 `stepNumber` 상태는 이제 사용자에게 보여지는 움직임을 반영합니다. 우리가 움직인 후에, 우린 `this.state`의 인자의 일부로 `stepNumber: history.length`를 추가함으로써 `stepNumber`를 업데이트할 필요가 있습니다. 이것은 새로운 움직임이 있은 후에 같은 움직임에 머무르는 것을 보여주지 않음을 보증합니다.

우리는 또 `this.state.history`를 읽는 대신에  `this.state.history.slice(0, this.state.stepNumber + 1)`를 읽을 것입니다. 이것은 우리가 "이전으로 돌아가기" 후에 돌아간 시점부터 새롭게 움직임을 만들 수 있도록 해줍니다. 더이상 올바르지 않은 미래의 히스토리들은 전부 날립니다.

```js
handleClick(i) {
  const history = this.state.history.slice(0, this.state.stepNumber + 1);
  const current = history[history.length - 1];
  const squares = current.squares.slice();
  if (calculateWinner(squares) || squares[i]) {
    return;  
  }
  squares[i] = this.state.xIsNext ? 'X' : 'O';
  this.setState({
    history: history.concat([{
      squares: squares
    }]),
    stepNumber: history.length,
    xIsNext: !this.state.xIsNext,
  });
}
```

마지막으로, 우린 Game 컴포넌트의 `render` 메소드를 항상 마지막 움직임을 렌더링 하는 것에서 `stepNumber`에 따른 선택된 움직임을 렌더링 하도록 수정할 것입니다.

```js
render() {
  const history = this.state.history;
  const current = history[this.state.stepNumber];
  const winner = calculateWinner(current.squares);
  
  // 나머지는 변경하지 않아도 됩니다.
}
```

만일 우리가 game의 히스토리에서 아무 스탭이나 클릭했을 경우, 틱택토 게임 보드는 즉시 그 스탭이 일어났던 때를 보여주도록 업데이트 될 것입니다.

[여기까지의 소스 보기](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)

## 요약하기

축하합니다! 이제 막 틱택토 게임을 만들었습니다! 이 게임은

- 우리가 틱택토 게임을 플레이 할 수 있게 해줍니다.
- 한 플레이어가 게임을 이겼을 때, 승자를 표기해줍니다.
- 게임이 진행되면서 게임의 히스토리를 저장합니다.
- 플레이어가 게임의 히스토리를 리뷰할 수 있게 해주고 이전 움직임들을 보여줄 수 있습니다.

잘했습니다! 리액트의 동작 방식에 대해 꽤 괜찮은 이해를 얻었길 바랍니다.

여기서 마지막 결과를 확인하세요: **[마지막 결과](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**

만일 시간이 더 있고 새로운 리액트 기술들을 연습하고 싶다면, 틱택토 게임의 추가기능에 대한 아이디어가 있습니다. 번호가 증가할수록 구현하기 어렵습니다. 

1. (행, 열)과 같은 형식으로 move history에 각각 움직임의 위치를 기록해보세요.
2. 움직임 리스트에서 현재 선택된 아이템을 굵게 표기해보세요.
3. square를 만들기 위해 2개의 반복문을 사용하여 Board를 다시 작성해보세요.
4. 토글 버튼을 추가하여 움직임을 오름차, 내림차 순으로 정렬할 수 있게 해보세요.
5. 누군가 승리했을 때, 승리의 증거가 되는 3개의 네모를 하이라이팅 해보세요.
6. 누구도 이기지 못했을 때, 무승부라는 메시지를 표기하세요.

이 튜토리얼을 통해, 우리는 원소(elements), 컴포넌트(components), props, 상태(state)와 같은 리액트의 개념들을 건드려봤습니다. 이 주제에 대한 더욱 자세한 설명을 위해서, [이 문서들](https://reactjs.org/docs/hello-world.html)을 확인해보세요. 컴포넌트를 정의하는 것에 대해 더 배우기 위해서 [컴포넌트 API 레퍼런스](https://reactjs.org/docs/react-component.html)도 확인해보세요.

