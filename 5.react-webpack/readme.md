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

박스 밖에서, 웹팩은 웹팩은 오직 자바스크립트와 JSON 파일만 이해합니다. **Loaders**는 웹팩이 다른 타입의 파일들도 처리할 수 있고 그것들을 유효한 어플리케이션이 사용할 수 있는 유효한 **[모듈(modules)](https://webpack.js.org/concepts/modules/)** 로 변환하고 dependency graph에 추가할 수 있도록 해줍니다.

> 알아둬야 할 것 : `css` 파일들과 같이 다른 어떤 타입의 모듈을 `import` 할 수 있는 능력은 웹팩에 특화된 능력입니다. 그리고 다른 번들러나 태스크 러너에 의해서는 지원되지 않을 수도 있습니다. 우리는 이러한 언어의 확장이 개발자들이 더욱 정확한 dependency graph를 빌드할 수 있도록 돕는 것을 보장한다고 느낍니다.

하이 레벨에서, 웹팩 설정에서 **loaders**는 2개의 프로퍼티를 가집니다.

1. `test` 프로퍼티는 어떤 파일이 변환(transform)되어야 하는지를 구분합니다.
2. `use` 프로퍼티는 변환(transform)할 때 어떤 loader가 사용되어야 할지를 가리킵니다.

**webpack.config.js**
```js
const path = require('path');

module.exports = {
  output: {
    filename: 'my-first-webpack.bundle.js'
  },
  module: {
    rules: [
      { test : /\.txt$/, use: 'raw-loader' }
    ]
  }
};
```

위의 설정에서는 2개의 요구된 프로퍼티인 `test`와 `use`를 가진 하나의 모듈에 대해 `rules` 프로퍼티를 정의했습니다. 이것은 웹팩 컴파일러에 다음과 같은 사실을 알려줍니다.

> "헤이 웹팩 컴파일러, `require()` / `import` 문 내부에 있는 '.txt'파일을 resolve할 때, 번들에 추가하기 전, 변환(transform)하기 위해 `raw-loader`를 사용해줘.

> 정규표현식을 이용하여 파일을 매칭시킬 때, 따옴표를 사용함에 있어서 조심하세요. 예를 들면 `/\.txt$/`는 `'/\.txt$/'`나 `"/\.txt$/"`와 같지 않습니다. 맨 앞의 정규표현식은 웹팩에게 .txt로 끝나는 파일을 매칭시키라고 하는 것이고 뒤에 것은 절대 경로에 일치하는 하나의 파일 '.txt'를 찾아달라고 하는 것입니다. 아마 의도한 바가 아닐 것입니다.

[loader section](https://webpack.js.org/concepts/loaders/)에 로더를 추가할 때 더 많은 정보를 얻고싶으시다면 앞의 loader section 글자를 클릭해보세요.

## 플러그인(Plugins)

로더가 모듈의 몇몇 특정한 타입의 모듈들을 변환(transform)하기 위해 사용되는 반면에, 플러그인은 번들 최적화, 자원 관리, 환경변수 삽입과 같은 보다 많은 범위의 작업을 수행하는 데에 있어 능력을 끌어올릴 수 있습니다.

> [플러그인 인터페이스](https://webpack.js.org/api/plugins/)를 확인하고 웹팩의 능력치를 확장하기 위해 플러그인을 어떻게 사용할 수 있는지도 알아보세요.

플러그인을 사용하기 위해, `require()`를 해야합니다. 그리고 `module.export`에 `plugin`배열을 추가하고 그 안에 플러그인을 넣어봅시다. 대부분의 플러그인은 옵션을 이용하여 커스터마이징이 가능합니다. 플러그인을 많은 다른 목적을 위해서 몇번이든 설정할 수 있습니다. `new` 연산자를 통한 호출을 이용하여 인스턴스를 생성하면 됩니다.

**webpack.config.js**
```js
const HtmlWebpackPlugin = require('html-webpack-plugin'); //installed via npm
const webpack = require('webpack'); //to access built-in plugins

module.exports = {
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
```

위의 예제에서 `html-webpack-plugin`은 생성된 번들을 자동으로 어플리케이션에 주입하여 HTML 파일을 생성해냅니다. 

> 웹팩이 제공하는 많은 독창적인 플러그인들이 존재합니다. [플러그인 리스트](https://webpack.js.org/plugins/)를 확인하세요!

웹팩 설정에서 플러그인을 사용하는 것은 직관적입니다. 하지만, 더 알아볼 가치가 있는 다양한 사용 용례들이 있습니다. [여기를 클릭해서 더 알아보세요.](https://webpack.js.org/concepts/plugins/)

## 모드(Mode)

`mode` 파라미터를 `development`, `production`이나 `none`으로 셋팅함으로써, 각 환경에 맞는 웹팩의 빌트인 최적화를 사용할 수 있습니다. 기본 값은 `production`입니다.

```js
module.exports = {
  mode: 'production'
};
```

[모드 설정](https://webpack.js.org/configuration/mode/)에 대해 더 알아보세요. 그리고 각 값에 어떤 최적화가 일어나는지도 알아보세요.

## 브라우저 호환성(Browser Compatibility)

웹팩은 [ES5-호환](https://kangax.github.io/compat-table/es5/)인 모든 브라우저를 지원합니다. 웹팩은 `import()`와 `require.ensure()`를 위한 `Promise`를 필요로 합니다. 만약 오래된 브라우저를 지원하고 싶다면, 이러한 식들을 사용하기 전에 [poly-fill 불러오기]가 필요할 것입니다.
