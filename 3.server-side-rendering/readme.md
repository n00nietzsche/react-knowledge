# 들어가기 전에
- 이 포스팅은 https://flaviocopes.com/react-server-side-rendering/ 에 있는 포스팅을 번역한 것입니다. 오역이나 의역이 있을 수 있습니다. 지적해주시면 확인 후 바로 정정하겠습니다.

- original source of this posting is from https://flaviocopes.com/react-server-side-rendering/ If the original author requests deletion, it will be deleted immediately.

- Translated by Jake Seo (서진규)

	- https://velog.io/@jakeseo_me
	- https://github.com/n00nietzsche
    
> 리액트 지식 정리, #3 리액트에서 서버사이드 랜더링하기 (번역)

서버사이드 랜더링은 무엇이고? 리액트에서 서버사이드 랜더링은 어떻게 할까요?

**서버사이드 랜더링(Server Side Rendering)** 은 주로 **SSR** 이라는 이름으로 많이 불립니다. 서버사이드 랜더링은 자바스크립트 어플리케이션의 렌더링을 브라우저에서 하는 것이 아니라 서버에서 하는 것을 말합니다.

그럼 왜 서버에서 렌더링을 해야 할까요?

- 첫 페이지를 로딩하는데 더욱 적은 시간이 걸리게 해줍니다. 이러한 기능은 사용자에게 더 좋은 경험을 주는 요소 중 하나입니다.
- SEO([Search Engine Optimization](https://en.wikipedia.org/wiki/Search_engine_optimization))에 필수적입니다. 검색엔진은 아직은 효율적이고 정확하게 클라이언트 사이드에서 렌더링되는 어플리케이션을 색인할 수 없습니다. 구글에서는 최근 인덱싱을 강화했음에도 불구하고 다른 검색엔진들과 구글 모두 완벽하게 인덱싱하지 못하는 경우가 있습니다. 또한 구글은 빨리 로딩되는 페이지를 선호합니다. 클라이언트 사이드에서 로딩되는 페이지는 속도가 좋지 못합니다.
- 웹 페이지를 소셜미디어에서 공유할 때, 사이트를 공유하기 위해 필요한 메타 데이터를 더 쉽게 모을 수 있습니다.

서버사이드 렌더링이 없이는, 서버의 모든 파일들은 body가 없는 HTML 페이지와 같습니다. 그냥 브라우저가 어플리케이션을 렌더링하기 위한 스크립트 태그만 있는 거라고 생각하시면 됩니다.

클라이언트 사이드에서 렌더링되는 앱들은 처음 페이지 로딩 이후 유저와 연속적인 상호작용이 있는 경우에 아주 좋습니다. 서버 사이드 렌더링은 우리 앱을 백엔드에서 렌더링 된 앱과 클라이언트에서 렌더링 된 앱 사이 아주 좋은 타협점으로 갈 수 있도록 해줍니다. 페이지는 서버사이드에서 생성되지만 페이지에서의 모든 상호작용은 일단 로딩된 후에는 클라이언트 사이드에서 일어납니다.

하지만 서버사이드 렌더링은 단점도 있습니다.

- 서버사이드 렌더링의 개념 증명은 매우 간단하다고 말할 수 있지만, 서버사이드 렌더링의 복잡도는 어플리케이션의 복잡도와 함께 증가합니다.
- 큰 사이즈를 가진 어플리케이션의 서버사이드 렌더링을 하는 것은 꽤 자원 중심적(resource-intensive)일 수 있습니다. 그리고 싱글 보틀넥을 가진 경우, 클라이언트 사이드 렌더링을 할 때보다 더 느린 경험을 제공할 수도 있습니다.

# 최대한 간단하게 서버사이드 렌더링을 하는 리액트 앱 만들어보기

서버사이드 렌더링의 세팅은 매우매우 복잡해질 수 있습니다. 그리고 대부분의 튜토리얼에서는 시작부터 리덕스와 리액트 라우터와 많은 다른 개념들을 포함합니다.

서버사이드 렌더링이 어떻게 동작하는지 이해하기 위해, 개념을 증명하기 위한 코드를 구현하는 기본부터 시작해봅시다.

> 그냥 서버사이드 렌더링을 제공하는데 사용되는 라이브러리만 알고 싶은 것이고 세팅 작업에 대해 별로 알고 싶지 않으면 이 단락은 스킵해도 상관없습니다. 

기본적인 서버사이드 렌더링을 구현하기 위해 우리는 Express를 사용할 것입니다.

> Express를 처음 사용해보신다면 혹은 뭔가 좀 알고 싶으시다면 저자의 무료 핸드북을 참조해보세요. [링크](https://flaviocopes.com/page/ebooks/)

경고: SSR의 복잡도는 어플리케이션의 복잡도와 함께 증가할 수 있습니다. 앞으로 할 것은 기본 리액트 앱을 렌더링하기 위한 최소한의 설정입니다. 더욱 복잡한 니즈를 위해서는 리액트를 위한 서버사이드 렌더링을 확인할 필요가 있을 것입니다. 

아마 리액트 앱을 만들기 위해서 `create-react-app`을 사용한 적이 많았을 겁니다. 지금 만드는 중이었다면, 서버사이드 렌더링을 해보기 위해서 지금 `npx create-react-app ssr` 명령어를 사용해봅시다.

메인 앱 폴더에 가서, 다음 명령어를 실행하세요

```bash
npm install express
```

이제 ssr 디렉토리에 폴더들이 있을 겁니다. 새로운 폴더인 `server`를 만드세요. 그리고 폴더 내부에 `server.js`라는 이름의 파일도 하나 만드세요.

`create-react-app`의 컨벤션에 따라, 앱은 `src/App.js`파일에 있습니다. 우리는 그 컴포넌트를 로드할 것입니다. 그리고 그것을 `react-dom`에 의해 제공되는 `ReactDOMServer.renderToString()`([메소드 설명](https://reactjs.org/docs/react-dom-server.html))을 이용해 문자열로 렌더링 할 것입니다.

`./build/index.html` 파일의 컨텐츠에서 기본적으로 어플리케이션이 후킹되는 곳에 있는 태그인 `<div id="root"></div>`의 placeholder를 `<div id="root">\${ReactDOMServer.renderToString(<App />)</div>`로 바꿀 것입니다.

`build`폴더 내부의 모든 내용은 만들어진 그대로 정적으로 Express로 이용할 것입니다. 

클라이언트 어플리케이션에서, `src/index.js`에서 `ReactDOM.render()`를 호출하는 대신,
```js
ReactDOM.render(<App />, document.getElementById('root'))
```

`ReactDOM.hydrate()`를 호출할 것입니다. 이 메소드는 하는 일은 똑같지만 리액트가 로드된 이후에 존재하는 마크업에 이벤트 리스너를 추가할 수 있습니다.

```js
ReactDOM.hydrate(<App />, document.getElementById('root'))
```

모든 Node.js의 코드는 바벨에 의해 트랜스컴파일링 될 필요가 있습니다. 서버사이드 Node.js의 코드는 JSX나 ES 모듈(우리가 `include` 문을 위해서 쓰는)에 대해서는 아무것도 모릅니다.

다음 3개의 패키지를 설치하세요.

```bash
npm install @babel/register @babel/preset-env @babel/preset-react ignore-styles express
```

[`ignore-styles`](https://www.npmjs.com/package/ignore-styles)는 바벨 유틸리티인데, `import`문법으로 추가된 CSS 파일들을 무시합니다.

`server/index.js`안에 엔트리 포인트를 만들어봅시다.

```js
require('ignore-styles')

require('@babel/register')({
  ignore: [/(node_modules)/],
  presets: ['@babel/preset-env', '@babel/preset-react']
})

require('./server')
```

리액트 어플리케이션을 빌드해보세요. build/folder가 생성될 것입니다.

```bash
npm run build
```

이제 다음 명령어를 실행해보세요.

```bash
node server/index.js
```

이 프로젝트는 SSR을 위해 극단적으로 단순화되었다고 했습니다. 그래서,

- imports를 사용할 때, 이미지를 올바르게 랜더링하지 못합니다. 올바르게 렌더링하기 위해서는 Webpack이 필요합니다. (그리고 더 복잡한 프로세스가 요구됩니다.)
- Page의 헤더 메타데이터를 다루지 못합니다. SEO와 소셜 공유 목적을 위해서는 헤더의 메타데이터가 필수적입니다.

그래서 이 프로젝트는 `ReactDOMServer.renderToString()`과 `ReactDOM.hydrate`를 이용하여 간단한 서버사이드 렌더링을 구현하는 훌륭한 예제인 반면에 실제로 사용하기엔 매우 부족한 예제입니다.

# 라이브러리를 이용한 서버사이드 렌더링

서버사이드 렌더링은 제대로 하기 힘듭니다 그리고 리액트는 사실상 서버사이드 렌더링을 구현을 제공하지 않습니다.

아직 논쟁이 많지만, 이점을 얻기 위한 문제와 복잡도와 오버헤드는 페이지를 제공하기 위한 다른 방법을 쓰는 것보다 가치가 있습니다. [레딧의 이 포스팅](https://www.reddit.com/r/reactjs/comments/7o6oj6/serverside_rendering_not_worth_it/)은 이러한 것들에 대한 의견이 많습니다.

서버사이드 렌더링이 중요한 문제가 될 때는, 이 문제를 해결하기 위해 처음부터 미리 만들어진 라이브러리와 툴에 의존하는 것이 좋다는 것이 제 생각입니다. 

특히, **Next.js**와 **Gatsby**를 추천합니다. 다음에는 이것들에 대해 다뤄보겠습니다.
