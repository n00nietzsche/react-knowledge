# 들어가기 전에
- 이 포스팅은 https://reactjs.net/bundling/webpack.html 에 있는 포스팅을 번역한 것입니다. 오역이나 의역이 있을 수 있습니다. 지적해주시면 확인 후 바로 정정하겠습니다.

- original source of this posting is from https://reactjs.net/bundling/webpack.html If the original author requests deletion, it will be deleted immediately.

- Translated by Jake Seo (서진규)

	- https://velog.io/@jakeseo_me
	- https://github.com/n00nietzsche
    
> 리액트 지식 정리 #5, 웹팩이란? (번역)

# 웹팩

## 개념



웹팩은 Node.js 위에서 만들어진 인기 있는 모듈 번들링 시스템입니다. 자바스크립트와 CSS파일의 조합(combination)과 최소화(minification) 뿐만 아니라 이미지 파일(spriting)과 같은 리소스들도 이 플러그인의 사용을 통해 다룰 수 있습니다. 웹팩은 Cassette나 ASP.NET 조합, 최소화의 대안이 될 수 있습니다. 이 가이드에서는 이미 웹팩을 깔았다고 가정할 것입니다.

ReactJS.NET의 서버사이드 렌더링과 함께 웹팩을 사용하기 위해, 서버사이드 렌더링에 필요로 되는 코드만을 포함한 분리된 번들(엔드포인트)을 만드는 것을 권장합니다. 
