# 들어가기 전에
- 이 포스팅은 https://reactjs.org/tutorial/tutorial.html 에 있는 포스팅을 번역한 것입니다. 오역이나 의역이 있을 수 있습니다. 지적해주시면 확인 후 바로 정정하겠습니다.

- original source of this posting is from https://reactjs.org/tutorial/tutorial.html If the original author requests deletion, it will be deleted immediately.

- Translated by Jake Seo (서진규)

	- https://velog.io/@jakeseo_me
	- https://github.com/n00nietzsche
    
> 리액트로 서버사이드 랜더링하기 (번역)

서버사이드 랜더링은 무엇이고? 리액트에서 서버사이드 랜더링은 어떻게 할까요?

**서버사이드 랜더링(Server Side Rendering)** 은 주로 **SSR** 이라는 이름으로 많이 불립니다. 서버사이드 랜더링은 자바스크립트 어플리케이션의 렌더링을 브라우저에서 하는 것이 아니라 서버에서 하는 것을 말합니다.

그럼 왜 서버에서 렌더링을 해야 할까요?
- 첫 페이지를 로딩하는데 더욱 적은 시간이 걸리게 해줍니다. 이러한 기능은 사용자에게 더 좋은 경험을 주는 요소 중 하나입니다.
- SEO([Search Engine Optimization](https://en.wikipedia.org/wiki/Search_engine_optimization))에 필수적입니다. 검색엔진은 아직은 효율적이고 정확하게 클라이언트 사이드에서 렌더링되는 어플리케이션을 색인할 수 없습니다. 구글에서는 최근 인덱싱을 강화했음에도 불구하고 다른 검색엔진들과 구글 모두 완벽하게 인덱싱하지 못하는 경우가 있습니다. 또한 구글은 빨리 로딩되는 페이지를 선호합니다. 클라이언트 사이드에서 로딩되는 페이지는 속도가 좋지 못합니다.
- 
