# 들어가기 전에
- 이 포스팅은 https://reactjs.net/bundling/webpack.html 에 있는 포스팅을 번역한 것입니다. 오역이나 의역이 있을 수 있습니다. 지적해주시면 확인 후 바로 정정하겠습니다.

- original source of this posting is from https://reactjs.net/bundling/webpack.html If the original author requests deletion, it will be deleted immediately.

- Translated by Jake Seo (서진규)

	- https://velog.io/@jakeseo_me
	- https://github.com/n00nietzsche
    
> 리액트 지식 정리 #5, 웹팩이란? (번역)

# 웹팩

## 개념

핵심적인 개념으로는, 웹팩은 현대 자바스크립트 어플리케이션을 위한 *정적인 모듈 번들러*입니다. 웹팩이 어플리케이션을 처리할 때, 내부적으로 프로젝트가 필요로 하는 모든 모듈을 맵핑하고 한개 또는 그 이상의 번들을 생성하는 [의존성 그래프](https://webpack.js.org/concepts/dependency-graph/)를 만듭니다. 

> 의존성 그래프란?
> 한 파일이 다른 파일을 의존할 때, 웹팩은 이것을 `의존성(dependency)`으로 취급합니다. 의존성 그래프는 웹팩이 코드가 아닌 리소스들도 가져올 수 있게 해줍니다. 이를테면 이미지, 웹 폰트 등을 제공합니다. 또한 그것들을 어플리케이션의 `의존성(dependencies)`으로 제공합니다.
>
>웹팩이 어플리케이션을 처리할 때, 웹팩은 설정 파일이나 커멘드 라인에 있는 정의된 모듈 리스트부터 시작합니다. 이러한 [엔트리 포인트(시작점)](https://webpack.js.org/concepts/entry-points/)부터 시작하면서, 웹팩은 재귀적으로 어플리케이션에 필요한 모든 모듈을 포함하는 의존성 그래프(dependency graph)를 만듭니다. 그리고 그 모듈들을 작은 숫자의 번들 안에 넣습니다. 주로 브라우저에 의해 로딩되는 것은 1개입니다.

버전 4.0.0부터, **웹팩은 프로젝트를 번들링하기 위해 설정 파일을 필요로 하지않습니다.** 그럼에도 불구하고 [설정](https://webpack.js.org/configuration/)은 당연히 사용자에 맞게 가능합니다.

시작하기 위해서는 **핵심 개념**들을 이해하면 됩니다.

- [엔트리](https://webpack.js.org/concepts/#entry)
- [출력](https://webpack.js.org/concepts/#output)
- [로더](https://webpack.js.org/concepts/#loaders)
- [플러그인](https://webpack.js.org/concepts/#plugins)
- [모드](https://webpack.js.org/concepts/#mode)
- [브라우저 호환성](https://webpack.js.org/concepts/#browser-compatibility)

이 문서는 이러한 개념들의 깊은 이해를 주기 위해서 만들어졌습니다. 상세한 개념이 포함된 USE CASE 링크도 제공하겠습니다.

모듈 번들러란 것 그리고 그들이 하부에서 어떻게 작동하는지에 대한 더 나은 이해를 위해서, 아래 리소스를 참조하세요. 

- [어플리케이션 수동 번들링하기](https://www.youtube.com/watch?v=UNMkLHzofQI)
- [간단한 번들러 라이브 코딩](https://www.youtube.com/watch?v=Gc9-7PBqOC8)
- [간단한 모듈 번들러의 상세한 설명](https://github.com/ronami/minipack)

## 엔트리

엔트리 포인트는 웹팩이 denpenency graph를 만들기 위해 어떤 모듈을 사용할지를 가리키는 것입니다. 웹팩은 직접적이든 간접적이든 엔트리 포인트가 의존하는 어떤 다른 모듈들과 라이브러리들을 알아낼 것입니다.

기본값으로 `./src/index.js`가 설정되어 있습니다. 하지만 웹팩 설정에서 엔트리 프로퍼티를 설정함으로써 다른 파일을 설정할 수도 있습니다. 예를 들면

**webpack.config.js**
```js
module.exports = {
  entry: './path/to/my/entry/file.js'  
};
```

[엔트리 포인트 섹션에 대해 더 배워보기](https://webpack.js.org/concepts/entry-points/)

## 아웃풋(Output, 출력)
>역자 주: 아웃풋이라는 단어는 대부분의 프로그래머가 친숙할 것이라 생각하기에 한글 그대로 아웃풋으로 번역하겠습니다.

**아웃풋** 프로퍼티는 웹팩이 번들을 어디에 생성할지에 대해 그리고 파일들의 이름을 어떻게 지을지에 대해 알려줍니다. 메인 아웃풋 파일을 위한 기본 값은 `./dist/main.js`이고, 나머지 생성된 파일은 `./dist`가 기본 값입니다.

설정에서 `output` 부분을 수정하면, 이 부분이 어떻게 진행될지에 대해 설정할 수 있습니다.

**webpack.config.js**
```js
const path = require('path');

module.export = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js'
  }
};
```

위의 예에서, 우리는 `output.filename`와 `output.path` 프로퍼티를 사용하여 웹팩에게 우리 번들의 이름과 어디에 생겨날지에 대한 정보를 설정할 수 있습니다. 맨 위에 import된 path 모듈에 대해 궁금하다면, path 모듈은 파일 path를 다루기 위한 [node.js의 핵심 모듈](https://nodejs.org/api/modules.html)입니다. 

> `output` 프로퍼티는 [많은 설정 가능한 특성들](https://webpack.js.org/configuration/output/)이 있고 이 뒤에 숨겨진 개념들을 더 알고 싶다면, [여기서](https://webpack.js.org/concepts/output/) 아웃풋 섹션에 대한 정보를 더 읽어보시면 됩니다.

## 로더(Loaders)

