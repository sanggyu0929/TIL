## Computed

> `computed` 프로퍼티는 `methods`와 비슷하지만, `computed`는 **캐싱(cache)을 가지고 있다.**

### 캐싱이란?

> `캐시(cache)`는 잠시 저장해 둔다는 의미를 가지고 있다.  
> 네트워크 영역에서 캐시는 **로컬 저장소에 파일을 미리 받아놓는 것**을 의미한다.  
> 웹 서버에서 매번 번거롭고 느리게 로딩 해야 하는 _파일들을 미리 로딩해두고, 발빠른 응답을 주기도 한다._ [출처](https://net-gate.tistory.com/11)

## Computed 프로퍼티로 퍼포먼스 최적화

> `computed` 프로퍼티는 Vue 인스턴스 Function 내에서 `this` 키워드와 연결된다.  
> `computed` 프로퍼티는 `data , methods`와 같은 방법으로 `<template>`안에서 접근할 수 있다.  
> `computed` 프로퍼티를 `get`과 `set` 두가지 프로퍼티를 가진 object로 변경해야 한다.

## 사용 예제

```js
const vm = new Vue({
  el: "#app",
  data: {
    msg: "Hello Vue!",
  },
  computed: {
    reversedMsg: {
      get() {
        return this.msg.split("").reverse().join("");
      },
      set(value) {
        this.msg = value;
      },
    },
  },
});
```

> `set` methods를 설정하면, `value`와 같이 매개변수를 받는다.  
> 해당 매개변수는 `computed` 프로퍼티에 **특정 값을 등록하고자 할 때 입력할 새로운 값을 포함**하고 있다.  
> 그래서 `set` methods 안에서 `data`프로퍼티를 간단하게 업데이트 할 수 있다.
