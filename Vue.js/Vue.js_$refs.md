## `$refs`

> DOM과 엘리먼트를 직접 조작하는 메서드들은 예전부터 많이 쓰였고, 지금도 많이 사용하고 있다.  
> `getElementsById` `getElementsByClassName` `Document.creatElement()` 등등 DOM을 직접 조작해 HTML 구조를 자바스크립트로 변경이 가능하다.  
> 하지만 Vue에서는 이런 메서드의 사용을 피하라고 권고하고 있다.  
> 웹 브라우저 단에서 DOM에 변화가 일어나면 CSS를 다시 연산/레이아웃/구성하며 페이지 리페인트를 하기 때문에 시간 로스가 심해지기 때문이다.  
> 물론 React와 Vue 모두 실제 DOM이 아닌 Virtual DOM을 사용하기 때문에 DOM조작 메서드를 사용해도 DOM처리 횟수가 생각보다 많아 지지는 않지만 사용은 지양하는게 최근 프론트엔드 개발 트렌드이다.

1. JavaScript로 Props&Event 거치지 않고 자식 컴포넌트 접근
2. DOM조작 메서드 없이 엘리먼트 조작

### 사용 방법

> HTML에 `ref="name"`라고 지어주면 된다.

```html
<input ref="input" />
```

```js
methods: {
  focus: function () {
    this.$refs.input.focus()
  }
}
```

`input tag`에 `ref`를 지정 해주고, JavaScript `methods`를 통해 엘리먼트에 직접 포커스를 명령한다.
