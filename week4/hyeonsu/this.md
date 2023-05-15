정리된 노션 링크입니다:
https://shell-breakfast-4f4.notion.site/2023-05-15-this-58d246bf1d914879b5726805b5732c03

# 2023.05.15[this]

<aside>
1️⃣ **자바스크립트에서 this는 몇가지로 추론 될 수 있나요? 아는대로 말해주세요**

---

</aside>

<aside>
✅ 전역 범위에서 this 는 전역 객체를 참조합니다. 브라우저 환경에서는 window, node.js 환경에서는 global 을 참조합니다. 객체 메서드에서의 this 는 메서드가 속한 객체를 참조합니다. 중첩된 객체에서는, 접근자 바로 앞의 객체를 참조합니다. 생성자 함수에서 this 는 생성자 함수로 새로 생성된 객체를 참조합니다. call, apply, bind 등의 메서드를 사용한 명시적 바인딩을 사용한 경우, this 는 인수로 전달되어 바인딩된 객체를 참조합니다. 화살표 함수는 자신만의 this 를 가지지 않습니다. 대신 외부 스코프의 this 를 참조합니다. 만약 화살표 함수가 중첩된 구조라면, 화살표 함수가 아닌 가장 가까운 객체나 함수의 스코프를 참조합니다. 이벤트 핸들러에서의 this 는 이벤트가 발생한 요소를 참조합니다.

</aside>

<aside>
2️⃣ **일반함수의 this와 화살표 함수의 this는 어떻게 다른가요?**

---

</aside>

<aside>
✅ 일반 함수는 호출될 때마다 this 가 동적으로 결정됩니다. 반면 화살표 함수는 자신만의 this 를 가지지 않으며 외부 스코프의 this 를 상속합니다. 이때 화살표 함수의 this 는 함수가 호출된 곳이 아닌, 정의된 곳의 스코프를 참조합니다. 또 화살표 함수는 cal,,apply,bind 를 사용할 수 없으며 전역 범위에서 참조할 경우 undefined 를 반환하게 됩니다.

```
const obj = {
  name: 'John',
  regularFunction: function() {
    console.log(this.name); // 'John'
  },
  arrowFunction: () => {
    console.log(this.name); // 외부 스코프의 this를 상속하므로 undefined 또는 전역 객체의 name을 참조
  }
};

const regularFn = obj.regularFunction;
regularFn(); // 전역 범위에서 호출되므로, this는 전역 객체를 참조하여 undefined 또는 전역 객체의 name을 참조

const arrowFn = obj.arrowFunction;
arrowFn(); // 화살표 함수는 Lexical this를 가지므로, 상위 스코프인 obj의 this를 상속하여 'John'을 출력
```

일반 함수는 호출되는 방법에 따라 this가 동적으로 결정되기 때문에 호출 위치에 따라 this가 달라질 수 있습니다. 반면에 화살표 함수는 항상 자신을 감싸는 함수의 this를 상속받으므로 일관된 동작을 보장합니다.

</aside>

<aside>
3️⃣ **Call, Apply, Bind 함수에 대해 설명해주세요**

---

</aside>

<aside>
✅ call 메서드는 this 값과 함께 인수 목록을 전달합니다. apply 는 call 과 비슷하지만 인수 목록을 배열로 전달한다는 차이가 있습니다. bind 함수는 this 값으로 설정할 객체를 지정해 새로운 함수를 생성합니다. call 과 apply 는 즉시 호출 함수이며 bind 는 새로운 함수를 생성한다는 점에서 차이가 있습니다.

</aside>

<aside>
4️⃣ **use strict모드에서의 this?**

---

</aside>

<aside>
✅ use strict 모드를 사용할 경우, 전역 범위와 일반 함수 호출에서 this 값이 undefined 를 가리키게 됩니다. 이는 use strict 모드가 전역 객체를 참조하는 것을 막음으로써 의도치 않은 결과를 불러일으키지 않게 하기 위함입니다.

</aside>