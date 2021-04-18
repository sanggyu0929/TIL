## Vue.js란?

> Vue.js는 화면단 라이브러리이자 프레임워크라 볼 수 있다.  
> 사용자 인터페이스를 만들기 위한 [점진적인 프레임워크](https://medium.com/@rubeena.ajeed/introduction-to-vue-js-a16614f20f77)(Progressive Framework)이다.

### 특징

> UI 화면 개발 방법 중 하나인 MVVM 패턴의 뷰 모델에 해당하는 화면단 라이브러리이다.  
> ![vue MVVM](https://gblobscdn.gitbook.com/assets%2F-M26jG1xuJ_y_q6GUJdp%2F-M26n5U2kzzz42LMgqau%2F-M26n8pXW395QA10W5VR%2Fview-model.png?alt=media)

### Vue.js 설치

- cdn을 통한 설치
  > 프로토 타이핑 또는 학습 목적으로 사용할 경우.

```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

> 프로덕션 환경인 경우

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.0"></script>
```

> 기본 ES 모듈을 사용하는 경우

```html
<script type="module">
  import Vue from "https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.esm.browser.js";
</script>
```

- [직접 다운로드](https://kr.vuejs.org/v2/guide/installation.html)
- NPM
  > Vue를 사용하여 대규모 애플리케이션을 구축할 때 NPM을 이용한 설치를 권장하고 있다.

```Shell
# 최신 안정화 버전
$ npm install vue
```
